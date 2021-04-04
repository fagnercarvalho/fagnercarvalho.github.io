---
layout: post
title: "Free space on Raspberry Pi"
date: 2021-04-04
comments: true
categories: raspberrypi raspberry pi pihole docker disk
---

I have been using a 16GB SD card (I know, could be larger) in a Raspberry Pi for a few years now and never had a problem but recently I started working in a side project and decided to use Docker on this Pi. Because of this I almost filled the SD card in just a few months.

In this post I'm going to give you a few commands that should help you to reclaim some space in your SD card and continue your experiments or side projects. I take no responsibility for any undesired data loss and I ask you to do the proper research about any of the commands posted here. Enjoy!

Also, very important: please backup the contents of your SD card periodically and especially before you start doing this. To do this, run this on Linux in an unmounted partition (not tested, I'm using Windows right now. Yes I know!).

{% gist a5807675864300a2032e497fd3f7e7df backup-raspberrypi.md %}

If you are using Windows use Win32DiskImager, type a file name for your backup image, select your SD card and click Read.

When looking for this topic online the first tip was to remove WolframAlpha and LibreOffice. The thing is, if you want to use Raspbian in a Raspberry Pi that will serve only as a server you want to choose Raspbian Lite and not the full desktop version. In any case, if you already installed the desktop version run the following commands to remove WolframAlpha and LibreOffice:

{% gist a5807675864300a2032e497fd3f7e7df remove-wolfram-libre-office.md %}

If you use Pi-hole you can remove the SQLite database created by Pihole to store logs:

{% gist a5807675864300a2032e497fd3f7e7df remove-pihole-db.md %}

You can also clean the APT cache and remove any unused dependencies.

{% gist a5807675864300a2032e497fd3f7e7df clean-apt.md %}

And finally, run the following command to clean your Docker cache (don't worry, you need to confirm after running the command):

{% gist a5807675864300a2032e497fd3f7e7df clear-docker-cache.md %}

After cleaning everything run a command to see your available space:

{% gist a5807675864300a2032e497fd3f7e7df see-available-space.md %}

If you still don't have enough available space run this command in your root system folder for getting which folders/files are using most of the space in your card:

{% gist a5807675864300a2032e497fd3f7e7df check-used-space.md %}

You will need to check these folders/file one by one and use your judgement to see if they can be deleted or not. Normally you can delete everything from your /tmp folder but I wouldn't mess with anything else.

I hope this helped you, have a good day!