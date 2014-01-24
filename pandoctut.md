---
title: Sustainable Authorship in Plain Text Using Pandoc and Markdown
author: Dennis Tenen, Grant Wythoff
date: January 20, 2014
tags: tutorial, pandoc, plain text, draft
bibliography: pandoctut.bib
---

![The Lexoriter system, c. 1983. From @price_definitive_1984.](lexoriter.jpg)

# Philosophy
Markdown is a syntax for formatting plain text files that is currently enjoying a period of growth, not just as a tool for writing scholarly papers but as a convention for online editing in general. Major sites like Reddit, GitHub, and Wordpress support Markdown authorship natively. It is now possible to write a wide range of documents in one format -- articles, blog posts, wikis, syllabi, and recommendation letters -- using the same set of tools and techniques to search, discover, backup, and distribute our materials. The popularity of Markdown in such diverse contexts has led to a rich ecosystem of practitioners, authoring tools, and publishing platforms.

Although Markdown's rising popularity is relatively recent, plain text has been around since the electronic typewriter. It is still possible to open a file written in any number of "dead" plain text word processors from the past several decades: AlphaPlus, Perfect Writer, Text Wizard, Spellbinder, WordStar or Isaac Asmiov's favorite SCRIPSIT 2.0, made by Radio Shack.  But opening a turn of the 21st century document written in Word Perfect or Apple's Pages may cause problems.

