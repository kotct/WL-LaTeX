WL-LaTeX
========

A collection of LaTeX related-files that are intended to be useful at WLCSC.

Getting Started with LaTeX
--------------------------

### Linux

From the package manager, install the `texlive` package.
You can now compile LaTeX with `latex`, `pdflatex`, or something else!
This is not recommended, however.
It is suggested that you then install the `latexmk` package.
On Fedora 19, be sure not to accidentally install the `latex-mk` package, as that is something different.
This package will make compiling stuff easier when you are using BibTeX or something similar, when you need more than one command to compile.
The following code is suggested for customizing latexmk to work nicer.

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
	else
		latexmk -h
	fi
}

alias latexmk=latex_make
```

This function and alias will make you be able to simply call `latexmk filename` and the PDF will be created for you, with no other annoying files around.

Now you have easy LaTeX compilation set up, so the next step is to prepare for compiling files using `sty/mla13.sty`.
If you currently try to compile the MLA template, you will find that no citations are listed.
This is because mla13 requires Biber, which does not come with TeXLive.
Sadly, just installing the `biber` package cannot be done, because it does not exist.
We then need to add a custom repository.
For Fedora, it would be [fedora-biber](http://repos.fedorapeople.org/repos/mef/biber/fedora-biber.repo).
Add the file in `/etc/yum.repos.d`.
Now, you can try to install the `biber` package.
Sadly, there is a broken dependency.
To fix that, you will need to install the Fedora 18 version of the package.
You can find it on [this webpage](http://www.mail-archive.com/texlive@linux.cz/msg00579.html) (follow the link that the person provided in response).
After installing that package, you can install the `biber` package and now you are ready to compile.

Now `latexmk mla` will compile the template file.
You can see the citations now work, due to Biber.

sty/mla13.sty
-----------

The version in this repository is a modified version of [jmclawson](https://github.com/jmclawson)'s [fork](https://github.com/jmclawson/mla13) of [mla13](https://github.com/jackson13info/mla13) by [jackson13info](https://github.com/jackson13info).
Sammidysam has made the modifications to this file.

For templates, see the `templates/mla/` folder.
For examples, see the `examples/mla/` folder.

bst/Overley.bst
---------------

An original BibTeX style file created by computerguy505 using makebst. 
This file is released under the LaTeX public license.
The most recent version of said license is located at: 
www.latex-project.org/lppl.txt
