---
title: "Introduction"
description: "A web application designed to help bridge the knowledge gaps between recruiters and technology workers (developers, designers, testers, etc.)."
lead: "A web application designed to help bridge the knowledge gaps between recruiters and technology workers (developers, designers, testers, etc.)."
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "start-here"
weight: 100
toc: true
---

## Why Does This Project Exist?

This project is an attempt to provide a place for people in both the recruitment and technology industries to exchange information and get a better understanding of each others domains.

For instance, it can be very easy for developers to rattle of a series of acronyms and words which recruiters (specifically those in the technology space) may not have heard of or understand the meaning of. It is also possible for the same to happen in the opposite direction: a recruiter could use some words and phrases that a candidate may never have heard of.

The goal of this application is to slowly, over time, add more and more basic descriptions of terms and domain-specific language that either a candidate or a recruiter can look up.

## Topics and Pages

Each page within the Recruiter Glossary is designed to give information on a single topic. Most pages will have up to four sections, and will have supporting links throughout:

### 10,000ft Overview

This gives a very un-detailed, sometimes partially incorrect, description of what the topic is. It will be "partially incorrect" as it will be just correct enough to get the point across without bogging anyone down in the details

### Beginner Information

This will be more detailed than the 10,000ft overview - but not by a great deal. The idea here is give someone enough of a basic understanding in order to use this topic/feature/whatever, without having to understand it a great deal.

### Intermediary Information

This will be much more detailed than the beginner information, and will be written in a way that someone who wants to understand what it is that they are doing.

### Advanced Information

This will be a description of the topic in a much more detailed way than any of the others. The idea is that this may be what an expert will be expected to know in an interview setting.

{{< details "why not all sections?" >}}
Sometimes a topic or feature will not require a great deal of explanation before it can be used. As such, not all of the above sections will be provided.
{{< /details >}}

## Search

The Recruitment Glossary has a search function (available at the top left of every page), which you can use to search for anything within the Recruitment Glossary itself. This search function can be accessed by pressing the `Ctrl` + `/` keys on your keyboard, too.

The following is an example of a search being performed for the phrase "git"; the search is being performed on a very early version of the Recruitment Glossary:

{{< picture img="/images/docs/introduction/git-search" alt="a screenshot of the Recruitment Glossary application showing that a user has searched for the word 'git'. The results of the search are shown as a drop-down under the search system" caption="" >}}

## Contributing

This web application is actually hosted on GitHub, and PRs are very much appreciated. You can contribute to the project [here](https://getdoks.org/docs/contributing/how-to-contribute/).

All of the content here is presented under an [MIT license](https://tldrlegal.com/license/mit-license). And the web application is based on the [doks](https://getdoks.org/) theme for [Hugo](https://gohugo.io).

## Building & Running

Next up: building and running locally. [Quick Start →]({{< relref "quick-start" >}})
