Getting Started with LaTeX
==========================

These instructions assume that Linux is being used.

There are two options to setting up LaTeX on Linux.
You can either install it from [the TeXLive website](http://www.tug.org/texlive/) or via your package manager.
Either way is a completely viable option.

Also make sure that you have biblatex or biber installed, and that you have the mla13.sty file installed globally.

Fedora
------

These instructions were done for Fedora 19.
If something does not work, open an issue.
If you installed via the TeXLive website, you can skip the installation of TeXLive and Latexmk.
The customization of Latexmk should also still be done.

To install TeXLive from the package manager, call `sudo yum install texlive` from the terminal.
After installing, you can now compile LaTeX with `latex`, `pdflatex`, or something else!
This is not recommended, however.
It is suggested that you then install the `latexmk` package with the command `sudo yum install latexmk`.
Be sure not to accidentally install the `latex-mk` package, as that is something different.
This package will make compiling stuff easier when you are using BibTeX or something similar.
As in, when you need more than one command to compile.
The following code is suggested for customizing latexmk to work nicer.
You can add it to your `.bashrc` file.

```bash
# Alias latexmk to make as pdf and clean up
latex_make() {
	# list of additional to extensions to delete
	# latexmk doesn't necessarily agree with these
	delete=(run.xml bbl)

	if [ ! -z "$1" ]
	then
		nopath=$(basename "$1")
		file="${nopath%.*}"

		latexmk "$file" -pdf
		latexmk "$file" -c

		for i in "${delete[@]}"
		do
			if [ -e "$file.$i" ]
			then
				rm "$file.$i"
			fi
		done
		
		# Sometimes this file is made, and it is annoying.
		if [ -e "$file-blx.bib" ]
		then
			rm "$file-blx.bib"
		fi
	else
		latexmk -h
	fi
}

alias latexmk=latex_make
```

This function and alias will make you be able to simply call `latexmk filename` and the PDF will be created for you, with no other annoying files around.
If you do not want PDFs to be created or do not want cleaning, then you do not need the function and alias at all.

Now `latexmk mla` will compile the template file successfully.
