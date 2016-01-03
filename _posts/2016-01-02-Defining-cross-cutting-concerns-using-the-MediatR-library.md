---
layout: post
title: "Defining cross cutting concerns using the MediatR library"
date: 2016-01-02
comments: true
categories: programming csharp architecture
---

Hello! A few months ago I did a freelance gig in which I found myself having trouble to define where exactly to put things like logging, authentication, persistence common logic and so on. These elements are somehow detached from the core business logic and are very similar or exact the same in every application. If you decide to insert them in all your methods you are going to have a lot of repeated and unmaintainable code very fast.

This things are commonly called 'cross-cutting concerns', a concept brought from Aspect-Oriented programming, and they unfortunately don't work well with Object-Oriented programming [[1]](#ref1). This happens because in every object you feel the need to use a cross-cutting concern you are going to reference a object that defines the concern you are looking for, like a Logger class. Now imagine that you need to audit your code and so every operation happening in your system needs to be logged. Yes, this is bad.

![Cross-cutting in OO]({{ site.baseurl }}public/images/cross-cutting-in-oo.png)
<small>
Figure 1. Crosscutting concerns in a OO language (from Rashid, 2010, p. 24)
</small>

Now, a great way to solve this was using a library called [MediatR](https://github.com/jbogard/MediatR) ([note](#note)). MediatR is mediator design-pattern implementation in .NET that allows the developer to execute commands following the [CQRS pattern](http://martinfowler.com/bliki/CQRS.html).
My first contact with the library was when I read a article about, guess what, [Tackling cross-cutting concerns with a mediator pipeline](https://lostechies.com/jimmybogard/2014/09/09/tackling-cross-cutting-concerns-with-a-mediator-pipeline/). I recommend you to read the article before continue reading this post because he defines the whole class structure that I using to build the concerns implementation below.

So, after I read the article I immediately decided to use the library and define a application framework for my next project and it's been a huge success so far. I going to share code snippets from some of the concerns that I implemented. They are very simple but show how you can separate repeated cross-cutting code from what really matters in your application: the business core.

First, the `ExceptionHandler`, handling unexpected exceptions and throwing validation exceptions made by the Validation handler (implementation available in the Jimmy article linked above).

{% gist f6f0cb4ddf3880a8826d exception-handler.cs %}

The `DatabaseHandler`, that wraps a transaction using Entity Framework for every request executed and also logs every SQL executed against the database during the transaction lifetime.

{% gist f6f0cb4ddf3880a8826d database-handler.cs %}

`LoggingHandler` class used to log every request and response object.

{% gist f6f0cb4ddf3880a8826d logging-handler.cs %}

Last but not least, `Logger.cs` class used in both `LoggingHandler` and `DatabaseHandler` classes.

{% gist f6f0cb4ddf3880a8826d logger.cs %}

So, that's it. If you want to learn more [download MediatR from NuGet](https://www.nuget.org/packages/MediatR/) and read [Jimmy MediatR articles at LosTechies](https://www.google.com.br/search?q=mediatr+site:https:%2F%2Flostechies.com).

<a name="note"></a> **Note** This framework was developed by Jimmy Bogard, the same guy behind AutoMapper (please, if you don't know what AutoMapper is please access the [AutoMapper documentation here](https://github.com/AutoMapper/AutoMapper/wiki) and
learn the basics at least!).

<a name="ref1"></a> [1] Rashid, Awais (2013). Aspect-Oriented Database Systems. United Kingdom: Springer.
