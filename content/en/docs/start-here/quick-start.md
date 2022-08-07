---
title: "Quick Start"
description: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
lead: "A one page summary of how to get Recruitment Glossary up and running locally. This is required in order to add content to it."
date: 2020-11-16T13:59:39+01:00
lastmod: 2020-11-16T13:59:39+01:00
draft: false
images: []
menu:
  docs:
    parent: "start-here"
weight: 110
toc: true
---

## Requirements

- [Git](https://git-scm.com/) — latest source release
- [Node.js](https://nodejs.org/) — latest LTS version or newer

{{< details "Why Node.js?" >}}
Recruitment Glossary uses npm (included with Node.js) to centralize dependency management, making it [easy to update]({{< relref "how-to-update" >}}) resources, build tooling, plugins, and build scripts.
{{< /details >}}

## Cloning the Code

Firstly, you will need to use Git to clone the code for this repository down to your local machine. The code is hosted at [a GitHub repo](https://github.com/jamie-taylor-rjj/Recruitment-Glossary), and can be cloned with the following command:

```bash
git clone https://github.com/jamie-taylor-rjj/Recruitment-Glossary.git
```

This will copy all of the files from the GitHub repository down to your local machine, placing them in a RecruitmentGlossary directory.

{{< details "git or gh?" >}}
There are (at the time of recording) two ways to clone a remote repository to your computer from GitHub:

1. [git](https://git-scm.com/)
1. [gh](https://github.com/cli/cli)

Both achieve the same thing, and either is preferred. gh is a newer (and GitHub only) way of interacting with repositories, but use whichever process you prefer.
{{< /details >}}

## Building & Running Locally

### Installing Dependencies

In order to build the repository locally, you'll first need to install all of the npm dependencies. This can be done by running the following command in the RecruitmentGlossary directory:

```bash
npm install
```

{{< details "npm install" >}}
Whenever you run this comment, npm (which is part of Node.js) will read through the package.json file and download all of the dependencies listed there. It will place all of the downloaded dependecies in the `node_modules` directory. Without the dependencies in this directory, the build and run commands will not work.
{{< /details >}}

### Running the WebApp

Once the install process completes, you can start the web application locally by running:

```bash
npm run start
```

This will start build the web application, and start a local web server. The web server will serve the built web application, and will be available at [localhost:1313](http://localhost:1313/).

## Help

If the above commands don't work for you, first check the [Troubleshooting]({{< relref "troubleshooting" >}}) page.

If the webapp still does not build locally, then please take a look at filing an issue in the [GitHub repository](https://github.com/jamie-taylor-rjj/Recruitment-Glossary/issues) for this project. However, please do check that you have installed the correct versions of the dependencies listed above before posting an issue.

## Other commands

Doks (the theme that Recruitment Glossary is based on) comes with commands for common tasks. [Technologies Used →]({{< relref "technologies-used" >}})
