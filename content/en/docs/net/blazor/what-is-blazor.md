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

{{< alert icon="💡" text="This section of the page intentionally simplifies all of the Blazor application hosting paradigms. See the [Intermediary Information](#intermediary-information) section for a more in-depth discussion of the different hosting paradigms." />}}

Blazor is a suite of technologies which aims to allow developers to create rich web applications. Code for a Blazor application is written in either [C#]({{< relref "what-is-c-sharp" >}}) (pronounced "C Sharp") and [F#]({{< relref "what-is-f-sharp" >}}) (pronounced "F Sharp"), and can be converted to [Web Assembly](https://webassembly.org/) before it is delivered to the browser.

Initially, Blazor was designed as a way to run .NET applications in the browser using WebAssembly. This was achieved using one of two hosting models:

- Blazor WebAssembly
- Blazor Server

In Blazor WebAssembly, all code in order to run the application is converted to WebAssembly, downloaded to the browser, and runs from there. This paradigm does not require an internet connection once the code has downloaded to the browser, but can lead to large downloads.

In Blazor Server, a small amount of code is downloaded to the browser which sets of a [SignalR]({{< relref "what-is-signalr" >}}) connection to the server. This server is then used to send user actions and receive HTML DOM element updates. This paradigm requires a very small initial download, but requires a stable and constant internet connection in order to use the application.

## Beginner Information

Blazor allows developers to build interactive web applications using C# instead of JavaScript. A simple Blazor component might look like this:

{{< highlight csharp "linenos=inline">}}
@page "/counter"

<h1>Counter</h1>

<p>Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
{{< /highlight >}}

This component demonstrates the basic Blazor syntax where C# code is mixed with HTML using Razor syntax. The `@` symbol is used to transition from HTML to C# code.

Blazor applications are built using components, which are reusable UI elements that encapsulate both markup and logic. Components can accept parameters, handle events, and maintain state, making them similar to modern JavaScript frameworks like React or Angular.

## Intermediary Information

Blazor offers several hosting models to suit different application needs:

**Blazor WebAssembly (WASM):**

- Runs entirely in the browser using WebAssembly
- No server dependency after initial download
- Larger initial payload but better offline experience
- Direct DOM manipulation for better performance

**Blazor Server:**

- Runs on the server with SignalR connection to browser
- Smaller initial download
- Requires constant server connection
- Server-side rendering with real-time updates

**Blazor Hybrid:**

- Combines web technologies with native app frameworks
- Used in [.NET MAUI]({{< relref "what-is-maui" >}}) applications
- Allows sharing UI code between web and native apps

Blazor supports dependency injection, routing, forms validation, and integrates well with existing .NET libraries. It also provides JavaScript interoperability (JSInterop) for calling JavaScript functions from C# and vice versa:

{{< highlight csharp "linenos=inline">}}
@inject IJSRuntime JSRuntime

@code {
    private async Task ShowAlert()
    {
        await JSRuntime.InvokeVoidAsync("alert", "Hello from Blazor!");
    }
}
{{< /highlight >}}

## Advanced Information

Blazor provides advanced features for enterprise applications including:

**Performance Optimization:**

- Virtualization for large datasets
- Prerendering for faster initial loads
- Lazy loading of components and assemblies
- Server-side rendering (SSR) with .NET 8+

**State Management:**

- Cascading parameters for component trees
- State containers for application-wide state
- Integration with Redux-like patterns

**Security:**

- Built-in authentication and authorization
- Integration with ASP.NET Core Identity
- Support for JWT tokens and OAuth providers

**Deployment:**

- Static site generation for JAMstack deployments
- Docker container support
- Azure Static Web Apps integration
- Progressive Web App (PWA) capabilities

Blazor's architecture allows for shared code between client and server, making it particularly attractive for full-stack .NET development teams. The framework continues to evolve with features like streaming rendering, enhanced navigation, and improved JavaScript interoperability.

## External Links
