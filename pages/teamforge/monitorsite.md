---
title: Monitor Your Site
keywords: monitor site, server status, logs, log level, build information, 
tags: [ctf_20.2, site_admin_tasks, logs, monitoring]
sidebar: teamforge_sidebar
permalink: monitorsite.html
last_updated: Jul 13, 2020
summary: To facilitate troubleshooting, keep an eye on key data about your Digital.ai TeamForge site.
---

## Check Your Server's Status
As a first troubleshooting step, check the **Server Status** page to see if your servers are running and connected to the main TeamForge server.

{% include note.html content="The **Server Status** page provides only the current status of each server. It is not a diagnostic tool, and you must correct any connection or configuration issues on the server in question." %}

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **SYSTEM TOOLS**.
3. On the **System Tools** menu, click **Server Status**.
4. Find the status of the server you are interested in.
   
   For each server, you see one of the following status messages:
   * **OK**--The server is running and connected to the main TeamForge server.
   * **Could Not Connect**--The server is not running or is not connected to the main TeamForge server.

## Get Build Information
For solving some kinds of problems, it may be useful to know which software components are installed, the exact build number, and other technical information about your TeamForge site.

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **SYSTEM TOOLS**.
3. On the **System Tools** menu, click **Build Information**.
   The **Build Information** page consists of the following information: TeamForge version number, build number, operating system name and version number, instance (any packages of customizations that have been applied) and a list of installed RPMs.

<!-- ## Get Reports on Site Activity {#siteactivityreport}

You can keep track of various kinds of user activity, such as the number of user logins, source code commits, and tracker activity on your site.

* Monitor the total number of commits on your site by all users, in all projects, per day. You can track SCM commits to Subversion repositories and to Git repositories as well, if you have the [TeamForge Git integration][gitoverview] set up.
* Check how many users log into your site in a given period. For example, to assess the impact of changes you've made to your site's look and feel (see [Customize TeamForge][customize]), look for trends in the user login numbers for the week following the changes.
* Check the artifacts that are created and closed in a given period.

1. Go to **My Workspace > Admin**.
2. Click **REPORTS** from the **Projects** menu and select one of the available reports.
3. Click a **Zoom** option to see a week, a month, a quarter, 6 months, or a year of activity. The **Max** option shows all the data that's ever been collected.
4. Use the **From** and **To** date fields to zero in on the exact period of activity you are interested in.
5. Roll your cursor over any data point on the graph to see the exact numbers that determine that point's position.
6. Click **Grid View** to see the data as a table. You can toggle between chart and grid view as needed. -->

{% include links.html %}