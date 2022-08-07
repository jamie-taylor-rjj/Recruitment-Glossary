---
title: "What is .NET?"
description: "Just what is .NET, why are there lots of different versions, and what can developers do with it?"
lead: "Just what is .NET, why are there lots of different versions, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "net"
weight: 630
toc: true
---

## 10,000 ft Overview

.NET is a term used to describe a number of different technologies, all owned and maintained ny Microsoft. These technologies include (but are not limited to):

- .NET Framework
- .NET Core
- [Xamarin]({{< relref "xamarin/what-is-xamarin" >}})
- [Blazor]({{< relref "blazor/what-is-blazor" >}})
- [Maui]({{< relref "maui/what-is-maui" >}})

## Beginner Information

.NET can usually mean either .NET Framework (a technology for building applications for Windows-only) or .NET Core (for building applcations on Windows, MacOS, or some [Linux distributions]({{< relref  "what-is-linux" >}})).

.NET Framework was originally released in 2002, and .NET Core was originally released in 2016. In November 2020, .NET Core was renamed to .NET for the .NET 5 release; going forward, ".NET" will refer to the cross-platform variant and ".NET Framework" refer to the Windows-only variant.

{{< alert icon="💡" text="It is important to note that .NET Framework (the Windows-only version) is **NOT** going away any time soon." />}}

## Intermediary Information

.NET Core started life as a combination of an open-source re-write of .NET Framework and the Mono runtime. Mono was created as a one-to-one binary equivalent runtime for .NET Framework applications, but was cross-platform.

[Xamarin]({{< relref "xamarin/what-is-xamarin" >}}) was created as a way to build and run applications for Android and iOS (both are Unix-like operating systems), using XAML-like syntax to describe the user interface. When Microsoft bought Xamarin, they started work on better tooling for Xamarin, and started converting the Mono runtime to [Web Assembly](https://webassembly.org/) such that it could be run in the browser; this created the [Blazor]({{< relref "blazor/what-is-blazor" >}}) project.

There was no offical way to build GUI-based when .NET Core was first released (whereas .NET Framework has WinForms, WPF, UWP, and WinUI). But shortly after the release of .NET 6, Microsoft released [.NET Maui]({{< relref "maui/what-is-maui" >}}), which is the next evolution of Xamarin Forms. This allows developers to build GUI-based applications for .NET and run them on:

- Windows
- Android
- iOS
- MacOS
- Web
- Tizen

## Advanced Information

## External Links

- [.NET](https://en.wikipedia.org/wiki/.NET) @ wikipedia
