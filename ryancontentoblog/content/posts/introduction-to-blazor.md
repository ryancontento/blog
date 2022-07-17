---
title: "Introduction to Blazor"
date: 2022-07-03T21:58:06-04:00
draft: false
toc: false
images:
categories: [Blazor, Development]
tags: [.NET, Blazor, C#, Intro]
---

Blazor is Microsofts latest SPA (Single Page Application) framework. Blazor is [open source](<[https://github.com/dotnet/aspnetcore/tree/main/src/Components](https://github.com/dotnet/aspnetcore/tree/main/src/Components)>), cross platform, and uses the power of WebAssembly to allow us to use .NET in the browser! If you love C#, .NET MVC, or just new and interesting frameworks, Blazor may be for you.

![Blazor Logo](/img/blazor.jpg)

## What’s WebAssembly?

WebAssembly (abbreviated *Wasm*) is a binary instruction format for a stack-based virtual machine. Wasm is designed as a portable compilation target for programming languages, enabling deployment on the web for client and server applications. [source: webassembly.org/](<[https://webassembly.org/](https://webassembly.org/)>).

Support of WASM is growing quickly and is supported on Safari, Firefox, and all Chromium based browsers.

WebAssembly is supported by the W3C just like JavaScript, and is here to stay. This is very exciting for a wide range of languages, but we’re here to talk about the implications for C#.

### What Are the Benefits?

- Can leverage previous experience with C#.
- Leverage the existing .NET ecosystem.
- Allows you to share app logic across server and client.
- Still has the ability to utilize JavaScript when needed.

### What Are the Drawbacks?

- Can not fully manipulate the DOM like JavaScript (as of time of writing).
- Long initial load time.

## Components

Like most modern front-end web frameworks, Blazor is built around the concept of UI components. Components in Blazor are elements of UI, such as a pages, dialog boxes, or forms. If you have any experience with .NET MVC, you will instantly recognize a Blazor component (.razor page). That’s correct, just like in MVC, we are using razor pages. This means you have access to all of the power of Razor when building out your entire UI. For those uninitiated with razor, you may be familiar with its JavaScript cousin JSX. Instead of JavaScript, with razor we are writing HTML and C# in the same file. Before Blazor, this was only possible when done on the server, but now this can be done right in the clients browser.

Here is a simple counter component which is also routable (see the @page directive at the top of the file):

```csharp
@page "/counter"

<PageTitle>Counter</PageTitle>

<h1>Counter</h1>

<p role="status">Current count: @currentCount</p>

<button class="btn btn-primary" @onclick="IncrementCount">Click me</button>

@code {
    private int currentCount = 0;

    private void IncrementCount()
    {
        currentCount++;
    }
}
```

That @page directive is all that is needed to create a routable component (page). Another important directive to take note of is the @code directive. This is how you declare a block of C# code on the razor page. There are a number of directives available in Blazor which we will review further in another post. Some of these other directives are:

    - @inject
    - @attribute
    - @ref
    - @layout

## Blazor WASM VS Blazor Server

This is a concept best covered in its own post, but it is worth noting that there are two main hosting options when making a Blazor application. Blazor WASM, the option I personally always choose, is the true full client side WebAssembly app. Blazor WASM will still need to work with an API to do things such as CRUD operations with a database, but on it can run on its own hosted as static files too. Blazor Server uses [SignalR](<[https://docs.microsoft.com/en-us/aspnet/core/signalr/introduction?view=aspnetcore-6.0](https://docs.microsoft.com/en-us/aspnet/core/signalr/introduction?view=aspnetcore-6.0)>) and the server will be handling UI updates. That is where I will leave this topic for now, but there is plenty of information in the Microsoft documentation.

## JavaScript Interoperability

While I noted that one of the drawbacks of Blazor is that it does not have full access to the DOM, you still have access to using JavaScript in these situations via JavaScript interop. If you are doing very straight forward JavaScript, this can be worked out by simply creating a file with the logic and linking to it on the index.html file in the wwwroot of the project. When combining C# and JavaScript logic, there are a number of rules that must be followed. This is something we will dive into deeper in another future post.

## Final Notes

This is just the first of many posts on this awesome framework. I will be getting into some specific tutorials and deeper dives on specific topics in the future. If you have any requests for covering specifics, please feel free to reach out [here](<[https://ryancontento.dev/#contact](https://ryancontento.dev/#contact)>).
