---
title: "What is C#?"
description: "Just what is C# and how is it different to .NET?"
lead: "Just what is C# and how is it different to .NET?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "net"
weight: 120
toc: true
---

## 10,000 ft Overview

C# (pronounced "C Sharp") is mixed paradigm programming language - focussing on both object-orientation and functional programming paradigms.

It was first created by Anders Hejlsberg (creator of Turbo Pascal and Delphi), and Mads Torgersen is the current lead designer of the language - Anders has moved on to working on TypeScript.

C# is one of two languages which are officially supported by [.NET]({{< relref "what-is-net" >}}).

{{< alert icon="💡" text="This is an example of a &quot;[lie to children](https://en.wikipedia.org/wiki/Lie-to-children)&quot; in that it isn't 100% technically correct, but correct enough to get the point across. This is because there are a few other languages which are supported by .NET, but the two most common ones are C# and F#." />}}

## Beginner Information

C# is a programming language which is similar to most of the other C-family of programming languages (like C, C++, Java, etc.), and has a mixture of [static](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) and [dynamic](https://en.wikipedia.org/wiki/Dynamic_programming_language) (or "duck") typing (duck typing is supported using th `dynamic` type).

There are a lot of similarities between Java and C#, such as in the following code block (the canonical "Hello, World!" examples).

First, C#:

```csharp
// this example uses the older style C# syntax)
using System;

namespace HelloWorld
{
  public class MyClass
  {
    public static void Main(string[] args)
    {
      Console.WriteLine("Hello, World!");
    }
  }
}
```

And now, Java:

```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Hello, World!");
  }
}
```

## Intermediary Information

## Advanced Information

## External Links

- [Static type checking](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) @ Wikipedia
- [Dynamic programming languages](https://en.wikipedia.org/wiki/Dynamic_programming_language) @ Wikipedia
