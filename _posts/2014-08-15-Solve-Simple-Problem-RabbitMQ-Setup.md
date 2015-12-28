---
layout: post
title: "Solve a simple problem during RabbitMQ setup in Windows"
date: 2014-08-15
comments: true
categories: programming csharp
redirect_from: "programming/csharp/2014/08/15/Solve-Simple-Problem-RabbitMQ-Setup/"
---

![RabbitMQ]({{ site.baseurl }}public/images/RabbitMQLogo.png)

Hello!
So, for you that dont know what is exactly RabbitMQ, let me briefly explain before anything else: RabbitMQ is a framework that provides a messaging system based on the AMQP standard ([click here to know more](http://en.wikipedia.org/wiki/Advanced_Message_Queuing_Protocol)).

Considering my experience developing Microsoft solutions today I got interested in learn how to use [EasyNetQ](https://github.com/mikehadlow/EasyNetQ), a .NET API implementation for RabbitMQ. Before trying to do anything using EasyNetQ I start following the Quick Start Guide for EasyNetQ and had some problems. This post focus on those problems and describes a simple way to solve them.

First you just need to follow the previously cited Quick Start Tutorial [clicking here](https://github.com/mikehadlow/EasyNetQ/wiki/Quick-Start).

If you follow this tutorial carefully everything will run smoothly but if you are like me maybe you pass through the same problems.
At first I was struggling trying to find a way to install the management plugin, a plugin that provides a nice web interface where you can manage your server queues. So, after awhile, I discover that I need to run the following command (using cmd):

{% gist d64236bf015c3a263d0d enable-rabbitmq.cmd %}

This command need to be executed pointing to the 'C:\Program Files (x86)\RabbitMQ Server\rabbitmq_server-version\sbin' folder. But, for some reason, I cant seem to access my interface presumably located in http://localhost:15647. After spending some time I found and run a rabbitmq-server.bat located in the sbin folder, where I finally can see my error:

{% gist d64236bf015c3a263d0d weird-error %}

For some reason RabbitMQ cant seem to know that MYHOST need to be translated to localhost/127.0.0.1 resulting in a server shutdown. To solve this particular problem I just needed to run the following command in cmd:

{% gist d64236bf015c3a263d0d set-computername.cmd %}

After that I run this command in the sbin folder:

{% gist d64236bf015c3a263d0d restart-rabbitmq.cmd %}

After that my server starts succesfully and I finally can use the EasyNetQ!

So, thats it! If you have any questions you are free to ask in the commentary box below.

Have a nice day!
