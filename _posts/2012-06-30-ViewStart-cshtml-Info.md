---
layout: post

title: _ViewStart.cshtml Info
subtitle:
date: 2012-06-30 14:52:00
tags: [asp.net mvc]
#category: technology
#cover_image: blog-cover.jpg

excerpt: In ASP.NET MVC3 "master pages" are handled in the _ViewStart.cshtml file. As the name suggests the code in this file is executed before each view is

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

In ASP.NET MVC3 “master pages” are handled in the **_ViewStart.cshtml** file. As the name suggests the code in this file is executed before each view is rendered (see [Scott Gu’s blog post](http://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx) for more details).

Now that you understand the basic use of _ViewStart.cshtml file lets go over the scope applied to these files. The _ViewStart.cshtml file will affect all views in the same directory and below the location of it. Also you can have another _ViewStart.cshtml file under a sub-folder which will be executed after the top level _ViewStart.cshtml. Using this feature you can in effect override the top level _ViewStart.cshtml with one closer to the view.

![alt text](images/articles/2012-06-30-viewstart_example.png "ViewStart Example")

Now when the **Index.cshtml view** under the __Home__ folder is rendered, it will first execute the
**/Views/_ViewStart.cshtml** file and then it will render the **Index.cshtml View**.

However, when the **Index.cshtml view** under the <u>DifferentMasterPage</u> folder is rendered, it will
first execute the **/Views/_ViewStart.cshtml** file, then it will execute
the **/Views/DifferentMasterPage/_ViewStart.cshtml** file, and then it will
render the **Index.cshtml View**.
