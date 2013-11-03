% Fall 2013

# Philosophy 
Authoring, storing, and retrieving documents are activities at the center of the humanities research workflow. And yet, many base their practice on proprietary tools and formats which struggle with even the most basic requirements of academic writing. The readers will relate to being frustrated with the fragility of footnotes, bibliographies, figures, and book drafts authored in MS Word. Still, most journals insist on submissions in .docx format. More than causing personal frustration, the reliance on fragile tools and formats has long-term negative implications for the community. In such an environment, journals must outsource typesetting, alienating authors from the material contexts of publication, furthermore adding unnecessary barriers to unfettered circulation of knowledge. Closed formats ultimately lead to closed intellectual communities.

In this tutorial, we would like to suggest an alternative workflow built around open-source tools and transparent formats. Inspired by best practices in a variety of disciplines, we were guided by the following principles:

1. *Preference for plain-text, fully transparent, human-readable formats.* When writing in Word or Google Docs, what you see is not what you get. The file contains hidden automatically-generated formatting characters. When things go wrong, the obfuscated typesetting layer is difficult to troubleshoot. Plain text ensures transparency and answers to the standards of long-term preservation. MS Word may go the way of Word Perfect in the future, but plain text will always remain easy to read, catalog, mine, and transform. As an additional feature, plain text enables easy and powerful versioning of the document. 

2. *Platform independence.* Writing in plain text means you can easily share, edit, and archive your documents in virtually any environment. Your plain text files will be accessible on cell phones, tablets, or, perhaps, on a low-powered terminal in some remote library. Plain text is backwards compatible and future proof. Whatever software or hardware comes along next, it will be able to understand your plain text files. 

3. *Separation of form and content.* Writing and formatting at the same time is distracting. The idea is to write first, and format later, as close as possible to the time of publication.

4. *Support for the academic apparatus.* The workflow needs to handle footnotes, figures, and bibliographies gracefully.

5. *One source many destinations.* As the vectors of publication multiply, we need to be able to generate a multiplicity of formats including for slide projection, print, web, and mobile. Ideally, we would like to be able to generate most common formats without breaking bibliographic dependencies. 

Markdown and LaTeX answer all of these requirements. We choose to author the primary text in Markdown (and not LaTeX) because it offers the most light-weight and clutter free syntax (hence, mark  *down*) and because when coupled with Pandoc it allows for the greatest flexibility in outputs (including .doc and .tex files).^[There are no good solutions for arriving at MS Word from LaTeX.]

# Use cases
We will cover three use cases in this tutorial. In the first, you will learn the basics of markdown and use Pandoc to generate a simple .pdf file. In the second, we will add some figures and bibliography, generate an MS Word document, and then change the citation style form MLA to Chicago. Finally, we will use Pandoc in conjunction with reveal.js to make some attractive slides. File management and versioning using Git will be covered in another tutorial. 

As a side-effect of this tutorial, you will be introduced to the basics of command line file management--a skill necessary for many more advanced research workflows. 

# Mindset
Readers with experience in data science, software development, or server administration may want to skip this section and go straight to software requirements. For all others, we would like to take a moment to discuss what to do when things go wrong. It it quite likely, that at several points of this (or any other) tutorial commands, or instruction will fail to work as expected. The magic of computing is in its universal reproducibility. Software works in similar ways on varied platforms, on machines in various state of disrepair, and under the precarious conditions of competing standards, 

# Software requirements
You will need to following software installed on your computer:

* A plain text editor. For beginners, we recommend Text Wrangler on a Mac, Notepad++ for Windows, and gEdit for Linux. More advanced users may want to experiment with flavors of Emacs of Vim. It does not matter what you use as long as it is explicitly a plain text editor. 

* Pandoc. Pandoc was created and is maintained by John MacFarlane at UC Berkeley. This is humanities computing at its best and will serve as the engine of our workflow. With Pandoc, you will be able to compile text and bibliography into beautifully formatted and flexible documents.

* LaTeX. Although LaTeX is not covered in this tutorial, it is used by Pandoc for .pdf creation. Advanced users will often convert into LaTeX directly to have more granular control over the typesetting of the .pdf.

# Case 1: Markdown basics

# Case 2: Working with Bibliographies

# Case 3: Slides 
