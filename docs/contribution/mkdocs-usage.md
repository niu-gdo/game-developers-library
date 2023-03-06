# Using MkDocs
By Jake Rogers

## MkDocs
GDL uses MkDocs to convert .md files into html & CSS files. When MkDocs builds, it finds any .md files found within the /docs/ directory and generates a cohesive website from what it finds, featuring a few extra goodies:

* Navigation window, which groups pages based on the docs/ subdirectory structure
* A search bar, which not only finds pages, but keywords within pages.
* Per-page table of contents, constructed from using headings.
* Themes and dark mode.

All that is to say, you can create sleek pages as easily as you would create a markdown file!

[MkDoc's Website](https://www.mkdocs.org/)
### Material for MkDocs
GDL also uses Material for MkDocs as a theme template throughout the site.

[Squidfunk's Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)

## Installation
NIU Game Developers Organization members only need two things to contribue:

* A GitHub account added to our organization (Contact administrators of [NIU-GDO](https://github.com/niu-gdo)).  
* A UNIX terminal, capable of installing the mkdocs package and pip.
    * Windows users can easily use WSL2 or a Virtual Machine for this purpose.

In a UNIX terminal, do the following:  
1. Install mkdocs. Run `sudo apt install mkdocs`  
2. Install pip. Run `sudo apt install python3-pip`  
3. Using pip, install Material for MkDocs. Run `pip install mkdocs-material`  

You should now have both MkDocs and Material for MkDocs installed!

## Editing with MkDocs

While some text editors allow you to see formatted .md files as you edit them, you will notice that your local branches of GDL do not look anything like the website. This, of course, is because MkDocs has not yet converted the .md files to the formal website. 

If you want mkdocs to build the actual site, run `mkdocs build` in the root directory of the project, and you will see a site/ directory produced. This directory will contain all of the files needed for the actual website, including an index.html.

### MkDocs Serve
We don't, however, want to build mkdocs everytime we make a change. Fortunately, you can run `mkdocs serve` instead to start a live-hosted process for the site. The terminal will display a link you can open on a web browser to view the page, and any changes to .md files will automatically reload the page and display the changes!

Use Ctrl+C to stop the `mkdocs serve` process.