---
layout: post

title: Using BIDS 2008 to access TFS 2010
date: 2012-09-04 18:03:00
subtitle: ""
tags: [BIDS 2008, TFS 2010, VS 2008]
#category: technology
#cover_image: blog-cover.jpg

excerpt: "Recently I had a client that needed to use BIDS to create some SSRS reports but they wanted to use TFS2010 for their source control. The latest version"

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

Recently I had a client that needed to use BIDS to create some SSRS reports but they wanted to use TFS2010 for their source control. The latest version of BIDS is really a VS2008 shell so I knew it wouldn't be as simple as installing Team Explorer. I was sure I wasn't the first person to come across this issue so I pulled out my [favorite research tool](http://www.google.com/) and did some research on the exact steps that need to be taken to enable Team Explorer for BIDS 2008.

I found several blog posts about the subject but this [blog post by Joost van Rossum](http://microsoft-ssis.blogspot.com/2012/04/ssis-2008-with-team-foundation-server.html) not only gave me the exact steps to Team Explorer in VS2008 so it would connect with TFS2010 but also was written from the perspective of using BIDS2008 and not just VS2008. Here is an overview of the steps that Joost lined out in his blog post:

1. Install Team Explorer 2008 <sup>[download link](http://www.microsoft.com/en-us/download/details.aspx?id=16338)</sup>
2. Install SP1 for Visual Studio 2008 <sup>[download link](http://www.microsoft.com/en-us/download/details.aspx?id=13276)</sup>
3. Install VSTS 2008 SP1 Forward Compatibility Update for TFS2010 <sup>[download link](http://www.microsoft.com/en-us/download/details.aspx?id=10834)</sup>
4. Once you have all those pieces installed you have to create your server reference like this <sup><nobr>http://&lt;serverName&gt;:&lt;port&gt;/&lt;vdir&gt;/&lt;collectionName&gt;</nobr> <nobr>(e.g. http://TfsServer:8080/tfs/ProjectCollectionName)</nobr></sup> <br />which is different than you do in VS2010.

So I followed the above steps and thought everything was working great until I tried to log in to TFS using BIDS 2008 and received this error message popup:
![alt text](images/articles/2012-09-04-unable_to_switch_servers.png "Unable to switch servers at this time.  The Team Explorer is busy.")


So I went back to my [favorite research tool](http://www.google.com/) to do some more research and came across this [blog post by Tom Hudley](http://technical.blog.thomashundley.com/post/2011/07/21/Team-Explorer-2008-and-TFS-2010.aspx)

At the end of his post I discovered that my problem was with a single character! So as soon as I removed the **/** on the end of my server url everything worked like a charm!

Thanks for the help [Joost](http://microsoft-ssis.blogspot.com/) and [Tom](http://technical.blog.thomashundley.com/)!
