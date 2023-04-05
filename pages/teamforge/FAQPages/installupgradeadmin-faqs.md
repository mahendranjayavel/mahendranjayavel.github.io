---
title: FAQs on Install/Upgrade/Administration
keywords: FAQ, frequently asked questions
tags: [ctf_20.2, ctf_20.1, ctf_18.3, faq, installation, upgrade, project_admin_tasks, site_admin_tasks, postgres]
sidebar: teamforge_sidebar
permalink: installupgradeadmin-faqs.html
last_updated: Aug 27, 2020
summary: These are some of the frequently asked questions on the installation, upgrade, and site admin related activities in TeamForge.
---
## PostgreSQL deployment fails with the following error during `teamforge provision`. What should I do?
<!-- Artifact [artf396872] postgres deployment fails during provision. FAQ added. -->
**Error**

```shell
Deploying postgres...
  Create log folders                                        Done            0.00 secs
  Create symlink for pgdata folder                          Done            0.00 secs
  Create PostgreSQL control script                          Done            0.26 secs
  Check and Initialise TeamForge Database                   Your PostgreSQL installation has been found to be outdated and needs to be upgraded to version 11. This can be done automatically.Do you wish to proceed? [y/N]y
Failed
su - postgres -c '/usr/pgsql-11/bin/pg_upgrade -d /opt/collabnet/teamforge/var/pgsql/9.6/data -D /opt/collabnet/teamforge/var/pgsql/11/data -b /usr/pgsql-9.6/bin -B /usr/pgsql-11/bin' failed
Deployment failed. See /opt/collabnet/teamforge/log/runtime/runtime.log for details.
Exception raised:
Cannot bootstrap service 'gerrit-database-performance-postgres' while in status 'not deployed'
````

**Error from the log file**

```shell
Performing Consistency Checks
-----------------------------
Checking cluster versions ok
The source cluster was not shut down cleanly.
````

**Solution**

Run the following commands.
```shell
su - postgres -c "/usr/pgsql-9.6/bin/pg_ctl start -D /opt/collabnet/teamforge/var/pgsql/9.6/data/"
su - postgres -c "/usr/pgsql-9.6/bin/pg_ctl stop -D /opt/collabnet/teamforge/var/pgsql/9.6/data/"
teamforge provision
````

{{site.data.alerts.hr_shaded}}
## I see the following error, `ERROR: relation "django_site" does not exist at character 78`, in the `postgresql.logs` file while installing TeamForge. What is the cause of this error?
<!-- https://forge.collab.net/sf/go/[artf413978] django_site table query, error logged to postgresql.logs file -->

This error is cause by an SQL statement in one of the TeamForge scripts that tries to query the Review Board's `django_site` table even before it gets created. You can safely ignore this error and proceed. 

{{site.data.alerts.hr_shaded}}
## What could cause the `teamforge reload` command, run immediately after updating the ETL_JAVA_OPTS token, to fail?
<!-- [artf415222] ETL fails to stop in 180s due to which teamforge reload does not work -->
Running the `teamforge reload` command after updating the `ETL_JAVA_OPTS` token stops the ETL service first in order to deploy, start and initialize the ETL service again. If the ETL service is not stopped within 180 seconds, the `teamforge reload` command times out and the `teamforge reload` command cannot recognize the changes to the `ETL_JAVA_OPTS` token the next time you run the command.   

{{site.data.alerts.hr_shaded}}
<!-- https://forge.collab.net/sf/go/artf318224#3 -->
## TeamForge upgrade fails when migrating Baseline database to the latest schema. This happens when upgrading from TeamForge 18.3 to 19.0. What should I do? {#ctf190upgradeerror}

**Error**

{% include image.html file="190-ctfupgradeerror.png" %}


Run the following SQL command on the Baseline server and then provision TeamForge.

```shell
CREATE TABLE snpsht_baseline_field_value
(
baseline_id character varying(32) COLLATE pg_catalog."default" NOT NULL,
id character varying(32) COLLATE pg_catalog."default" NOT NULL,
field_id character varying(32) COLLATE pg_catalog."default" NOT NULL,
is_default_value boolean NOT NULL,
value character varying(255) COLLATE pg_catalog."default",
metastatus_id integer,
display_order integer NOT NULL,
is_deleted boolean NOT NULL,
CONSTRAINT pk_snpsht_baseline_field_value PRIMARY KEY (baseline_id, id)
)
````
{{site.data.alerts.hr_shaded}}

