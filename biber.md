Biber
=====

Installing Biber is not needed by anything in this repository, but instructions for installing Biber on Fedora are below.

Sadly, just installing the `biber` package cannot be done, because it does not exist.
We then need to add a custom repository.
It is [fedora-biber](http://repos.fedorapeople.org/repos/mef/biber/fedora-biber.repo).
Add the file in `/etc/yum.repos.d`.
Now, you can try to install the `biber` package via the command `sudo yum install biber`.
Sadly, there is a broken dependency.
To fix that, you will need to install the Fedora 18 version of the package.
You can find it on [this webpage](http://www.mail-archive.com/texlive@linux.cz/msg00579.html).
Follow the link that the person provided in response to somebody complaining of the broken dependency.
After installing that package, you can install the `biber` package via the command `sudo yum install biber`.
Now it is installed for use where you'd like.
