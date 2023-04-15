---
title: FAQs on Emails 
keywords: FAQ, frequently asked questions
tags: [faq, emails]
sidebar: teamforge_sidebar
permalink: emails-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on email communications in TeamForge.
---

## What are the X-headers used to sort and filter emails sent by TeamForge?

{% include callout.html type="primary" content="X-headers are special instructions that are added to many email messages. Messages that come from your TeamForge site have X-headers describing the purpose of the email, the event that triggered it, and lots of other information." %}

You can use these X-headers to sort and filter emails sent by TeamForge.

<table>
<tr>
<th>X-header</th>
<th>Example</th>
<th>Description</th>
</tr>
<tr>
<td>X-TeamForge-Application</td>
<td>Tracker</td>
<td>Application, if applicable. Values include Documents, Wiki, Source Code, TeamForge, Tasks, Tracker, Discussion, File Releases.</td>
</tr>
<tr>
<td>X-TeamForge-Artifact-Monitoring</td>
<td>true</td>
<td>For artifacts, true if the user is monitoring the artifact directly. If value is false, you are monitoring the folder, not the artifact.</td>
</tr>
<tr>
<td>X-TeamForge-AssignedTo</td>
<td>admin</td>
<td>User assigned to artifact or task.</td>
</tr>
<tr>
<td>X-TeamForge-CommitPath</td>
<td>/path/to/my/branch</td>
<td>For Subversion commit emails: reports the greatest common path of all files in the commit. For example, if you modify the paths /a/b/file1 and /a/c/file2, the value of the X-TeamForge-CommitPath header is /a. If you modify /a/b/file1 and /file2, the value is / (the root path of the repository).</td>
</tr>
<tr>
<td>X-TeamForge-FolderId</td>
<td>tracker1005</td>
<td>If the object is a folder, the object’s ID, or the ID of the object’s container.</td>
</tr>
<tr>
<td>X-TeamForge-Forum</td>
<td>New user forum</td>
<td>For posts, this is the forum title.</td>
</tr>
<tr>
<td>X-TeamForge-PlanningFolder</td>
<td>/path/to/my/folder</td>
<td>The path to a planning folder.</td>
</tr>
<tr>
<td>X-TeamForge-ProjectId</td>
<td>proj1006</td>
<td>Project ID, if applicable.</td>
</tr>
<tr>
<td>X-TeamForge-ServerName</td>
<td>collab.net</td>
<td>Hostname portion of TeamForge URL.</td>
</tr>
<tr>
<td>X-TeamForge-Status</td>
<td>Open</td>
<td>Status of artifacts, tasks, documents, and document reviews. Values include:
<ul>
<li>For artifacts: Open, Closed, Pending, or user-defined.</li>
<li>For tasks: Not Started, OK, Complete, Warning, or Alert.</li>
<li>For documents: Draft, Review, or Final.</li>
<li>For document reviews: Open or Closed.</li>
</ul>
</td>
</tr>
<tr>
<td>X-TeamForge-Type</td>
<td>Artifact</td>
<td>The type of the object, if applicable. Values include Tracker, Artifact, Document Folder, Document, Document Version, Wiki Page, Wiki Page Version, Task Folder, Task, FRS Package, FRS Release, Discussion Forum, Discussion Topic, SCM Repository, SCM Commit.</td>
</tr>
</table>

## Why is my email taking a long time to arrive?

TeamForge uses the James MTA to send and parse all email coming to and from the system. In this case, the best course of action is to look in the james mailet logfile.

Your logfile will help you to determine what is going on with the emails that are being sent from your system. Your logfiles will look very similar to this:

