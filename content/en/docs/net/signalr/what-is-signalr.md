---
title: "What is SignalR?"
description: "Just what is SignalR, and what can developers do with it?"
lead: "Just what is SignalR, and what can developers do with it?"
date: 2023-12-04T11:30:00+01:00
lastmod: 2023-12-04T11:30:00+01:00
draft: false
images: []
menu:
  docs:
    parent: "signalr"
weight: 100
toc: true
---

## 10,000 ft Overview

SignalR is a .NET library which allows developers of ASP .NET and ASP .NET Core applications to create real-time communications between the browser and a web server without having to perform a full page refresh. This allows the server to push code to the browser at a stage after the page has rendered without having to request it using AJAX (for instance).

## Beginner Information

SignalR simplifies real-time web functionality by providing a high-level API for server-to-client communication. A basic SignalR hub might look like this:

{{< highlight csharp "linenos=inline">}}
public class ChatHub : Hub
{
    public async Task SendMessage(string user, string message)
    {
        await Clients.All.SendAsync("ReceiveMessage", user, message);
    }

    public async Task JoinGroup(string groupName)
    {
        await Groups.AddToGroupAsync(Context.ConnectionId, groupName);
    }
}
{{< /highlight >}}

On the client side (JavaScript):

{{< highlight javascript "linenos=inline">}}
const connection = new signalR.HubConnectionBuilder()
    .withUrl("/chathub")
    .build();

connection.on("ReceiveMessage", function (user, message) {
    const msg = user + ": " + message;
    document.getElementById("messagesList").innerHTML += "<li>" + msg + "</li>";
});

connection.start().then(function () {
    document.getElementById("sendButton").addEventListener("click", function () {
        const user = document.getElementById("userInput").value;
        const message = document.getElementById("messageInput").value;
        connection.invoke("SendMessage", user, message);
    });
});
{{< /highlight >}}

SignalR automatically handles the complexity of choosing the best transport method (WebSockets, Server-Sent Events, or Long Polling) based on client and server capabilities.

## Intermediary Information

SignalR provides several advanced features for building robust real-time applications:

**Connection Management:**

- Automatic reconnection with exponential backoff
- Connection lifetime events (connected, disconnected, reconnecting)
- Group management for broadcasting to specific user sets
- User identity mapping for targeted messaging

**Transport Fallbacks:**

- WebSockets (preferred for full-duplex communication)
- Server-Sent Events (for browsers supporting EventSource)
- Long Polling (fallback for older browsers)
- Automatic negotiation between client and server

**Authentication and Authorization:**

{{< highlight csharp "linenos=inline">}}
[Authorize]
public class SecureChatHub : Hub
{
    public async Task SendToUser(string userId, string message)
    {
        await Clients.User(userId).SendAsync("ReceiveMessage", message);
    }

    public override async Task OnConnectedAsync()
    {
        var userId = Context.User.Identity.Name;
        await Groups.AddToGroupAsync(Context.ConnectionId, $"User_{userId}");
        await base.OnConnectedAsync();
    }
}
{{< /highlight >}}

**Scaling Out:**

- Redis backplane for multiple server instances
- Azure Service Bus support
- SQL Server backplane option
- Custom backplane implementations

## Advanced Information

SignalR offers enterprise-grade features for production applications:

**Performance Optimization:**

- Connection pooling and management
- Message buffer control
- Binary message support using MessagePack
- Streaming support for large data transfers

**Monitoring and Diagnostics:**

- Built-in logging and metrics
- Health checks integration
- Performance counters
- Distributed tracing support

**Client Libraries:**

- .NET Client for desktop/mobile apps
- JavaScript/TypeScript for web browsers
- Java client for Android applications
- Python client for cross-platform development

**Advanced Scenarios:**

{{< highlight csharp "linenos=inline">}}
public class AdvancedHub : Hub
{
    public async IAsyncEnumerable<string> StreamData(
        CancellationToken cancellationToken)
    {
        for (var i = 0; i < 100; i++)
        {
            yield return $"Data item {i}";
            await Task.Delay(100, cancellationToken);
        }
    }

    public async Task UploadStream(IAsyncEnumerable<string> stream)
    {
        await foreach (var item in stream)
        {
            // Process streamed data
            await ProcessDataAsync(item);
        }
    }
}
{{< /highlight >}}

SignalR is commonly used in applications requiring real-time updates such as chat applications, live dashboards, collaborative editing tools, gaming applications, and financial trading platforms. Its integration with ASP.NET Core makes it a natural choice for .NET developers building real-time web applications.

## External Links
