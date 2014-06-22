---
title: Slide Shows with Pandoc 
author: Dennis Tenen, Grant Wythoff
date: January 18, 2014
tags: tutorial, plain text, pandoc, slides, draft
---

# Case 1: Simple Slides

In this scenario, we will use the same Pandoc Markup plain text language to produce a slide deck that can be viewed in any desktop or mobile web browser. Several options are available to produce HTML slides, including DZ Slides, Beamer, and Slidy. A full overview of slide show formats is available online.^[<http://johnmacfarlane.net/pandoc/README.html#producing-slide-shows-with-pandoc>]. Slidy offers the simplest of the options, producing elegant, text-driven slides. More advanced readers may want to experiment with Reveal.js which offers more options, but also requires external dependencies.

For the purposes of this tutorial, let's pretend that your project.md file is now the basis for a presentation. Footnotes links and images work as they did in previous examples. The major semantic difference now is that our `# Headings` and `## Subheadings` will now become a controlling structure for slides and not for chapters or article sections. Start with the header block as before, and try something along the lines of:

```
# Part I
## Slide I.1

Some text here.

## Slide II.2
### Header 1
Some text.

### Header 2
More text.

# Part II
## Slide II.1
What an amazing slide.

## Slide II.2
Some text.
```

The first header that is followed by content is called "slide level." In our case, the slide level is two hash marks deep. All headers on the slide level will create new slides. All headers *above* the slide level (one hash mark, in our case) create new sections, while all headers below the slide level (three hash marks) create divisions within the slide. For even simpler slide control you can do something like this:

```
# Slide 1
Some text.

# Slide 2
Some text.
```

Note that for `# Slide 1` to become a slide level control it must have some content in the slide. You can also use a horizontal rule `-----` to create slides without section headers. If you need to make a note for yourself, but don't want it to show up on the slides, you can use HTML style comments like so:

```
<!-- This is a comment -->
```

We often print out our Markdown source as notes for the presentation. To convert your source Markdown file into a slide deck, run the following command in your terminal:

`$ pandoc -t slidy --self-contained project.md -o slides.html`

The `-t` flag stands for "to format," which is Slidy in our case. Slidy will generate a slide deck that can be shown or shared in any browser, obviating the need for PowerPoint or Keynote. We use the `--self-contained` flag because we want to generate a single self-contained .html file. Without it Slidy might create several support files that will clutter our project folder. Open the slides.html file in your browser and go into the full screen mode (F11 usually) for the presentation.

Once you master Slidy defaults you may want to experiment with custom CSS stylesheets or with other more sophisticated slide packages like Reveal. However, the spirit of plain text authoring encourages the writer to prefer *semantic* structures over visual embellishment. The better presentation will always be the one that is clearly organized into units that make sense to the audience. And no amount of visual embellishment will hide muddled thought. Keep your slides simple and you will find yourself spending more time on writing, rather than merely formatting, your presentation.

Case 2: Beamer 