## The `teamforge apply-permissions` command, when run, removes the setcap IDs. What should I do?

<!--artf315517-->
The `teamforge apply-permissions` command, when run, removes the setcap IDs for `/var/www-local/fcgi-bin/cliserver.fcgi`. As a workaround, run the following command immediately after running the `teamforge apply-permissions` command:

```shell
setcap cap_setuid,cap_setgid,cap_sys_chroot+iep /var/www-local/fcgi-bin/cliserver.fcgi
````
{{site.data.alerts.hr_shaded}}

## I have Git and Subversion on separate servers. I am getting a TeamForge system error when I try to access an existing repo. What should I do. 

Make sure that TeamForge, Git and Subversion servers have their time and date synchronized. 

If you have Git integration on a separate server, both TeamForge and Git servers must have their time and date synchronized. Similarly, If Subversion is on a separate server, both TeamForge and Subversion servers must have their time and date synchronized.
{{site.data.alerts.hr_shaded}}

## What should I do if the Reports Database migration fails while upgrading to TeamForge with the following error.

<!-- https://forge.collab.net/sf/go/artf315305#5 -->

**Error Message**

```shell
"Caused by: org.postgresql.util.PSQLException: ERROR: could not create unique index "schema_version_pk"
Detail: Key (surrogate_id)=(1) is duplicated"
````
1. Verify the `schema_version` table for multiple entries.
   1. Connect to the Reports Database.
      ```shell
      /opt/collabnet/teamforge/runtime/scripts/psql-reporting-wrapper
      ````
   2. Run `select * from schema_version;` and verify if the `schema_version` table has two entries such as the following. 
      
      | major | minor | sp | hotfix |
      |-------+-------+----+--------|
      | 17 | 11 | 0 | 0 |
      | 17 | 11 | 0 | 0 |

   3. If yes, proceed with the following workaround steps. 
   4. Run the following commands and confirm the `schema_version` table entries in the file `/tmp/datamart_schemaversion.txt`
      ```shell
      /opt/collabnet/teamforge/runtime/scripts/psql-reporting-wrapper
      \o /tmp/datamart_schemaversion.txt
      ````
   5. Delete one of the entries. 
      ```shell
      delete from schema_version where ctid not in (select max(ctid) from schema_version group by major,minor,sp,hotfix);
      ````
   6. Verify that only one entry exists and provision TeamForge. 
      ```shell
      select * from schema_version; 
      ````
2. {% include installupgrade/deploy_services_without_note.html %}
{{site.data.alerts.hr_shaded}}

## Why am I getting "Could not connect" status for my email and search server?

On the **System Tools** page, when you see "Could not connect status for search and email servers," you must stop and start your phoenix.sh process.

You may also need to set the JAVA_HOME environment variable to the location of your JDK.

The stop/start Phoenix commands:

```shell
sh /opt/collabnet/teamforge/runtime/scripts/phoenix.sh stop
sh /opt/collabnet/teamforge/runtime/scripts/phoenix.sh start
````
{{site.data.alerts.hr_shaded}}

## Why are the dynamic images that TeamForge creates broken?

If you have a fresh install of TeamForge and you're noticing that the dynamic images are not correct, you may be missing a library that is needed to create the images.

The easiest way to find this is to check and see if you have the xorg-x11-depreciated-libs rpm installed:

```shell
rpm -qva | grep xorg-x11-depreciated
````

Watch for the results. If you see that you have the xorg-x11-depreciated-libs rpm installed, and after a server restart you're still not seeing the images, please open a support request. If you do not have the xorg-x11-depreciated-libs rpm installed, it can usually be installed by performing a simple `up2date xorg-x11-deprecated-libs` and restarting TeamForge.
{{site.data.alerts.hr_shaded}}

## Due to firewall restrictions I cannot send email from James. How can I resolve this?

If James is unable to send email directly due to firewall restrictions, or mail being rejected from the application servers IP address, you may have to configure it to use a gateway mail server to send outgoing messages through.

To do this, you will need to add the following to the `<mailet match="All" class="?RemoteDelivery">` directive in the james config file at `/opt/collabnet/teamforge/james/james-<version>/apps/james/SAR-INF/config.xml`:

