---
title: Sustainable Authorship in Plain Text Using Pandoc and Markdown
author: Dennis Tenen, Grant Wythoff
tags: tutorial, pandoc, plain text, draft
---

Contains the source files for the Pandoc Tutorial to appear in the Programming Historian 2. 

```
  main.md           main document
  pandoctut.bib     bibliography
  mla.csl           mla stylesheet
```

To compile run:  
`$ pandoc -S -o main.pdf --filter pandoc-citeproc main.md`
