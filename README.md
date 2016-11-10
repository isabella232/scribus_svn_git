# README

This repository contains the meta-data used to convert the Scribus SVN
(svn://scribus.net) repository to Git.

The trunk and all branches and tags are imported from SVN into Git.

The SVN repository contains an additional folder "Scribus" at the
project root. This folder is skipped during conversion, so that the
programm sources appear in the repository root.

The git_repo_init.sh script configures an empty Git repository to
receive the SVN commits.

The update_from_svn.sh script pulls new commits from SVN, creates Git
tags from SVN tags and pushes the result to the configured "origin"
Git remote repository. (To congigure this origin Git remote repo, 
just do a "git remote add repo_name repo_url" in the shell).

## Requirements

- bash
- git
- subversion
- git-svn
- whitail or dialog

## How to setup

First, you will have to clone this repository. We suppose you are cloning it into `~/src`, but you can pick any directory you prefer.

    cd ~/src
    git clone https://github.com/scribusproject/scribus_svn_git.git

Then create a local repository called `scribus-github-sync` (or any other name you see fit) that you will use to contain the sync.

    cd ~/src
    git init scribus-github-sync

Finally, use the scripts from the `scribus_svn_git` repository to setup the local repository so that it can be used for syncing the Scribus repositories. (it will take some time)

    cd ~/src/scribus-github-sync
    ~/src/scribus_svn_git/git_repo_init.sh
    git remote add origin https://github.com/scribusproject/scribus.git

## How to sync

Now, each time you want to update the `scribusproject/scribus` you go into the `scribus_svn_git` repository and run the update script:

   cd ~/src/scribus-github-sync
   ~/src/scribus_svn_git/update_from_svn.sh


## Caveat

All SVN commiters need to be listed in svn_authors.txt. A missing
author will lead to an error:

    Author: <username> not defined in /path/to/svn_authors.txt file

In this case, add the new commiter to the svn_authors.txt file with
the following format:

    username = Full Name <email@address.xzy>

and re-run the import.

## External references

* github to svn and svn to github sync scripts using another git repo : http://zone.spip.org/trac/spip-zone/browser/_outils_/svn2git/trunk