```shell
<gateway>smtp.example.com</gateway>
<gatewayPort>25</gatewayPort>
````

You should find these commented out on line 362 of the config file. If your gateway mail server requires authentication to send email, you may also add the following directives:

```shell
<username>username</username> 
<password>password</password>
````
{{site.data.alerts.hr_shaded}}

## Why am I not getting any error messages when executing the Subversion upgrade script?

Error messages may come when Subversion is installed with a dependent package from an unknown source.

The Subversion working copy script assumes that Subversion is installed with the dependent packages from a proper source repository(RHEL/CollabNet). If you install any dependent packages from any unknown source that is not authorized by RHEL/CollabNet, it will result in inconsistency and this cannot be handled by the Subversion working copy script.
{{site.data.alerts.hr_shaded}}

## Why do I get a JBoss error "failed to start in 240 seconds, giving up now" while installing TeamForge?

You get this error when the system's RAM is less than the minimum recommended value of 4GB. However, it's most likely that JBoss will start within a few minutes.

To make sure that JBoss starts up, check the service.log file using this command:

```shell
tail -f /opt/collabnet/teamforge/log/apps/service.log
````
If you see messages like the following, the TeamForge application will start in a few minutes.

```shell
 Check Port Available PASSED: Port 4444 on localhost is available
 Check Port Available PASSED: Port 4445 on localhost is available
 Waiting for application server to start up.. this can take a few minutes.
````
{{site.data.alerts.hr_shaded}}

## JBoss crashed with out of memory error, how do I prevent this?

This can indicate that the JVM heap size is set too small.

You can adjust this by changing the -Xms and -Xmx settings of the _JBOSS_JAVA_OPTS_ token in `site-options.conf` and rebuilding runtime.

This will appear if the JBoss application server has crashed and you find this error in the server.log:

```shell
INFO [STDOUT] java.lang.OutOfMemoryError: Java heap space
````

The default maximum heap size of 640MB can cause issues on a heavily used site. If the CTF application is the only thing running on the server, you can increase this to half of the total physical ram on the machine. This should still allow enough memory for the OS and other necessary processes. If you are also running the app, database and scm on the same machine a maximum heap size of 1/4 or the total ram maybe a better setting. Determining the right JVM settings for your install will require testing with your particular usage patterns and database.

You can view the current memory usage under the JVM Environment section of the JBoss webconsole at http://<CTF_SERVER>:8080/web-console/. You will need to log in using the CTF admin password.
{{site.data.alerts.hr_shaded}}

## JBoss status is in 'starting' for a long time. How to have JBoss started successfully?

If JBoss is not started successfully (status remains 'starting' for a long time), you may have to wait until it starts up successfully or you can kill JBoss process (using its PID) and restart it again.

The following error messages show up when you try to start or stop JBoss respectively while its status is still 'starting':

```shell
Cannot execute action as another process is holding the lock.

Cannot stop service 'jboss' while in status 'starting'
````

To kill the JBoss process:

```shell
kill 9 <JBoss PID>
````
{{site.data.alerts.hr_shaded}}

## Why am I not able to see the status of the Postgres in the collabnet startup script?

You may not be able to see the status of the Postgres if the host name of the HOST_ token is set to localhost in a SaaS multibox setup.

The Teamforge installer fails to add the IP address of the database box to the listen address in the postgresql.conf file if the host name of the HOST_ token is set to localhost in a SaaS multibox setup.

 {% include note.html content="You must add the IP address of the database box to the listen address in the postgresql.conf file." %}
{{site.data.alerts.hr_shaded}}

## Why does the SOAP service show "could not connect" on the Server Status page when everything else appears to work?

This can be caused by an incorrect host name in `/etc/sourceforge.properties`. Rebuilding runtime will correct this, assuming the hostname is set correctly in the `site-options.conf` file.

This issue can occur when using the restore.py script to restore data from a TeamForge instance with a different hostname.
{{site.data.alerts.hr_shaded}}

## Why does startup fail or produce errors?

If TeamForge fails to start up, or is starting but is throwing errors on every page, then typically something went wrong during the JBoss bootstrap process.

Fortunately, JBoss logs this process to: `/opt/collabnet/teamforge/jboss/jboss-<version>/server/default/log/boot.log`.

TeamForge writes its startup and shutdown info, as well as any system errors to `/usr/local/ soureforge/log/server.log`. If you encounter a system error while using TeamForge, it is logged here. Additionally, if you see an 'exid' string in the application, the Java stack trace for that exid will be logged in this file.
{{site.data.alerts.hr_shaded}}

## Why do I get a URL "not found" or "moved permanently" error after applying a patch/upgrade?

If you are experiencing a URL "NOT FOUND" or "MOVED PERMANENTLY" error after applying a patch or upgrade, then set Apache ProxyPreserveHost token to ON in the `httpd.conf` file.

If you have applied a patch or upgrade and are now receiving the following error:

```shell
<The document has moved <a href="https://www.<site>/sf/global/jsp/buildtime.html" 
    format="html" scope="external">here</a>.</p>
