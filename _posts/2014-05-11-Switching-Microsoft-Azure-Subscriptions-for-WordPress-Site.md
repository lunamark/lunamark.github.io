---
layout: post

title: Switching Microsoft Azure Subscriptions for WordPress Site
subtitle: 
date: 2014-05-11 20:22:00
tags: [ASP.NET, IIS7, Server Config]
#category: technology
#cover_image: blog-cover.jpg

excerpt: "Have you ever wanted to move your WordPress Microsoft Azure Website from a pay-as-you-go subscription to a BizSpark subscription"

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

Have you ever wanted to move your WordPress [Microsoft Azure Website](http://azure.microsoft.com/) from a pay-as-you-go subscription to the subscription that you get with an [MSDN license](http://msdn.microsoft.com/subscriptions)? It's not as easy as you would think. Today I spent several hours battling with [Microsoft Azure](http://azure.microsoft.com/), [ClearDB](http://www.cleardb.com/) (service Microsoft Azure uses for MySql databases) and [WordPress](http://wordpress.org/) trying to move my website, [lunamark.com](http://lunamark.com/), from my pay-as-you-go subscription to my subscription that is tied to my MSDN license.

A month ago, I setup my new business website lunamark.com using Microsoft Azure Websites. At that time I did not have my MSDN license, so I setup a pay-as-you-go subscription in order to use my custom domain. Moving my website from a pay-as-you-go subscription to the new subscription tied to my MSDN license took longer than I anticipated and required more steps. In the event that you have to move a Microsoft Azure Website between subscriptions, I hope the following notes will make it easier for you.

1. Backup your website
    + Backup the files for the source website by downloading the _wwwroot_ folder using your favorite FTP program (I used [Cyberduck for Mac](http://cyberduck.io/). Find your FTP credentials in the source website's publish profile.
    + Backup your database which is a linked resource to the source website by using _mysqldump_.  If you don't have that on your computer you can download the [MySQL Suite](http://dev.mysql.com/downloads/mysql/) which will include both the _mysqldump_ and _mysql_ commands. Thanks to [John Papa's blog post](http://www.johnpapa.net/azurecleardbmysql/ I was able to do easily backup and restore my MySql database. Here is the command I used on my Mac to backup my database:<br />
    <code style="font-size: small">
    /usr/local/mysql/bin/mysqldump -e -u[user] -p[password]
        -h[host] [database] &gt; [output file]
    </code><br />
    _Note: the -e makes multiple values rows for the insert syntax but is not required_
2. Create a new Microsoft Azure Website (from WordPress gallery). &nbsp;I will refer to this website as the destination website to keep the two straight.
*Note: This will require a new name (new_name.azurewebsites.net). Later we will need to replace the old_name with the new_name in the backup sql file created above.*
3. Get the connection string from the the destination website created in step 2 and use it to update the *wwwroot/wp-config.php* file downloaded from the source website with the new database name and login information.
4. Connect to the destination website with your favorite FTP program and delete the wwwroot folder.
5. Upload the source wwwroot folder with the updated wp-config.php file (which should now be configured to use the destination's MySQL database)
6. Edit the [output file] that was created in step 1 and replace the *old_name* of the website with the *new_name* that was created in step 2
7. Use the _mysql_ command to update your _new_ database.<br />
<code style="font-size: small">
/usr/local/mysql/bin/mysql u[user] -p[password]
    -h[host] [database] &lt; [input file]
</code><br />
*Note: the [input file] would be the name of the [output file] that was created above and modified to replace the name of the old_name with the new_name of the Microsoft Azure Website*
8. Make sure you remove the old Microsoft Azure Website's reference to the custom domain name you are planning to use.
9. Now set it up your custom domain in the new Microsoft Azure Website.
10. Last, I would recommend stopping the old Microsoft Azure Website to verify the new website is working as desired before deleting the old website

**Please Note:** The steps described above will require some downtime for your website. If downtime on your website is not an option, then watch [this Scott Hanselman video](http://www.hanselman.com/blog/PennyPinchingVideoMovingAnAzureWebsiteBetweenDataCenters.aspx) where he recommends to use a load balancer to not have any downtime.