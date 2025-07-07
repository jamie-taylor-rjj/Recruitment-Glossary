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

<!-- markdownlint-disable MD009-->
{{< highlight fsharp "linenos=inline">}}
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
<!-- markdownlint-enable MD009 -->

## Intermediary Information

F# is designed around immutability by default, which means that once a value is assigned, it cannot be changed. This leads to more predictable code and fewer bugs related to state changes. Here's an example of immutable data structures:

{{< highlight fsharp "linenos=inline">}}
// Immutable record type
type Person = {
    Name: string
    Age: int
}

let person1 = { Name = "Alice"; Age = 30 }
// To "change" a value, you create a new record
let person2 = { person1 with Age = 31 }
{{< /highlight >}}

F# excels at data transformation and processing, making it particularly suitable for:

- Financial modeling and calculations
- Data analysis and scientific computing
- Web APIs and services
- Domain-specific languages (DSLs)

The language provides powerful pattern matching capabilities that allow developers to handle complex data structures elegantly:

{{< highlight fsharp "linenos=inline">}}
type Shape = 
    | Circle of radius: float
    | Rectangle of width: float * height: float
    | Triangle of base: float * height: float

let calculateArea shape =
    match shape with
    | Circle radius -> Math.PI * radius * radius
    | Rectangle (width, height) -> width * height
    | Triangle (base, height) -> 0.5 * base * height
{{< /highlight >}}

## Advanced Information

F# provides advanced features like computation expressions (similar to monads in Haskell), type providers for accessing external data sources, and async workflows for handling asynchronous operations. These features make F# particularly powerful for enterprise applications dealing with complex data processing and integration scenarios.

The language's type system supports algebraic data types, generics, and units of measure, making it excellent for domains requiring mathematical precision and type safety. F# also interoperates seamlessly with existing .NET libraries and can be used alongside C# in the same solution.

For performance-critical applications, F# provides tail-call optimization and efficient collection types. The language's emphasis on immutability and functional programming patterns often leads to more parallelizable code, making it suitable for concurrent and distributed systems.

## External Links

- [Static type checking](https://en.wikipedia.org/wiki/Type_system#Static_type_checking) @ Wikipedia
- [Dynamic programming languages](https://en.wikipedia.org/wiki/Dynamic_programming_language) @ Wikipedia