<hr> <address>Apache/2.2.3 (Red Hat) Server at www.<site>.com Port 80</address> </body></html>
Not Found 
The requested URL /sf/sfmain/do/userPicker/projects.pftool//sfmain/do/listMonitoringUsers/projects.pftool/discussion.
announcements was not found on this server
````
Or if you are trying to add users to a monitoring list, and are receiving the following error:

```shell
Not Found
The requested URL 
    /sf/sfmain/do/userPicker/projects.pftool//sfmain/do/listMonitoringUsers/projects.pftool/discussion.announcements 
    was not found on this server.    
````

Set the ProxyPreserveHost token to ON in the `httpd.conf` file.
{{site.data.alerts.hr_shaded}}

## How do I require approval for new user accounts?

You can configure the system so that new users can create their own accounts, but the accounts are not activated until a site admin approves them.

To enable this mode of operation, add the following line to `/opt/collabnet/teamforge/sourceforge_home/etc/sourceforge_configuration.properties`:

```shell
sf.approveNewUserAccounts=true
````

Once this line has been added to the file, restart TeamForge for it to take effect.

Please note that site admins can still create accounts for new users and they will not be held for approval. Also note that the user will receive an email from TeamForge telling them to confirm their password by clicking on the given link, and the link will not work. The password is properly set on account approval.
{{site.data.alerts.hr_shaded}}

## How does TeamForge use Velocity templates?

Velocity is the templating language that Digital.ai TeamForge uses to render areas of the site with dynamic information.

You can override the instructions contained in any of these Velocity templates by placing a file of the same name in the equivalent path in the `branding` repository in the `look` project on your site.

Velocity templates are located in the `templates` directory in the branding repository.

<table>
<tr>
<th>Velocity File</th>
<th>Description</th>
</tr>
<tr>
<td>menu_bar.vm</td>
<td>Controls the rendering of the top bar across all pages in the system. Displays a small login form, the site logo and current user information as well as the search and projects drop down menus.</td>
</tr>
<tr>
<td>blank_menu_bar.vm</td>
<td>Contains only the top logo, without the menu that appears below it.</td>
</tr>
<tr>
<td>body_header.vm</td>
<td>Rendered immediately after the opening body tag. If a site requires everything to be contained in some other container, this template can be used.</td>
</tr>
<tr>
<td>body_footer.vm</td>
<td>Rendered immediately before the closing body tag. If a site requires everything to be contained in some other container, this template can be used.</td>
</tr>
<tr>
<td>button_bar.vm</td>
<td>Controls the rendering of the bar beneath the menu bar, which contains the 'Quick Jump" link as well as the buttons that appear on any project page (the one containing the applications). Site admin pages, user settings pages (e.g. my workspace, dashboard) and project pages use different sets of buttons that are passed into this template for rendering.</td>
</tr>
<tr>
<td>content_header.vm</td>
<td>Rendered after the button bar; wraps the actual contents of the page being viewed.</td>
</tr>
<tr>
<td>content_footer.vm</td>
<td>Rendered before the body footer; wraps the actual contents of the page being viewed. Contains the Copyright notice.</td>
</tr>
<tr>
<td>sfmain/home.vm</td>
<td>Velocity template that generates the site home page.</td>
</tr>
<tr>
<td>sfmain/project_home.vm</td>
<td>Velocity template that generates the default project home page.</td>
</tr>
</table>

{% include image.html file="csfe-brandingtemplates.png" %}

{{site.data.alerts.hr_shaded}}	

## What happens when log files get too big?

Log files can grow very large over time. To maintain reasonable log file sizes, log files are rotated automatically on a schedule.

During this automatic log rotation, live logs are archived every day at `00:00`.

Archived logs are stored in compressed form in a directory alongside the live log. For example, if live logs are stored at `<LOG_DIR>/{apps, apache,...}`, then compressed log archives are stored at `<LOG_ARCHIVE_DIR>/{apps, apache,...}`.

