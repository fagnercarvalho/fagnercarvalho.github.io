---
layout: post
title: "Live reload in .NET Core"
date: 2020-09-06
comments: true
categories: csharp dotnet aspnet razor console web
---

This week I was looking for a way to do live reloading in ASP.NET Core projects. 

Don't judge me but I actually never cared that much about live reloading, I lived life in a constant state of stopping and starting applications every after a few changes. What changed is that after working with React for a few months I really liked the idea of reflecting changes from your code in the application instantly (well, almost).

For ASP.NET Core projects you need to do a few changes in your code to enable live reloading.

First, you need to install the `Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation` NuGet package into your target application. 

Then add `AddRazorRuntimeCompilation` to your `Startup` class.

{% gist 61291f22668a665f7fd5ebbabf2e597a razorruntime.cs %}

This will enable live reloading for Razor Pages and Views. Don't worry, the reloading will take a few seconds in the first time but it should be faster for subsequent changes.

For enabling the same for C# files you have two options:
* Change your `launchSettings.json` in case you are using Visual Studio.
* Use the `dotnet watch run` command.

If you are using Visual Studio, change the `launchSettings.json` like this:

{% gist 61291f22668a665f7fd5ebbabf2e597a launchsettings-aspnet.json %}

This also works for console apps. In this case use:

{% gist 61291f22668a665f7fd5ebbabf2e597a launchsettings-console.json %}

In case you aren't using Visual Studio (you could be using Rider or VS Code), you can use the `dotnet watch run` command. For this, go to your project folder via command prompt and simply run `dotnet watch run`. You should have the same experience you have in Visual Studio. Nice, isn't it?

Now the .NET CLI will be listening and in case you change a C# file the application will be restarted with your changes applied. For Razor files, the .cshtml files will be recompiled and your changes will be visible in runtime. 

![Live Reloading]({{ site.url }}public/images/LiveReloading.png)

The only missing piece here is actually doing a live reload in the browser. Until right now the changes in C# and Razor files are being reflected in runtime but you need to reload the browser manually. To change this Rick Strahl made [an awesome ASP.NET middleware that does this for you](https://weblog.west-wind.com/posts/2019/Jun/03/Building-Live-Reload-Middleware-for-ASPNET-Core). I will not be talking about this here but this is included in my sample. 

If you want to get access to the source code for the ASP.NET Core and Console applications please go to [ASP.NET Core live reloading](https://github.com/fagnercarvalho/LiveReloadNetCore) and [Console Application live reloading](https://github.com/fagnercarvalho/LiveReloadConsoleNetCore).