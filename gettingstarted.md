Getting Started with LaTeX
==========================

Linux
-----

There are two options to setting up LaTeX on Linux.
You can either install it from [the TeXLive website](http://www.tug.org/texlive/) or via your package manager.
Either way is a completely viable option.

### Fedora

These instructions were done on Fedora 19.
If something does not work, open an issue.
If you installed via the TeXLive website, you can skip the installation of TeXLive, Biber, and Latexmk.
The customization of Latexmk should also still be done.

From the terminal, call `sudo yum install texlive`.
After installing, you can now compile LaTeX with `latex`, `pdflatex`, or something else!
This is not recommended, however.
It is suggested that you then install the `latexmk` package with the command `sudo yum install latexmk`.
On Fedora 19, be sure not to accidentally install the `latex-mk` package, as that is something different.
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
	else
		latexmk -h
	fi
}

alias latexmk=latex_make
```

This function and alias will make you be able to simply call `latexmk filename` and the PDF will be created for you, with no other annoying files around.
If you do not want PDFs to be created or do not want cleaning, then you do not need the function and alias at all.

Now you have easy LaTeX compilation set up, so the next step is to prepare for compiling files using mla13.
If you currently try to compile the MLA template, you will find that no citations are listed.
This is because mla13 requires Biber, which does not come with TeXLive on Fedora because the Fedora TeXLive is out-of-date.
Sadly, just installing the `biber` package cannot be done, because it does not exist.
We then need to add a custom repository.
It is be [fedora-biber](http://repos.fedorapeople.org/repos/mef/biber/fedora-biber.repo).
Add the file in `/etc/yum.repos.d`.
Now, you can try to install the `biber` package via the command `sudo yum install biber`.
Sadly, there is a broken dependency.
To fix that, you will need to install the Fedora 18 version of the package.
You can find it on [this webpage](http://www.mail-archive.com/texlive@linux.cz/msg00579.html).
Follow the link that the person provided in response to somebody complaining of the broken dependency.
After installing that package, you can install the `biber` package via the command `sudo yum install biber` and now you are ready to compile.

Now `latexmk mla` will compile the template file.
You can see the citations now work, due to Biber now being installed.

Mac OS
------

Currently no installation of TeXLive on Mac OS has been done to know the best instructions.
It is assumed that installing [MacTeX](http://www.tug.org/mactex/) should have all necessary programs installed.
How to customize Latexmk on Mac OS like on Linux is currently not known.
Any Mac users that have instructions would be greatly appreciated.

Windows
-------

Currently no installation of TeXLive on Mac OS has been done to know the best instructions.
It is assumed that installing [TeXLive](http://www.tug.org/texlive/acquire-netinstall.html) should have all necessary programs installed.
It is unlikely that Latexmk can be easily customized like on Mac OS or Linux on Windows.
Because of that, more stress will be put on the developer to delete files when necessary.
Any Windows users that have instructions would be greatly appreciated.
