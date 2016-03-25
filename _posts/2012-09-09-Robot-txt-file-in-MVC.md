---
layout: post

title: Robots.txt file in MVC3
subtitle: ""
date: 2012-09-19 00:14:00
tags: [asp.net mvc]
#category: technology
#cover_image: blog-cover.jpg

excerpt: "Recently I was asked to look at adding a robots.txt file to a client's website that we built on ASP.NET MVC3. So I did some research and found out"

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

Recently I was asked to look at adding a robots.txt file to a client's website that we built on ASP.NET MVC3. So I did some [research](http://www.google.com/) and found out some interesting information about the robots.txt file.

1. The file is just a suggestion and bots are [not require](http://www.robotstxt.org/faq/blockjustbad.html) to follow what you ask them to do via the robots.txt file.
2. The file is really an exclusion list instead of an inclusion list. This means you have to put the places you don't want the bots to view which could be a bad idea in that it would give the bad bots areas they should focus on hacking.

After using my [favorite research tool](http://www.google.com/) we decided to not put a robots.txt file on the website initially. Soon after our deploy we noticed in the [ELMAH](http://code.google.com/p/elmah/) logs that we were seeing a considerable amount of errors which contained this error message:

> The controller for path '/robots.txt' was not found or does not implement IController.

So now we decided we at least needed an empty robots.txt file out there to prevent all these unnecessary errors. So I did some more [research](http://www.google.com/ and developed a solution for MVC3:
+ Basically you just add the physical robots.txt file to the website by adding it to the project at the root level. It could be empty or could contain the basic level of content required in a robots.txt.

Now that you have the physical file on the website it will ignore the ASP.NET MVC3 routing as long as you haven't changed [the default setting of the RouteExistingFiles property of the RouteCollection which will ignore routing if a physical file is found that matches the URL pattern](http://msdn.microsoft.com/en-us/library/cc668201%28v=vs.100%29.aspx#scenarios_when_routing_is_not_applied).

To ensure that the physical file will always be served up even if someone changes the RouteExistingFiles property you can add the following ignore route code to the global.asax.cs file:<br />

<pre><code class="csharp">routes.IgnoreRoute("{robotstxt}", new {robotstxt=@"(.*/)?robots.txt(/.*"});</code></pre>

Your mileage may vary with the robots.txt file and it might not be a bad idea to have a robots.txt with some exclusions if you really need to exclude some of your content from web crawlers or bots.

This particular client didn't really need one because most if not all the content of their website required that you log into their website so bots and web crawlers wouldn't get much content from crawling their entire site.
