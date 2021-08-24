# zscript-docs
 A nicer, prettified, organized documentation for ZScript

# Getting started on writing
[Download and install MkDocs](https://www.mkdocs.org/getting-started/). You'll need the latest version of [Python](https://www.python.org).

Once done, you can edit the documentation for /2.53.2/ or /2.55A-F/. In one of those folders, you'll find:

* mkdocs.yml, which contains an itemized `nav` list of all relevant files (for the sidebar) and options for MkDocs generation. The format should be pretty self-explanatory.
* A /docs/ subfolder containing all of the relevant .md files. This is where the actual documentation text is stored.

The .md files are written using [Markdown](https://daringfireball.net/projects/markdown/). There are a few syntactical differences:

* Specifying a block of text, then writing a colon on the next line and indenting the following text creates a definition tag:

      This is a definition label
      :     This is the text containing the definitions for the above.
            
            This is another paragraph relevant to the above definition.
            
* Writing three exclamation points (`!!!`) and then a word (e.g. `note` or `caution`), then indenting the following text creates an [Admonition](https://python-markdown.github.io/extensions/admonition/) note:

      !!! note
            This text will show up in a note box, hopefully.

You can run `mkdocs serve` from the command line, then navigate to [http://localhost:8000/](http://localhost:8000/) in your browser to see the document in HTML format. It will automatically update as you save the .md files. To close the server, just hit `CTRL-C` in the command prompt you started the server from.
