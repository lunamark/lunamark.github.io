---
layout: post

title: Setting up DBMail in SQL Server 2012
subtitle: 
date: 2012-11-13 20:23:00
tags: [Database Mail, DBMail, SQL Server 2012]
#category: technology
#cover_image: blog-cover.jpg

author:
  name: Paul Gower
  twitter: paulmgower
  #gplus: 100687498195339762535 
  bio: Principal Consultant / Owner, Lunamark
  image: paul.jpg
---

Recently I needed to setup database mail in SQL Server 2012 and here is what I did (so if/when i have to do it again I will remember how to do it):

Run this script to create the sysmail account and profile:
<pre><code class="sql">use msdb
GO
DECLARE @ProfileName VARCHAR(255)
DECLARE @AccountName VARCHAR(255)
DECLARE @SMTPAddress VARCHAR(255)
DECLARE @EmailAddress VARCHAR(128)
DECLARE @DisplayUser VARCHAR(128)

SET @ProfileName = 'DefaultDBMailProfile';
SET @AccountName = 'DefaultDBMailAccount';
SET @SMTPAddress = 'smtp server address goes here';
SET @EmailAddress = 'from email address goes here';
SET @DisplayUser = 'from display name goes here';

EXECUTE msdb.dbo.sysmail_add_account_sp
@account_name = @AccountName,
@email_address = @EmailAddress,
@display_name = @DisplayUser,
@mailserver_name = @SMTPAddress

EXECUTE msdb.dbo.sysmail_add_profile_sp
@profile_name = @ProfileName

EXECUTE msdb.dbo.sysmail_add_profileaccount_sp
@profile_name = @ProfileName,
@account_name = @AccountName,
@sequence_number = 1 ;
</code></pre>

Run this script to enable Database Mail on the server ([MSDN Link to Database Mail XPs Server Configuration Option](http://msdn.microsoft.com/en-us/library/ms191189.aspx)):
<pre><code class="sql">USE Master
GO
sp_configure 'show advanced options', 1
GO
reconfigure with override
GO
sp_configure 'Database Mail XPs', 1
GO
reconfigure 
GO
sp_configure 'show advanced options', 0
GO
</code></pre>

To test and make sure you have it setup you can use this script:

<pre><code class="sql">EXEC msdb.dbo.sp_send_dbmail
@recipients = 'to email address goes here',
@body= 'Test Email Body', 
@subject = 'Test Email Subject',
@profile_name = 'DefaultDBMailProfile'
</code></pre>

**Please note:** many of the variables in the above scripts have test data in them. Be sure to set the variables to the values that apply to your environment.
