---
layout: post

title: Frustration with Umbraco Nested Content
subtitle: 
date: 2016-07-08 15:00:00
tags: [Umbraco]
#category: technology
cover_image: frustrated.jpg

excerpt: "In a more recent project, I discovered that the Nested Content control I have grown to love did not work the way I had initially thought."

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

Over the past several months, I have been using [Umbraco](//umbraco.com) with a few clients and have really enjoyed getting to know the platform.  _So please understand that although I have over 15 years experience developing in C#.NET, I am still learning about the best way to do things in Umbraco_.

**Update:** [Go here](/Use-ListView-to-Add-Child-Nodes.html) to see the solution I decided to use to solve this frustration.  After writing this article I decided to not use the Nested Content plugin at all and was able to actually use the built-in Umbraco controls.

##I need a way to associate a Nested Content node to an Umbraco Member

In a more recent project, I discovered that the [Nested Content](//our.umbraco.org/projects/backoffice-extensions/nested-content/) control, I have grown to love, did not work the way I had initially thought.  I knew it stored the data in a JSON string for the property but it had never dawned on me that it didn't create the **nodes in Umbraco**.  My initial thought was to create an [Umbraco Relation](//umbraco.com/follow-us/blog-archive/2012/12/7/getting-to-know-umbraco-relations/) and associate the Umbraco Member to the Nested Content node.  Sadly, I found this [form post asking a similar question](//our.umbraco.org/projects/backoffice-extensions/nested-content/nested-content-feedback/63488-does-nested-content-get-an-id-value) and as you can see in Matt Bailsford's first response:

> Unfortunately nested content can't have an ID value as they don't truely exist

I did find the [issue/feature](//github.com/leekelleher/umbraco-nested-content/issues/7) that was discussed in the forum post; however, it just adds parent information to the `DetachedPublishedContent` object and doesn't solve my issue.  After reading the form post and the conversations of [Hendy Racher](//github.com/Hendy), [Matt Bailsford](//github.com/mattbrailsford) and [Lee Kelleher](//github.com/leekelleher) in the [github pull request](//github.com/leekelleher/umbraco-nested-content/pull/8), I still don't understand why Nested Content doesn't *create a node in Umbraco*.

So basically I need the Nested Content nodes **to be created as Umbraco nodes** and _then_ stored as a JSON string in the property field.  There are a few ways that I see this could be accomplished:

1. **Create a Custom Property Editor for Umbraco Backoffice** - I would start with a copy of Nested Content and add code to create the node and attach it before saving the node as a JSON string.

2. **Use the [Umbraco Multinode Treepicker control](//our.umbraco.org/documentation/getting-started/backoffice/property-editors/built-in-property-editors/multinode-treepicker)** - This control was suggested by Hendy and Jeavon in [this forum post](//our.umbraco.org/forum/umbraco-7/using-umbraco-7/55537-Multiple-Content-Picker-in-Umbraco-7) as a way to allow a user to select multiple content nodes.  Unfortunately going this route would require the user to create the "nested content" nodes first.  Then they could associate those "nested content" nodes with the original node.  We really like the user experience of the Nested Content control where it allows you to create nodes dynamically in the property editor.

3. **Find a way to associate the Member to the "Nested Content" node** - This option would require that I store an association between the top node and it's respective "nested content" node to a Member in Umbraco.  There are two issues that come to mind when trying to go this route:     
    1. _How should I associate the "nested content" node to the Member in a standard Umbraco way?_ - I immediately think of creating a link table in the database but, in my understanding, that is not the standard Umbraco way.  I am still fuzzy about the best way to do this inside Umbraco.
    2. _Is there a way to uniquely identify the "nested content" node?_ - I realize there is a sort order value being set according to the pull request I found above but if the user reorders the nested content items will it change the "nested content" node to member association?

At this point, I am leaning towards going with **option 1**, but I want to *investigate option 3* a little more as well.  Also I don't believe this is a new problem that someone hasn't already solved, and I hate to create another custom property editor if there is one just like it out there already.  

**So if you know of a better way to solve this problem please let me know.**  Sound off in the comments below or reach out to me via [Twitter](//twitter.com/paulmgower) or [LinkedIn](//linkedin.com/in/pmgower)!

Once I develop or discover the best solution to this problem, I will write another article about how the solution was implemented and update this article to link to it.