The directory structure of the log directory is preserved in the log archive directory.

 {% include note.html content="Empty log files are not compressed." %}
{{site.data.alerts.hr_shaded}}

## How do I make the monitoring messages be sent from Forge Administrator?

You can change the default behavior for site options by changing the value from "false" to "true" in this statement: 

```shell
# MONITORING_EMAIL_FROM_ADMINISTRATOR=false
````

If this site option token is set to `true`, then "From:" field is the Forge Administrator, else it is from the user who made the change that initialized the monitoring email.

{{site.data.alerts.hr_shaded}}

## How do I enable post-commit logging?

You do this by editing the `post-commit.py` file.

Edit the `/opt/collabnet/teamforge/runtime/sourceforge_home/integration/post-commit.py` file.

Search for `log.setLogging(False)` and modify the value from `False` to `True`.
{{site.data.alerts.hr_shaded}}

## What is the suggested log configuration for a production system?

To troubleshoot installation issues, the default log4j configuration is set to DEBUG. This can cause the log files to become quite large. Once your system is successfully installed and in use, you should drop the log levels down to INFO.

See [Change the Logging Level on Your Site][changeloglevel] for how to do this.

If you still have a problem with very large log files, you may want to set up log rotation. Log rotation means to move the log files to a compressed archive to keep them under control.
{{site.data.alerts.hr_shaded}}

## How do I remove the build and test link from TeamForge pages?

The site administrator can remove these links by checking out and editing the branding repository from the look project.

To remove the build and test links from your TeamForge navigation panel, check out the branding repository from look project and reconfigure the links as shown in the following code sample:

 {% include note.html content="You must be logged on as administrator to perform this task." %}

```shell
[branding_stage]$ cd branding
[branding]$ mkdir -p i18n/com/vasoftware/sf/i18n/apps/sfmain
[branding]$ echo "configure_build_and_test.systemUrl.default=" > i18n/com/vasoftware/sf/i18n/apps/sfmain/application.properties
[branding]$ svn add i18n
A i18n
A i18n/com 
A i18n/com/vasoftware
A i18n/com/vasoftware/sf
A i18n/com/vasoftware/sf/i18n
A i18n/com/vasoftware/sf/i18n/apps
A i18n/com/vasoftware/sf/i18n/apps/sfmain
A i18n/com/vasoftware/sf/i18n/apps/sfmain/application.properties
[branding]$ svn commit
" Old: "enter paragraph information and use html tags for bullet points.
````
{{site.data.alerts.hr_shaded}}

## How do I resolve timeouts when calling web services?

This is due to the requested operation taking longer then your client SOAP stack is configured to wait before throwing a timeout. You will need to reference your client documentation to see how to update the timeout properties of the connection.

For AXIS in java, you can do this via the `sun.net.client.defaultReadTimeout` property.

