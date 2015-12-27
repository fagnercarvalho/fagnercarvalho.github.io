---
layout: post
title: "CORS vs JSONP"
date: 2014-10-07
comments: true
categories: programming web
redirect_from: "programming/web/2014/10/07/CORS-vs-JSONP/"
---

Hello!
So, here I am again! Sorry for the delay, almost 2 months since I last posted here. Anyway, I here today to talk about CORS and JSONP. Basically I will introduce the terms and cite some implementation examples using JavaScript and ASP.NET WebAPI (because I am a .NET fan, of course!).


## JSONP
First I will talk about JSONP. The acronym stands for "JSON with padding". We have a lot of resources telling about the concept in the internet today, so I will be short. "JSON with padding" its basically a hack that makes possible inter-domain requests. And that's it. This hack consists from return a function (often named 'callback' or whathever you want) that receives a JSON parameter like the following.

{% highlight javascript %}
processJSON({ 'name': 'Fagner', 'age': '22' })
{% endhighlight %}

A lot of APIs from well know companies like Instagram and Github provides JSONP APIs to developers. [Click here](http://www.programmableweb.com/category/all/apis?search_id=137822&data_format=21174) to access a list of JSON APIs available today. The main advantage to use JSONP is the the compatibility with some old browsers like IE 7< and the main disadvantage concerns the security: like I said before JSONP is a hack created when nobody had a option to make cross-domain requests, so the creators didn't seem to be bothered too much by security.

In the code below you can see a simple example using the polymer-jsonp [web component](http://customelements.io/) to do a simple JSONP request to the Battelfield 4 API.

{% highlight javascript linenos %}
<polymer-jsonp auto url="http://api.bf4stats.com/api/playerInfo?name={{name}}&plat={{platform}}&output=jsonp&opt=names,imagePaths&callback="
response="{{response}}" on-polymer-response="{{responseHandler}}"/>
{% endhighlight %}

## CORS
Instead of using a hack you can use a better a safe way: CORS.
CORS stands for "Cross-Origin Resource Sharing". CORS introduced a new HTTP header to allow cross-domain requests called "Access-Control-Allow-Origin".

Using ASP.NET WebAPI, If you want to enable CORS you just need to follow this 3 simple steps:

1. Install the package Microsoft.AspNet.WebApi.Cors using NuGet;

2. Insert the following line of code in our WebApiConfig located in the App_Start folder:

{% highlight csharp %}
config.EnableCors();
{% endhighlight %}

3. Insert the EnableCorsAttribute in all ours Controllers that you interested in enabling CORS.

{% highlight csharp %}
[EnableCors(origins: "http://fagner.azurewebsites.net", headers: "*", methods: "*")]
{% endhighlight %}

So, thats it! If you have any questions you are free to ask in the commentary box below.

Have a nice day!
