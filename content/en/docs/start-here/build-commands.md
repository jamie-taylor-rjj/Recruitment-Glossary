---
title: "Build Commands"
description: "A list of the most useful commands that the Recruitment Glossary code base ships with."
lead: "A list of the most useful commands that the Recruitment Glossary code base ships with."
date: 2020-10-13T15:21:01+02:00
lastmod: 2020-10-13T15:21:01+02:00
draft: false
images: []
menu:
  docs:
    parent: "start-here"
weight: 140
toc: true
---

{{< alert icon="💡" text="You can change the commands in the scripts section of `./package.json`." />}}

## create

Create new content for your site:

{{< highlight bash >}}
npm run create [path] [flags]
{{< /highlight >}}

See also the Hugo docs: [hugo new](https://gohugo.io/commands/hugo_new/).

### Docs based tree

Create a docs based tree — with a single command:

{{< highlight bash >}}
npm run create -- --kind docs [section]
{{< /highlight >}}

For example, create a docs based tree named guides:

{{< highlight bash >}}
npm run create -- --kind docs guides
{{< /highlight >}}

## lint

Check scripts, styles, and markdown for errors:

{{< highlight bash >}}
npm run lint
{{< /highlight >}}

### scripts

Check scripts for errors:

{{< highlight bash >}}
npm run lint:scripts [-- --fix]
{{< /highlight >}}

### styles

Check styles for errors:

{{< highlight bash >}}
npm run lint:styles [-- --fix]
{{< /highlight >}}

### markdown

Check markdown for errors:

{{< highlight bash >}}
npm run lint:markdown [-- --fix]
{{< /highlight >}}

## clean

Delete temporary directories:

{{< highlight bash >}}
npm run clean
{{< /highlight >}}

## start

Start local development server:

{{< highlight bash >}}
npm run start
{{< /highlight >}}

## build

Build production website:

{{< highlight bash >}}
npm run build
{{< /highlight >}}

### functions

Build Lambda functions:

{{< highlight bash >}}
npm run build:functions
{{< /highlight >}}

### preview

Build production website including draft and future content:

{{< highlight bash >}}
npm run build:preview
{{< /highlight >}}
