---
title: "What is WPF?"
description: "Just what is WPF, and what can developers do with it?"
lead: "Just what is WPF, and what can developers do with it?"
date: 2020-10-06T08:49:31+00:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "wpf"
weight: 100
toc: true
---

## 10,000 ft Overview

WPF (Windows Presentation Foundation) is Microsoft's flagship desktop application framework for building rich Windows applications. It was first introduced in 2006 as part of [.NET]({{< relref "what-is-net" >}}) Framework 3.0 and provides a comprehensive platform for creating desktop applications with sophisticated user interfaces.

WPF applications are built using [C#]({{< relref "what-is-c-sharp" >}}) (pronounced "C Sharp") or [F#]({{< relref "what-is-f-sharp" >}}) (pronounced "F Sharp") for business logic, combined with XAML (eXtensible Application Markup Language) for defining the user interface.

Unlike traditional Windows Forms applications, WPF uses a vector-based rendering system that provides resolution independence, hardware acceleration, and rich multimedia capabilities including 2D and 3D graphics, animations, and media playback.

## Beginner Information

WPF applications separate the user interface definition (XAML) from the business logic (C#), following the Model-View-ViewModel (MVVM) pattern. A simple WPF window might look like this:

**XAML (MainWindow.xaml):**
{{< highlight xml "linenos=inline">}}
<Window x:Class="MyWpfApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        Title="My WPF Application" Height="350" Width="525">
    <Grid>
        <StackPanel Margin="20">
            <TextBlock Text="Welcome to WPF!" FontSize="24" HorizontalAlignment="Center"/>
            <TextBox x:Name="UserInput" Margin="0,20,0,10" />
            <Button Content="Click Me!" Click="Button_Click" />
            <TextBlock x:Name="OutputText" Margin="0,10,0,0" />
        </StackPanel>
    </Grid>
</Window>
{{< /highlight >}}

**C# Code-Behind (MainWindow.xaml.cs):**
{{< highlight csharp "linenos=inline">}}
using System.Windows;

namespace MyWpfApp
{
    public partial class MainWindow : Window
    {
        public MainWindow()
        {
            InitializeComponent();
        }

        private void Button_Click(object sender, RoutedEventArgs e)
        {
            OutputText.Text = $"Hello, {UserInput.Text}!";
        }
    }
}
{{< /highlight >}}

Key WPF concepts include:
- **XAML**: Declarative markup for UI definition
- **Data Binding**: Connecting UI elements to data sources
- **Controls**: Rich set of built-in UI elements
- **Layouts**: Flexible positioning systems (Grid, StackPanel, DockPanel)
- **Resources**: Reusable styles and templates

## Intermediary Information

WPF provides powerful data binding capabilities that enable the MVVM (Model-View-ViewModel) pattern, separating concerns and making applications more maintainable and testable.

**Data Binding Example:**
{{< highlight xml "linenos=inline">}}
<Window x:Class="DataBindingExample.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">
    <Grid>
        <StackPanel>
            <TextBox Text="{Binding UserName, UpdateSourceTrigger=PropertyChanged}" />
            <TextBlock Text="{Binding Greeting}" FontSize="16" />
            <Button Content="Update" Command="{Binding UpdateCommand}" />
        </StackPanel>
    </Grid>
</Window>
{{< /highlight >}}

**ViewModel Implementation:**
{{< highlight csharp "linenos=inline">}}
public class MainViewModel : INotifyPropertyChanged
{
    private string _userName;
    
    public string UserName
    {
        get => _userName;
        set
        {
            _userName = value;
            OnPropertyChanged();
            OnPropertyChanged(nameof(Greeting));
        }
    }
    
    public string Greeting => $"Hello, {UserName}!";
    
    public ICommand UpdateCommand { get; }
    
    public MainViewModel()
    {
        UpdateCommand = new RelayCommand(UpdateGreeting);
    }
    
    private void UpdateGreeting()
    {
        // Business logic here
    }
    
    public event PropertyChangedEventHandler PropertyChanged;
    
    protected virtual void OnPropertyChanged([CallerMemberName] string propertyName = null)
    {
        PropertyChanged?.Invoke(this, new PropertyChangedEventArgs(propertyName));
    }
}
{{< /highlight >}}

**Advanced Features:**
- **Styles and Templates**: Custom appearance and behavior
- **Animations**: Built-in support for smooth transitions
- **Custom Controls**: Extending WPF's control library
- **Dependency Properties**: Enhanced property system with binding support
- **Routed Events**: Event handling across the visual tree

**Graphics and Media:**
- Vector graphics with scalability
- 2D and 3D graphics capabilities
- Media playback and streaming
- Hardware acceleration via DirectX

## Advanced Information

WPF offers enterprise-grade features for complex desktop applications:

**Performance Optimization:**
- **Virtualization**: Efficient handling of large datasets in ItemsControl
- **Freezable Objects**: Immutable objects for better performance
- **Hardware Acceleration**: GPU-based rendering
- **Memory Management**: Proper disposal of resources and event handlers

**Custom Controls and Templating:**
{{< highlight csharp "linenos=inline">}}
public class CustomButton : Button
{
    public static readonly DependencyProperty CustomTextProperty =
        DependencyProperty.Register("CustomText", typeof(string), 
            typeof(CustomButton), new PropertyMetadata(string.Empty));
    
    public string CustomText
    {
        get => (string)GetValue(CustomTextProperty);
        set => SetValue(CustomTextProperty, value);
    }
    
    static CustomButton()
    {
        DefaultStyleKeyProperty.OverrideMetadata(typeof(CustomButton),
            new FrameworkPropertyMetadata(typeof(CustomButton)));
    }
}
{{< /highlight >}}

**Enterprise Integration:**
- **WCF Integration**: Service-oriented architecture support
- **Entity Framework**: Database integration and ORM
- **Prism Framework**: Modular application development
- **ClickOnce Deployment**: Easy application distribution
- **Accessibility Support**: Built-in accessibility features

**Modern WPF Development:**
- **.NET Core/.NET 5+**: Cross-platform support (Windows only)
- **MVVM Toolkits**: Community and Microsoft MVVM libraries
- **Reactive Extensions**: Reactive programming patterns
- **Dependency Injection**: Modern IoC container support

{{< alert icon="💡" text="While WPF remains a powerful desktop framework, Microsoft has also developed newer alternatives like WinUI 3 for Windows App SDK and [.NET MAUI]({{< relref \"what-is-maui\" >}}) for cross-platform development. However, WPF continues to be actively maintained and is still the preferred choice for many Windows desktop applications." />}}

**Migration and Modernization:**
- WPF applications can be migrated to .NET Core/.NET 5+ for improved performance
- Integration with modern .NET features and tooling
- Containerization support for enterprise deployment
- Cloud integration with Azure services

WPF remains a cornerstone technology for Windows desktop development, offering unmatched flexibility and power for creating sophisticated user interfaces while maintaining excellent performance and enterprise-grade capabilities.

## External Links

- [WPF Documentation](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/) @ Microsoft Docs
- [XAML Overview](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/xaml/) @ Microsoft Docs
- [WPF Architecture](https://docs.microsoft.com/en-us/dotnet/desktop/wpf/advanced/wpf-architecture) @ Microsoft Docs