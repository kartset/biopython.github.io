---
title: GitMigration
permalink: wiki/GitMigration
layout: wiki
---

We are currently testing the benefits of migration to Git distributed
version control.

[GitHub](http://github.com/) currently hosts the Biopython Git
repository at <http://github.com/biopython/biopython/>

This is the official repository. Currently it is synchronized with the
main [CVS](CVS "wikilink") trunk every hour, so it should be up to date
most of the time. All developers and potential contributors are
encouraged to try out this repository. Instructions on developing
Biopython with Git follow below.

Prerequisites
=============

Installing Git
--------------

You will need to install Git on your computer. Git (http://git-scm.com/)
is available for all major operating systems. Please use the appropriate
installation method as described below.

### Linux

Git is now packaged in all major Linux distributions, you should find it
in your package manager.

#### Ubuntu/Debian

You can install Git from the `git-core` package. e.g., `sudo` `apt-get`
`install` `git-core`

You'll probably also want to install the following packages: `gitk`
`git-gui` `git-doc`

### Mac OS X

Download the `.dmg` disk image from
<http://code.google.com/p/git-osx-installer/>

### Windows

Two options exist for Windows:
[msysGit](http://code.google.com/p/msysgit/) and running Git under
[Cygwin](http://www.cygwin.com/).

#### msysGit (Recommended)

[msysGit](http://code.google.com/p/msysgit/) is a port of Git that runs
natively on Windows via the MinGW library. Because Git was not
originally designed to run on Windows, and since this is a port, some
bugs exist, though are rarely encountered in everyday use of Git. See
their website for download and installation instructions. Additionally,
you can watch [Scott Chacon's screencast on installing msysGit on
Windows](http://gitcasts.com/posts/git-on-windows), and see [this GitHub
guide](http://github.com/guides/using-git-and-github-for-the-windows-for-newbies).

#### Cygwin

[Cygwin](http://www.cygwin.com/) provides a Linux-like environment for
Windows. It includes access to repositories of many software packages
available commonly in Linux distributions, including Git. You can find
the `git` package under the "devel" category.

Creating a GitHub account (Optional)
------------------------------------

Once you have Git installed on your machine, you can obtain the code and
start developing. Since the code is hosted at GitHub, however, you may
wish to take advantage of the site's offered features by signing up for
a GitHub account. While a GitHub account is completely optional and not
required for obtaining the Biopython code or participating in
development, a GitHub account will enable all other Biopython developers
to track (and review) your changes to the code base, and will help you
track other developers' contributions. This fosters a social,
collaborative environment for the Biopython community.

If you don't already have a GitHub account, you can create one
[here](http://github.com/plans) (the free plan is absolutely enough).
Once you have created your account, upload an SSH public key by clicking
on '[Account](https://github.com/account/)' after logging in. For more
information on generating and uploading an SSH public key, see [this
GitHub guide](http://github.com/guides/providing-your-ssh-key).

Obtaining the source code
=========================

If you want to make changes, then there are two ways of getting the
source code tree onto your machine: by simply "cloning" the repository,
or by "forking" the repository on GitHub. They're not that different, in
fact both will result in a directory on your machine containing a full
copy of the repository on your machine. However, if you have a GitHub
account, you can make your repository a public branch of the project. If
you do so, other people will be able to easily review your code, make
their own branches from it or merge it back to the trunk.

In fact you can change this later, using the .git/config file, but to
make it easier I'll describe the two possibilities separately.

Cloning the repository without a GitHub account
-----------------------------------------------

Getting a copy of the repository (called "cloning" in Git terminology)
without GitHub account is very simple:

` git clone `[`git://github.com/biopython/biopython.git`](git://github.com/biopython/biopython.git)

This command creates a local copy of the entire Biopython repository on
your machine (your own personal copy of the official repository with its
complete history). You can now make local changes and commit them to
this local copy.

If you want other people to see your changes, however, you need to take
care of publishing your branch to a public server yourself.
Alternatively, using GitHub takes care of this for you.

Forking Biopython using a GitHub account
----------------------------------------

If you are logged in to GitHub, you can go to the Biopython repository
page

[`http://github.com/biopython/biopython/tree/master`](http://github.com/biopython/biopython/tree/master)

and click on a button named 'Fork'. This will create a fork (basically a
copy) of the official Biopython repository, still on publically viewable
on GitHub, but listed under your personal account.

Now, assuming that you have Git installed on your computer, execute the
following commands locally on your machine:

`git clone git@github.com:`<your username>`/biopython.git`

Where <your username>, not surprisingly, stands for your GitHub
username. You have just created a local copy of the biopython repository
on your machine.

You may want to also link your branch with the official distribution:

`git remote add official_dist `[`git://github.com/biopython/biopython.git`](git://github.com/biopython/biopython.git)

You can find more info here:
<http://github.com/guides/keeping-a-git-fork-in-sync-with-the-forked-repo>

To add additional contributors to your branch on GitHub, select 'edit'
and then add them to the 'Repository Collaborators' section. You will
need to know their username on GitHub.

Making changes
==============

Now you can make changes to your branch. Since your local branch is a
full repository, you can commit your changes as often as you like. In
fact, you should commit as often as possible, because smaller commits
are much better to manage and document. Let us assume you've made
changes to the file Bio/x.py. You need to add this file to your
change-set:

`git add Bio/x.py`

and now you commit:

`git commit -m "added feature Y in Bio.x"`

Your commits in Git are local, i.e. they affect only your working branch
on your computer, and not the whole Biopython tree or even your fork on
GitHub. You don't need an internet connection to commit, so you can do
it very often.

Once you think your changes are fine and should be reviewed by others,
you can push your changes back to the GitHub server:

`git push origin`

If you think you changes are worth including in the main Biopython
distribution, then [file an (enhancement) bug on
Bugzilla](http://bugzilla.open-bio.org/), and include a link to your
updated branch (i.e. your branch on GitHub, or another public Git
server). You could also attach a patch on Bugzilla. If the changes are
accepted, one of the Biopython developers will have to check this code
into our [CVS](CVS "wikilink") repository, and within the hour this
should update the main Biopython branch on GitHub.

On GitHub itself, you can inform keepers of the main branch of your
changes by sending a 'pull request' from the main page of your branch.
Once the file has been committed to the main branch, you may want to
delete your now redundant bug fix branch on GitHub. Branches can be
deleted by selecting 'edit' and then 'delete repository' from the bottom
of the edit page.

Evaluating changes
------------------

This section describes the steps to evaluate and integrate changes for
Biopython core developers, or anyone accepting changes on a branch. The
following commands will show you a diff of modifications on another
branch. First add a reference to the remote repository, and fetch the
changes locally:

` git remote add username/biopython-mods `[`git://github.com/username/biopython-mods.git`](git://github.com/username/biopython-mods.git)  
` git fetch username/biopython-mods`  
` `

To double check the branch is integrated:

` git branch -r`

Finally, get the diff of the modifications:

` git diff origin/master username/biopython-mods/master`

If you later want to remove the reference to the branch:

` git branch -r -d username/biopython-mods/master`

Alternatively, from within GitHub you can use the fork-queue to cherry
pick commits from other people's forked branches. See [this github blog
post](http://github.com/blog/270-the-fork-queue) for details. While this
defaults to applying the changes to your current branch, you would
typically do this using a new integration branch, then fetch it to your
local machine to test everything, before merging it to your main branch.

Additional Resources
====================

There is a lot of different nice guides to using Git on the web:

-   <http://github.com/guides/git-cheat-sheet>
-   <http://zrusin.blogspot.com/2007/09/git-cheat-sheet.html>
-   <http://www.kernel.org/pub/software/scm/git/docs/v1.4.4.4/cvs-migration.html>
