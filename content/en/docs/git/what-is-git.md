---
title: "What is Git?"
description: "Just what is Git, and why do developers use it?"
lead: "Just what is Git, and why do developers use it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "git"
weight: 630
toc: true
---

## 10,000 ft Overview

Git is a source control system. It allows developers, designers, and all other content creators to track the changes that they make to almost any type of file.

Whilst it works best with text-based files (i.e. source code, text files, etc.), it also works with binary formats (i.e. audio, documents, images, 3D models, etc.).

Whilst Git is one of the most common source control systems, there are many others including (but not limited to):

- Concurent Version System (aka cvs)
- Subversion (aka svn)
- Mercurial
- Team Foundation Version Control

## Basic Information

Git was initially created by Linus Torvalds, but has been maintained by Junio Hamano since 2005. It was originally created to make the work of maintaining the [Linux kernel]({{< relref "what-is-linux" >}})
 easier.

Git is a command line application, but there are many different GUI (Graphical User Interface) applications which hide the complexity of the command line. Some of the most commonly used Git GUI applications are:

- GitHub Desktop
- GitKraken
- SourceTree
- TortoiseGit

## Basic Usage

Suppose that you wish to work on the repository for this website, you would need to "clone" (i.e. copy down) the git repository from `https://github.com/jamie-taylor-rjj/Recruitment-Glossary`. This achieved by issuing the following command:

{{< highlight bash >}}
git clone https://github.com/jamie-taylor-rjj/Recruitment-Glossary.git
{{< /highlight >}}

{{< details "Cannot find command 'git'" >}}
Whilst Git is usually installed on all MacOS and Linux-based distributions, it is not installed on Windows by default.
As such, you may need to [download and install Git](https://git-scm.com/download/win) before continuing onward.
{{< /details >}}

This will make a local copy of the GitHub repository for this project.

When you have made a number of changes, you can see the files that you have altered or created using the `status` command:

{{< highlight bash >}}
git status
{{< /highlight >}}

You should received output similar to the following:

{{< highlight bash >}}
On branch feature/git
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   content/en/docs/git/what-is-git.md
{{< /highlight >}}

(the above is the output that was received when working on this file)

When you are happy with this changes, they need to be added to a changeset using the `add` command:

{{< highlight bash >}}
git add content/en/docs/git/what-is-git.md
{{< /highlight >}}

This command will take the changes that you have made to this file and add it to either a new changeset or the current changeset.

Changesets need to be committed to the local repository's git instance before they are considered stored. This is achieved with the `commit` command, and frequently paired with a human readable message which describes the changes that you made.

{{< highlight bash >}}
git commit -m "Added the Basic Usage section to the Git page."
{{< /highlight >}}

## Useful Links

- [List of version control software](https://en.wikipedia.org/wiki/List_of_version-control_software) @ wikipedia
- [Git](https://en.wikibooks.org/wiki/Git) @ wikibooks
