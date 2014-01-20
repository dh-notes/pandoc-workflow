---
title: Sustainable Authorship in Plain Text Using Pandoc and Markdown
author: Dennis Tenen, Grant Wythoff
date: January 20, 2014
tags: tutorial, pandoc, plain text, draft
---

# Philosophy
Some positive stuff.

Writing, storing, and retrieving documents are activities central to the humanities research workflow. And yet, many scholars base their practice on proprietary tools and formats that fall short of even the most basic requirements of academic writing. The reader will relate to being frustrated with the fragility of footnotes, bibliographies, figures, and book drafts authored in MS Word. Still, most journals insist on submissions in .docx format. More than causing personal frustration, the reliance on fragile tools and formats has long-term negative implications for the community. In such an environment, journals must outsource typesetting, alienating authors from the material contexts of publication and furthermore adding unnecessary barriers to the unfettered circulation of knowledge. Closed formats ultimately lead to closed intellectual communities.^[See <http://www.antipope.org/charlie/blog-static/2013/10/why-microsoft-word-must-die.html> for an extended discussion of this topic.]

In this tutorial, we would like to suggest an alternative workflow built around open-source tools and transparent formats. 

# Target Audience
Professional writers and researchers constitute our primary audience. The tutorial assumes no prior technical knowledge, but can scale with experience. We often suggest more advanced techniques towards the end of each section. These are clearly marked, and can be returned to after some practice and experimentation.

A secondary objective in writing this tutorial was to introduce the Markdown + Pandoc combination to journal and book editors. Although not covered in this tutorial, Pandoc offers a powerful template system (through LaTeX), which can be used to greatly streamline workflows particular to academic publishing. In a perfect world, journals would accept paper submissions in Markdown and run batch Pandoc processes to normalize for style and formatting. Getting familiar with the mechanics of writing in plain text is a good first step towards that vision.

# Principles
Inspired by best practices in a variety of disciplines, we were guided by the following principles:

1. *Preference for human-readable formats.* When writing in Word or Google Docs, what you see is not what you get. The .doc file contains hidden, automatically-generated formatting characters. When things go wrong, the obfuscated typesetting layer is difficult for the user to troubleshoot. Something as simple as dropping in an image or pasting text can entirely throw off your document's formatting.

2. *Leveraging the transparency and sustainability of plain-text.* Plain text both ensures transparency and answers the standards of long-term preservation. MS Word may go the way of Word Perfect in the future, but plain text will always remain easy to read, catalog, mine, and transform. Furthermore, plain text enables easy and powerful versioning of the document, which is useful in collaboration and organizing drafts. Your plain text files will be accessible on cell phones, tablets, or, perhaps, on a low-powered terminal in some remote library. Plain text is backwards compatible and future proof. Whatever software or hardware comes along next, it will be able to understand your plain text files.

3. *Separation of form and content.* Writing and formatting at the same time is distracting. The idea is to write first, and format later, as close as possible to the time of publication. A task like switching from Chicago to MLA formatting should be painless. Journal editors who want to save time on needless formatting and copy editing should be able to provide their authors with a formatting template which takes care of the typesetting minutia.

4. *Support for the academic apparatus.* The workflow needs to handle footnotes, figures, international characters, and bibliographies gracefully.

5. *Platform independence: one source many destinations.* As the vectors of publication multiply, we need to be able to generate a multiplicity of formats including for slide projection, print, web, and mobile. Ideally, we would like to be able to generate the most common formats without breaking bibliographic dependencies. Our workflow needs to be portable as well--it would be nice to be able to copy a folder to a thumbdrive and know that it contains everything needed for publication. Writing in plain text means you can easily share, edit, and archive your documents in virtually any environment.

Markdown and LaTeX answer all of these requirements. We choose to author the primary text in Markdown (and not LaTeX) because it offers the most light-weight and clutter free syntax (hence, mark  *down*) and because when coupled with Pandoc it allows for the greatest flexibility in outputs (including .docx and .tex files).^[There are no good solutions for directly arriving at MS Word from LaTeX.]

# Use cases
In this tutorial, you will learn to use Pandoc--a command line tool that converts plain text files a number of beautifully formatted file types: PDF, .docx, HTML, .tex, slide decks, and more.^[<http://johnmacfarlane.net/pandoc/>]

We will cover three use cases here. In the first, you will learn the basics of markdown--an easy to read and write plain text markup syntax--and use Pandoc to generate a simple .docx or .pdf file.^[Don't worry if you don't understand some of of this terminology yet!] In the second, we will add some figures and bibliography, generate an MS Word document, and then change the citation style form Chicago to MLA. Finally, we will use Pandoc create some attractive slides for a presentation.

As a side-effect of this tutorial, you will be introduced to the basics of command line file management--a skill necessary for many more advanced research workflows.


# Software requirements

You will need to use your search engine and the links provided in the footnotes to install the following software on your computer:

* A **plain text editor**. Entering the world of plain-text editing expands your choice of innovative authoring tools dramatically. Search online for "markdown text editor" and experiment with your options. It does not matter what you use as long as it is explicitly a plain text editor.

* **Unix terminal emulator**. Working "in the command line" is equivalent to typing commands into the terminal. On a Mac you simply need to use your finder for "Terminal". On Windows, use PowerShell. Linux users are likely to be familiar with their terminals already.

* **Pandoc**.^[Detailed, platform-specific installation instructions available at <http://johnmacfarlane.net/pandoc/installing.html>.] Pandoc was created and is maintained by John MacFarlane, Professor of Philosophy at the University of California, Berkeley. This is humanities computing at its best and will serve as the engine of our workflow. With Pandoc, you will be able to compile text and bibliography into beautifully formatted and flexible documents. To verify that Pandoc is installed, enter `pandoc --version` into the command line.

* **LaTeX**.^[Detailed, platform-specific installation instructions available at <http://johnmacfarlane.net/pandoc/installing.html>.] Although LaTeX is not covered in this tutorial, it is used by Pandoc for .pdf creation. Advanced users will often convert into LaTeX directly to have more granular control over the typesetting of the .pdf. Beginners may want to consider skipping this step. Otherwise, type `latex -v` to see if LaTeX was installed correctly (you will get an error if it was not and some information on the version if it was).

* **Zotero or Endnote**. Bibliographic reference software like Zotero and Endnote are indispensable tools for organizing and formatting citations in a research paper. These programs can export your libraries as a BibTeX file (which you will learn more about in Case 2 below). This file, itself a formatted plain text document of all your citations, will allow you to quickly and easily cite references using @tags. It should be noted that it's also possible to type all of your bibliographic references by hand, which some readers may prefer when working with non-standardized premodern sources or character encodings. For an example of how to format your bibliographic citation file by hand, *you can download this sample BibTeX file.*

With this in mind, we purposefully omit some of the granular, platform- or hardware-bound details. For example, it makes no sense to provide installation instructions for Notepad++, when the Notepad++ website will always have instructions that are both more current and more complete. Similarly, the mechanics of Pandoc markdown are best explored by searching for "Pandoc markdown" on Google, with the likely first result being Pandoc's homepage. Instead of following the tutorial in a mechanical way, you should strive to understand the solutions offered here as a methodology, which may need to be tailored further to fit your environment.

# Markdown basics

In this first section, we will learn the basics of writing in Markdown syntax.

To begin, create a new folder, or "directory", for this project. You are likely to have some system of organizing your documents, projects, illustrations, and bibliographies. But often, your document, its illustrations, and bibliography live in different folders, which makes them hard to track. Our goal is to create a single folder for each project, with all relevant materials included. This will allow you to call a variety of elements (i.e. an image or a citation) easily and succinctly within the body of your plain text document.

Markdown is a convention for structuring your plain-text documents semantically. The idea is to identify logical structures in your document (a title, sections, subsections, footnotes, etc.), mark them with some unobtrusive characters, and then "compile" the resulting text with a typesetting interpreter which will format the document consistently, according to a specified style.

Markdown conventions come in several "flavors" designed for use in particular contexts, such as blogs, wikis, or code repositories. Pandoc is one such flavor of Markdown, geared for academic use. Its conventions are described one the "Pandoc's Markdown" page on John MacFarlane's website.^[<http://johnmacfarlane.net/pandoc/demo/example9/pandocs-markdown.html>]

Let's now create a simple document in Markdown. Open a plain-text editor of your choice and begin typing. The markdown document begins with a title block that should look like this:^[Search for "pandoc YAML block" for an alternative and more powerful way to format the title block. Using the YAML title block will allow you to specify the bibliography in the header, rather than through the command line.]

```
% Plain Text Workflow
% Dennis Tenen, Grant Wythoff
% January 20, 2014
```

Pandoc-flavored Markdown automatically interprets the first header line as your title, second as author, and third as date. Let's suppose our document contains three sections, each subdivided into two subsections. Leave a blank line after the date and type something like this:

```
# Section 1
## Subsection 1.1
## Subsection 1.2
# Section 2
# Section 3
```

Go ahead and enter some dummy text as well. You can use asterisks to add bold or italicized emphasis to your words, like this: `*italics*` and `**bold**`. We should also add a link and a footnote to our text to to cover the basic components of an average paper. Type:  `Needs a note.^[my first footnote!]` and `My first [link](www.eff.com)`.^[When the text of the link and the address are the same it is faster to write `<www.eff.org>`]

Finally, let's add an illustration. Copy an image (any small image) to your folder, and type in `![image caption](your_image.jpg)`. When you are done types let's save the document as `project.md`, where .md stands for Markdown. Next, save a couple images you'd like to use in your document to this folder for later use.

If you'd like to get an idea of how this markup will be interpreted as HTML formatting, try [this online sandbox](http://daringfireball.net/projects/markdown/dingus) and play around with various kinds of syntax.  Move on once you're comfortable with the basics.  Remember that certain elements of *Pandoc*-flavored Markdown (such as the title block and footnotes) will not work in this web form, which only covers the basics.

There are programs that allow you to watch a live preview of Markdown output as you edit your plain text file.,  But in order to maintain full control over your files and take advantage of Pandoc's ability to support the complete scholarly apparatus, from bibliographies to illustrations, we recommend that you stick with simple, plain text files stored on your computer.  The workflow we outline here uses only free and open source tools created by and for the academic community.

So let's see what Pandoc allows us to do with our Markdown file.

# Getting in touch with your inner terminal

(If you are already familiar with the using command line, feel free to skip this section.) Modern operating systems are designed to obscure the file structure on your hard drive. There is a good reason for this: many system files have long and confusing names, and should not be touched. Taking a few moments to get in touch with your filing system will help orient your activities immensely. You need to learn only a few commands to get started. 

First, open your terminal window. You should see a prompt that looks something like this: `computer-name:~username $`. The tilde indicates your "home" directory,^[In fact you can type `$ cd ~` at any point to return to your home directory.]. The dollar sign is just a prompt for you to type something. The dollar sign in the instructions indicates you must type what follows into the terminal prompt (as opposed to typing it into your document). It is very likely that your "Documents" folder is located here. Type `$ pwd` and then hit enter to list the full name of your working directory. Use `$ pwd` whenever you feel lost in the command prompt.

The next command is `$ ls` (list) which simply lists the files in the current directory.^[Remember to hit enter after every command.] Finally, you can type `$ cd DIRECTORY_NAME` to change directory and `$ cd ..` to go back up the folder structure.^[Readers already familiar with the terminal should experiment with `$ pushd`, `$ popd`, and `$ cd -`.] Once you start typing the directory name, use the *tab* key to auto complete the text--this is particularly useful for long directory names, or directories names that contain spaces.^[It is a good idea to get into the habit of not using spaces in folder or file names. Dashes-or_underscores instead of spaces in your filenames ensure lasting cross-platform compatibility.]

These three terminal commands: `pwd`,  `ls`,  and `cd` are all you need for this tutorial. Practice them for a few minutes to navigate your documents folder and think about they way you have organized your files. At some point you should raise your terminal awareness by going through Zed. A. Shaw's excellent *Command Line Crash Course.*^[<http://cli.learncodethehardway.org/book/>].

# Using Pandoc to convert Markdown to an MS Word document

We are now ready to cast our first conversion. Open your terminal window, use `$ pwd` and `$ cd` to navigate to the correct folder for your project. Once you are there, type `$ ls` in the terminal to list the files. If you see your .md and your images, you are in the right place. To convert .md into .docx type `$ pandoc -o project.docx project.md`. Open the file with MS Word to check your results. Alternatively, you can run `$ pandoc -o project.odt project.md` if you would like to produce an Open Office document, the open source alternative to MS Word.^[For more on Open Office, see <http://www.openoffice.org/why/index.html>.]

If you are not familiar with command line tools, imagine reading the above command as saying something like: "Pandoc, create an MS Word file out of my Markdown file." The `-o` part is a "flag," which in this case says something like "instead of me explicitly telling you the source and the target file formats, just guess by looking at the file extension." Many options are available through such flags in Pandoc. You can see the complete list on Pandoc's website^[<http://johnmacfarlane.net/pandoc/README.html>] or by typing `$ man pandoc` in the terminal.

The structure of this command works the same way in producing a PDF from your Markdown file.  This time, try `$ pandoc -o project.pdf project.md`, and you will have a beautifully formatted PDF of the document now saved in your project directory.

More advanced users who have LaTeX installed may want to experiment by converting Markdown into .tex or specially formatted .pdf files. You can, for example, specify a LaTeX style file (saved to the same directory), and run something like:

`$ pandoc -H format.sty -o project.pdf --number-sections --toc project.tex`

At this point, you should spend some time exploring some of other features of Markdown like quotations (referenced by `>` symbol), bullet lists which start with `*`, verbatim line breaks which start with `|` (useful for poetry), tables, and a few of the other functions listed on the Pandoc's markdown page. Pay particular attention to empty space and the flow of paragraphs. The documentation puts it succinctly when it defines a paragraph to be "one or more lines of text followed by one or more blank line." Note that "newlines are treated as spaces" and that "if you need a hard line break, put two or more spaces at the end of a line." The best way to understand what that means is to experiment freely. Use your editor's preview mode or just run Pandoc to see the results of your experiments.

Above all, avoid the urge to format. Remember that you are identifying *semantic* units: sections, subsections, emphasis, footnotes, and figures.^[Even `*italics*` and `**bold**` in Markdown are not really formatting marks, but indicate different level of *emphasis*.] The formatting will happen later, once you know the venue and the requirements of publication.

# Working with Bibliographies

In this section, we will add a bibliography to our document and then convert from Chicago to MLA formats.

If you are not using a reference manger like Endnote or Zotero, you should. Zotero slots into the free software toolkit much better than most of its for-profit competitors. Like Pandoc, it was created by the academic community, which welcomes efforts to extend the tool's functionality. Go ahead and open a reference manager of your choice and add some sample entries. When you are ready, find the option to export your bibliography in BibTeX (.bib) format. Save your .bib file in your project directory, and give it a reasonable title like "project.bib".

The general idea is to use Zotero as a sort of a "master list" for your references, and to generate these much smaller .bib files that will live in the same directory as your project. Go ahead and open your .bib file with the plain-text editor of your choice.^[Note that the .bib extension may be "registered" to Zotero in your operating system. That means when you click on a .bib file it is likely that Zotero will be called to open it, whereas we want to open it within a text editor. Eventually, you may want to associate the .bib extension with your text editor.] Your .bib file should contain multiple entries that look something like this:  

```
@article{fyfe_digital_2011,
	title = {Digital Pedagogy Unplugged},
	volume = {5},
	url = {http://digitalhumanities.org/dhq/vol/5/3/000106/000106.html},
	number = {3},
	urldate = {2013-09-28},
	author = {Fyfe, Paul},
	year = {2011},
	file = {fyfe_digital_pedagogy_unplugged_2011.pdf}
}
```

Take a moment to orient yourself here. You will rarely have to edit these by hand, but it is important to understand that .bib is another convention for keeping your bibliographies organized. Each entry consists of a document type, "article" in our case, a unique identifier (fyfe_digital_2011), and the relevant meta-data on title, volume, author, and so on. The thing we care most about is the unique ID which immediately follows the curly bracket in the first line of each entry. The unique ID is what allows us to connect the bibliography with the main document. Leave this file open for now and go back to your main project.md file.

Edit the footnote in the first line of your main .md file to look like something like this, where `@fyfe_digital_2011` is replaced with one of the unique IDs from your .bib file:

`Some sentence that needs citation.^[@fyfe_digital_2011 argues that too.]`

Once we run the markdown through Pandoc, "@fyfe_digital_2011" will be expanded to a full citation in the style of your choice. To generate a bibliography simply include a section called `# Bibliography` at the end of document.

Let's see if this works. Save your file, switch to the terminal window and run:

 `$ pandoc -S --biblio project.bib project.md -o project.docx`.

The upper case `S` flag stands for "smart", a mode which produces "typographically correct output, converting straight quotes to curly quotes, \-\-\- to em-dashes, \-\- to en-dashes and \.\.\. to ellipses." The `biblio` flag tells pandoc where we are keeping our bibliography, and you should already be familiar with `-o` from previous examples.^[Note that you can skip the "biblio" flag if you are specifying the path to .bib in your YAML header block.] The result should be a decently formatted MS Word file. If you have LaTeX installed, convert into .pdf using the same syntax for prettier results. Do not worry if things are not exactly the way you like them--remember, you are going to fine-tune the formatting at later, as close as possible to the time of publication. For now we are just creating drafts based on reasonable defaults.

Note that if you decide to use a YAML metadata header rather than the simple title block, you can call this bibliography file directly in the document rather than in your compile command.  So, rather than 

```
% Plain Text Workflow
% Dennis Tenen, Grant Wythoff
% January 20, 2014
```

you would use

```
---
title: Plain Text Workflow
author: |
    Dennis Tenen\
    Grant Wythoff
date: January 20, 2014
bibliography: project.bib
---
```

Recall that a `|` flag tells Pandoc to interpret line breaks as written, so that the two author's names appear on separate lines.

Thus a file with the YAML metadata header written as above and compiled with the command `$ pandoc -S project.md -o project.docx` would produce the same results as a file with a simple title block and the command `$ pandoc -S --biblio project.bib project.md -o project.docx`. Experiment with both: the choice is up to the user's preference.

## Changing citation styles

The default citation style in Pandoc is Chicago author-date. We can specify a different style by using stylesheet, written in a "citation style language" (yet another plain-text convention, in this case for describing citation styles) and usually denoted by the .csl file extension. Luckily, there is an organization that maintains an archive of common citation styles, some even tailored for specific journals. Visit <http://editor.citationstyles.org/about/> to find the .csl file for Modern Language Association, download `modern-language-association.csl`, and save to your project directory as `mla.csl`. Now we need to tell Pandoc to use the MLA stylesheet instead of the default Chicago. We do this by passing the `--csl` flag:

`$ pandoc -S --biblio project.bib --csl mla.csl project.md -o project.docx`

Parse the command into English as you are typing. In my head, I translate the above into something like: "Pandoc, be smart about formatting, take the bibliography from project.bib using the MLA stylesheet, and convert my Markdown file into MS Word (as you can guess from the extension)." As you get more familiar with citation stylesheets, consider adding your custom-tailored .csl files for journals in your field to the archive as a service to the community.

This citation style file can also be declared in the YAML metadata header, rather than in the compile command, using `csl: mla.csl`.  Your header would now read:

```
---
title: Plain Text Workflow
author: |
    Dennis Tenen\
    Grant Wythoff
date: January 20, 2014
bibliography: project.bib
csl: mla.csl
---
```

# Summary

To recapitulate: you now have a project directory which contains a number of "source" files, your `project.md` file, `project.bib` file, a `.csl` file, some images, along with some "target" files which we created during the tutorial, such as the `project.docx`, `project.pdf`, and `slides.html`. You are also able to write papers in Markdown, to create drafts in multiple formats, to add bibliographies, to change citation styles, and to create slide decks for presentations.

# Useful Resources
Pandoc can handle many more formats that are worth exploring. Your notes, blog entries, code documentation, and wikis can all be authored in Markdown. Increasingly, many platforms like Wordpress and GitHub render Markdown natively. In the long term, your research will benefit from such unified workflows, making it easier to save, search, share, and organize your materials.^[The source files for this document can be found on <https://github.com/dhcolumbia/pandoc-workflow>. Use the "raw" option when viewing in GitHub to see the source Markdown. The authors would like to thank Alex Gil, his colleagues from Columbia's Digital Humanities Center, and the participants of openLab at the Studio in the Butler library for testing the code in this tutorial on a variety of platforms.]

Markdown is enjoying a period of growth at the moment, not just as a tool for writing scholarly papers but as a convention for online editing in general. Major sites like Reddit, GitHub, and Wordpress support Markdown authorship natively. It is now possible to write a wide range of documents: articles, blog posts, wikis, syllabi, and recommendation letters in one format, subject to unified workflows of search, discovery, backup, and distribution. The popularity of Markdown in such diverse contexts has led to a diverse and innovative ecosystem of support authoring tools, support groups, and publishing platforms. 

There is no better place to start looking for support than John MacFarlane's [site](https://leanpub.com/) and the affiliated [mailing list](https://groups.google.com/forum/#!forum/pandoc-discuss). At least two "Question and Answer" type sites can field questions on Pandoc: [Stack Overflow](http://stackoverflow.com/questions/tagged/pandoc) and [Digital Humanities Q&A](http://digitalhumanities.org/answers/). Finally, a group of friendly regulars staff the #Pandoc channel on Freenode IRC. 

Although we suggest starting out with a simple editor, many (70+, according to [this blog post](http://web.archive.org/web/20140120195538/http://mashable.com/2013/06/24/markdown-tools/)) other, Markdown-specific alternatives to MS Word are available online, and often free of cost. From these, we liked Mou . Draft, Authorea, 

Esuch as [Marked](http://marked2app.com/) (Mac, proprietary), [Markdown Pro](http://www.markdownpro.com/) (Mac, proprietary), and [nvALT](http://brettterpstra.com/projects/nvalt/) (Mac, free). Several web-based platforms have recently emerged that provide slick, graphic interfaces for collaborative writing and version tracking using Markdown, like [Authorea](https://www.authorea.com/), [Penflip](https://www.penflip.com/), [Draft](https://draftin.com/), and [Editorially](https://editorially.com/).ditors
Platforms
Get Involved

 we suggest learning about the Freenode Internet Relay Chat (IRC) servers, a helpful online community that is often willing to help with many of the tools discussed in this article.^[<irchelp.org> can help you get started with IRC.] Generally, your troubleshooting heuristic should start with googling the exact error message (by using double quotes in Google), asking the IRC channel, and then posting to relevant Q&A sites like Stack Exchange or Digital Humanities Questions & Answers. Finally, if all else fails, we are happy to answer your questions directly by email.
