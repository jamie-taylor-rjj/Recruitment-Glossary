---
title: "How to Update"
description: "Steps to ensure that you have the latest version of the Recruitment Glossary, when developing for it locally."
lead: "Steps to ensure that you have the latest version of the Recruitment Glossary, when developing for it locally."
date: 2020-11-12T13:26:54+01:00
lastmod: 2020-11-12T13:26:54+01:00
draft: false
images: []
menu:
  docs:
    parent: "help"
weight: 610
toc: true
---

{{< alert icon="💡" text="Learn more about git and how to use it at the [git specific pages →]({{< relref `what-is-git` >}})" />}}

## Pull the latest version

It is always a good idea to ensure that you have the latest version of the code before embarking on any local development. As such, you should always make a point of running the following command before doing any new work on Recruitment Glossary:

```bash
git pull
```

The above command assumes that you have:

- [Cloned the code](/docs/prologue/quick-start/#cloning-the-code)
- and have a terminal open in the directory where the code exists

This command will go out to GitHub and pull the latest changes down to your local version of the repository. It will not overwrite any local changes, and may give an error if there are local changes (depending on what they are). You will also be asked to merge any incoming changes (those from the GitHub repo) into your local changes, if git cannot merge them itself.

### Pushing changes the GitHub

Once you have made some changes and have committed them, you will need to push the changes back to the upstream GitHub repository.

{{< details "Upstream? Remotes?" >}}
The version of the code hosted on GitHub is known as an upstream remote repository.

When you cloned the repository down to your machine, the version on your machine made a note of where it came from (the remote repository). This remote repository is known as upstream, as that is where this code came from.
{{< /details >}}

In order to do this, you will need to run the following command:

```bash
git push
```

This will take all of the commits that you have made and push them back to the remote repository.

{{< alert icon="💡" text="Learn more about [semantic versioning](https://docs.npmjs.com/about-semantic-versioning) and [advanced range syntax](https://docs.npmjs.com/cli/v6/using-npm/semver#advanced-range-syntax)." />}}

## Check for outdated packages

The [`npm outdated`](https://docs.npmjs.com/cli/v7/commands/npm-outdated) command will check the registry to see if any (or, specific) installed packages are currently outdated:

```bash
npm outdated [[<@scope>/]<pkg> ...]
```

## Update packages

The [`npm update`](https://docs.npmjs.com/cli/v7/commands/npm-update) command will update all the packages listed to the latest version (specified by the tag config), respecting semver:

```bash
npm update [<pkg>...]
```
