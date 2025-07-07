---
title: "What is .NET MAUI?"
description: "Just what is .NET MAUI, and what can developers do with it?"
lead: "Just what is .NET MAUI, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "net-maui"
weight: 100
toc: true
---

## 10,000 ft Overview

.NET MAUI was originally released to the public alongside .NET 6, in November 2021, and is a cross platform technology, which uses [.NET]({{< relref "what-is-net" >}}) to create cross-platform applications which can target the following platforms:

- Windows
- MacOS
- Android
- iOS

.NET MAUI allows developers to write GUI-based applications in any of the .NET languages (i.e [C#]({{< relref "what-is-c-sharp" >}}) (pronounced "C Sharp") and [F#]({{< relref "what-is-f-sharp" >}}) (pronounced "F Sharp")) rather than platform specific languages.

As with [Xamarin]({{< relref "what-is-xamarin" >}}), .NET MAUI translates .NET API calls to those of the target platform. This allows a developer to write code in using both C# and .NET (for instance) and for it to be used on an Android device (for instance).

## Beginner Information

.NET MAUI follows the "write once, run anywhere" philosophy, allowing developers to share business logic and UI code across multiple platforms. A simple MAUI page might look like this:

{{< highlight csharp "linenos=inline">}}
public partial class MainPage : ContentPage
{
    int count = 0;

    public MainPage()
    {
        InitializeComponent();
    }

    private void OnCounterClicked(object sender, EventArgs e)
    {
        count++;
        CounterBtn.Text = $"Clicked {count} times";
    }
}
{{< /highlight >}}

The corresponding XAML markup:

{{< highlight xml "linenos=inline">}}
<ContentPage x:Class="MyApp.MainPage"
             xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml">
    <ScrollView>
        <VerticalStackLayout Spacing="25" Padding="30,0">
            <Label Text="Welcome to .NET MAUI!" FontSize="18" />
            <Button x:Name="CounterBtn" Text="Click me" Clicked="OnCounterClicked" />
        </VerticalStackLayout>
    </ScrollView>
</ContentPage>
{{< /highlight >}}

MAUI applications use XAML for UI definition and C# for business logic, similar to WPF and Xamarin.Forms. The framework provides native controls that are mapped to platform-specific implementations, ensuring native look and feel on each platform.

## Intermediary Information

.NET MAUI provides several architectural advantages over traditional mobile development:

**Single Project Structure:**

- One project targets multiple platforms
- Shared resources and dependencies
- Platform-specific code when needed
- Conditional compilation for platform differences

**Native Performance:**

- Compiles to native code on each platform
- Direct access to platform APIs
- Hardware acceleration support
- Memory management optimizations

**UI Approaches:**

- XAML for declarative UI
- C# code for programmatic UI
- [Blazor]({{< relref "what-is-blazor" >}}) Hybrid for web-based UI
- Community toolkit for additional controls

Platform-specific features can be accessed through dependency injection:

{{< highlight csharp "linenos=inline">}}
#if ANDROID
public class AndroidSpecificService : ISpecificService
{
    public string GetPlatformInfo()
    {
        return $"Android {Android.OS.Build.VERSION.Release}";
    }
}
#elif IOS
public class iOSSpecificService : ISpecificService
{
    public string GetPlatformInfo()
    {
        return $"iOS {UIKit.UIDevice.CurrentDevice.SystemVersion}";
    }
}
#endif
{{< /highlight >}}

## Advanced Information

.NET MAUI offers advanced capabilities for enterprise mobile development:

**Performance Optimization:**

- Ahead-of-time (AOT) compilation
- Trimming for smaller app sizes
- Native AOT for iOS and Android
- Memory profiling and optimization tools

**Enterprise Features:**

- Authentication and authorization
- Data encryption and secure storage
- API integration with HttpClient
- Offline data synchronization
- Push notifications

**Deployment and Distribution:**

- Microsoft Store integration
- Enterprise app distribution
- Continuous integration/deployment
- App signing and provisioning

**Architecture Patterns:**

- Model-View-ViewModel (MVVM)
- Dependency injection container
- Command pattern for UI actions
- Data binding and templating

MAUI represents the evolution of Microsoft's cross-platform strategy, unifying web and native development under a single framework. It's particularly valuable for organizations with existing .NET expertise who want to expand into mobile development without learning entirely new technology stacks.

## External Links
