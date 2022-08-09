---
title: "What is F#?"
description: "Just what is F# and how is it different to .NET and C#?"
lead: "Just what is F# and how is it different to .NET and C#?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "net"
weight: 130
toc: true
---

## 10,000 ft Overview

F# (pronounced "F Sharp") is a functional programming language, which also has object orientation features.

It was designed by Don Syme (creator of the generics type system in C#).

F# is one of two languages which are officially supported by [.NET]({{< relref "what-is-net" >}}).

{{< alert icon="💡" text="This is an example of a &quot;[lie to children](https://en.wikipedia.org/wiki/Lie-to-children)&quot; in that it isn't 100% technically correct, but correct enough to get the point across. This is because there are a few other languages which are supported by .NET, but the two most common ones are C# and F#." />}}

## Beginner Information

F# is a programming language which is similar to Haskell and other functional programming languages. "Functional" here describes the idea that all parts of the application code base should be composed of functions (rather than objects), and that these functions should never alter the global state of the application.

The syntax of an F# program listing can be seen as rather simplified - here is "Hello, world!" in F#:

{{< highlight fsharp >}}
printfn "Hello world!"
{{< /highlight >}}

But don't like the above simplicity fool you, as a more complex programs require a more complex programming style. For instance, here is the Fibonacci sequence in F# (courtesy of [The Sharp Dev](https://thesharperdev.com/posts/fsharp-fibonacci-five-ways/)):

{{< highlight fsharp "linenos=inline">}}
 <!-- markdownlint-disable-next-line -->
let fib5 n = 
    let mutable last = 0
    let mutable next = 1
    seq {
        0
        1
        for i in 1 .. (n - 1) do
            let temp = last + next
            last <- next
            next <- temp
            next
        }

let run = fib5 10 |> Seq.iter (printfn "%d")
{{< /highlight >}}

## Intermediary Information

## Advanced Information

## External Links

- [Static type checking](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) @ Wikipedia
- [Dynamic programming languages](https://en.wikipedia.org/wiki/Dynamic_programming_language) @ Wikipedia
