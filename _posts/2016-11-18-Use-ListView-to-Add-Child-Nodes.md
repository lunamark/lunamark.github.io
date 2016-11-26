---
layout: post

title: Use ListView to Add Child Nodes
subtitle: 
date: 2016-11-18 15:00:00
tags: [Umbraco]
#category: technology
cover_image: stone-relaxation.jpg

excerpt: ""

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

In a [previous blog post](/Frustration-with-Umbraco-Nested-Content.html), I wrote about my frustration with the Nested Content plugin due to my unique requirements for my current project.  However, as I have learned more about Umbraco I have discovered a better way to implement a solution with built-in [Umbraco](//umbraco.com).

##Instead of Nested Content control, just create child nodes using List View.

The main reason for using the [Nested Content](//our.umbraco.org/projects/backoffice-extensions/nested-content/) control was because we liked the user experience when adding child nodes to the parent node but as described in my previous post unfortunately Nested Content doesn't create _real_ nodes as I initially thought.  So to get a decent user experience we decided to use the a ListView property editor for the children nodes.  This way they are created as **_real_ Umbraco nodes** and then I can use an [Umbraco Relation](//umbraco.com/follow-us/blog-archive/2012/12/7/getting-to-know-umbraco-relations/) to associate the child node(s) to the Umbraco Member account.

###How to use ListView property instead of Nested Content

This might be something that is really easy to understand for more _experienced_ Umbraco developers but I decided to describe the steps I used in case someone else has a similar problem and is new to Umbraco.

1. **Add a property**    
[![Add a property](/images/articles/2016-11-26-01-add-property_thumb.jpg)][add-property]

2. **Select the ListView editor**    
[![ListView property](/images/articles/2016-11-26-02-listview-property-editor_thumb.jpg)][select-listview]

3. **Setup the ListView property (default name is _DocuentType - PropertyName - PropertyType_)**    
[![ListView property](/images/articles/2016-11-26-03-listview-property-default-name_thumb.jpg)][setup-listview]

4. **Submit the property**  
[![ListView property](/images/articles/2016-11-26-04-listview-property-set_thumb.jpg)][submit-property]

5. **Set Parent's DocumentType Permissions**  
[![ListView property](/images/articles/2016-11-26-05-permissions_thumb.jpg)][parent-permissions]

6. **Choose Child's DocumentType**  
[![ListView property](/images/articles/2016-11-26-06-permissions-child_thumb.jpg)][choose-child]

7. **Notice Child's DocumentType is added**  
[![ListView property](/images/articles/2016-11-26-07-permissions-child-added_thumb.jpg)][child-added]

8. **Now you can add children via ListView's Create option**  
[![ListView property](/images/articles/2016-11-26-08-listview-example-child_thumb.jpg)][child-create-available]

[add-property]: /images/articles/2016-11-26-01-add-property.jpg "Click to see larger screenshot"
[select-listview]: /images/articles/2016-11-26-02-listview-property-editor.jpg "Click to see larger screenshot"
[setup-listview]: /images/articles/2016-11-26-03-listview-property-default-name.jpg "Click to see larger screenshot"
[submit-property]: /images/articles/2016-11-26-04-listview-property-set.jpg "Click to see larger screenshot"
[parent-permissions]: /images/articles/2016-11-26-05-permissions.jpg "Click to see larger screenshot"
[choose-child]: /images/articles/2016-11-26-06-permissions-child.jpg "Click to see larger screenshot"
[child-added]: /images/articles/2016-11-26-07-permissions-child-added.jpg "Click to see larger screenshot"
[child-create-available]: /images/articles/2016-11-26-08-listview-example-child.jpg "Click to see larger screenshot"

**Would enjoy discussing with you a different way to solve this problem!**  Sound off in the comments below or reach out to me via [Twitter](//twitter.com/paulmgower) or [LinkedIn](//linkedin.com/in/pmgower)!