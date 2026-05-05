# CLAUDE.md — Personal Website (Hugo Academic)

Project-specific instructions for editing Santiago López-Cariboni's academic website.

## Source of truth

The website mirrors **the latest English CV**:

```
/Users/slopezcariboni/Dropbox/Research/CV - Hompage/last_version/CV_en<YEAR>.Rmd
```

When the user asks to "sync with CV" or "update the website", **always open this file first**. If multiple CVs exist (e.g. `CV_en2026.Rmd`, `CV_en2026_RSF.Rmd`), the plain `CV_en<YEAR>.Rmd` is the master.

## Site stack

- Hugo + `themes/hugo-academic` (Wowchemy v4-style)
- Source markdown is rendered at build time. No Rmd → Hugo step needed.
- Remote: `git@github.com:lopez-cariboni/lopez-cariboni.git`, branch `master`

## Where to edit what

| Change requested | File(s) to edit |
|---|---|
| Bio paragraph, role, interests, education list, social icons | `content/authors/admin/_index.md` |
| Profile photo | `content/authors/admin/avatar.jpg` (see "Avatar gotcha" below) |
| Top-nav menu (CV link, sections) | `config/_default/menus.toml` |
| CV PDF served by the site | `static/files/cv.pdf` (copy from `last_version/CV_en<YEAR>.pdf`) |
| Experience widget on homepage | `content/home/experience.md` |
| Teaching page | `content/courses/_index.md` |
| One project | `content/project/<Name>/index.md` |
| One publication | `content/publication/<Name>/index.md` |

## Avatar gotcha

The about widget at `themes/hugo-academic/layouts/partials/widgets/about.html` resolves the photo with:

```go
{{ $avatar := ($person_page.Resources.ByType "image").GetMatch "*avatar*" }}
```

The glob is `*avatar*` — **any file whose name contains "avatar" matches**. `GetMatch` returns the first hit alphabetically, so an old `avatar.jpeg` will win over a new `avatar.jpg`. To swap the photo:

1. Copy the new picture to `content/authors/admin/avatar.jpg`.
2. **Rename any other `*avatar*` file** in that directory so the glob no longer matches it (e.g. `_OLD_pic1.jpeg`). Don't just leave `avatar.jpeg` next to `avatar.jpg`.
3. Original picture file (e.g. `foto_decon.jpg`) can stay in the folder for reference.

## Co-authors for projects

The CV's "Ongoing projects" section lists projects but **does not always list every co-author**. When the user says "add co-authors", look in:

```
/Users/slopezcariboni/Dropbox/Research/Papers/<ProjectName>/
```

Authoritative sources by file type:
- ANII grant PDFs (`Proyecto ANII/FSE_*.pdf` or `FCE_*.pdf`) → "Recursos humanos" section lists the team with roles
- `CLAUDE.md` inside the project folder may have a "Co-authors" block (often empty — fall back to grant PDF)
- File suffixes like `_slc`, `_MG`, `_<Name>` in `Declaración jurada` files reveal team members
- Manuscript drafts (`manuscript/`) — author block on title page

**Never invent co-authors.** If the project folder doesn't have them and the CV doesn't either, ask the user.

## Project page convention

The user prefers project pages **simplified to one-liner format**:

```yaml
---
title: <short title>
subtitle: With <Name>, <Name>, and <Name>.
summary: With [Name](url) (Affiliation), [Name](url) (Affiliation). One sentence on the project.
tags: [...]
date: "YYYY-MM-DD"
image:
  caption: ""
  focal_point: Smart
---
```

No long abstract paragraphs, no "Supported by:" boilerplate. Empty bodies are fine — the summary carries the content.

## Publication conventions

- `date` field controls sort order on the publications page → use **year of print publication** (not online-first date). E.g. CPS 2024 vol 57 even if online-first 2022.
- `publication` field should include `Journal, Vol(Issue): pages` — match the CV exactly.
- Author list: use `admin` for Santiago and markdown links for co-authors with personal sites:
  ```yaml
  authors:
  - "[Co-author Name](https://their-site.com)"
  - admin
  ```
- `publication_types`: `"2"` = journal article, `"3"` = preprint/working paper, `"5"` = book, `"6"` = book chapter

## CV link

The CV link in the top menu (`config/_default/menus.toml`) points to `files/cv.pdf` — i.e. the local copy at `static/files/cv.pdf`. **When the CV is updated**, re-copy it:

```bash
cp "/Users/slopezcariboni/Dropbox/Research/CV - Hompage/last_version/CV_en<YEAR>.pdf" \
   "/Users/slopezcariboni/Dropbox/Research/CV - Hompage/lopez-cariboni/static/files/cv.pdf"
```

Don't re-link to a Dropbox URL — the previous one was stale and broke silently.

## Tone / wording preferences (from past sessions)

- Role: "Full Professor" (not "Profesor Titular Gr. 5" parenthetical, not "Associate Professor").
- Bio: short, no "since 20XX" trailing clauses.
- Spanish proper nouns (Departamento, dECON, LAPolMeth, EGAP) trigger spelling warnings — ignore.

## Commit + push workflow

1. Edit files.
2. `git add` specific files (not `git add .` — keeps stray local files out).
3. Commit message: short imperative subject + bullet list of what changed. Sign with the configured Co-Authored-By trailer.
4. `git push origin master`. Site rebuilds from `master`.

Recent commit style is just "santi" but the user is fine with descriptive messages.

## Audit checklist for "sync with CV"

When asked to revise everything against the CV:

1. **Profile** (`content/authors/admin/_index.md`): role, bio, interests, organizations, education years.
2. **Experience widget** (`content/home/experience.md`): titles, date ranges.
3. **Teaching** (`content/courses/_index.md`): every course in CV's Teaching section, with current date ranges. Include Graduate Students.
4. **Projects** (`content/project/*/index.md`): one per CV "Ongoing projects" entry. Co-authors from `Papers/<Project>/`.
5. **Publications** (`content/publication/*/index.md`): every entry in CV's "Journal articles" + edited volumes/chapters. Verify `date`, `publication` (journal + Vol(Issue): pages).
6. **CV PDF** (`static/files/cv.pdf`): re-copy from `last_version/`.
