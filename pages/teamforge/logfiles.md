---
title: TeamForge Logs
keywords: logs, log files
tags: [ctf_20.2, logs, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: logfiles.html
last_updated: Jul 13, 2020
summary: System administrators can use logs to debug problems and ensure that the application is performing to expectations.
---
## Read Your Site's Logs
Inspecting the system logs for your TeamForge site may product useful information for solving problems.

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **SYSTEM TOOLS**.
3. On the **System Tools** menu, click **System Logs**. All the logs the server has written are listed.
4. On the **System Logs** page, click the log file you are interested in.

## Change the Location of Log Files
To change where log files are written to, set the value of the [LOG_DIR][siteoptiontokens.html#LOG_DIR] token with the location where you want the log files to be written and provision TeamForge.

## Configure Your Site's Log Level
Change your site's log level in the **Configure Logging** page.

The Configure Logging page lets you change the application server (JBoss) log level. Changing the application server log level affects only the `server.log` and `vamessages.log` files.

1. Go to **My Workspace > Admin**.
2. On the site administration navigation bar, click **SYSTEM TOOLS**.
3. On the **System Tools** menu, click **Configure Logging**.
4. On the **Configure Logging** page, select either **INFO** or **DEBUG** from the **LOG LEVEL** drop-down list.
   * The default log level is INFO.
   * JBoss restart is not required after changing the log level using the **Configure Logging** page.

   {% include warning.html content="The `server.log` and `vamessages.log` files grow in size if you change the log level from `INFO` to `DEBUG`." %}
5. Click **Save**.

## Raise the Logging Level of Long-running Database Requests

For easier troubleshooting, you can dictate that certain database requests that run for a specific duration get logged in a handy central log file.

For example, database requests that run longer than 10 seconds are likely candidates for troubleshooting. You can have such requests automatically logged in the `/opt/collabnet/teamfoge/log/apps/query.log` file for your inspection. The exact length of time after which a request becomes problematic depends on your environment.

How it works:
* All database queries are logged at `DEBUG` level by default.
<!-- * By default, the `vamessages.log` file is configured to include all events logged at the `INFO` level or higher. -->
* Database queries that run over a configurable time limit are logged at `INFO` rather than `DEBUG` in the `/opt/collabnet/teamfoge/log/apps/query.log` file.

For more information, see [LOG_QUERY_TIME_THRESHOLD][siteoptiontokens.html#LOG_QUERY_TIME_THRESHOLD]. 


## JBoss Logs
The JBoss application server writes several different logs under the `<TEAMFORGE_INSTALL_DIR>/log` directory.

| Log File         | Description                                                                                                                                                                                                                                                                             |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| boot.log         | Logs the JBoss startup and shut down notifications. This log is overwritten each time JBoss is (re)started.                                                                                                                                                                              |
| localhost_access | Records access to the application from a remote host, similar to the Apache `access_log`. This log is rotated each day, and the files have a date stamp appended to their name, such as `localhost_access2004-11-26.log`.                                                               |
| server.log       | Logs all the activities of the application server, including any exceptions. This log is the best place to begin debugging TeamForge server error exception ids (exid).                                                                                                       |
| session-info.log | Records when new sessions are created. This log is overwritten each time JBoss is (re)started.                                                                                                                                                                                          |
| vamessages.log   | Records TeamForge-specific actions, including some SQL queries that are sent to the backend database. This log is rotated each time it reaches 100MB in size. When rotated the older files have a number appended to the end, such as `vamessages.log.1` and `vamessages.log.2`. |
| query.log   | The database queries along with the query parameters are logged in `/opt/collabnet/teamfoge/log/apps/query.log`. |

## Oracle logging
The most important Oracle log is the `alert` log, which is found in `$ORACLE_HOME/admin/$SID/bdump/alert_$SID.log`.

An Oracle database performs logging on a wide array of functionality. The majority of the logs that are generated are stored under `$ORACLE_HOME/admin/$SID/`. Many logs are stored under this directory hierarchy, but alert is the most important. This log records all database activity, including serious problems.

The `alert` log is not rotated or overwritten, and can become quite large over time, especially on an active database.

Additional logs are created under the same directory hierarchy, for specific incidents. If a problem is recorded in the alert log, the other logs should be inspected for additional details.

For more information, as well as support in the maintenance of an Oracle database, contact Oracle Support or Oracle's [Metalink](http://metalink.oracle.com/) site.

## SCM (Subversion) Logs
Software configuration management (SCM) servers generate several logs from the TeamForge; however, in the interest of completeness they are all documented here.

| Log File                  | Description                                                                                                                                                                                                                                                                           |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| catalina.out              | This log contains information on the startup and runtime activities of the Tomcat server. This log is not rotated, nor is it overwritten, and is appended continuously over the lifetime of the server.                                                                               |
| localhost_log             | This log contains a record of Subversion browsing URL construction. When a user attempts to browse a Subversion repository in his or her web browser, the URL construction process is documented in this log. This log is rotated for each date that there is activity. |
| localhost_admin_log       | This log contains a record of the initial startup and deployment of the managed integration server. A new date stamped log is generated each time the integration server is started.                                                                                                  |
| vaexternalintegration.log | This log contains information on the operations that are being executed by the managed integration server. This log is stored in `/log.`                                                                                                                                                |

## Email Logs
Both the TeamForge email and search backends are managed from a parent daemon known as Phoenix. If the mail backend is not operating properly, the first troubleshooting step is to check the `phoenix.log` to see if it encountered difficulties starting up.

### Overview
The Phoenix daemon logs its activities to the phoenix.log file, which is stored under `SOURCEFORGE_INSTALL_DIR/james/james-2.2.0/logs`. This log is overwritten each time Phoenix is (re)started. Phoenix is run as part of the TeamForge standalone server init script.

TeamForge email is handled by the JAMES server. JAMES logs all of its activities under `SOURCEFORGE_INSTALL_DIR/james/james-2.2.0/apps/james/logs`. A new log is created for each date when there is activity, and additional logs are created if james is restarted on a date when there is activity. The date is embedded in the log name (such as `james-2005-04-28-01-00.log`).

### Active Logs
Sixteen different logs are created by james for different components of its functionality. This topic describes only the ones that are used actively by TeamForge.

<table>
<tr>
<th>Log File</th>
<th>Description</th>
</tr>
<tr>
<td>james-$date.log</td>
<td>The James log records the overall mail handling behavior of the James server.</td>
</tr>
<tr>
<td>mailet-$date.log</td>
<td>The mailet log records how each piece of email is handled. If there is a mail delivery problem, this log is the best place to begin investigation.</td>
</tr>
<tr>
<td>mailstore-$date.log</td>
<td>The mailstore log records the behavior of mail spools, and the storage of mail. This log should normally not contain errors unless James is unable to write or read mail to or from the file system.</td>
</tr>
<tr>
<td>smtpserver-$date.log</td>
<td>The smtpserver log records all inbound mail handling results. If email to discussion forums is not posting, or is getting rejected, this log would be the best place to begin investigation.</td>
</tr>
<tr>
<td>spoolmanager-$date.log</td>
<td>The spoolmanager log records the processing of mail spools. This log could be of value in troubleshooting mail delivery or handling problems.</td>
</tr>
</table>

## Search Logs
Both the TeamForge search and email backends are managed from a parent daemon known as Phoenix. If the search backend is not operating properly, the first troubleshooting step is to check the `phoenix.log` file to see if it encountered difficulties starting up.

The Phoenix daemon logs its activities to the `phoenix.log` file, which is stored under `SOURCEFORGE_INSTALL_DIR/james/james-2.2.0/logs`. This log is overwritten each time Phoenix is (re)started.

Phoenix is run as part of the TeamForge standalone server init script.

Once started successfully, the search server waits for new content to be indexed or searches to be performed. The search server logs its activities under `SOURCEFORGE_INSTALL_DIR/james/james-2.2.0/apps/search/logs`. The logs that are created are all named default with the date stamp appended to them (such as `default-20041126.log`). A new log is created for each date that there is indexing activity.

If the search server is not running, or expected search results are not being provided, the default log is the best place to investigate further.

## Project Build Library (PBL) Audit Log
You can use this page to view the complete list of actions performed in the Project Build Library.

### Contents
Information about the following types of actions is displayed in this page:

* Change a File Description
* Create a Directory
* Delete a File or Directory
* Download a File
* Move a File or Directory
* Upload a File

{% include note.html content="The value displayed in the `Event` field is the value passed in the `--comment` parameter from the **Project Build Library** client." %}

### Getting There
On the project home page, click **Build Library** in the left navigation bar and select the **Audit Log** tab.

### Access
This page is accessible for all users who have at least the view permission for the project.

## Profile Audit Log
Use this page to view the complete list of actions performed on a profile.

### Getting There
On the Profile Library page, click the Audit Log tab.

### Access
This page is accessible for all users who have at least the view permission for the project to which the profile is allowed.

### Example
x
When a user updates any of the profile fields on the **Profile Admin** page, the following details are displayed in this page:

* The old value for the field.
* The new value for the field.
* The name of user who updated the field.
* The time when the change occurred.

## User Audit Log
You can use this page to view the list of actions performed by the user in the **TeamForge Lab Management** system.

For example, when a user logs into the web interface of the TeamForge Lab Management system, the event is displayed in this page.

### Getting There
On the **Administration** tab, click **User Audit Logs** in the left navigation bar.

### Access
This page is accessible to all users who have at least the Domain Administrator role.

## Host Audit Log
You can use this page to view the complete list of actions performed on a host.

### Getting There
On the TeamForge Lab Management Host home page, click the **Audit Log** tab.

### Access
This page is accessible for all users who have at least the view permission for the project to which the host is assigned.

### Example
When the IP address for the host is changed, the following details are displayed in this page:

* The old IP address.
* The new IP address.
* The name of user who changed the IP address.
* The time when the change occurred.

## Project Audit Log
The Project audit log page shows the complete list of changes applied to a project.

### Getting There
On the TeamForge Lab Management Project home page, click **Audit Logs** in the left navigation bar.

### Access
This page is accessible for all users who have at least the view permission for the project.

### Example
When a profile is added to the list of buildable profiles for this project, the following information appears on this page:

* The action that was taken.
* The user who performed the change.
* The time when this change occurred.

## etl.log
This file contains information from extract-transform-load runs, including data transformation warnings and errors.

{% include note.html content="Transformation errors do not constitute a failed ETL run. For example, if a corrupt row of data in one of the source tables causes transformation errors, this is treated as a `skipped record` and gets logged." %}

{% include links.html %}