---
title: "What is Xamarin?"
description: "Just what is Xamarin, and what can developers do with it?"
lead: "Just what is Xamarin, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2020-10-06T08:49:31+00:00
draft: false
images: []
menu:
  docs:
    parent: "xamarin"
weight: 100
toc: true
---

{{< alert icon="⚠️" text="Microsoft has announced that Xamarin has being superseded by [.NET MAUI]({{< relref \"what-is-maui\" >}}), which provides the next evolution of cross-platform development with .NET. Xamarin is no longer supported, and all projects using Xamarin should be migrated to .NET MAUI for future development." />}}

## 10,000 ft Overview

Xamarin was a technology created by a team of developers lead by [Miguel de Icaza](https://en.wikipedia.org/wiki/Miguel_de_Icaza). It used the [Mono runtime]({{< relref "what-is-mono" >}}) in order to build applications for iOS and Android.

This was an important innovation, as it allowed developers to use both [.NET]({{< relref "what-is-net" >}}) and [C#]({{< relref "what-is-c-sharp" >}}) (pronounced "C Sharp") to build mobile applications; allowing them to have a single code base, in a common language, rather than separate code bases for iOS (using Swift) and Android (using either Java or Kotlin).

## Beginner Information

Xamarin applications are built using [C#]({{< relref "what-is-c-sharp" >}}) and XAML, allowing developers to share business logic across platforms while maintaining native UI performance. A simple Xamarin.Forms page might look like this:

{{< highlight csharp "linenos=inline">}}
public partial class MainPage : ContentPage
{
    public MainPage()
    {
        InitializeComponent();
    }

    private void OnButtonClicked(object sender, EventArgs e)
    {
        DisplayAlert("Hello", "Welcome to Xamarin!", "OK");
    }
}
{{< /highlight >}}

With corresponding XAML:

{{< highlight xml "linenos=inline">}}
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="MyApp.MainPage">
    <StackLayout Padding="10,35,10,10">
        <Label Text="Welcome to Xamarin.Forms!" FontSize="Medium" />
        <Button Text="Click Me" Clicked="OnButtonClicked" />
    </StackLayout>
</ContentPage>
{{< /highlight >}}

Xamarin comes in two main flavors:

- **Xamarin.Forms**: Cross-platform UI toolkit with shared UI code
- **Xamarin.Native**: Platform-specific UI with shared business logic

Both approaches allow developers to access native APIs and achieve native performance while sharing significant amounts of code between iOS and Android applications.

## Intermediary Information

Xamarin provides several architectural advantages for mobile development:

**Code Sharing Strategies:**

- Shared business logic and data access
- Platform-specific UI implementations
- Dependency injection for platform services
- Custom renderers for platform-specific behavior

**Native API Access:**

{{< highlight csharp "linenos=inline">}}
// iOS-specific code
#if __IOS__
using UIKit;
public void ShowNativeAlert()
{
    var alert = UIAlertController.Create("Title", "Message", UIAlertControllerStyle.Alert);
    alert.AddAction(UIAlertAction.Create("OK", UIAlertActionStyle.Default, null));
    UIApplication.SharedApplication.KeyWindow.RootViewController.PresentViewController(alert, true, null);
}
#endif

// Android-specific code
#if __ANDROID__
using Android.App;
public void ShowNativeAlert()
{
    var builder = new AlertDialog.Builder(this);
    builder.SetTitle("Title");
    builder.SetMessage("Message");
    builder.SetPositiveButton("OK", (dialog, which) => { });
    builder.Show();
}
#endif
{{< /highlight >}}

**Data Binding and MVVM:**

- Two-way data binding between UI and ViewModels
- Command pattern for user interactions
- Property change notifications
- Dependency injection for services

**Performance Considerations:**

- Native compilation for each platform
- Ahead-of-time (AOT) compilation on iOS
- Linker optimization for app size reduction
- Platform-specific optimizations

## Advanced Information

Xamarin offers enterprise-grade features for large-scale mobile development:

**Testing and Quality Assurance:**

- Xamarin.UITest for automated UI testing
- Unit testing with platform-specific test runners
- Cloud testing with Xamarin Test Cloud
- Code coverage and performance profiling

**Enterprise Integration:**

- Microsoft Enterprise Mobility + Security integration
- Azure Active Directory authentication
- Mobile Application Management (MAM)
- Certificate pinning and app wrapping

**Development Workflow:**

- Visual Studio integration with debugging
- Hot reload for rapid development
- Xamarin.Forms Shell for navigation
- CollectionView for performant lists

**Migration Path:**

{{< alert icon="⚠️" text="Microsoft has announced that Xamarin has being superseded by [.NET MAUI]({{< relref \"what-is-maui\" >}}), which provides the next evolution of cross-platform development with .NET. Xamarin is no longer supported, and all projects using Xamarin should be migrated to .NET MAUI for future development." />}}

Xamarin paved the way for modern cross-platform development by proving that native performance and shared code could coexist. Many of its concepts and patterns have been carried forward into [.NET MAUI]({{< relref "what-is-maui" >}}), making it an important foundation technology in the Microsoft ecosystem.

Legacy Xamarin applications can be migrated to .NET MAUI using Microsoft's migration tools and guidance, allowing teams to modernize their mobile applications while preserving their existing investments.

## External Links
