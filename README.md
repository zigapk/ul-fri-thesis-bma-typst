# Master's Thesis template for UNI LJ FRI in Typst

Typst port of the official UL FRI master's thesis LaTeX template ([UL-FRI/thesis-BMA](https://github.com/UL-FRI/thesis-BMA)) into Typst.

## Comparison

- `output.pdf` — compiled Typst output from the sample document
- [Original LaTeX output](https://github.com/UL-FRI/thesis-BMA/blob/master/thesis_template.pdf) — the reference PDF from the official LaTeX template

## Quick start

```typ
#import "template/lib.typ": *

#let config = (
  title: "Naslov magistrskega dela",
  title-en: "English Title",
  author: "Ime Priimek",
  email: "ime.priimek@example.com",
  year: "2026",
  keywords: "ključna, beseda",
  keywords-en: "key, word",
  supervisor: "doc. dr. Ime Priimek",
  cosupervisor: none,
  program: "MAGISTRSKI ŠTUDIJSKI PROGRAM DRUGE STOPNJE\nRAČUNALNIŠTVO IN INFORMATIKA",
  track: "Računalništvo in Informatika",
  code-published: true,
  code-url: "https://github.com/...",
)

#show: thesis.with(config: config)

// Front pages
#title-page(config: config)
#copyright-page(config: config)
#acknowledgments-page()[Your acknowledgments here.]
#dedication-page()[Your dedication here.]

// Table of contents
#set page(numbering: none, header: none, footer: none)
#outline(title: "Kazalo", depth: 2, indent: 1.5em)
#clear-empty-double-page()

// Abbreviations
#abbreviations-page((
  ("SVM", [support vector machine], [metoda podpornih vektorjev]),
))

// Abstracts
#povzetek(config: config)[Povzetek v slovenščini.]
#abstract-page(config: config)[Abstract in English.]

// Main matter
#set page(numbering: "1", header: mainmatter-header, footer: mainmatter-footer)
#counter(page).update(1)
#set heading(numbering: "1.1")
#set ref(supplement: none)

#include "chapters/introduction.typ"
// ...

// Appendix
#set heading(numbering: "A.1")
#counter(heading).update(0)
#set figure(numbering: dependent-numbering("A.1"))
#set math.equation(numbering: dependent-numbering("(A.1)"), supplement: none)

#include "chapters/appendix.typ"

// Bibliography
#set heading(numbering: none, outlined: false)
#bibliography("bibliography.bib", title: "Literatura", style: "template/elsevier-with-titles.csl", full: true)
```

## Using in your thesis

Add this repository as a git submodule in your thesis project:

```sh
git submodule add https://github.com/<user>/unilj-fri-thesis-bma.git template
```

Then import from the submodule:

```typ
#import "template/lib.typ": *
```

If you need to modify the template, edit the submodule directly and push your changes.

## Compiling

```sh
typst compile main.typ output.pdf
```

## Structure

```
template/
  typst.toml              Package manifest
  lib.typ                 Package entrypoint (re-exports everything)
  style.typ               Page setup, fonts, headings, TOC, headers/footers
  front.typ               Title page, copyright, acknowledgments, dedication, abbreviations
  abstract.typ            Povzetek + Abstract
  elsevier-with-titles.csl  Bibliography style (Elsevier numeric with titles)
  assets/cc-licenca/      CC license icons

main.typ                  Sample document (for comparison with LaTeX template)
chapters/                 Sample chapter files
bibliography.bib          Sample bibliography
figures/                  Sample figures
output.pdf                Compiled sample output
```

## Bibliography

The template uses the `elsevier-with-titles` CSL style, which is the standard CSL equivalent of the `elsarticle-num` BibTeX style specified in the official LaTeX template.

## License

MIT
