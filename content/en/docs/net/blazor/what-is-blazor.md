---
title: "What is Blazor?"
description: "Just what is Blazor, and what can developers do with it?"
lead: "Just what is Blazor, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "Blazor"
weight: 100
toc: true
---

## 10,000 ft Overview

{{< alert icon="💡" text="This section of the page intentionally simplifies all of the Blazor application hosting paradigms. See the [Advanced Information](#advanced-information) section for a more in-depth discussion of the different hosting paradigms." />}}

Blazor is a suite of technologies which aims to allow developers to create rich web applications. Code for a Blazor application is written in either [C#]({{< relref "what-is-c-sharp" >}}) (pronounced "C Sharp") and [F#]({{< relref "what-is-f-sharp" >}}) (pronounced "F Sharp"), and can be converted to [Web Assembly](https://webassembly.org/) before it is delivered to the browser.

Initially, Blazor was designed as a way to run .NET applications in the browser using WebAssembly. This was achieved using one of two hosting models:

- Blazor WebAssembly
- Blazor Server

In Blazor WebAssembly, all code in order to run the application is converted to WebAssembly, downloaded to the browser, and runs from there. This paradigm does not require an internet connection once the code has downloaded to the browser, but can lead to large downloads.

In Blazor Server, a small amount of code is downloaded to the browser which sets of a [SignalR]({{< relref "what-is-signalr" >}}) connection to the server. This server is then used to send user actions and receive HTML DOM element updates. This paradigm requires a very small initial download, but requires a stable and constant internet connection in order to use the application.

## Beginner Information

## Intermediary Information

## Advanced Information

## External Links