Writing, storing, and retrieving documents are activities central to the humanities research workflow. And yet, authors base their practice on proprietary tools and formats that fall short of even the most basic requirements of scholarly writing. The reader will relate to being frustrated with the fragility of footnotes, bibliographies, figures, and book drafts authored in MS Word. Still, most journals insist on submissions in .docx format. More than causing personal frustration, this reliance on fragile tools and formats has long-term negative implications for the academic community. In such an environment, journals must outsource typesetting, alienating authors from the material contexts of publication and furthermore adding unnecessary barriers to the unfettered circulation of knowledge. Closed formats ultimately lead to closed intellectual communities.^[See <http://www.antipope.org/charlie/blog-static/2013/10/why-microsoft-word-must-die.html> for an extended discussion of this topic.]

Not only does writing in plain text guarantee that your files will remain readable ten, fifteen, twenty years from now, it also allows you to simply and easily share every element of the scholarly apparatus across all possible platforms, from bibliographies to illustrations to citation styles.  In this tutorial, we outline a workflow that frees the researcher from proprietary word processing software and fragile file formats. This alternative workflow is built entirely around open-source tools and transparent formats.

# Target Audience
Professional writers and researchers constitute our primary audience. The tutorial assumes no prior technical knowledge, but can scale with experience. We often suggest more advanced techniques towards the end of each section. These are clearly marked, and can be revisited after some practice and experimentation.

A secondary objective in writing this tutorial is to introduce the Markdown + Pandoc combination to journal and book editors. Although not covered in this tutorial, Pandoc offers a powerful template system (through LaTeX), which can be used to greatly streamline workflows particular to academic publishing. In a perfect world, journals would accept paper submissions in Markdown and run batch Pandoc processes to normalize for style and formatting. Getting familiar with the mechanics of writing in plain text is a good first step towards that vision.

# Principles
Inspired by best practices in a variety of disciplines, we were guided by the following principles:

1. *Preference for human-readable formats.* When writing in Word or Google Docs, what you see is not what you get. The .doc file contains hidden, automatically-generated formatting characters. When things go wrong, the obfuscated typesetting layer is difficult for the user to troubleshoot. Something as simple as dropping in an image or pasting text can entirely throw off your document's formatting.

2. *Sustainability.* Plain text both ensures transparency and answers the standards of long-term preservation. MS Word may go the way of Word Perfect in the future, but plain text will always remain easy to read, catalog, mine, and transform. Furthermore, plain text enables easy and powerful versioning of the document, which is useful in collaboration and organizing drafts. Your plain text files will be accessible on cell phones, tablets, or, perhaps, on a low-powered terminal in some remote library. Plain text is backwards compatible and future proof. Whatever software or hardware comes along next, it will be able to understand your plain text files.

3. *Separation of form and content.* Writing and formatting at the same time is distracting. The idea is to write first, and format later, as close as possible to the time of publication. A task like switching from Chicago to MLA formatting should be painless. Journal editors who want to save time on needless formatting and copy editing should be able to provide their authors with a formatting template which takes care of the typesetting minutia.

4. *Support for the academic apparatus.* The workflow needs to handle footnotes, figures, international characters, and bibliographies gracefully.

5. *Platform independence: one source many destinations.* As the vectors of publication multiply, we need to be able to generate a multiplicity of formats including for slide projection, print, web, and mobile. Ideally, we would like to be able to generate the most common formats without breaking bibliographic dependencies. Our workflow needs to be portable as well--it would be nice to be able to copy a folder to a thumbdrive and know that it contains everything needed for publication. Writing in plain text means you can easily share, edit, and archive your documents in virtually any environment.

Markdown and LaTeX answer all of these requirements. We chose Markdown (and not LaTeX) because it offers the most light-weight and clutter free syntax (hence, mark  *down*) and because when coupled with Pandoc it allows for the greatest flexibility in outputs (including .docx and .tex files).^[There are no good solutions for directly arriving at MS Word from LaTeX.]

# Objectives
In this tutorial, you will first learn the basics of markdown--an easy to read and write plain text markup syntax--and next use Pandoc to generate a simple .doc or .pdf file.  Pandoc is a command line tool that converts plain text files into a number of beautifully formatted file types: PDF, .docx, HTML, .tex, slide decks, and more.^[<http://johnmacfarlane.net/pandoc/>] ^[Don't worry if you don't understand some of of this terminology yet!] You will then learn to add figures and bibliography, and finally change the citation style from Chicago to MLA.

A bonus of this tutorial is that you will be introduced to the basics of command line file management--a skill necessary for many more advanced research workflows.

# Software requirements

You will need to use your search engine and the links provided in the footnotes to install the following software on your computer:

* A **plain text editor**. Entering the world of plain-text editing expands your choice of innovative authoring tools dramatically. Search online for "markdown text editor" and experiment with your options. It does not matter what you use as long as it is explicitly a plain text editor.

* **Unix terminal emulator**. Working "in the command line" is equivalent to typing commands into the terminal. On a Mac you simply need to use your finder for "Terminal". On Windows, use PowerShell. Linux users are likely to be familiar with their terminals already. We will cover the basics of how to find and use the command line below.

* **Pandoc**. Detailed, platform-specific installation instructions are available at <http://johnmacfarlane.net/pandoc/installing.html>. *Installation of Pandoc on your machine is crucial for this tutorial*, so be sure to take your time and click through the instructions. Pandoc was created and is maintained by John MacFarlane, Professor of Philosophy at the University of California, Berkeley. This is humanities computing at its best and will serve as the engine of our workflow. With Pandoc, you will be able to compile text and bibliography into beautifully formatted and flexible documents. Once you've followed the installation instructions, verify that Pandoc is installed by entering `pandoc --version` into the command line. We assume that you have at least version 1.12.3, released in January 2014.

* **LaTeX**. Detailed, platform-specific installation instructions available at <http://johnmacfarlane.net/pandoc/installing.html>. Although LaTeX is not covered in this tutorial, it is used by Pandoc for .pdf creation. Advanced users will often convert into LaTeX directly to have more granular control over the typesetting of the .pdf. Beginners may want to consider skipping this step. Otherwise, type `latex -v` to see if LaTeX was installed correctly (you will get an error if it was not and some information on the version if it was).

* **Zotero or Endnote**. Bibliographic reference software like Zotero and Endnote are indispensable tools for organizing and formatting citations in a research paper. These programs can export your libraries as a BibTeX file (which you will learn more about in Case 2 below). This file, itself a formatted plain text document of all your citations, will allow you to quickly and easily cite references using `@tags`. It should be noted that it's also possible to type all of your bibliographic references by hand, using [our bibliography](https://github.com/dhcolumbia/pandoc-workflow/blob/master/pandoctut.bib) as a template.

We purposefully omit some of the granular, platform- or operating system-bound details of software installation. For example, it makes no sense to provide installation instructions for LaTeX, when the online instructions for your operating system will always remain more current and more complete. Similarly, the mechanics of Pandoc markdown are best explored by searching for "Pandoc markdown" on Google, with the likely first result being Pandoc's homepage. Instead of following the tutorial in a mechanical way, we recommend you strive to understand the solutions offered here as a methodology, which may need to be tailored further to fit your environment.

# Markdown basics

In this first section, we will learn the basics of writing in Markdown syntax.

To begin, create a new folder that will house this project. You are likely to have some system of organizing your documents, projects, illustrations, and bibliographies. But often, your document, its illustrations, and bibliography live in different folders, which makes them hard to track. Our goal is to create a single folder for each project, with all relevant materials included. This will allow you to call a variety of elements (i.e. an image or a citation) easily and succinctly within the body of your plain text document, and, later, to share the whole thing as a stand-alone package. The general rule of thumb is one paper, one folder.

Markdown is a convention for structuring your plain-text documents semantically. The idea is to identify logical structures in your document (a title, sections, subsections, footnotes, etc.), mark them with some unobtrusive characters, and then "compile" the resulting text with a typesetting interpreter which will format the document consistently, according to a specified style.

Markdown conventions come in several "flavors" designed for use in particular contexts, such as blogs, wikis, or code repositories. Pandoc is one such flavor of Markdown, geared for academic use. Its conventions are described one the "Pandoc's Markdown" page on John MacFarlane's website.^[<http://johnmacfarlane.net/pandoc/demo/example9/pandocs-markdown.html>] Take the time to read through the documents there before continuing with the tutorial.

Let's now create a simple document in Markdown. Open a plain-text editor of your choice and begin typing. The markdown document begins with something called a ["YAML"](https://en.wikipedia.org/wiki/YAML) block, which contains some useful metadata. It should look like this:

```
---
title: Plain Text Workflow
author: Dennis Tenen, Grant Wythoff
date: January 20, 2014
---
```

Pandoc-flavored Markdown stores each of the above values, and "prints" them in the appropriate location of your outputted document once you are ready to typeset. We will later learn to add other, more powerful fields to the YAML block. For now, let's pretend we are writing a paper that contains three sections, each subdivided into two subsections. Leave a blank line after last three dashes in the YAML block and type:

```
# Section 1

## Subsection 1.1
Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium doloremque laudantium, totam rem aperiam, eaque ipsa quae ab illo inventore veritatis et quasi architecto beatae vitae dicta sunt explicabo. Nemo enim ipsam voluptatem quia voluptas sit aspernatur aut odit aut fugit, sed quia consequuntur magni dolores eos qui ratione voluptatem sequi nesciunt. Neque porro quisquam est, qui dolorem ipsum quia dolor sit amet, consectetur, adipisci velit, sed quia non numquam eius modi tempora incidunt ut labore et dolore magnam aliquam quaerat voluptatem. Ut enim ad minima veniam, quis nostrum exercitationem ullam corporis suscipit laboriosam, nisi ut aliquid ex ea commodi consequatur?

## Subsection 1.2

# Section 2

# Section 3
```

Go ahead and enter some dummy text as well. Empty space is meaningful in Markdown: do not indent your paragraphs. Instead, separate paragraphs by using an blank line. Blank lines must also precede section headers.

You can use asterisks to add bold or italicized emphasis to your words, like this: `*italics*` and `**bold**`. We should also add a link and a footnote to our text to to cover the basic components of an average paper. Type:  

`Needs a note.^[my first footnote!]`

and

`My first [link](www.eff.com)`.^[When the text of the link and the address are the same it is faster to write `<www.eff.org>`]

Finally, let's add an illustration. Copy an image (any small image) to your folder, and type in 

`![image caption](your_image.jpg)`

The exclamation mark signals an image. Let's now save the document as `main.md`, where .md stands for Markdown. Next, save a couple images you'd like to use in your document to this folder for later use.

If you'd like to get an idea of how this markup will be interpreted as HTML formatting, try [this online sandbox](http://daringfireball.net/projects/markdown/dingus) and play around with various kinds of syntax.  Move on once you're comfortable with the basics.  Remember that certain elements of *Pandoc*-flavored Markdown (such as the title block and footnotes) will not work in this web form, which only accepts the basics.

There are programs that allow you to watch a live preview of Markdown output as you edit your plain text file, which we detail below in the Useful Resources section. Few of them support footnotes, figures, and bibliographies however. To take full advantage of Pandoc, we recommend that you stick with simple, plain text files stored locally, on your computer. 

Let's see what Pandoc can do with Markdown.

# Getting in touch with your inner terminal
The command line is a friendly place, once you get used to it. If you are already familiar with using the command line, feel free to skip this section. For others, it is important to understand that modern operating systems are designed to obscure the file structure on your hard drive. There is a good reason for this: many system files have long and confusing names, and should not be touched. But, understanding where your files "live" on the disk will help orient your activities immensely. Interacting with the command line directly will introduce you to a range of powerful tools that can serve as a basis for more advanced work. For the purposes of this tutorial, you need to learn only a few, very simple commands.

First, open a command line window. If you are using a Mac, open Terminal in the ‘Applications/Utilities’ directory. On Windows, you'll use PowerShell. On Windows 7 or later, click Start, type "powershell" in "Search programs and files," and hit enter. For a detailed introduction to using the command line, see Zed A. Shaw's excellent *Command Line Crash Course.*^[<http://cli.learncodethehardway.org/book/>]

Once opened, you should see a text window and a prompt that looks something like this: `computer-name:~username $`. The tilde indicates your "home" directory.^[In fact you can type `$ cd ~` at any point to return to your home directory.] The dollar sign is just a prompt for you to type something. The dollar sign in the instructions indicates you must type what follows into the terminal prompt (as opposed to typing it into your document). It is very likely that your "Documents" folder is located here. Type `$ pwd` and then hit enter to list the full name of your working directory, in other words the location of the folder that you are currently in. Use `$ pwd` whenever you feel lost in the command prompt.

The next command is `$ ls` (list) which simply lists the files in the current directory.^[Remember to hit enter after every command.] Finally, you can type `$ cd DIRECTORY_NAME` (where `DIRECTORY_NAME` is the name of the folder you'd like to navigate to) in order to change directory and `$ cd ..` to go back up the folder structure.^[Readers already familiar with the terminal should experiment with `$ pushd`, `$ popd`, and `$ cd -`.] Once you start typing the directory name, use the *Tab* key to auto complete the text. This is particularly useful for long directory names, or directories names that contain spaces.^[It is a good idea to get into the habit of not using spaces in folder or file names. Dashes-or_underscores instead of spaces in your filenames ensure lasting cross-platform compatibility.]

These three terminal commands: `pwd`,  `ls`,  and `cd` are all you need for this tutorial. Practice them for a few minutes to navigate your documents folder and think about they way you have organized your files. Follow along with your regular graphical file manager to keep your bearings. This may be a good time to do some house-cleaning. 

# Using Pandoc to convert Markdown to an MS Word document
We are now ready to typeset! Open your terminal window, use `$ pwd` and `$ cd` to navigate to the correct folder for your project. Once you are there, type `$ ls` in the terminal to list the files. If you see your .md file and your images, you are in the right place. To convert .md into .docx type:  

`$ pandoc -o main.docx main.md`  

Open the file with MS Word to check your results. Alternatively, if you use Open or Libre Office you can run:  

`$ pandoc -o project.odt main.md`   

If you are new to the command line, imagine reading the above command as saying something like: "Pandoc, create an MS Word file out of my Markdown file." The `-o` part is a "flag," which in this case says something like "instead of me explicitly telling you the source and the target file formats, just guess by looking at the file extension." Many options are available through such flags in Pandoc. You can see the complete list on Pandoc's website^[<http://johnmacfarlane.net/pandoc/README.html>] or by typing `$ man pandoc` in the terminal.

More advanced users who have LaTeX installed may want to experiment by converting Markdown into .tex or specially formatted .pdf files. Once LaTeX is installed, a beautifully formatted PDF file can be created using the same command structure:

`$ pandoc -o main.pdf main.md`

With time, you will be able to fine tune the formatting of PDF documents by specifying a LaTeX style file (saved to the same directory), and running something like:

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

Take a moment to orient yourself here. You will rarely have to edit these by hand, but it is important to understand that .bib is another convention for keeping your bibliographies organized. Each entry consists of a document type, "article" in our case, a unique identifier (fyfe_digital_2011), and the relevant meta-data on title, volume, author, and so on. The thing we care most about is the unique ID which immediately follows the curly bracket in the first line of each entry. The unique ID is what allows us to connect the bibliography with the main document. Leave this file open for now and go back to your `main.md` file.

Edit the footnote in the first line of your `main.md` file to look like something like this, where `@fyfe_digital_2011` is replaced with one of the unique IDs from your `project.bib` file:

`Some sentence that needs citation.^[@fyfe_digital_2011 argues that too.]`

Once we run the markdown through Pandoc, "@fyfe_digital_2011" will be expanded to a full citation in the style of your choice. To generate a bibliography simply include a section called `# Bibliography` at the end of document.

Now, go back to your metadata header at the top of your .md document, and specify the bibliography file to be used, like so:

```
---
title: Plain Text Workflow
author: Dennis Tenen, Grant Wythoff
date: January 20, 2014
bibliography: project.bib
---
```

Let's see if this works. Save your file, switch to the terminal window and run:

 `$ pandoc -S -o main.docx --filter pandoc-citeproc main.md`

The upper case `S` flag stands for "smart", a mode which produces "typographically correct output, converting straight quotes to curly quotes, \-\-\- to em-dashes, \-\- to en-dashes and \.\.\. to ellipses." The "pandoc-citeproc" filter parses all of your citation tags. The result should be a decently formatted MS Word file. If you have LaTeX installed, convert into .pdf using the same syntax for prettier results. Do not worry if things are not exactly the way you like them--remember, you are going to fine-tune the formatting all at once and at later time, as close as possible to the time of publication. For now we are just creating drafts based on reasonable defaults.

## Changing citation styles
The default citation style in Pandoc is Chicago author-date. We can specify a different style by using stylesheet, written in a "citation style language" (yet another plain-text convention, in this case for describing citation styles) and usually denoted by the .csl file extension. Luckily, there is an organization that maintains an archive of common citation styles, some even tailored for specific journals. Visit <http://editor.citationstyles.org/about/> to find the .csl file for Modern Language Association, download `modern-language-association.csl`, and save to your project directory as `mla.csl`. Now we need to tell Pandoc to use the MLA stylesheet instead of the default Chicago. We do this by updating the YAML header:

```
---
title: Plain Text Workflow
author: Dennis Tenen, Grant Wythoff
date: January 20, 2014
bibliography: project.bib
csl: mla.csl
---
```

You then simply use the same command:

`$ pandoc -S -o main.docx --filter pandoc-citeproc main.md`

Parse the command into English as you are typing. In my head, I translate the above into something like: "Pandoc, be smart about formatting, and output a Word Doc using the citation filter on my Markdown file (as you can guess from the extension)." As you get more familiar with citation stylesheets, consider adding your custom-tailored .csl files for journals in your field to the archive as a service to the community.

# Summary
You should now be able to write papers in Markdown, to create drafts in multiple formats, to add bibliographies, and to easily change citation styles. A final look at the project directory will reveal a number of "source" files: your `main.md` file, `project.bib` file, a `.csl` file, and some images. Besides the source files you should see some some "target" files that we created during the tutorial: `main.docx` or `main.pdf`. Your folder should look something like this:

```
Pandoc-tutorial/
    main.md
    project.bib
    mla.csl
    image.jpg
    main.docx
```

Treat you source files as an authoritative version of your text, and you target files as disposable "print outs" that you can easily generate with Pandoc on the fly. All revisions should go into `main.md`. The `main.docx` file is there for final-stage clean up and formatting. For example, if the journal requires double-spaced manuscripts, you can quickly double-space in Open Office or Microsoft Word. But don't spend too much time formatting. Remember, it all gets stripped out when your manuscript goes to print. The reclaimed cycles spent on needless formatting can be put to better use in polishing the prose of your draft.

# Useful Resources
Should you run into trouble, there is no better place to start looking for support than John MacFarlane's [site](https://leanpub.com/) and the affiliated [mailing list](https://groups.google.com/forum/#!forum/pandoc-discuss). At least two "Question and Answer" type sites can field questions on Pandoc: [Stack Overflow](http://stackoverflow.com/questions/tagged/pandoc) and [Digital Humanities Q&A](http://digitalhumanities.org/answers/). Questions may also be asked live, on Freenode IRC, #Pandoc channel, frequented by a friendly group of regulars.

Although we suggest starting out with a simple editor, many (70+, according to [this blog post](http://web.archive.org/web/20140120195538/http://mashable.com/2013/06/24/markdown-tools/)) other, Markdown-specific alternatives to MS Word are available online, and often free of cost. From the standalone ones, we liked [Mou](http://mouapp.com/), [Write Monkey](http://writemonkey.com), and [Sublime Text](http://www.sublimetext.com/). Several web-based platforms have recently emerged that provide slick, graphic interfaces for collaborative writing and version tracking using Markdown. These include: <prose.io>,  [Authorea](https://www.authorea.com/), [Penflip](https://www.penflip.com/), [Draft](https://draftin.com/), and [Editorially](https://editorially.com/).

But the ecosystem is not limited to editors. [Gitit](http://gitit.net/) and [Ikiwiki](https://github.com/dubiousjim/pandoc-iki) support authoring in Markdown with Pandoc as parser. To this list we may a range of tools that generate fast, static webpages, [Yst](https://github.com/jgm/yst), [Jekyll](https://github.com/fauno/jekyll-pandoc-multiple-formats), [Hakyll](http://jaspervdj.be/hakyll/), and [bash shell script](https://github.com/wcaleb/website) by the historian Caleb MacDaniel.

Finally, whole publishing platforms are forming around the use of Markdown. Markdown to marketplace platform [Leanpub](https://leanpub.com) could be an interesting alternative to the traditional publishing model. And we ourselves are experimenting with academic journal design based on GitHub and Readtheocs.org (tools usually used for technical documentation).

Besides Markdown, Pandoc can handle many more formats that are worth exploring. Your notes, blog entries, code documentation, and wikis can all be authored in Markdown. Increasingly, many platforms like Wordpress and GitHub render Markdown natively. In the long term, your research will benefit from such unified workflows, making it easier to save, search, share, and organize your materials.^[The source files for this document can be found on <https://github.com/dhcolumbia/pandoc-workflow>. Use the "raw" option when viewing in GitHub to see the source Markdown. The authors would like to thank Alex Gil, his colleagues from Columbia's Digital Humanities Center, and the participants of openLab at the Studio in the Butler library for testing the code in this tutorial on a variety of platforms.]

# Bibliography