```shell
07/02/07 07:54:43
INFO James.Mailet: ?RemoteDelivery: 
Attempting delivery of Mail1170135534355-39088-to-domain.invalid to host domain.invalid at 192.168.0.1 to
addresses [invalid.user@domain.invalid] 07/02/07 07:55:43 
INFO James.Mailet: ?RemoteDelivery: Could not connect to SMTP host: 192.168.0.1, port: 25; nested exception
is: java.net.?ConnectException: connection to 192.168.0.1 timed out 07/02/07 07:58:43
INFO James.Mailet: ?RemoteDelivery: Storing message
Mail1170135534355-39088-to-domain.invalid into outgoing after 7 retries 07/02/07
07:58:43 INFO James.Mailet: ?RemoteDelivery: Attempting delivery of
Mail1170831482124-2756-to-company.com to host mx.company.com. at 127.0.0.1 to addresses
[good.user@company.com] 
````

As you can see, the James MTA stores outgoing emails to resend at a later time. These files can be located in this directory: `/opt/collabnet/teamforge/james/james-<ver>/apps/james/var/mail/outgoing/`


When you do a directory listing of the files, you will see a listing of files very similar to this:

```shell
4D61696C313137303833323131343031322.Repository.?FileObjectStore
4D61696C313137303833323131343031322.Repository.?FileStreamStore 
````

The FileObjectStore is a binary file, but, the FileStreamStore can be viewed with an editor or your favorite paging program in order to determine the contents. Sometimes, the directory can grow to a large number, where you will not be able to use a standard bash expander to delete all of the files. In that case, use the following shell script to remove all of the objects from the outgoing directory:

```shell
for i in * ; do /bin/rm $i; done 
```
{{site.data.alerts.hr_shaded}}

## Why would some users not get email?

Check your dnsserver-<date and time>.log.

James records all errors related to resolving DNS for outbound mail to: `/opt/collabnet/teamforge/james/james-<version>/apps/james/logs/dnsserver-.log`. If you find that some of your TeamForge users are receiving email, but significant groups of others are not, you should consult this log to determine if James is experiencing difficulties in resolving their domain or MX records.
{{site.data.alerts.hr_shaded}}

## Why do search and email server show "Could not connect"?

Typically this means the tomcat container for James and the search service are not running.

You can restart this with the commands shown below. You may need to set the JAVA_HOME environment variable to the location of your JDK.

```shell
sh /opt/collabnet/teamforge/dist/james/james-2.2.0/bin/phoenix.sh stop
sh /opt/collabnet/teamforge/dist/james/james-2.2.0/bin/phoenix.sh start
````

### Why can't TeamForge send my outbound mail?

If you are unable to send email directly due to firewall restrictions, or if mail is being rejected by the application server's IP address, configure TeamForge to send outgoing messages through a gateway mail server.

Configure TeamForge to send outgoing message through a gateway mail server by adding the following to the `<mailet match="All" class="RemoteDelivery">` directive in the configuration file at `/opt/collabnet/teamforge/runtime/james/apps/james/SAR-INF/config.xml`:

```shell
<gateway>smtp.example.com</gateway>
<gatewayPort>25</gatewayPort>
````
If your gateway mail server requires authentication to send email, you may also add the following directives:

```shell
<username>username</username>
<password>password</password> 
````
{{site.data.alerts.hr_shaded}}

## Can I customize my site's email notifications?

The default text for Digital.ai TeamForge email notifications can be customized.

Email templates are located in the `templates/mail` directory in the branding repository.

Some email templates that are commonly customized are:

 * user_welcome.vm
 * account_request_rejection.vm
 * project_approve_pending.vm
 * user_forgot_password.vm

Email template formatting follows the standard Velocity conventions:

```shell
user_welcome.vm
##subject
Welcome to Digital.ai TeamForge  5.0!
##subject
##body
The Welcome message goes here...
##body
Email subject line
Email message text
````
{{site.data.alerts.hr_shaded}}

## Can I specify an alternate email address?

Yes, of course you can specify one or more alternate email address. TeamForge supports user profiles with one primary email address and up to three secondary email addresses.

The email address specified while creation of a user account is considered the primary email address. The alternate email addresses are optional and can be specified while updating the user profile.

 {% include note.html content="To add your secondary email addresses, use the **Admin > Users** page to update your profile." %}

### How can I check if port 25 is open?

