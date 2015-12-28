---
layout: post
title: "Using dependency injection in MongoDB CSharp Driver"
date: 2015-01-14
comments: true
categories: programming csharp
redirect_from: "programming/csharp/2015/01/14/Dependency-Injection-MongoDB-CSharp/"
---

Hello! So, it seems that I delayed once again new posts in here. Since I promisse to no one that I need to post here on regular basis I dont think that I need to apologize, hehe (just kidding). So, as the title says I here to talk a little about dependency injection and post a code snippet about using DI on MongoDB CSharp Driver basic classes.

## Dependency Injection

If you dont want to know or already know the concept behind dependency injection, [just jump to the code](#code).
As you may know dependency injection helps us programmers to control code dependencies easier. When you use dependency injection (or DI) depending on the language that you are using you just need to use a attribute, annotation or something else that helps to inject (like the name says, doh!) the dependencies into your code without the need to instantiate or set the objects manually.

For example, in Java, using Spring Framework, you just use something like this:

{% gist 19a0af7b0234bf8b0b55 di.java %}

In AngularJS, the $scope parameter passed thought every Controller on your app that represents the DOM elements from the page are created using dependency injection:

{% gist 19a0af7b0234bf8b0b55 di.js %}

And finally, in C#, using Ninject:

{% gist 19a0af7b0234bf8b0b55 di.cs %}

You can have 3 types of DI:

- Constructor injection: most common one. Just inject your dependencies in the object constructor;
- Setter injection: associate object dependencies using setter methods.
- Interface injection: associate dependencies using setter methods defined in interfaces.

Ninject provides a very elegant way to perform DI on C#, and my MongoDB code snippet posted right below was made using this framework, but you have many other options for use DI on C# like [Unity](http://msdn.microsoft.com/en-us/library/ff647202.aspx) or [Autofac](http://autofac.org/) frameworks.

## <a name="code"></a> DI on MongoDB CSharp Driver

MongoDB CSharp Driver, as the name says, is a library provived to access MongoDB databases using C#. In this library you have classes like MongoCollection, MongoDocument, MongoDatabase and so on that helps to interact with a MongoDB instance and develop a application with MongoDB and C# together as backend.

The code snippet below provides a simple way to use DI with Ninject to instantiate MongoDB Driver classes.
You just need to associate classes to interfaces and say to Ninject that he needs to create a Object instance when a IObject is indicated.

{% gist 19a0af7b0234bf8b0b55 di-mongo.cs %}

Then you just need to create your code and Ninject, if properly configured, will instantiate your objects automatically.

{% gist 19a0af7b0234bf8b0b55 repository.cs %}

So, thats it! If you have any questions you are free to ask in the commentary box below.

See you later!
