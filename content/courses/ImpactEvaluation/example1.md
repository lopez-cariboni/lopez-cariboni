---
title: |
 | Evaluación de Impacto: Taller 1
 | Aleatorización y modelo de regresión lineal simple
linktitle: Lab 1 (aleatorización)
toc: true
type: docs
author: "Marzo, 2020"
date: 'Entrega: Martes 30 de marzo'
draft: false
menu:
  example:
    parent: Talleres
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
output:
  html_document:
    toc: true
    number_sections: true
    toc_depth: 2
    toc_float: true
    theme: spacelab
    highlight: tango
urlcolor: BrickRed
---


***

```{r setup, include = FALSE}
knitr::opts_chunk$set(fig.align = "center", eval=TRUE)
```

**Objetivo:** luego de hacer este taller los estudiantes serán capaces de...

- *Leer* datos en `R`
- *Describir* las variables relevantes de la intervención (en cantidad de observaciones , media muestral, desvío estándar muestral, valor mínimo observado en la muestra, y valor máximo observado en la muestra).
- *Obtener* medias condicionales y otros estadísticos (desvío estándar, coeficientes de varaición, mediana) para subgrupos de la muestra.

***

# Aleatorización en `R`

Hay muchas maneras de hacer aleatorización para garantizar el equilibrio entre grupos. Algunas son difíciles, por ejemplo, monedas y sombreros. 

Afortunadamente, la aleatorización flexible y replicable es muy fácil de hacer con el software disponible en forma gratuita. En siguiente código `R` se realiza asignación aleatoria, especificando el número de unidades a tratar. Aquí, `N` es el número de unidades participantes en el estudio y `m` es el número de unidades a las que se desea tratar. El número "semilla" permite replicar el mismo sorteo cada vez que ejecuta el código.

```{r}
ra <- function(N,m,seed){
 set.seed(seed)
 assign <- cbind(Unidad = 1:N, Sorteo = 1:N %in% sample(1:N,m))
 return(assign)
 }
ra(20,12,seed=1000)

```

De esta manera identificamos a cada `unidad` y su estatus de tratamiento en la variable `sorteo`.

Hay muchas otras formas de aleatorziación, muchas de ellas se comentan en [***este post de EGAP***](http://egap.org/methods-guides/10-things-you-need-know-randomization) y son ilustradas con código en `R`.


***

# Leer datos - programa de inserción laboral


En el país "A", durante el año 2009 se implementó un programa para apoyar la inserción laboral de personas que enfrentaban problemas de acceso al sector formal. Por restricciones presupuestales sólo hubo disponibilidad para 3022 cupos, los que se asignaron por sorteo. En el programa se inscribieron 8328 personas, y quienes no salieron sorteados como titulares quedaron como suplentes (5306 personas). Algunos de los convocados a participar finalmente no participaron, en cuyo caso fueron sustituidos por suplentes. Se cuenta con datos de los 8328 inscriptos, en particular respecto a las siguientes variables:

- `cotizacion`	cotizacion=1 si la persona registra al menos una cotización en un empleo formal entre 2010 y 2011; cotizacion=0 en otro caso
- `participa`	participa=1 si la persona participó efectivamente del programa; participa= 0 en otro caso
- `cprevia`	cprevia=1 si la persona registra haber tenido un empleo formal en 2007 o 2008 ; y cprevia=0 en otro caso
- `Sorteo`	sorteo=1 la persona fue convocada a participar del programa


```{r, message = FALSE, warning = FALSE}

# install.packages("readstata13") # Instalar si no existe este paquete en tu biblioteca
library(readstata13)

df <- read.dta13("https://www.dropbox.com/s/y4oix826u2pr5fc/taller1_2020.dta?dl=1")
```

El código de arriba levantará los datos a la memoria de  `R`. Normalmente uno debe evitar tener referencias absolutas al lugar donde están los datos. Aquí bajamos los datos de una dirección web. También podemos subirlos desde un directorio de trabajo.

En este caso utilizamos el comando `read.dta13` del paquete `readstata13` que nos permite leer archivos de `STATA`. Puedes leer más sobre sobre [***cómo instalar paquetes en `R`***](https://daviddalpiaz.github.io/appliedstats/introduction-to-r.html#installing-packages). Para leer bases de datos guardadas en `*.csv` utilizamos la función `read.csv()` del paquete `foreign`. Pueden ver muchas formas de [***leer datos en `R`***](https://bookdown.org/rdpeng/rprogdatascience/getting-data-in-and-out-of-r.html)

***

# Descriptivos: ¿Como funcionó la aleatorización?

La función `summary` muestra estadísticos para cada variable dentro de `df` o para todas a la vez.

```{r, message = FALSE, warning = FALSE}

summary(df$cotizacion)

summary(df$participa)

summary(df$titulares)

summary(df$cprevia)

summary(df$sorteo)

summary(df$hombre)

```

O los estadísticos descriptivos de todas las variables en `df` de una sola vez. 

```{r, message = FALSE, warning = FALSE}

summary(df)


dim(df)

```

También se puede obtener otros momentos o estadísticos (en el conjunto de la población) o momentos condicionales (en subpoblaciones) por ejemplo: la media, el desvío estándar, el coeficiente de variación y la mediana.
Utilizamos la función `stat.desc` del paquete `pastecs`.


```{r}
# install.packages("pastecs") # Instalar una vez.
library(pastecs)

stat.desc(df, basic=F)

stat.desc(df[df$participa==1,], basic=F)

stat.desc(df[df$participa==0,], basic=F)
```

Ahora computamos correlaciones entre variables seleccionadas. 

```{r}

vars <- c("cprevia", "sorteo", "participa", "cotizacion")

cor(df[vars]) 

```
Como puede notarse, 


Si utiliza la función `cov` computamos la matriz de varianzas y covarianzas.

```{r}
cov(df[vars])
```


***


# Inferencia. Balance en co-variables.

Queremos obtener resultados de una "prueba t". Para obtener la media de una variable por subgrupos y hacer prueba de diferencia de medias en `R`:


```{r}
t.test(df$cprevia ~ df$sorteo, var.equal = TRUE)
```



El mismo test se puede implementar mediante la regresión lineal simple o múltiple, estimador MCO.


```{r}
modelo <- lm(cprevia ~ sorteo, data = df)
summary(modelo)
```



# Inferencia. Estimación de impacto


```{r}
t.test(df$cotizacion ~ df$participa, var.equal = TRUE)
```


```{r}
t.test(df$cotizacion ~ df$sorteo, var.equal = TRUE)
```


Veamos que el efecto de participar en el programa también se puede encontrar con MCO.


```{r}
modelo <- lm(cotizacion ~ participa, data = df)
summary(modelo)
```


 ***


# Ejercicios

1. verificar que el coeficiente asociado a la variable participa en la regresión es igual a:
     + la diferencia de medias 
     + el ratio entre la covarianza entre cotización y participa dividido la varianza de participa

2. Responder a las siguientes preguntas: 
    + ¿cuál es la fórmula del error estándar del coeficiente asociado a participa? ¿cuál es su utilidad?
    + ¿y del estadístico t/z?
    + ¿qué es el p-valor, como se obtiene y cuál es su utilidad?
    + ¿qué es el Intervalo de confianza al 95%, como se obtiene y cuál es su utilidad?