If you know the mail server is up and running, check whether you can talk over port 25 to your mail server. This can be done using a one-line command: 

```shell
telnet <appserver name> 25 Substitute the <appserver name> with your own server.
````

Once you type this into your DOS window and hit return, you should see some sort of response from your mail server, as shown below:

<div class="well well-lg">
Trying 208.75.196.84... Connected to cu190.cubit.sp.collab.net (208.75.196.84). Escape character is '^]'. 220 cu190.cubit.sp.collab.net SMTP Server (JAMES SMTP Server 2.2.0) ready Mon, 27 Jul 2009 06:38:20 -0700 (PDT)
</div>
{{site.data.alerts.hr_shaded}}

## When a discussion forum is set up, do all members receive a notification mail?

Yes. A mail informing users about the creation of discussion forum is sent to all the members of the project who have the Discussions (check box) selected as a monitored application.

Users can enable **Discussions** as a monitored application. To do that:

 1. Go to **My Workspace > My Page > Monitoring** and select a project from the **Edit Monitoring Subscriptions and Preferences** pane.

 2. Select the _Monitored Applications_ tab.

 3. Select the **Discussions** check box and click **Save**.
{{site.data.alerts.hr_shaded}}

## I am unable to edit a specific artifact via email, but I can do so via the web UI. Why is this?

There may be workflow rules applied to the tracker that require specific fields to be set. As you can only define the artifact title and description via email, the artifact creation fails. If you wish to create artifacts in this tracker via email, the tracker admin will need to disable these workflow rules.

In addition, you may not be able to edit artifacts belonging to a tracker via email, if the tracker has two mandatory flex fields with parent-child relationship, but no default value relationship between the default values of the parent and child flex fields. In such cases, it is recommended to always establish the default value relationship between flex fields that have a parent-child relationship.
{{site.data.alerts.hr_shaded}}

## How do I set up a local alias via James?

In situations where you need to obtain a SSL certificate for your domain, and your SSL certificate provider only permits you to use addresses related to your TeamForge domain, it may be necessary to generate an email alias from within TeamForge. Since there is currently no way to do this through the UI, you'll have to do it from the James administrative interface.

First, you'll need to connect to the James administrative interface on your system. If you've followed our best practices guide in our knowledgebase, you'll know that you should have port 4555 firewalled to everyone but localhost. SSH to your TeamForge server, and then issue the following command:

```shell
telnet localhost 4555
```

This will bring up the Remote Administration Tool:

```shell
[root@app1 root]# telnet localhost 4555 
Trying 127.0.0.1... Connected to localhost (127.0.0.1). 
Escape character is '^]'. JAMES Remote Administration Tool 2.2.0
Please enter your login and password 
Login id: admin Password: (text is echoed locally) 
Welcome admin. HELP for a list of commands 
```

First, we'll need to add a new user:

```shell
adduser <username> <password> 
````

Then, we'll need to set the forwarding address of that user.

```shell
setforwarding <username> <email address where you want email to go> 
````

Finally, we'll exit the James administrative interface.

```shell
quit
````

Your changes should be in place.
{{site.data.alerts.hr_shaded}}

## Does TeamForge support using /etc/aliases for local mail delivery?

No, TeamForge uses the James SMTP server, which does not use the `/etc/aliases` file.

To enable local mail aliases, you will need to configure user mapping in the `XMLVirtualUserTable` in the `/opt/collabnet/teamforge/runtime/james/apps/james/SAR-INF/config.xml` file.

 {% include note.html content="Please note that while the James SMTP server is used as part of TeamForge, customizations such as these cannot be supported by CollabNet." %}
{{site.data.alerts.hr_shaded}}

## How can I stay informed about events on TeamForge site?

To keep up with changes, you can be notified by an automatic email when an item you are interested in is updated.

Monitoring items lets you stay up to date automatically on all changes without having to log into Digital.ai TeamForge and check the status of each item.

