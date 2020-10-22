---
# Course title, summary, and position.
linktitle: Evaluación de Impacto (2020)
summary: Métodos cuantitativos para la evaluación de impacto de políticas y programas.
weight: 0

# Page metadata.
title: Evaluación de Impacto
# date: "2018-09-09T00:00:00Z"
# lastmod: "2018-09-09T00:00:00Z"
draft: false  # Is this a draft? true/false
toc: true  # Show table of contents? true/false
type: docs  # Do not modify.

# Add menu entry to sidebar.
# - name: Declare this menu item as a parent with ID `name`.
# - weight: Position of link in menu.
menu:
  example:
    name: Programa
    weight: 1
---

1. **Docentes**: [Santiago López Cariboni](mailto:santiago.lopez@cienciassociales.edu.uy) y [Graciela Sanroman](mailto:graciela.sanroman@cienciassociales.edu.uy)

2. **Créditos**: 6

3. **Carga horaria**: 30 horas

4. **Modalidad de enseñanza**: Taller 

5. **Conocimientos previos recomendados**: Será requisito para cursar tener conocimientos de estadística inferencial y análisis multivariado.

6. **Objetivos**: En este curso se presentan al estudiante las herramientas básicas para poder evaluar políticas públicas y programas. El objetivo es desarrollar las técnicas utilizadas en el campo de la evaluación de impacto de programas sociales y mostrar su aplicación práctica utilizando el programa Stata. Aquellos que aprueben este curso serán capaces de entender correctamente un diseño de evaluación de impacto; así como replicar e interpretar el análisis estadístico de artículos e informes de evaluaciones realizadas que utilicen los métodos abordados en el curso.

7. **Contenidos**



	* ***Tema 1. Introducción: causalidad y contrafactual*** 

		1.1 Contexto contrafactual   
		1.2 Regresión y causalidad (regresores endógenos y autoselección)   
		1.3 El problema de evaluación de programas: parámetros de interés   
		1.4 Diseños para la inferencia causal   
		1.5 Validez interna, validez externa 

	* ***Tema 2. Métodos experimentales: asignación aleatoria***
 
		2.1 Diseños experimentales   
		2.2 Principales problemas: imperfección del cumplimiento; desgaste y derrames      
		2.3 Estimación 

	* ***Tema 3. Variables instrumentales***

		3.1 Variables instrumentales como solución al problema de cumplimiento imperfecto en diseños aleatorizados   
		3.2 Estimación por Variables Instrumentales (VI)

	* ***Tema 4. Regresión discontinua***

		4.1 Evaluación de programas que utilizan un índice de elegibilidad   
		4.2 El diseño de regresión discontinua: marcado y difuso 

	* ***Tema 5. Diferencias en diferencias y control sintético***

		5.1 Supuestos y estimación mediante diferencias en diferencias   
		5.3 Introducción al método de control sintético 

	* ***Tema 6. Matching***

		6.1 Propensity score y métodos de reponderación   
		6.2 Matching    
		6.3 Matching + Diferencias en diferencias   

8. **Método de trabajo**: Se realizará en la modalidad de taller. En el curso se abordarán los temas teóricos con un nivel básico y en cada tema se realizará una instancia de taller/laboratorio en la que se reproducirán e interpretarán los resultados empíricos de artículos o ejemplos seleccionados con ese fin. El software a utilizar será el STATA. Se realizará una instancia presencial de 2 horas con una frecuencia mínima semanal. En cada instancia se indicarán los ejercicios que los estudiantes deberán entregar en la sesión siguiente. Los profesores estarán disponibles en sus lugares de trabajo en DECON para consulta en los siguientes horarios: lunes, miércoles y viernes de 15 a 17. 

9. **Sistema de evaluación**: La evaluación del curso será mediante la realización de 3 ejercicios domiciliarios (con una puntaje de 20 puntos cada uno) y una prueba o trabajo final (con un puntaje de 40 puntos). Los estudiantes que alcancen una nota mínima de 7 en cada ejercicio y en la prueba final y obtengan un promedio de 9 o más en total exonerarán el curso. Aquellos estudiantes que alcancen el mínimo en cada domiciliario y en la prueba final y obtengan un promedio en el total entre 3 y 8 podrán rendir un examen reglamentado. Para reglamentar o exonerar los estudiantes deber registrar 75% de asistencias. Quienes no cumplan con los requisitos anteriores podrán rendir el examen libre. 


10. **Bibliografía:**
	
* ***Obligatoria***:   
Gertler, P. J., Martínez, S., Premand, P., Rawlings, L. B., & Vermeersch, C. M. (2017). *La evaluación de impacto en la práctica*. Banco Internacional para la Reconstrucción y el Desarrollo/Banco Mundial

* ***Ampliatoria***:  
Angrist, J. D., & Pischke, J. S. (2008). *Mostly harmless econometrics: An empiricist's companion*. Princeton University Press.  
Gerber, A. S., & Green, D. P. (2012). *Field experiments: Design, analysis, and interpretation*. WW Norton.   
Glennerster, R., & Takavarasha, K. (2013). Running randomized evaluations: A practical guide. Princeton University Press.   
Imbens, G. y Rubin, D.B. (2015). *Causal Inference for Statistics, Social and Biomedical Sciences*. Cambridge University Press.   
Khandker, S. R., Koolwal, G. B., Samad, H. A. (2009). *Handbook on Impact Evaluation: Quantitative Methods and Practices*. The World Bank, Washington D.C.




<!-- ## Flexibility -->

<!-- This feature can be used for publishing content such as: -->

<!-- * **Online courses** -->
<!-- * **Project or software documentation** -->
<!-- * **Tutorials** -->

<!-- The `courses` folder may be renamed. For example, we can rename it to `docs` for software/project documentation or `tutorials` for creating an online course. -->

<!-- ## Delete tutorials -->

<!-- **To remove these pages, delete the `courses` folder and see below to delete the associated menu link.** -->

<!-- ## Update site menu -->

<!-- After renaming or deleting the `courses` folder, you may wish to update any `[[main]]` menu links to it by editing your menu configuration at `config/_default/menus.toml`. -->

<!-- For example, if you delete this folder, you can remove the following from your menu configuration: -->

<!-- ```toml -->
<!-- [[main]] -->
<!--   name = "Courses" -->
<!--   url = "courses/" -->
<!--   weight = 50 -->
<!-- ``` -->

<!-- Or, if you are creating a software documentation site, you can rename the `courses` folder to `docs` and update the associated *Courses* menu configuration to: -->

<!-- ```toml -->
<!-- [[main]] -->
<!--   name = "Docs" -->
<!--   url = "docs/" -->
<!--   weight = 50 -->
<!-- ``` -->

<!-- ## Update the docs menu -->

<!-- If you use the *docs* layout, note that the name of the menu in the front matter should be in the form `[menu.X]` where `X` is the folder name. Hence, if you rename the `courses/example/` folder, you should also rename the menu definitions in the front matter of files within `courses/example/` from `[menu.example]` to `[menu.<NewFolderName>]`. -->