```shell
System.setProperty("sun.net.client.defaultReadTimeout", "600000"); //10 minute timeout, in ms
````


{% include links.html %}

<!--### How Do TeamForge Licenses Work? {#teamforgelicenses}

When you purchase a TeamForge license, you get the right to assign licenses to a specified number of users.

TeamForge supports a more flexible and granular approach to tool instantiation. TeamForge's license model consists of the following license types: ALM, SCM, DevOps, Version Control, Collaboration and Trackers. These license types are tailored to suit the needs of specific set of users that need access to certain tools and functions. A TeamForge user's license type determines the tools available to the user in TeamForge.

 {% include attention.html content="While TeamForge supports more selective tool options with these new license changes, there's no impact on customers, both new and existing, requiring all the tools that TeamForge supports." %}

The following table lists the license types and the tools that go with them (refer to the table at the end of this topic for a complete list of tools and functions).

<table>
<tr><th>License Type</th><th>Available Tools</th></tr>
<tr>
<td>
	ALM
</td>
<td>
	Offers the full range of ALM tools and functions to users.
</td>
</tr>
<tr>
<td>
	SCM
</td>
<td>
	Offers core Source Code Management tools and functions to users. Includes all the ALM tools and functions but Tracker and Documents component.
</td>
</tr>
<tr>
<td>
	Version Control
</td>
<td>
	Offers Source Code Management, File Releases and Review tools and functions to users.
</td>
</tr>
<tr>
<td>
	DevOps
</td>
<td>
	Package Management (Application & Environment) and File Releases tools and functions to users.
</td>
</tr>
<tr>
<td>
	Collaboration
</td>
<td>
	Offers a range of collaboration tools such as Documents, Wiki and Discussion Forums to users.
</td>
</tr>
<tr>
<td>
	Trackers
</td>
<td>
	Offers TeamForge's Tracker capability (Trackers, Planning Folder, Teams, Planning Board, Task Board and Kanban Board)to users. Also includes File Releases.
</td>
</tr>
</table>

In addition to the tools offering, the Reporting framework is also controlled by the licenses you have. Meaning, you can view and generate reports based on the license types assigned to you. For example, you must have SCM license to view or generate SCM activity reports.

Check with your CollabNet representative if you aren't sure how many licenses or what kind of licenses you want/have.

 * Your license key contains a few important numbers:

   * The number of users eligible to use specific licenses such as ALM, SCM, DevOps, Version Control, Collaboration and Trackers.

   * The IP address of the machine that your site runs on.

   For example, if your organization has 80 users who will use only the source code management features, 10 users who will use DevOps and 100 users who need the Application Lifecycle Management features, your license key string may look like this: 
   
   ```shell
   ALM=100:SCM=80:DEVOPS=10:supervillaininc:144.16.116.25.:302D02150080D7853DB3E5C6F67EABC65BD3AC17D4D35CB3Z00214141D70455B18583BF0A5000CA56B34817ADF8DBFI32353A6E657492617369633A38372E3139342E3136102E31322E`
   ````

   * Your license key only works for the IP address (or range of addresses) of the hardware that your Digital.ai TeamForge is running on, as specified in your order form. If your site uses a separate server for its database or source code repositories, make sure your license key reflects the IP addresses of all the necessary servers. If any of these addresses change, ask your CollabNet representative to generate a new key.
   
   * When you create a user account, you can assign the user with available licenses.

   * You can purchase a TeamForge license for as many years as you want. The validity period is encoded into your license when it is generated by your CollabNet representative.

   * How many users your site can support depends on the type of license. Check with your CollabNet representative if you aren't sure what kind of licenses you have.

   * Your license key is attached to the IP address of the server where your site runs. You can get a license key for a single IP address or for a range of IP addresses.

   * Your service year starts the first time you log into your site, or the first time you create or edit any item on your site, such as a tracker artifact or a document. Whichever of these events comes first starts the clock.

   * The expiration date of your license is shown on the License Info page. (Go to **My Workspace > Admin** and select **Projects > License Info**).

   * When your service year expires, you can still see the project data on your site, but you cannot make any changes to it. However, you can still carry out some critical maintenance functions for your site:

     * Enter a new license key.
     * Deactivate or delete users.
     * Change user passwords.
     * Get forgotten user passwords.

<table name="Tools Availability Matrix">
<tr>
<th>﻿Tools</th>
<th>ALM</th>
<th>SCM</th>
<th>Version Control</th>
<th>DevOps</th>
<th>Collaboration</th>
<th>Tracker</th>
</tr>

<tr>
<td>Agile Task and Planning Boards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Tracker</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Git/SVN Repository Management and Replication</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>  
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>
  
<tr>
<td>Code Review</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>Build Automation</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
</tr>
  
<tr>
<td>Test Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>File Releases</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>  
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Binary Repository Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>EventQ/Activity Stream</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td> 
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
  </tr>

<tr>
<td>Access Controls</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Project Work Spaces</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Wiki and Discussion Forums</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
</tr>

<tr>
<td>Document Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td></td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
</tr>
  
<tr>
<td>User Management</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Flexible Process and Toolchain Templates</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Reusable Dashboards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Categories and Groups</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td> 
</tr>

<tr>
<td>Cross Project Visibility</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>


<tr>
<td>Cross Project Reporting and Dashboards</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Cross Project Search</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Site-wide Administration</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Custom Branding and Custom Integrations</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>Security Architecture</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
<td>Single Tenant</td>
</tr>

<tr>
<td>Onsite and Hosted Provisioning</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
</tr>

<tr>
<td>SVN Auto Updates</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>

<tr>
<td>SVN Repository Backup and Monitoring</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>    
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td markdown="1">{% include inline_image.html file="status-success-small.png" %}</td>
<td></td>
<td></td>
<td></td>
</tr>
</table>-->