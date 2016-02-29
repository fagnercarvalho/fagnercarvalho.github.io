---
layout: post
title: "Omegle clone using SignalR"
date: 2016-02-28
comments: true
categories: csharp signalr
---

A few days ago I was looking through [SignalR](http://www.asp.net/signalr) and I had the idea to build an Omegle clone. The Omegle one-on-one random chat have a good fit with SignalR, so I decided to try it.

Talking about my implementation in more detail, the two most important parts of my application are the SignalR Hub call `ChatHub` and the `chat.js` file where I added SignalR hub client connection code.

In `ChatHub` the methods `OnConnected` and `OnDisconnected` were overridden from the `Hub` base class so I could add logic for when a new user connects to chat with someone or when disconnects (abruptly or not). Every connection is stored in a static variable `Chats` that are going to be deleted in case the application closes. I also created a `Send` method for when an user sends a message to the other user.

{% gist c8997eb4d77fe91f803c chathub.cs %}

The `Send` method just gets the other user and sends the message to him calling the `receiveMessage`. This method will be declared in the client, `chat.js`.

The `chat.js` is responsible for handling all client logic for connecting and disconnecting from the chat or sending and receiving messages. Every time you send a message your name is showed to you as "You" and "Stranger" to the other party just like Omegle and if you or your partner disconnect from the chat a message appears suggesting to begin a new chat.

Now, a screenshot showing the chat running:

![OmegleR]({{ site.baseurl }}public/images/OmegleR.png)

If you want to get access to the source code please go to [OmegleR GitHub repository](https://github.com/fagnercarvalho/OmegleR).
