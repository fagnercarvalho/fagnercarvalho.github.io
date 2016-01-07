---
layout: post
title: "Quick tips for building a API using Nancy"
date: 2016-01-07
comments: true
categories: programming csharp nancy
---

Hello! I writing this brief post to help everyone that is using Nancy for the first time to not make the same mistakes that I did. I'm not even remotely interested in covering all possible aspects involved in developing a web application using Nancy, I just thought I'd share some of my mental notes gathered a few months ago. So, here we go.

## Know how to properly use CORS
If you are using [CORS]({{ site.baseurl }}2014/10/07/CORS-vs-JSONP) avoid to use the wildcard in the Access-Control-Allow-Headers CORS header because he can have unpredictable behavior.

To use CORS in Nancy just do as follows (in Nancy Bootstrapper class):

{% gist 906c8731394019cc04e1 cors.cs %}

## Handle circular reference in JSON serializer
In case you are using Entity Framework and you have a relationship where both entities classes have navigation properties your JSON serializer will throw the following exception:

```
Self referencing loop detected for property 'propertyName' with type 'Models.Entity'.
```

In order to solve this you need to override the default serializer settings with
the ReferenceLoopHandling.Ignore option.

In Nancy, add the following in your Bootstrapper class:

{% gist 906c8731394019cc04e1 serializer.cs %}

## Use OnError pipeline + a good log library
The [OnError pipeline](https://github.com/NancyFx/Nancy/wiki/The-Application-Before,-After-and-OnError-pipelines#intercepting-the-request-when-an-error-occurred) allows you to intercept any unhandled exception in your application. From then on you can log your exception using a log library like [Nlog](http://nlog-project.org) or [log4net](https://logging.apache.org/log4net) along with a cloud logging service like [ExceptionLess](https://exceptionless.com), [Raygun](https://raygun.io) or [PaperTrail](https://papertrailapp.com).

## Avoid using Data Annotations in favor of FluentValidation
This is more of a general advice but always use the FluentValidation library
instead of the default Data Annotations for any server-side validation in your application. FluentValidation is totally decoupled from your POCO, it's easily testable and [offers more customization](https://github.com/JeremySkinner/FluentValidation/wiki) for validating your classes properties.
FluentValidation is fully compatible with Nancy, you just need to install the [Nancy.FluentValidation NuGet package](https://www.nuget.org/packages/Nancy.Validation.FluentValidation).

## Use StaticConfiguration.DisableErrorTraces
In case you are running your application in Debug mode you can see the whole stacktrace from any exception but if you publish your application in IIS or opt for self-host by default you are not going to see any in-depth information about any exception. To solve this problem just add the line `StaticConfiguration.DisableErrorTraces = false;` in your Nancy Bootstrapper `ApplicationStartup` method.

That's all folks!