You can monitor individual items, folders, and entire applications in each project for which you are a member. You can configure the frequency of email notifications to suit your personal preferences, and suspend monitoring messages entirely if you are out of the office or for any reason do not want to receive messages.

Items that can be monitored include:

 * Entire applications, such as all tasks or all documents.
 * Folders, such as task folders or document folders.
 * All items in a tracker, forum, or package.
 * Individual items, such as a task, a document, a tracker artifact, or a release.

You can tell by looking at each item whether you are currently monitoring it and how to begin or end monitoring it.

 * For each item, list of items, or folder, you see a **Monitor** button or menu option.
 * If you are currently monitoring an item, the **Monitor** option is replaced by a **Stop Monitoring** option, and the monitoring icon is displayed.

Whenever you create an item or edit an item, you automatically begin monitoring that item.

You do not receive monitoring notifications for your own changes to a monitored item.

If you have the appropriate permissions, you can see who is monitoring an item.

You can add other users to the monitored item. After a user is added to a monitored item, the user can continue monitoring the item, configure monitoring preferences for the item, or stop monitoring the item.
{{site.data.alerts.hr_shaded}}

## I receive a number of emails just because I am monitoring a folder. How can I restrict this?

Monitoring a folder might spam the mailboxes with emails that are generated for every small change.

Email notification preferences under the _Monitoring_ sub-tab under My Workspace can be modified to Send Daily Digest Email, which provides a summary of the email alerts.

 1. Go to **Projects > My Workspace**.

 2. Select **Monitoring** from the **My Page** menu.

 3. In **Edit Monitoring Subscriptions and Preferences** page, click **All Projects** and click on **Email notification preference**.

 4. For each project, the monitoring folders under various components (Tracker/File Releases/Tasks/Discussions/Wiki) can be customized to Daily Digest Email.
{{site.data.alerts.hr_shaded}}

## Can TeamForge accept email for more than one domain?

You can configure James to accept email for more than one domain by adding the additional domains to the `<servernames>` section in the `config.xml` file.

Add the domains to the `<servernames>` section of this file: `/opt/collabnet/teamforge/james/james-2.2.0/apps/james/SAR-INF/config.xml`.

Around line 53, you should see the following:

```shell
<servernames autodetect=""true"" autodetectIP=""true"">
   <servername>localhost</servername>
</servernames> 
````

You can add other host names for James to accept mail for by adding more `<servername>` blocks. The comments in the config.xml file explain this further. Please keep in mind that these changes may be overwritten by future TeamForge upgrades.
{{site.data.alerts.hr_shaded}}

## How do I configure TeamForge to send mail on a specific network adapter in a multi-NIC configuration?

When a host has multiple NICs, James will try to do the right thing when sending mail. In some network setups, this is not correct, and manual configuration is needed.

James requires multiple changes to fully configure how it interacts with the network. Open the `config.xml` file, located in `$SF_HOME/apps/james/james-2.2.0/apps/james/SAR-INF/` for version 5.1.

Locate the `<mailet match="All" class="RemoteDelivery">` section. Add a subnode `<bind>$addr</bind>` where `$addr` is the ip address that James should be sending mail from.

Near that area, there is a `<servernames...></servernames>` section. Confirm/change the two autodetect options (`autodetect`, `autodetectIP`) to `false`. Next, add the fully qualified host name, and the ip address that will be used, to their own `<servername>` entry.

After the changes are complete, save the config.xml and restart the application.
{{site.data.alerts.hr_shaded}}

## How do I send email from a specific sender address instead of the member address?

To send mail from a specific sender address set the _MONITORING_EMAIL_FROM_ADMINISTRATOR_ token to _true_ in the `site-options.conf` file.

TeamForge uses the member's email address as the sender address when it delivers the mail. To reconfigure this setting in the `site-options.conf` file, set the _MONITORING_EMAIL_FROM_ADMINISTRATOR_ token to _true_, as shown in the following code sample:

```shell
MONITORING_EMAIL_FROM_ADMINISTRATOR=true
````


{% include links.html %}