---
title: "What is Mono?"
description: "Just what is Mono, and what can developers do with it?"
lead: "Just what is Mono, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "mono"
weight: 100
toc: true
---

## 10,000 ft Overview

Mono is a reimplementation of .NET Framework, written entirely in C++. It was created by a team of developers lead by [Miguel de Icaza](https://en.wikipedia.org/wiki/Miguel_de_Icaza) as .NET Framework only ran on Windows. The goal for Mono was to make an unofficial platform agnostic .NET Runtime.

The work done by de Icaza and the rest of the time directly lead to the creation of [Xamarin]({{< relref "what-is-xamarin" >}}), .NET Core (and modern .NET), [Blazor]({{< relref "what-is-blazor" >}}), and [.NET MAUI]({{< relref "what-is-maui" >}}).

## Beginner Information

Mono was created to bring .NET Framework capabilities to Linux and macOS systems. It implements the Common Language Runtime (CLR), Base Class Library (BCL), and C# compiler, allowing .NET applications to run on Unix-like systems.

A simple C# application that runs on Mono looks identical to one running on .NET Framework:

{{< highlight csharp "linenos=inline">}}
using System;

namespace HelloMono
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello from Mono!");
            Console.WriteLine($"Running on: {Environment.OSVersion}");
        }
    }
}
{{< /highlight >}}

Mono achieved this by reverse-engineering the .NET Framework APIs and implementing them from scratch, ensuring binary compatibility with .NET applications. This meant that existing .NET applications could often run on Mono without any code changes.

The key components of Mono include:

- **Runtime Engine**: Executes .NET bytecode
- **Class Libraries**: Implementation of .NET Framework APIs
- **C# Compiler**: Compiles C# source code to bytecode
- **Development Tools**: Debugger, profiler, and other utilities

## Intermediary Information

Mono's architecture provided several innovative solutions to cross-platform .NET development:

**Ahead-of-Time (AOT) Compilation:**

Mono introduced AOT compilation, which translates .NET bytecode to native machine code at build time rather than runtime. This provided performance benefits and reduced startup times:

{{< highlight bash >}}
# Compile with AOT
mono --aot=full MyApplication.exe
{{< /highlight >}}

**Embedding Mono:**

Mono could be embedded into native applications, allowing C/C++ programs to host .NET code:

{{< highlight c "linenos=inline">}}
#include <mono/jit/jit.h>
#include <mono/metadata/assembly.h>

int main() {
    MonoDomain *domain = mono_jit_init("MyApp");
    MonoAssembly *assembly = mono_domain_assembly_open(domain, "MyApp.exe");

    // Execute managed code
    mono_jit_exec(domain, assembly, 0, NULL);
    
    mono_jit_cleanup(domain);
    return 0;
}
{{< /highlight >}}

**Platform Integration:**

Mono provided platform-specific bindings for native libraries:
- **MonoMac**: macOS Cocoa API bindings
- **MonoTouch**: iOS API bindings (predecessor to Xamarin.iOS)
- **Gtk#**: GTK+ bindings for Linux desktop applications

**WebAssembly Pioneer:**

Mono was one of the first runtimes to compile to WebAssembly, enabling .NET code to run in web browsers. This work directly led to [Blazor]({{< relref "what-is-blazor" >}}) WebAssembly.

## Advanced Information

Mono's contributions to the .NET ecosystem were foundational and far-reaching:

**Technical Innovations:**

- **Generational Garbage Collector**: Advanced memory management
- **LLVM Backend**: Integration with LLVM for optimized code generation
- **Continuous Integration**: Early adoption of automated testing across platforms
- **Static Linking**: Ability to create self-contained native executables

**Performance Optimizations:**

- **Profile-Guided Optimization**: Runtime profiling for better optimization
- **Tiered Compilation**: Adaptive optimization based on usage patterns
- **Memory Mapping**: Efficient loading of assemblies and resources

**Enterprise Features:**

- **COM Interop**: Integration with Windows COM components on Linux
- **SIMD Support**: Vector operations for performance-critical code
- **Debugging Tools**: Cross-platform debugging capabilities

**Legacy and Evolution:**

Mono's influence extends throughout the modern .NET ecosystem:

- **Xamarin Platform**: Built on Mono runtime for mobile development
- **.NET Core**: Incorporated many Mono innovations and architectural decisions
- **Unity Game Engine**: Uses Mono as its scripting runtime
- **WebAssembly Support**: Mono's WASM work became the foundation for Blazor

{{< alert icon="📚" text="While Mono continues to be maintained and used in specific scenarios like Unity and legacy Xamarin applications, Microsoft's focus has shifted to the unified .NET platform (.NET 5+) which incorporates the best aspects of both .NET Framework and Mono." />}}

Mono demonstrated that open-source implementations of proprietary technologies could not only match but often exceed the original in terms of innovation and cross-platform capability. Its legacy lives on in virtually every modern .NET cross-platform technology.

## External Links
