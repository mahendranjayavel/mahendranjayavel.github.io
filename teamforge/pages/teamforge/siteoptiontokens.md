---
title: TeamForge site-options.conf Tokens
keywords: site-options.conf, site option tokens
tags: [ctf_22.0, ctf_20.1, ctf_20.0, ctf_19.3, ctf_19.2, ctf_19.0, ctf_18.3, ctf_18.2, installation, upgrade, site-options.conf, config_files, site_admin_tasks, security]
sidebar: teamforge_sidebar
permalink: siteoptiontokens.html
last_updated: Apr 8, 2022
toc: true
layout: "pagetable"
summary: Here's a list of TeamForge `site-options.conf` tokens and configuration information.
---

## TeamForge Services and Domain Configuration Tokens

See [TeamForge Services and Domain Configuration Tokens][siteconfigtokens].

{{site.data.alerts.hr_shaded}}
 
## ACTIVITY_LINKS_CUSTOMIZATION
When this token is set to `true`, the **TeamForge Activity Chart** and the **Most Active Projects List** do not appear on the main page before the user logs in.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## ADHOC_QUERY_CONNECTION_TIMEOUT {#ADHOC_QUERY_CONNECTION_TIMEOUT}
Specifies the connection timeout for Adhoc query. 

**Values**: Integer

**Default**: 15000

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## ADHOC_QUERY_RESULTS_LIMT {#ADHOC_QUERY_RESULTS_LIMT}

Specifies the results limit for Adhoc query.

**Values**: Integer

**Default**: 1000

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}
 
## ADMIN_EMAIL
The `ADMIN_EMAIL` token specifies a valid email address for the site administrator. The mail account specified must be hosted on a separate server outside of the TeamForge Application Server. The `SYSTEM_EMAIL`, `ADMIN_EMAIL`, and `JAMES_POSTMASTER_EMAIL` tokens can specify the same address.

{% include important.html content="In TeamForge 6.x (and later), the sender name and address for system-generated emails is taken from the value of the `SYSTEM_EMAIL` token. Therefore, changing the admin user's full name or email address does not affect the sender details of system-generated emails. This is different from TeamForge 5.x, in which the sender name and address for system-generated emails is derived from the admin user's full name and email address." %}

**Values**: Email address specification

**Default**: `root@{\__APPLICATION_HOST\__}`
{{site.data.alerts.hr_shaded}}
 
## ALLOW_CASE_INSENSITIVE_LOGIN {#allowcaseinsensitivelogin}
In general, TeamForge usernames are validated case-sensitively. Set this token to true so that username validations are done case-insensitively.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## ALLOWED_HOSTS {#ALLOWED_HOSTS}

This token is used to specify the list of allowed hostnames. This token works only if the `site-options.conf` token [SECURE_REDIRECTS][siteoptiontokens.html#SECURE_REDIRECTS] is set to _true_. When the HOST header is not equal to `NODE_HOSTNAME` or `ALLOWED_HOSTS`, then it redirects to the custom 400 error page.

**Values**: xxx.com yyy.com zzz.com (multiple hosts)

**Default**: none

{{site.data.alerts.hr_shaded}}
 
## ALLOW_NO_PASSWORD_ON_USER_CREATION
The `ALLOW_NO_PASSWORD_ON_USER_CREATION`token, when set to true, allows the admin to create users with null password through SOAP when external authentication is enabled.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## ALLOW_PASSWORD_DICTIONARY_WORD {#ALLOW_PASSWORD_DICTIONARY_WORD}

You must set the `REQUIRE_PASSWORD_SECURITY` token to `true` in the `site-options.conf` file, for ALLOW_PASSWORD_DICTIONARY_WORD security setting to take effect.
{{site.data.alerts.hr_shaded}}
 
## ALLOW_USERNAME_IN_PASSWORD
The `ALLOW_USERNAME_IN_PASSWORD` token, when set to true, allows users to set a password that includes the string that they use for their user name on the site.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## APPLICATION_LOG_DIR
The `APPLICATION_LOG_DIR` token specifies the directory to which the application writes its log files. 

**Values**: Path specification

**Default**: `/opt/collabnet/teamforge/log/apps`
{{site.data.alerts.hr_shaded}}
 
## APPROVE_NEW_USER_ACCOUNTS {#APPROVE_NEW_USER_ACCOUNTS}
The `APPROVE_NEW_USER_ACCOUNTS` token specifies whether a site administrator must approve the requests to join the site.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}
 
## ARTIFACT_DESC_EDITOR
The `ARTIFACT_DESC_EDITOR` token allows you to choose the type of text that can be used for artifact description using the editor tool.

**Values**: Plain Text

**Default**: Plain Text
{{site.data.alerts.hr_shaded}}
 
## ARTIFACT_LIST_LIMIT
The `ARTIFACT_LIST_LIMIT` token specifies the maximum number of artifacts displayed in and exported from the **Planned Tracker Artifacts** tab available in **File Releases**.

**Values**: Integer

**Default**: 5000
{{site.data.alerts.hr_shaded}}
 
## AUTO_DATA
TeamForge 7.1 and later support automatic password creation. Once you turn on automatic password creation, the `AUTO_DATA` token is auto-generated by the installer during runtime recreation.

{% include warning.html content="The `AUTO_DATA` token is not a user-editable site options token. Do not modify this token manually." %}

The following password-related `site-options.conf` tokens can have the passwords automatically created if set to *$auto$*. When set to *$auto$*, the passwords for the tokens are randomly generated, encrypted and stored in the `AUTO_DATA` token that is added automatically to the `site-options.conf` file during runtime recreation.

```shell
DATABASE_PASSWORD=$auto$
DATABASE_READ_ONLY_PASSWORD=$auto$
REPORTS_DATABASE_PASSWORD=$auto$
REPORTS_DATABASE_READ_ONLY_PASSWORD=$auto$
ETL_SOAP_SHARED_SECRET=$auto$
JAMES_ADMIN_PASSWORD=$auto$
BDCS_ADMIN_PASSWORD=$auto$
MIRROR_DATABASE_PASSWORD=$auto$
SCM_ADMIN_PASSWORD=$auto$
````

{% include warning.html content="As this `AUTO_DATA` token is auto-generated and managed by the TeamForge installer, do not modify this token manually during TeamForge upgrades. When you upgrade TeamForge, you must copy this token intact (along with its value) from the old `site-options.conf` file to the upgraded site's `site-options.conf` file, before recreating the runtime. This applies to all the servers in a distributed set up (copy the AUTO_DATA token and its value to all the servers)." %}

**This feature is enabled by default**. You can, however, override any of the above password-related tokens with the password of your choice.
{{site.data.alerts.hr_shaded}}

## BASELINE_BULKDATA_BATCHSIZE {#BASELINE_BULKDATA_BATCHSIZE}
Number of database records a thread (asynchronous) can handle at a time.

**Values**: 500, 600, 700, ...

**Default**: 500

{{site.data.alerts.hr_shaded}}

## BASELINE_BULKDATA_WORKER {#BASELINE_BULKDATA_WORKER}
Number of threads (asynchronous) dedicated for baseline creation.

**Values**: 100, 200, 300, ...

**Default**: 100
{{site.data.alerts.hr_shaded}}


## BASELINE_COMPARE_ROOT_FOLDER {#BASELINE_COMPARE_ROOT_FOLDER}

This token is used to configure the location where the Excel file is generated and stored when you export the diff of two Baselines.

**Values**: folder path

{{site.data.alerts.hr_shaded}}

## BASELINE_CTF_MAX_CONN {#BASELINE_CTF_MAX_CONN}
Maximum number of connections to TeamForge database.

**Values**: 1 - 20

**Default**: 20
{{site.data.alerts.hr_shaded}}

## BASELINE_CACHE_ENABLED {#BASELINE_CACHE_ENABLED}
This token is used to control the caching of Binaries (Nexus) within Baselines. The default value is _false_.

Loading a large number of Nexus repositories while creating baslines or baseline definitions can last for longer durations—typically slowing down the entire process itself. 

By enabling caching for baselines and setting up webhooks for the Nexus repositories, you can quickly load the list of Nexus repositories available to filter when you create or modify baselines or baseline definitions.

For more information, see [Enable Caching for Baselines][binary-repo-caching].

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## BASELINE_CACHE_EXPIRE_TIME {#BASELINE_CACHE_EXPIRE_TIME}
Expiration time for baseline data cache. 

**Values**: Integer (in minutes)

**Default**: 60 minutes 
{{site.data.alerts.hr_shaded}}

## BASELINE_CACHE_PURGE_TIME {#BASELINE_CACHE_PURGE_TIME}
Time taken to purge baseline data cache.

**Values**: Integer (in minutes)

**Default**: 10 minutes
{{site.data.alerts.hr_shaded}}

## BASELINE_FILE_STORAGE {#BASELINE_FILE_STORAGE}
Specifies the file location of baseline functions such as packaging and so on. 

**Values**: File path

{{site.data.alerts.hr_shaded}}

## BASELINE_LIQUIBASE_LOGLEVEL {#BASELINE_LIQUIBASE_LOGLEVEL}
<!-- Artifact artf394932 : [Baseline] Add new property named logLevel as info for baseline database migration in liquibase.properties -->
Use this token to add log entries related to baseline database migration. Set this token to `debug` to troubleshoot, issues, if any, during baseline database migration. 

**Default**: info

**Values**: info/debug/warning/severe/off

{{site.data.alerts.hr_shaded}}


## BASELINE_LOG_FILE {#BASELINE_LOG_FILE}

Specifies path of the baseline log file. 

**Values**: file path

**Default**: `/opt/collabnet/teamforge/log/baseline/baseline.log`

{{site.data.alerts.hr_shaded}}

## BASELINE_LOG_LEVEL {#BASELINE_LOG_LEVEL}
Specifies the log level for baseline service. The default log level is INFO.

**Values**: INFO, WARN/WARNING, ERROR, PANIC, DEBUG, FATAL 

**Default**: INFO 
{{site.data.alerts.hr_shaded}}

## BASELINE_LOG_MAX_AGE {#BASELINE_LOG_MAX_AGE}

Specifies the maximum age of baseline log file. Maximum configurable value is 28 days.

**Values**: Integer (in days)

{{site.data.alerts.hr_shaded}}

## BASELINE_LOG_MAX_BACKUP {#BASELINE_LOG_MAX_BACKUP}

Specifies the maximum number of last written log files used for backup. Up to 3 log files can be used.

**Values**: Integer 

{{site.data.alerts.hr_shaded}}

## BASELINE_LOG_MAX_COMPRESS {#BASELINE_LOG_MAX_COMPRESS}

Specifies whether to compress the maximum number of last written log files or not. 

**Values**: true, false

**Default**: true

{{site.data.alerts.hr_shaded}}

## BASELINE_LOG_MAX_SIZE {#BASELINE_LOG_MAX_SIZE} 

Specifies the maximum size of baseline log file. Maximum configurable size is 500MB.

**Values**: 100MB, 125MB, .... 500MB 

{{site.data.alerts.hr_shaded}}

## BASELINE_POST_INSTALL_PORT {#BASELINE_POST_INSTALL_PORT}
Specifies the port number of the server on which the `baseline-post-install` service is hosted. The default port is _9192_.

**Values**: Port number of server hosting `baseline-post-install` service

**Default**: 9192
{{site.data.alerts.hr_shaded}}

## BASELINE_PSQL_MAX_CONN {#BASELINE_PSQL_MAX_CONN}
Maximum number of connections to baseline database.

**Values**: 1 - 100

**Default**: 100
{{site.data.alerts.hr_shaded}}

## BCC_MAIL_BATCH_SIZE

Set the `ENABLE_BCC_MONITORING` token to **true** and then depending on your site's requirements, you can set the value of this `BCC_MAIL_BATCH_SIZE` token to configure the number of monitoring emails delivered in a single delivery.

When a work item such as an artifact or discussion is updated, instead of sending separate monitoring emails to all monitoring users, you can now choose to have just one monitoring email sent with all monitoring users added to the BCC. This reduces the load on the email server and results in faster email delivery. You must enable this feature by setting `ENABLE_BCC_MONITORING` to **true** and then, depending on your site's requirements, you can optimize the value of this `BCC_MAIL_BATCH_SIZE` token to increase or decrease the number of emails delivered in a single delivery.

**Values**: Integer

**Default**: 100

This token was added in TeamForge 7.2.
{{site.data.alerts.hr_shaded}}
 
## BINARY_SETUP_TYPE

Set this token appropriately to have the binary application installed the way you want (as part of the TeamForge installation or upgrade).

TeamForge 8.0 and later support integration with Nexus OSS, an open source repository manager for binary artifacts. By default, the TeamForge installer installs a binary application (referred to as the `binary app` hereinafter), which is essentially a launching pad for all binary integrated applications such as Nexus OSS. Once this binary app is installed as part of TeamForge installation, you can integrate your Nexus servers and repositories with TeamForge.

Though the binary app is installed by default with TeamForge, you can change the value of this site option token, `BINARY_SETUP_TYPE`, to skip binary app installation altogether. You can also have this token configured to have the binary app installed and rolled out for all projects (both existing and new projects to be created) or only for new projects to be created or for select projects on a need basis.


**Values**:
* all: Binary app is installed and available for all projects.
* new: Binary app is installed and available for new projects only.
* manual: Binary app is installed at a site level and project administrators can add it to select projects on a need basis.
* none: TeamForge installer skips the binary app installation altogether.

**Default**: new

This token was added in TeamForge 8.0.
{{site.data.alerts.hr_shaded}}

## BINARIES_ENDPOINT_URL {#BINARIES_ENDPOINT_URL}

Specifies the URL of Nexus binaries server.

**Values**: Server URL

{{site.data.alerts.hr_shaded}}

## BROWSER_NO_CACHE {#browsernocache}

`BROWSER_NO_CACHE` is a new token added to `runtime-options.conf` file to enable or disable browser caching in TeamForge for better application performance. By default, the token is set to `false` in `runtime-options.conf` file. To disable browser caching, set the value to _true_ in `site-options.conf` file.

**Values**: true or false

**Default**: false

{{site.data.alerts.hr_shaded}}

## COMPARE_LIMIT {#COMPARE_LIMIT}

Maximum number of records allowed while comparing baselines. Only up to 10,000 records are allowed.

**Values**: 1 - 10000

**Default**: 10000
{{site.data.alerts.hr_shaded}}
 
## DATABASE_NAME

The `DATABASE_NAME` token specifies the name of the site's database.

**Values**: Alphanumeric string

**Default**: teamforge
{{site.data.alerts.hr_shaded}}

## DATABASE_PASSWORD

The `DATABASE_PASSWORD` token is the password for the Unix user that is authorized to read from and write to the site's database.

**Values**: Alphanumeric string

**Default**: $auto$
{{site.data.alerts.hr_shaded}}

## DATABASE_SSL {#DATABASE_SSL}

To prevent your data from being exposed in a readable format on the network, use the Secure Socket Layer (SSL) to encrypt the network traffic between the Application and the Database servers. The `DATABASE_SSL` token turns SSL `on` or `off` on sites that use a dedicated operational database server. 

You can have the TeamForge PostgreSQL database server run with SSL enabled by setting `DATABASE_SSL=on`. Once SSL is turned on, the PostgreSQL server listens to both normal and SSL connections on the same TCP port and negotiates with any connecting client on whether to use SSL or not.

To start in SSL mode, the server certificate and private key files must exist. These files are, by default, supposed to be named `server.crt` and `server.key`, respectively, in the database server's data directory. 

Use the `POSTGRES_SSL_CERT_FILE` and `POSTGRES_SSL_KEY_FILE` tokens to configure the location of the `server.crt` and `server.key` files of the TeamForge PostgreSQL database server respectively.

For example,
```shell
DATABASE_SSL=on
POSTGRES_SSL_CERT_FILE=/var/ops/ssl/dbserver.crt
POSTGRES_SSL_KEY_FILE=/var/ops/ssl/dbserver.key
````

Use the `POSTGRES_BASELINE_SSL_CERT_FILE` and `POSTGRES_BASELINE_SSL_KEY_FILE` tokens to configure the location of the `server.crt` and `server.key` files of the TeamForge Baselines PostgreSQL database server respectively.

For example,
```shell
DATABASE_SSL=on
POSTGRES_SSL_CERT_FILE=/var/ops/ssl/dbserver.crt
POSTGRES_SSL_KEY_FILE=/var/ops/ssl/dbserver.key
POSTGRES_BASELINE_SSL_CERT_FILE=/var/ops/ssl/baselinedb-server.crt
POSTGRES_BASELINE_SSL_KEY_FILE=/var/ops/ssl/baselinedb-server.key
````

**Values**: `on` or `off`

**Default**: `off`
{{site.data.alerts.hr_shaded}}
 
## DATABASE_TYPE

The `DATABASE_TYPE` token specifies the type of database in which the TeamForge site's data is stored.

**Values**: postgresql or oracle

**Default**: postgresql
{{site.data.alerts.hr_shaded}}
 
## DATABASE_USERNAME

The `DATABASE_USERNAME` token specifies the Unix user that is authorized to read from and write to the site's database.

**Values**: Alphanumeric string

**Default**: teamforge

**Comments**: For some advanced operations, you may need to log into the database as the database user. However, under normal conditions only the TeamForge site process itself needs to access the database.
{{site.data.alerts.hr_shaded}}
 
## DEFAULT_LOCALE

The `DEFAULT_LOCALE` token specifies the language in which automated email messages from the site are generated.

**Values**:

**Default**: en
{{site.data.alerts.hr_shaded}}
 
## DEFAULT_PROJECT_ACCESS

The `DEFAULT_PROJECT_ACCESS` token specifies the type of access that is assigned to a project when it is created. A project can be private, public, or gated.

**Values**: private, gated, public

**Default**: private
{{site.data.alerts.hr_shaded}}
 
## DISABLE_CREATE_INTEGRATION_SERVERS {#disable_create_integration_servers}

The `DISABLE_CREATE_INTEGRATION_SERVERS` token specifies whether the creation of new SCM integrations is allowed.

**Values**: true or false

**Default**: false

**Comments**: When this token is set to its default value of `false`, you can add SCM integration servers to your TeamForge site. Also, the **Discover Subversion Edge Servers** option, which enables you to find and connect to Subversion Edge servers on your LAN, is available.
{{site.data.alerts.hr_shaded}}
 
## DISABLE_REMOTE_PUBLISHING

Publishing repository, like the branding repository, is one of the default repositories that's created automatically when a TeamForge project is created and is intended to contain publicly-consumable files. However, site administrators can toggle access to Publishing Repositories and restrict access based on defined RBAC.

For more information on Publishing Repository, see [What is a Publishing repository? How does it work?][faqs.html#publishingrepository]. This token is set to false by default, meaning the Publishing Repository is publicly accessible.

If set to `true`:

* The Publishing Repository is stripped of its public access and behaves like any other Subversion repository with RBAC applied to it.
* Project Administrators can no longer view or modify the **PROJECT HOME OPTIONS** (see Create a custom project home page).

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}
 
## DISABLE_USER_SELF_CREATION {#DISABLE_USER_SELF_CREATION} {#DISABLE_USER_SELF_CREATION}

The `DISABLE_USER_SELF_CREATION` token restricts users from creating their own accounts on the TeamForge home page.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_ADD_HEADERS

The `DISCUSSION_ADD_HEADERS` token allows you to add custom headers to the emails posted in the forum.

**Values**:
You can choose to add or remove headers by specifying the particular information you want to be added or dropped from the header. For example, if you add `<#d#>` in the **Add header** field, the URL of that discussion will be added to the header of all the available messages in that discussion.

**Default**: None

**Example**:

```shell
DISCUSSION_ADD_HEADERS=headername1:value1, name2: value2 , post-id:<#n#>, forum-url:<#d#>, message-url:<#m#>, domain:<#h#>, list-name:<#l#>, list-address:<#l#>@<#h#>
````

**Comments**: Add one or more header names. The match of any of these headers in an outgoing message (via email) causes its addition with appropriate notification to the posting user.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_DROP_MIME_TYPES

The `DISCUSSION_DROP_MIME_TYPES` token allows you to delete the mime types submitted by email that contain arbitrary strings. 

**Values**: image/jpeg,image/jpg,text/xml

**Default**: Regular expression

**Example**:

```shell
DISCUSSION_DROP_MIME_TYPES=image/jpeg,image/jpg,text/xml
````

**Comments**: Add one or more mime types to the Drop mime types filter. The presence of any of these mime types in an incoming message (via email) causes its deletion with appropriate notification to the posting user. If a mime type is specified in both the Reject and Drop mime filters, then the Reject mime type filter must take higher precedence than the Drop mime type filter.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_EMAIL_MONITORING

The `DISCUSSION_EMAIL_MONITORING` token determines which users can monitor a forum on the site.

**Values**:

| Value | Description |
|----|----|
| 0 | Allow only forum administrators |
| 1 | Users with role permissions |
| 4 | All logged in users |
| 5 | Allow all site users and guests |

**Default**: 1

**Example**:
```shell
DISCUSSION_EMAIL_MONITORING=4
````

**Comments**: This setting applies to the site as a whole. Project owners can choose to be more restrictive in their own project by selecting a lower value on the project administration page.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_EMAIL_POSTING

The `DISCUSSION_EMAIL_POSTING` token determines which users on your site can post to forums by e-mail.

**Values**:

| Value | Description |
|----|----|
| 0 | Allow only forum administrators |
| 1 | Users with role permissions |
| 4 | All logged in users |
| 5 | Allow known email addresses only |
| 6 | Allow all site users and guests |


**Default**: 1

**Example**:

```shell
DISCUSSION_EMAIL_POSTING=4
````

**Comments**: This setting applies to the site as a whole. Project owners can choose to be more restrictive in their own project by selecting a lower value on the project administration page.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_FORUM_EDITOR

The `DISCUSSION_FORUM_EDITOR` token allows you to choose the type of text that can be used in discussion forum description using the editor tool.

**Values**: Plain Text

**Default**: Plain Text
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_MAX_ATTACHMENT_SIZE {#DISCUSSION_MAX_ATTACHMENT_SIZE}

The `DISCUSSION_MAX_ATTACHMENT_SIZE` token sets an upper limit to the size of files that users can attach to an email message sent to any discussion forum on the site.

**Values**: Integer (Megabytes)

**Default**: blank

**Comments**: A value of zero or less specifies that there is no limit, which is the same as the default behavior without the token.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_POST_EDITOR

The `DISCUSSION_POST_EDITOR` token allows you to choose the type of text that can be used for posting in discussion forums using the editor tool.

**Values**: Plain Text

**Default**: Plain Text
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_REJECT_CONTENT

The `DISCUSSION_REJECT_CONTENT` token allows you to block the discussion messages submitted by email that contain arbitrary strings.

**Values**: Regular expression

**Default**: None

**Example**:
```shell
DISCUSSION_REJECT_CONTENT=(?s).*word.*,(?s).*spam.*
````

**Comments**: Add one or more entries. Each regular expression must match an entire entry. The match of any of these entries in the body or subject of an incoming message (via email) causes its rejection, with appropriate notification to the posting user.

{% include note.html content="The content entry is case sensitive." %}
{{site.data.alerts.hr_shaded}}

## DISCUSSION_REJECT_HEADERS

The `DISCUSSION_REJECT_HEADERS` token allows you to block different headers submitted by email that contain arbitrary strings.

**Values**: Regular expression

**Default**: None

**Example**:
```shell
DISCUSSION_REJECT_HEADERS=(?s).*headername1:value2.*,(?s).*name2:value2.*
````

**Comments**: Add one or more header names. Each regular expression must match an entire header name. The match of any of these headers in an incoming message (via email)causes its rejection, with appropriate notification to the posting user.
{{site.data.alerts.hr_shaded}}
 
## DISCUSSION_REJECT_MIME_TYPES

The `DISCUSSION_REJECT_MIME_TYPES` token allows you to delete the mime types submitted by email that contain arbitrary strings.

**Values**: Application/PDF,text/xml

**Default**: Regular expression

**Example**:
```shell
DISCUSSION_REJECT_MIME_TYPES=application/pdf,text/xml
````

**Comments**: Add one or more mime types to the Reject MIME types filter. The presence of any of these mime types in an incoming message (via email) will cause its deletion with appropriate notification to the posting user.
{{site.data.alerts.hr_shaded}}
 
## DISPLAY_TIMEZONE {#displaytimezone}

The `DISPLAY_TIMEZONE` token, if set with a preferred time zone, takes precedence over the physical TeamForge server location's time zone and will be the default time zone that's displayed throughout the application. In other words, use this token to set a preferred time zone to display across the TeamForge application in case the TeamForge physical server and users are not on the same time zone.

**Values**:
The ID for a time zone can be either a full name such as America/Los_Angeles, or a custom ID in the form GMT[+|-]hh[[:]mm] such as GMT-08:00. It can also be in the form of a three letter abbreviation such as PST.

**Default**: 
If set, this token overrides the default time zone of the TeamForge server. TeamForge uses the default time zone of the JVM otherwise.
{{site.data.alerts.hr_shaded}}
 
## DOCUMENT_MAX_FILE_UPLOAD_SIZE {#DOCUMENT_MAX_FILE_UPLOAD_SIZE}

By default, you can upload documents of any size in TeamForge. The `DOCUMENT_MAX_FILE_UPLOAD_SIZE` token sets an upper limit to the size of the documents that can be uploaded. Use this token only if you want to restrict the size of the documents. 

**Values**: Integer (specify the number of Megabytes without the suffix `MB`)

**Default**: blank

**Comments**: 
A value of zero specifies that there is no limit, which is the same as the default behavior without the token. In other words, disabling this token, setting a value of 0, or leaving it blank sets the maximum file upload size to unlimited.
{{site.data.alerts.hr_shaded}}
 
## DOCUMENT_TEXT_EDITOR

The `DOCUMENT_TEXT_EDITOR` token allows you to choose the type of text that can be used for the document description using the editor tool.

**Values**: Plain Text

**Default**: Plain Text 
{{site.data.alerts.hr_shaded}}
 
## ELASTICSEARCH_JAVA_OPTS {#elasticsearch}

The `ELASTICSEARCH_JAVA_OPTS` token specifies the memory settings for the Java virtual machine that supports Elasticsearch, used by TeamForge Code Search.

**Values**: Java specifications

**Default**: 

`ELASTICSEARCH_JAVA_OPTS=-Dlog4j2.formatMsgNoLookups=true`

**Comments**:
<!-- (See: https://forge.collab.net/sf/go/artf300770) -->
As a result of changes to the logging framework in Java, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later.

* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
* ELASTICSEARCH_JAVA_OPTS
   
TeamForge provision fails on sites that use these options post upgrade to TeamForge 18.1 or later.

* New tokens, `ELASTICSEARCH_MIN_HEAP_SIZE` and `ELASTICSEARCH_MAX_HEAP_SIZE`, have been added in TeamForge 22.0, which are to be configured along with the  `ELASTICSEARCH_JAVA_OPTS` token. 
* Do not specify the minimum and maximum heap size in `ELASTICSEARCH_JAVA_OPTS`. Use `ELASTICSEARCH_MIN_HEAP_SIZE` and `ELASTICSEARCH_MAX_HEAP_SIZE` tokens instead. 
{{site.data.alerts.hr_shaded}}

## ELASTICSEARCH_MIN_HEAP_SIZE {#esminheap}

The `ELASTICSEARCH_MIN_HEAP_SIZE` token specifies the minimum memory settings for the Java virtual machine that supports Elasticsearch, used by TeamForge Code Search.

**Values**: Java specifications

**Default**: `-Xms2g`

{% include note.html content="By default, Elasticsearch JVM minimum heap size is set to 2GB in TeamForge. You can increase this, if required." %}
## ELASTICSEARCH_MAX_HEAP_SIZE {#esmaxheap}

The `ELASTICSEARCH_MAX_HEAP_SIZE` token specifies the maximum memory settings for the Java virtual machine that supports Elasticsearch, used by TeamForge Code Search.

**Values**: Java specifications

**Default**: `-Xmx2g`

{% include note.html content="By default, Elasticsearch JVM maximum heap size is set to 2GB in TeamForge. You can increase this, if required." %}
 
## ENABLE_BCC_MONITORING

When a work item such as an artifact or discussion is updated, instead of sending separate monitoring emails to all monitoring users, you can now choose to have just one monitoring email sent with all monitoring users added to the BCC. This reduces the load on the email server and results in faster email delivery. Set `ENABLE_BCC_MONITORING` to `true` to enable this feature.

**Values**: true or false

**Default**: false

**Comments**: 
Depending on your site's requirements, you can also optimize the value of `BCC_MAIL_BATCH_SIZE` to increase or decrease the number of emails delivered in a single delivery.
{{site.data.alerts.hr_shaded}}

## ENABLE_GO_PROFILING {#ENABLE_GO_PROFILING}
Debugs the baseline service, if enabled. By default, this token is disabled.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## ENABLE_SERVICE_MONITORING {#ENABLE_SERVICE_MONITORING}
If `ENABLE_SERVICE_MONITORING` token is set to `true`, then the services using monit will be enabled for service monitoring. By default, this token is set to `false`.

**Values**: true or false

**Default**: false

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## ENABLE_SITE_NEWS {#enablesitenews}

Site news is disabled by default. Set this token to `true` in `site-options.conf` file, customize the home page of your site and recreate runtime if you want to publish site news on your site's home page.

To publish site news, set this token to `true` in `site-options.conf` file, [customize the home page of your site (see "siteNews" html block)][customize.html#customizehomepage] and recreate runtime if you want to publish site news on your site's home page.

**Values**: true or false

**Default**: false

**Comments**:
This token was added in TeamForge 16.7. Until TeamForge 16.3, regardless of whether you have site news enabled or not, site news were processed in the background. With this ENABLE_SITE_NEWS token, there is no site news processing in the background (by default `ENABLE_SITE_NEWS=false`) thereby improving the site's home page performance a bit.
{{site.data.alerts.hr_shaded}}

## ENABLE_UI_FOR_CUSTOM_EVENT_HANDLERS {#enableuiforcustomeventhandlers}
To support branding and customization changes, set the `ENABLE_UI_FOR_CUSTOM_EVENT_HANDLERS` token to `true`.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## ENFORCE_MINIMUM_USERNAME_LENGTH {#enforceminusernamelength}

The `ENFORCE_MINIMUM_USERNAME_LENGTH` variable determines the minimum length that can be set for usernames.

**Values**: 0-31

**Default**: 0

{{site.data.alerts.hr_shaded}}

## ETL_JAVA_OPTS {#etljavaopts}

The `ETL_JAVA_OPTS` token specifies the memory settings for the Java virtual machine that supports the ETL (Extract Transform and Load) job.

**Values**: Java specifications

**Default**:

```shell
-Xms160m -Xmx512m -server -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp -verbose:gc -XX:+ PrintGCTimeStamps -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=600000 -Dsun.rmi.dgc.server.gcInterval=600000 - Djava.security.egd=file:/dev/urandom
````
{% include note.html content="If you've enabled ETL_JAVA_OPTS token in `site-options.conf` file and have added any parameter, you must provide the required JVM heap size as the default heap size is not taken into account." %}

**Comments**:
<!-- (See: https://forge.collab.net/sf/go/artf300770) -->TeamForge 18.1 (and later) supports Java 9. As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later.

* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
* ELASTICSEARCH_JAVA_OPTS

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## ETL_JOB_THREAD_COUNT
The `ETL_JOB_THREAD_COUNT` token specifies the number of Extract, Transform and Load (ETL) jobs that can be run simultaneously.

**Values**: 1-100

**Default**: 2

**Comments**:
If you only have a few jobs to be triggered few times a day, then one thread is sufficient. If you have tens of thousands of jobs, that needs to be triggered every minute, then you should consider increasing the thread count to 50 or 100 (this depends on the nature of the work that your jobs perform, and your resources).
{{site.data.alerts.hr_shaded}}

## ETL_JOB_TRIGGER_TIME {#etljobtriggertime}
The `ETL_JOB_TRIGGER_TIME` token specifies the time and date for recurrent Extract, Transform and Load (ETL)jobs.

**Values**: Cron expression.


**Default**:
0 30 2 * * ?

**Comments**:
This token takes a cron expression for a value, and not an absolute time value. The default value evaluates to 2.30 a.m. local time. For help with cron expressions, see [Cron Trigger Tutorial](http://www.quartz-scheduler.org/documentation/quartz-2.x/tutorials/crontrigger.html).

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## ETL_SOAP_SHARED_SECRET
The `ETL_SOAP_SHARED_SECRET` token enables users to access site-wide reporting data via a SOAP client.

**Values**: String (possibly encrypted).

**Default**: mightyetlsoapsecret
{{site.data.alerts.hr_shaded}}

## FILTER_DROPDOWN_MAX_SELECTION
By default, the drop-down lists with multi-select feature let you select up to 10 filter values. However, you can set any value that suits your requirement for this `FILTER_DROPDOWN_MAX_SELECTION` token to increase or decrease the count.

**Values**: Any positive integer.

**Default**: 10

This token was added in TeamForge 7.1.
{{site.data.alerts.hr_shaded}}

## FORBIDDEN_PASSWORD
The `FORBIDDEN_PASSWORD` token restricts specified words from being used as passwords.

**Values**: Comma-separated strings

**Default**: None
{{site.data.alerts.hr_shaded}}

## GERRIT_DATABASE_HOST
This is the Gerrit Postgres database host. The Gerrit configuration property, database.hostname, is derived from the value of `GERRIT_DATABASE_HOST` token in the `runtime-options.conf`. It can be overridden in `site-options.conf` and requires runtime creation with execution of the post installation script.

**Default**: 127.0.0.1
{{site.data.alerts.hr_shaded}}

## GERRIT_DATABASE_NAME
This refers the Gerrit database schema. The Gerrit configuration property, database.database, is derived from the value of `GERRIT_DATABASE_NAME` in `runtime-options.conf`. It can be overridden in `site-options.conf` and requires runtime creation with execution of post installation script.

**Default**: reviewdb
{{site.data.alerts.hr_shaded}}

## GERRIT_DATABASE_USER
This is the PostgresDB role name that has access to the Gerrit database `GERRIT_DATABASE_NAME`. The Gerrit configuration property, `database.username`, is derived from the value of `GERRIT_DATABASE_USER` in the `runtime-options.conf`. It can be overridden in `site-options.conf` and requires runtime creation with execution of post installation script.

**Default**: gerrit
{{site.data.alerts.hr_shaded}}

## GERRIT_GIT_PUSH_THRESHOLD {#gitpushthreshold}

The `GERRIT_GIT_PUSH_THRESHOLD` token determines the maximum number of commits in a single Git push. If the limit exceeds, only a single commit object is created in the TeamForge.

**Values**: Any positive integer.

**Default**: 30
{{site.data.alerts.hr_shaded}}

## GERRIT_GIT_REFRESH_PERIOD
The `GERRIT_GIT_REFRESH_PERIOD` token sets the interval in seconds after which Git Integration synchronizes all the repositories and all RBAC permission with TeamForge.

**Values**: Number of seconds

**Default**: 3600 seconds
{{site.data.alerts.hr_shaded}}

## GERRIT_REPLICATION_MODE
Use this site-options token to set the Git integration server as either `master` or `slave` server. In case you do not want replication (standalone mode) or you have only one primary source for repositories, set this token to master. On the other hand, if you have a master Git integration server and you want to replicate (mirror) its repositories on a secondary slave Git integration server, set this token to slave on the slave Git integration server.

**Values**: master or slave

**Default**: master

**Comments**: 
By default, in TeamForge 8.1 (and later), this token is set to master in the `runtime-options.conf` during runtime creation. As you cannot change the replication mode of a Git server after initial runtime creation, you have to set this to slave at the very beginning of your installation process in case you want to configure the server as a mirror of a `master` Git server. It is not possible to have a Git master and slave configured on the same node, but you can have multiple masters and slaves in your TeamForge environment. Each slave belongs to exactly one master. Once a replica server is set up, it is not possible to reassign it to a different master Git integration server at a later point in time.
{{site.data.alerts.hr_shaded}}

## GERRIT_REPLICATION_MASTER_EXTERNAL_SYSTEM_ID
If `GERRIT_REPLICATION_MODE` is set to `slave`, this token specifies external system ID of the `master` Git integration server.

**Values**: Alphanumeric string (exsy\<number>) of a master Git integration server

**Comments**:
This token is mandatory if `GERRIT_REPLICATION_MODE` is set to `slave`, without which the runtime creation shall fail. On the contrary, the runtime recreation will also fail if `GERRIT_REPLICATION_MODE` is set to `master` and this token is present in the `site-options.conf` file.
{{site.data.alerts.hr_shaded}}

## GERRIT_SMTP_SERVER
This is the hostname of the SMTP mail server for Gerrit. The Gerrit configuration property, `sendmail.smtpServer`, is derived from the value of `GERRIT_SMTP_SERVER` in the `runtime-options.conf`. It can be overridden in `site-options.conf` and requires runtime creation with execution of post installation script.

**Default**: localhost
{{site.data.alerts.hr_shaded}}

## GERRIT_SYNCH_PORT
The Port over which TeamForge communicates to Gerrit. The Gerrit configuration property, `teamforge.apiPort`, is derived from the value of `GERRIT_SYNCH_PORT` in the `runtime-options.conf`. It can be overridden in `site-options.conf` and requires runtime creation with execution of post installation script.

**Default**: 9081
{{site.data.alerts.hr_shaded}}

## GERRIT_USER_EMAIL {#gerrituseremail}

This token sets the user email account for sending emails from Gerrit. This refers to all Gerrit servers specified in `site-options.conf` file or through cluster/server specific parameters. For example, the "clusterId/serverId" in `[clusterId/serverId]:gerrit:user.email`  refers to the cluster or server that is used.

**Values**:

**Default**: 

{{site.data.alerts.hr_shaded}}

## HAPROXY_HTTP_REUSE_OPTION {#HAPROXY_HTTP_REUSE_OPTION}

This token is used to declare how idle HTTP connections can be shared between requests. The default value is `safe`, which ensures that in case the backend server closes the connection when the request is being sent, the browser silently retries to keep the connection alive.

**Values**: never/safe/aggressive/always

**Default**: safe

{{site.data.alerts.hr_shaded}}

## HIGHCHARTS_EXPORT_REQUEST_MAX_WAIT
This token is used to set the number of milliseconds that the Highcharts web application has to wait for response from the phantomjs server before it times out.

TeamForge chart export feature requires a pool of phantomjs servers to be running in the application server that is managed by a Highcharts web application. The phantomjs server pool runs as a blocking queue.

This token is used to specify the number of milliseconds that the Highcharts web application has to wait before it times out. In other words, the phantomjs server is expected to respond to the Highcharts web application within the time limit (in milliseconds) set in `HIGHCHARTS_EXPORT_REQUEST_MAX_WAIT`.

**Default**: 500 milliseconds

This token was added in TeamForge 7.2.
{{site.data.alerts.hr_shaded}}

## HIGHCHARTS_EXPORT_REQUEST_POOL_SIZE
TeamForge chart export feature requires a pool of phantomjs servers to be running in the application server that is managed by a Highcharts web application. This token is used to specify the number of phantomjs servers to be running in the pool.

**Default**: The default pool size is 10.

This token was added in TeamForge 7.2.
{{site.data.alerts.hr_shaded}}

## HTTPD_LOG_DIR
The `HTTPD_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's Apache service is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/httpd`
{{site.data.alerts.hr_shaded}}

## HTTP_MAX_PARAMETERS
The `HTTP_MAX_PARAMETERS` token determines the maximum number of parameters (fields) that could be submitted in one http request. This is relevant on pages such as the User-Role Matrix page. The `HTTP_MAX_PARAMETERS` can range from 0-25000.

**Values**: 0-25000

**Default**: 5000
{{site.data.alerts.hr_shaded}}

## INCLUDE_ORGANIZATION_USER_FIELD
The `INCLUDE_ORGANIZATION_USER_FIELD` token controls whether the organization entry is displayed while creating a user account.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## INDEXING_TIMEOUT
The `INDEXING_TIMEOUT` token allows you to configure the time limit for indexing a file.

**Values**: Integer (number of minutes)

**Default**: 5
{{site.data.alerts.hr_shaded}}

## INITIAL_PASSWORD_CHANGE_ACTIVATION_CODE_TIMEOUT
An administrator can optionally supply a password when creating a user. If the password is not specified while creating the user, the user is sent an email with a ticket to set the password. This `INITIAL_PASSWORD_CHANGE_ACTIVATION_CODE_TIMEOUT` token sets the duration (in hours) for which the password ticket is valid.

**Values**: Integer (hours)

**Default**: 72
{{site.data.alerts.hr_shaded}}

## INTEGRATION_JAVA_OPTS
This token specifies the memory settings for the Java virtual machine that supports the site's integrated source control services.

**Values**: Java specifications

**Default**:  
```shell
-Xms160m -Xmx160m -server -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp -verbose:gc -XX: +PrintGCTimeStamps -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=600000 -Dsun.rmi.dgc.server.gcInterval=600000 - Djava.security.egd=file:/dev/urandom
````

{% include note.html content="If you've enabled INTEGRATION_JAVA_OPTS token in `site-options.conf` file and have added any parameter, you must provide the required JVM heap size as the default heap size is not taken into account." %}

**Comments**:
<!-- (See: https://forge.collab.net/sf/go/artf300770) -->TeamForge 18.1 (and later) supports Java 9. As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later.

* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
* ELASTICSEARCH_JAVA_OPTS
   
TeamForge provision fails on sites that use these options post upgrade to TeamForge 18.1.
{{site.data.alerts.hr_shaded}}

## INTEGRATION_LOG_DIR
The `INTEGRATION_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's source code integrations is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/integration`
{{site.data.alerts.hr_shaded}}

## JAMES_DKIM_VERIFICATION {#JAMES_DKIM_VERIFICATION}
This token is used to enable or disable DomainKeys Identified Mail (DKIM) for outbound mails in TeamForge.  

**Values**: on, off

**Default**: off
{{site.data.alerts.hr_shaded}}

## JAMES_DKIM_SELECTOR {#JAMES_DKIM_SELECTOR}
This token specifies the string used to identify the DKIM public key information. It is specified as an attribute for the DKIM signature and is included in the DKIM header.

**Values**: a valid string parameter
{{site.data.alerts.hr_shaded}}

## JAMES_DKIM_SIGNINGDOMAIN {#JAMES_DKIM_SIGNINGDOMAIN}
This token specifies the public domain name to be associated with the email authenticated with DKIM.

**Values**: Domain name of the CTF instance
{{site.data.alerts.hr_shaded}}

## JAMES_DKIM_KEY_TYPE {#JAMES_DKIM_KEY_TYPE}
This token specifies the key type to be used for the domain name verification.

**Values**: 1024 / 2048

**Default**: `2048`
{{site.data.alerts.hr_shaded}}

## JAMES_GATEWAY_HOST {#JAMES_GATEWAY_HOST}
The `JAMES_GATEWAY_HOST` token specifies a mail server with Internet access, separate from the TeamForge server.

**Values**: Email address specification

**Default**: None

**Comments**: 
* Specifying a gateway host assures delivery of site email to users if your TeamForge server cannot connect to a DNS server or cannot get outside connections over port 25.
* The mail account specified must be hosted on a separate server from the TeamForge site server.
* The SYSTEM_EMAIL, ADMIN_EMAIL, and JAMES_POSTMASTER_EMAIL tokens can specify the same address.

{% include note.html content="Specify the gateway host by its fully qualified domain name, not a host name." %}

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## JAMES_GATEWAY_* {#JAMES_GATEWAY}
You can set up TeamForge to relay emails through an SMTP gateway (such as Amazon AES) that uses authentication. By default, James sends emails directly. However, you may prefer relaying emails through an enterprise relay server. Configuring the `JAMES_GATEWAY_*` tokens let you do that.

* `JAMES_GATEWAY_HOST` and `JAMES_GATEWAY_PORT` tokens specify the relay server's FQDN and port to use respectively. The `JAMES_GATEWAY_HOST` token specifies a mail server with Internet access, separate from the TeamForge Application Server. Specify the gateway host by its fully qualified domain name (FQDN), not a host name. {% include installupgrade/teamforgereload.html %}
* `JAMES_GATEWAY_USERNAME` and `JAMES_GATEWAY_PASSWORD` tokens specify the relay server credentials. These tokens are optional that should only be used if the relay server requires SMTP authentication.

For more information, see [Relay Emails Through SMTP Gateway with Authentication][manageemails.html#relayemailssmtp].
{{site.data.alerts.hr_shaded}}

## JAMES_LOG_DIR
The `JAMES_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's email component is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/james`
{{site.data.alerts.hr_shaded}}

## JAMES_POSTMASTER_EMAIL
The `JAMES_POSTMASTER_EMAIL` token specifies a valid email address for the person or machine that handles email for the domain, such as postmaster@supervillain.org.

**Values**: Email address specification

**Default**: `root@{__APPLICATION_HOST__}`

**Comments**:
* The mail account specified must be hosted on a separate server outsideof the TeamForge Application Server.
* The SYSTEM_EMAIL, ADMIN_EMAIL, and JAMES_POSTMASTER_EMAIL tokens can specify the same address.
{{site.data.alerts.hr_shaded}}

## JBOSS_ALARM_TIMEOUT
The `JBOSS_ALARM_TIMEOUT` token specifies the time duration within which the JBoss service is expected to respond to requests sent by jboss_watchdog.

**Values**: Integer

**Default**: 20
{{site.data.alerts.hr_shaded}}

## JBOSS_JAVA_OPTS

The `JBOSS_JAVA_OPTS` token specifies the memory settings for the JBoss Java virtual machine.

**Values**: Java specifications

**Default**: `-Xms1536m -Xmx1536m`

{% include note.html content="If you've enabled JBOSS_JAVA_OPTS token in `site-options.conf` file and have added any parameter, you must provide the required JVM heap size as the default heap size is not taken into account." %}

**Comments**:
All JVM parameters but `-Xms1536m` and -`Xmx1536m` have been hard-coded in the TeamForge core application. 

You cannot manually configure any of the following default JVM parameters in the ``site-options.conf`` file.
```conf
-XX:+UseParallelGC
-XX:MaxMetaspaceSize=512m
-XX:ReservedCodeCacheSize=128M
-server
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/tmp -verbose:gc
-XX:+PrintCodeCache
-Dsun.rmi.dgc.client.gcInterval=600000
-Dsun.rmi.dgc.server.gcInterval=600000
-Djava.security.egd=file:/dev/urandom
-Djava.awt.headless=true.
````
{% include warning.html content="When you change the default value of a JVM parameter such as `-XX:HeapDumpPath`, the JBoss runtime parameters include both the user defined and default values for the JVM parameter. However, JBoss runs with the default value and ignores any user defined value." %}

<!-- (See: https://forge.collab.net/sf/go/artf300770) -->TeamForge 18.1 (and later) supports Java 9. As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later.

* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
* ELASTICSEARCH_JAVA_OPTS

TeamForge provision fails on sites that use these options post upgrade to TeamForge 18.1.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

<!-- ## LINUX_USERNAME_MODE_ENABLED {#LINUX_USERNAME_MODE_ENABLED}
The `LINUX_USERNAME_MODE_ENABLED` token, if set to `true`, overrides the default TeamForge user naming convention that bars user names with anything but an alphabet as the first character. This token is commented out (disabled) by default and is available in the `site-options.conf` file.

{% include important.html content="It is recommended to use this token on sites with CVS integration. Do not set the `LINUX_USERNAME_MODE_ENABLED` to `true` on sites without CVS integration. Instead, you must set the [RELAXED_USERNAME_MODE_ENABLED][siteoptiontokens.html#RELAXED_USERNAME_MODE_ENABLED] token to `true` in case your site has no CVS integration." %}

**Values**: true or false

**Default**: false

{% include warning.html content="While TeamForge can allow user names with anything but an alphabet as the first character, the same may not be true with all or some of the integrated applications you may have on your site. As a word of caution, consider the job at hand and understand the consequences before overriding TeamForge's default user naming convention." %}
{{site.data.alerts.hr_shaded}} -->

## LISTEN_BACKLOG
The `LISTEN_BACKLOG` token is used to specify the maximum length of the queue for the pending connections in the Apache server.

**Values**: Integer

**Default**: The default value is obtained from the system Kernel configuration.

`/sbin/sysctl -n -e net.ipv4.tcp_max_syn_backlog`
{{site.data.alerts.hr_shaded}}

## LOGIN_ATTEMPT_LOCK {#LOGIN_ATTEMPT_LOCK}
This option controls locking out the user account after "n" invalid login attempts.
* Set this to zero or a negative number to lock the user account when the user provides an incorrect password for the first time.
* Set this to a positive number, say "2", to allow the user two wrong password attempts. The user account would be locked at the "x+1" (here, third) attempt. 

When a user's account is locked, either an administrator must unlock it or the user can use the "Forgot Your Password?" link to reset the password.
 
You must set the `REQUIRE_PASSWORD_SECURITY` token to `true` in the `site-options.conf` file, for `LOGIN_ATTEMPT_LOCK` setting to take effect.
{{site.data.alerts.hr_shaded}}

## LISTEN_IP
In a distributed setup, you can use this `<host>:<service>:LISTEN_IP` token to control which IPs the services bind to so that you can make sure that services are not overexposed than necessary.

By default, services bind to the IP address corresponding to the `<host>:PUBLIC_FQDN` token. However, you can override this using the `<host>:<service>:LISTEN_IP` token.

A few use cases:
* In a distributed setup, you may want to bind a particular IP address of the TeamForge database server (PostgreSQL server) to the `ctfcore-database` service:
  ```shell
  server-01:ctfcore-database:LISTEN_IP = 1.2.3.4
  ````
* To bind the mail service to a particular IP:
  ```shell
  localhost:mail:LISTEN_IP = 1.2.3.4
  ````
* To make TeamForge listen to a specific IP of a particular server, say the SCM server:
  ```shell
  myscmserver:LISTEN_IP = 1.2.3.4
  ````
* To bind all your services to one IP address (typically in a single server setup):
  ```shell
  localhost:LISTEN_IP = 1.2.3.4
  ````
{% include note.html content="You cannot use more than one IP address with the `LISTEN_IP` token." %}
{{site.data.alerts.hr_shaded}}

## LOG_DIR {#LOG_DIR}
The `LOG_DIR` token specifies the path where TeamForge log files are written.

**Values**: Path specification

**Default**: `{__SITE_DIR__}/log`
{{site.data.alerts.hr_shaded}}

## LOG_QUERY_TIME_THRESHOLD {#LOG_QUERY_TIME_THRESHOLD}
The `LOG_QUERY_TIME_THRESHOLD` token enables you to log database requests at INFO level if they run longer than a given period.

By default, database requests are logged at DEBUG level. Configuring a value for `LOG_QUERY_TIME_THRESHOLD` causes requests that run for a period greater than that value to be logged at the INFO level in the `/opt/collabnet/teamfoge/log/apps/query.log` file.

Set the value to zero to log all database queries at INFO.

**Values**: Integer (milliseconds)

**Default**: 1000
{{site.data.alerts.hr_shaded}}

## LOGIN_ATTEMPT_LOCK
Use the `LOGIN_ATTEMPT_LOCK` token to set the permissible number of unsuccessful login attempts after which the user account is automatically locked.

**Values**: 1-3

Important: You can now selectively disable this feature even if you have set the `REQUIRE_PASSWORD_SECURITY` site options token to `true`. Set any negative value (such as '-1' or '-10000') in case you want to disable this feature altogether.

Note that with TeamForge 8.1 and earlier versions, setting `LOGIN_ATTEMPT_LOCK=-1` means the user account would be locked at the very first unsuccessful login attempt. This behavior has been removed in TeamForge 8.2 (and later).

**Default**: 3
{{site.data.alerts.hr_shaded}}

## LOGIN_CONFIG_XML_FILE
The `LOGIN_CONFIG_XML_FILE` token specifies the path to the LDAP configuration file.

**Values**: Path specification

**Default**: `{__DATA_DIR__}/etc/login-config.xml`
{{site.data.alerts.hr_shaded}}

## LOGROTATE_ARCHIVE_COUNT
Use the `LOGROTATE_ARCHIVE_COUNT` token to set the number of most recent logs to be preserved at any give point in time.

**Values**: Any positive integer.

**Default**: 
The default value is "7". Meaning, logs for the last 7 days are preserved at any given point in time. Logs older than 7 days are removed from the log archive folder.

{% include note.html content="This token replaces the `LOGROTATE_MAXAGE` token." %}
{{site.data.alerts.hr_shaded}}

## MAX_DOCUMENTS_DOWNLOAD_SIZE {#MAX_DOCUMENTS_DOWNLOAD_SIZE}
Specifies the maximum file size (in MB) for the total number of documents being downloaded. The value of this token can be an integer or a float value.

**Values**: Integer or Float

**Default**: 500
{{site.data.alerts.hr_shaded}}


## MAX_DOCUMENTS_DOWNLOAD_LIMIT {#MAX_DOCUMENTS_DOWNLOAD_LIMIT}
Specifies the maximum number of documents that can be downloaded.

**Values**: Integer 

**Default**: 1000
{{site.data.alerts.hr_shaded}}

## MAX_PASSWORD_LENGTH {#MAX_PASSWORD_LENGTH}
The `MAX_PASSWORD_LENGTH` token sets the longest password that the system allows when a user account is created.

**Values**: Integer (number of characters)

**Default**: 256
{{site.data.alerts.hr_shaded}}

## MAX_POSTS_PER_MINUTE {#MAX_POSTS_PER_MINUTE}
This token is used to control the number of posts per minute. By default, its value is `10`. 

**Values**: Integer

**Default**: 10

**Comments**: 
Increase the value of this token if you don't want your users to get blacklisted accidentally.
{{site.data.alerts.hr_shaded}}

## MAX_WWW_CLIENTS
The `MAX_WWW_CLIENTS` token specifies the maximum number of Tomcat request processing threads to be created by the HTTP connector.

**Values**: Integer

**Default**: 250

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## MIGRATION_LOG_DIR
The `MIGRATION_LOG_DIR` token specifies the path where information about the conversion of site data is written during an upgrade.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/runtime`
{{site.data.alerts.hr_shaded}}

## MINIMUM_PASSWORD_LENGTH {#MINIMUM_PASSWORD_LENGTH}
The `MINIMUM_PASSWORD_LENGTH` token sets the shortest password that the system allows when a user account is created.

**Values**: Integer (number of characters)

**Default**: 6
{{site.data.alerts.hr_shaded}}

## MINIMUM_USERNAME_LENGTH
The `MINIMUM_USERNAME_LENGTH` token sets the shortest username that the system allows when a user account is created.

**Values**: Integer (number of characters)

**Default**: 3
{{site.data.alerts.hr_shaded}}

## MIRROR DATABASE HOST
The `MIRROR_DATABASE_HOST` token is a TeamForge database token that specifies the host of the database. This token allows to extract the reporting data from the mirror TeamForge database through the Extract, Transform and Load (ETL) process.

**Values**: Alphanumeric string

**Default**: 
The `MIRROR_` token takes the value of `DATABASE_` token.

**Example**:
Enter `MIRROR_DATABASE_HOST=cu349.cloud.sp.collab.net` (server name)

Add this token to the `site-options.conf` only if you setup a mirror database.
{{site.data.alerts.hr_shaded}}

## MIRROR_DATABASE_NAME
The `MIRROR_DATABASE_NAME` token is a TeamForge database token that specifies the name of the TeamForge database. This token allows to extract the reporting data from the mirror TeamForge database through the Extract, Transform and Load (ETL) process.

**Values**: Alphanumeric string

**Default**: 
The `MIRROR_` token takes the value of `DATABASE_` token.

**Example**:
Enter `MIRROR_DATABASE_NAME=ctfdb`

Add this token to the `site-options.conf` only if you setup a mirror database.
{{site.data.alerts.hr_shaded}}

## MIRROR_DATABASE_PASSWORD
The `MIRROR_DATABASE_PASSWORD` token is a TeamForge database token that specifies the password of the database. This token allows to extract the reporting data from the mirror TeamForge database through the Extract, Transform and Load (ETL) process.

**Values**: Alphanumeric string

**Default**: 
The `MIRROR_` token takes the value of `DATABASE_` token.

**Example**:
Enter `MIRROR_DATABASE_PASSWORD=ctfpwd`

Add this token to the `site-options.conf` only if you setup a mirror database.
{{site.data.alerts.hr_shaded}}

## MIRROR_DATABASE_PORT
The `MIRROR_DATABASE_PORT` token is a TeamForge database token that specifies the port number of the database. This token allows to extract the reporting data from the mirror TeamForge database through the Extract, Transform and Load (ETL) process.

**Values**: Port specification

**Default**:
The `MIRROR_` token takes the value of the `DATABASE_` token.

**Example**:
Enter `MIRROR_DATABASE_PORT=5432`.

Add this token to the `site-options.conf` only if you setup a mirror database.
{{site.data.alerts.hr_shaded}}

## MIRROR_DATABASE_USERNAME
The `MIRROR_DATABASE_USERNAME` token is a TeamForge database token that specifies the database user's name. This token allows to extract the reporting data from the mirror TeamForge database through the Extract, Transform and Load (ETL) process.

**Values**: Alphanumeric string

**Default**: 
The `MIRROR_` token takes the value of the `DATABASE_` token.

**Example**:
Enter `MIRROR_DATABASE_USERNAME=ctfuser`.

Add this token to the `site-options.conf` only if you setup a mirror database.
{{site.data.alerts.hr_shaded}}

## NEXUS_TYPE {#NEXUS_TYPE}
Enables baseline service to select either Nexus 2 or Nexus 3, if both are installed. 

**Values**: nexus2 or nexus3

**Default**:
{{site.data.alerts.hr_shaded}}

## NEXUS2_DEFAULT_PATH {#NEXUS2_DEFAULT_PATH}

Specifies the default REST API path of Nexus 2 server.

**Values**: default path of nexus server

**Default**: `/service/local/repositories`

{{site.data.alerts.hr_shaded}}

## NEXUS3_SEARCH_PATH {#NEXUS3_SEARCH_PATH}

Specifies the REST API path from which the details of Nexus 3 Assets are obtained.

**Values**: search path for next assets

**Default**: `/service/rest/v1/search`

{{site.data.alerts.hr_shaded}}

## NEXUS3_REPOSITORIES_PATH {#NEXUS3_REPOSITORIES_PATH}

Specifies the Nexus 3 server path from which the list of all available repositories is obtained.

**Values**: nexus repositories path

**Default**: `/service/rest/v1/repositories`

{{site.data.alerts.hr_shaded}}

## NEXUS3_SCRIPT_PATH {#NEXUS3_SCRIPT_PATH}

Specifies the path where the Nexus 3 scripts are created, executed, and deleted.

**Values**: nexus script path

**Default**: `/service/rest/v1/script`

{{site.data.alerts.hr_shaded}}

## NEXUS3_COMPONENTS_PATH {#NEXUS3_COMPONENTS_PATH}

Specifies the path from which the details of a specific Nexus 3 repository are obtained.

**Values**: nexus components path

**Default**: `/service/rest/v1/components`

{{site.data.alerts.hr_shaded}}

## NOTIFY_SITE_ADMINS_FOR_SITE_ACTIVITIES
The `NOTIFY_SITE_ADMINS_FOR_SITE_ACTIVITIES` token ensures that the activities at the site level are intimated to the site administrators through email notifications.

The site administrator can receive notifications on the following operations:
* User creation
* Project creation
* Blacklisted users
* SCM operations

**Values**: true or false

**Default**: true

This token was added in TeamForge 8.0.
{{site.data.alerts.hr_shaded}}

## OBFUSCATION_ENABLED
The `OBFUSCATION_ENABLED` token is used to run the TeamForge application in the obfuscation mode for security purpose. Password obfuscation is enabled by default. As a result, all password-related tokens are encrypted in all the TeamForge configuration files.

**Values**: true or false

**Default**: true

**Comments**:
When the TeamForge application is running in the obfuscation mode, the database login credentials, shared secrets etc., are encrypted and stored in the TeamForge configuration files for security reasons.
{{site.data.alerts.hr_shaded}}

## OBFUSCATION_KEY
The `OBFUSCATION_KEY` token is used by the TeamForge obfuscation component as an input to the obfuscation algorithm for encryption and decryption purposes.

**Values**: AlphaNumeric (length greater than or equal to 8 bytes)

**Default**: `XSJt43wN`
{{site.data.alerts.hr_shaded}}

## ONLY_SITE_ADMIN_CAN_EDIT_SINGLE_SIGN_ON {#sasinglesignon}
This site-options token, if set to `true`, ensures that only site administrators can turn on single sign on (SSO) for linked applications (including Build & Test). Set this token to `false` to have both site and project administrators turn SSO `on` and `off`.

**Values**: Either `true` or `false`.

**Default**: true

This token was added in TeamForge 7.2.
{{site.data.alerts.hr_shaded}}

## ORGANIZATION_EDITABLE
The `ORGANIZATION_EDITABLE` token allows or prevents editing the organization value of a user account.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## PASSWORD_CONTROL_EFFECTIVE_DATE {#PASSWORD_CONTROL_EFFECTIVE_DATE}
The `PASSWORD_CONTROL_EFFECTIVE_DATE` token is used to set the date from which the password security feature takes effect.

**Values**: Date (mm/dd/yyyy)

**Comments**:
The [REQUIRE_PASSWORD_SECURITY][siteoptiontokens.html#REQUIRE_PASSWORD_SECURITY] is the master token that enables the password security feature.

{% include important.html content="Setting the `PASSWORD_CONTROL_EFFECTIVE_DATE` token with a date is mandatory if `REQUIRE_PASSWORD_SECURITY` is set to `true`." %}

**Example 1**:

Consider a site with 130 users on which the password control kit (PCK) was not active. Of the 130 users, assume that:
* 100 users did not change password in last 100 days.
* 20 users did not change password in last 85 days.
* 10 users did not change password in last 75 days.

Assume that the following tokens are set on 01/01/2014 (current date):
```conf
REQUIRE_PASSWORD_SECURITY=true
PASSWORD_WARNING_PERIOD=20
PASSWORD_EXPIRY_PERIOD=90
PASSWORD_DISABLE_PERIOD=30
PASSWORD_DELETE_PERIOD=60
````

PCK runs on 01/01/2014 and if you have `PASSWORD_CONTROL_EFFECTIVE_DATE=01/10/2014` (set to a future date):
* 100 users with no password change for the past 100 days would get a warning message that their passwords will expire in 10 days.
* 20 users with no password change for the past 85 days would get a warning message that their passwords will expire in 10 days.
* 10 users with no password change for the past 75 days would get a warning message that their passwords will expire in 15 days.

**Example 2**:
Consider the following scenario in which:
* Current date = 01/01/2014
* PASSWORD_CONTROL_EFFECTIVE_DATE=01/01/2013

In this scenario, the password control effective date is set to a date in the past. As a result, password control takes immediate effect and the PCK starts disabling, deleting or expiring user accounts right away.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PASSWORD_DELETE_PERIOD
The `PASSWORD_DELETE_PERIOD` token specifies the time frame within which a disabled user account is automatically deleted.

**Values**: Integer (number of days)

**Default**: 60

{% include note.html content="The PASSWORD_DELETE_PERIOD can be disabled by setting the value to zero." %}

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PASSWORD_DISABLE_PERIOD
The `PASSWORD_DISABLE_PERIOD` token specifies the time frame within which a user (soft-expired) is turned into a disabled user.

**Values**: Integer (number of days)

**Default**: 30

**Comments**: 
A value of zero will disable this feature.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PASSWORD_EXPIRY_PERIOD
The `PASSWORD_EXPIRY_PERIOD` token specifies the number of days after which the users' password expires.

**Values**: Integer (number of days)

**Default**: 90

{% include note.html content="You cannot disable the password expiry feature by setting this token to `0`." %}

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PASSWORD_REQUIRES_MIXED_CASE {#PASSWORD_REQUIRES_MIXED_CASE}
The `PASSWORD_REQUIRES_MIXED_CASE` token specifies that the user password must contain mixed case letters.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## PASSWORD_REQUIRES_NON_ALPHANUM {#PASSWORD_REQUIRES_NON_ALPHANUM}
The `PASSWORD_REQUIRES_NON_ALPHANUM` token specifies that the user password must contain a non-alphanumeric character.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## PASSWORD_REQUIRES_NUMBER {#PASSWORD_REQUIRES_NUMBER}
The `PASSWORD_REQUIRES_NUMBER` token specifies that the user password must atleast contain one number.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## PASSWORD_WARNING_PERIOD
Set this token to alert users via emails about impending password expiration on a daily basis. Email alert starts "N" days before password expiration due date, where `PASSWORD_WARNING_PERIOD=N`, and ends only when the password is changed by the user.

**Values**: Positive integer (number of days).

**Default**: 14

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PASSWORD_HISTORY_AGE {#PASSWORD_HISTORY_AGE}
The maximum allowed value of `PASSWORD_HISTORY_AGE` token is `10`. This option disallows the previous "n" passwords, while setting a password. However, if this option is set to zero, a negative number or it is left empty, the user can use any previous password. The password being set must satisfy the existing password policy each time.

You must set the `REQUIRE_PASSWORD_SECURITY` token to `true` in the `site-options.conf` file, for `PASSWORD_HISTORY_AGE` security setting to take effect.
{{site.data.alerts.hr_shaded}}

## PHOENIX_JAVA_OPTS
The `PHOENIX_JAVA_OPTS` token specifies the memory settings for the Java virtual machine that supports the site's ability to send and receive email and to index data for search.

**Values**: Java specifications

**Default**: 

```shell
-Xms256m -Xmx256m -server -XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp -verbose:gc -XX:+ PrintGCTimeStamps -XX:+PrintGCDetails -Dsun.rmi.dgc.client.gcInterval=600000 -Dsun.rmi.dgc.server.gcInterval=600000 -Dsf .luceneOptimizeEvery=100000 -Djava.security.egd=file:/dev/urandom
````
{% include note.html content="If you've enabled PHOENIX_JAVA_OPTS token in `site-options.conf` file and have added any parameter, you must provide the required JVM heap size as the default heap size is not taken into account." %}

**Comments**:
<!-- (See: https://forge.collab.net/sf/go/artf300770) -->TeamForge 18.1 (and later) supports Java 9. As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later.

* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
* ELASTICSEARCH_JAVA_OPTS
   
TeamForge provision fails on sites that use these options post upgrade to TeamForge 18.1.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_COMMIT_DELAY
The `PGSQL_COMMIT_DELAY` token specifies the time delay between writing a commit record to the write ahead log (WAL) buffer and flushing the buffer out to disk.

**Values**: Integer (in microseconds)

**Default**: 250

**Comments**:
Together with the `PGSQL_COMMIT_SIBLINGS` token, this token allows a group of otherwise unrelated transactions to be flushed to disk at the same time, with possible significant performance gain.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_COMMIT_SIBLINGS
The `PGSQL_COMMIT_SIBLINGS` token sets the minimum number of concurrent open transactions to require before performing the delay specified by the `PGSQL_COMMIT_DELAY` option.

**Values**: Integer

**Default**: 10

**Comments**:
Together with the `PGSQL_COMMIT_DELAY` token, this token allows a group of otherwise unrelated transactions to be flushed to disk at the same time, with possible significant performance gain.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_EFFECTIVE_CACHE_SIZE
The `PGSQL_EFFECTIVE_CACHE_SIZE` token specifies the size of the OS data cache that is available to PostgreSQL. PostgreSQL can use that data to select the optimal way to execute requests.

**Comments**: 
The right value for this token depends in part on the available RAM on the server where your site is running. Set this value at the highest amount of RAM that you expect to be always available to PostgreSQL.

See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for values recommended by CollabNet.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_FSYNC {#PGSQL_FSYNC}

This token turns forced synchronization `on` or `off`. By default, the token is turned `on`. Turn this `off` at your own risk, as it can cause unrecoverable data corruption.

**Values**: on or off

**Default**: on

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_LOG_DIR
The `PGSQL_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's PostgreSQL database is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/pgsql`
{{site.data.alerts.hr_shaded}}

## PGSQL_LOG_MIN_DURATION {#pgsqllogminduration}
<!-- Artifact artf397136 : Document changes in adding new token in site-options -->
The `PGSQL_LOG_MIN_DURATION` token specifies the maximum number of seconds after which queries are logged as long running queries to the log file.

By default, this token is set to 10s. 

After setting up this token, which is by default disabled, you may either run the `teamforge provision` command to do a complete TeamForge provision or simply run the `teamforge reload` command to stop, deploy and restart the PostgreSQL database alone.

The default value, which was `-1` earlier, has been changed to 10 seconds (10s) in TeamForge 20.1. Setting this token to `0` or a negative value can adversely impact the TeamForge application's performance. 


**Values**: \<integer\>s

**Default**: `10s`
{{site.data.alerts.hr_shaded}}

## PGSQL_MAINTENANCE_WORK_MEM
The `PGSQL_MAINTENANCE_WORK_MEM` token specifies the maximum amount of memory to be used in maintenance operations such as VACUUM.

**Comments**: 
See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for values recommended by CollabNet.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_MAX_CONNECTIONS
The `PGSQL_MAX_CONNECTIONS` token determines the number of concurrent connections available to the database server.

**Values**: Integer

**Default**: 135
{{site.data.alerts.hr_shaded}}

## PGSQL_MAX_FSM_PAGES
The `PGSQL_MAX_FSM_PAGES` token tells the vacuum process how many pages to look for in the shared free-space map.

**Values**: Integer

**Default**: 500000

**Comments**: 
Each FSM page uses 6 bytes of RAM for administrative overhead, so increasing FSM substantially on systems low on RAM may be counter-productive.
{{site.data.alerts.hr_shaded}}

## PGSQL_MAX_FSM_RELATIONS
The `PGSQL_MAX_FSM_RELATIONS` token specifies how many relations (tables) will be tracked in the free space map.

**Default**: 500
{{site.data.alerts.hr_shaded}}

## PGSQL_MAX_STACK_DEPTH
The `PGSQL_MAX_STACK_DEPTH` token specifies the maximum safe depth of the server's execution stack.

**Values**: Integer

**Default**: 5120
{{site.data.alerts.hr_shaded}}

## PGSQL_SHARED_BUFFERS
The `PGSQL_SHARED_BUFFERS` token defines a block of memory that PostgreSQL will use to hold requests that are awaiting attention from the kernel buffer and CPU.

**Comments**: 
The right value for this token depends in part on the available RAM on the server where your site is running.

See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for values recommended by CollabNet.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PGSQL_STATEMENT_TIMEOUT
The `PGSQL_STATEMENT_TIMEOUT` token is set to prevent the Postgres queries from running for a long period of time.

**Values**: Integer (Milliseconds)

**Default**: 600000 (Milliseconds)

**Comments**: 
An error message is displayed for every timeout in the `postgres.log` file and the log message with the exid id is logged in the `vamessages.log` and `server.log` files.
{{site.data.alerts.hr_shaded}}

## PGSQL_VACUUM_COST_DELAY
The `PGSQL_VACUUM_COST_DELAY` token controls the length of time that an I/O process will sleep when the limit set by `vacuum_cost_limit` has been exceeded.

**Values**: Integer (milliseconds)

**Default**: 50
{{site.data.alerts.hr_shaded}}

## PGSQL_WAL_BUFFERS
The `PGSQL_WAL_BUFFERS` token specifies the number of buffers available for the Write Ahead Log.

**Comments**: 
If your database has many write transactions, setting this value bit higher than default may result better usage of disk space.

See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for values recommended by CollabNet.
{{site.data.alerts.hr_shaded}}

## PGSQL_WORK_MEM
The `PGSQL_WORK_MEM` token specifies the amount of memory to be used by internal sort operations and hash tables before switching to temporary disk files. .

**Comments**:
The right value for this token depends in part on the available RAM on the server where your site is running.

See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for values recommended by CollabNet.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## PLANNING_BOARD_SWIM_LANE_LIMIT
By default, not more than 250 cards are shown in a planning board swimlane. However, as a site administrator, you can increase or decrease the number of cards shown in the planning board swimlanes by configuring the site options token, `PLANNING_BOARD_SWIM_LANE_LIMIT`.

**Values**: A positive number.

**Default**: 250

**Comments**: 
When you select a planning folder in one of the swimlanes and if X is greater than N, (where X = number of artifacts in the selected planning folder and N = `PLANNING_BOARD_SWIM_LANE_LIMIT`), the message, Swimlanes in the Board View is currently configured to show N artifacts only, appears at the bottom of the swimlane.
{{site.data.alerts.hr_shaded}}

## PLANNING_FOLDER_DESC_EDITOR
The `PLANNING_FOLDER_DESC_EDITOR` token allows you to choose the type of text that can be used in the planning folder description using the editor tool.

**Values**: Plain Text

**Default**: Plain Text
{{site.data.alerts.hr_shaded}}

## POSTINSTALL_LOG_LEVEL {#POSTINSTALL_LOG_LEVEL}

Specifies the log level for `baseline-post-install` service. The default log level is INFO.

**Values**: INFO, WARN/WARNING, ERROR, PANIC, DEBUG, FATAL 

**Default**: INFO 
{{site.data.alerts.hr_shaded}}

## POSTINSTALL_LOG_FILE {#POSTINSTALL_LOG_FILE}

Specifies the log file location of baseline post install service.

**Values**: File path

{{site.data.alerts.hr_shaded}}

## RELAXED_USERNAME_MODE_ENABLED {#RELAXED_USERNAME_MODE_ENABLED}
The `RELAXED_USERNAME_MODE_ENABLED` token, if set to true, overrides the default TeamForge user naming convention that bars user names with anything but an alphabet as the first character. <!-- It is recommended to use this token on sites without CVS integration. -->

<!-- {% include warning.html content="Do not set the `RELAXED_USERNAME_MODE_ENABLED` to `true` on sites with CVS integration. Instead, you must set the [LINUX_USERNAME_MODE_ENABLED][siteoptiontokens.html#LINUX_USERNAME_MODE_ENABLED] token to `true` in case your site has CVS integration." %} -->

**Values**: true or false

**Default**: false

**Comments**:
This token is commented out (disabled) by default and is available in the `site-options.conf` file.

{% include warning.html content="While TeamForge can allow user names with anything but an alphabet as the first character, the same may not be true with all or some of the integrated applications you may have on your site. As a word of caution, consider the job at hand and understand the consequences before overriding TeamForge's default user naming convention." %}
{{site.data.alerts.hr_shaded}}

## REPORTS_DATABASE_NAME
The `REPORTS_DATABASE_NAME` token specifies the name of the site's reporting database, also known as the datamart.

**Values**: Alphanumeric string

**Default**: teamforge_datamart

**Comments**: 
It is OK for this token to have the same value as `DATABASE_NAME`, because they are running in separate pgsql processes.
{{site.data.alerts.hr_shaded}}

## REPORTS_DATABASE_PASSWORD
The `REPORTS_DATABASE_PASSWORD` token is the password for the Linux user that is authorized to read from and write to the site's reporting database.

**Values**: Alphanumeric string

**Default**: $auto$

**Comments**: 
It is OK for this token to have the same value as `DATABASE_PASSWWORD`, because they are running in separate PostgreSQL processes.
{{site.data.alerts.hr_shaded}}

## REPORTS_DATABASE_USERNAME
The `REPORTS_DATABASE_USERNAME` token specifies the Linux user that is authorized to read from and write to the site's reporting database.

**Values**: Alphanumeric string

**Default**: teamforge_datamart

**Comments**: 
For some advanced operations, you may need to log into the database as the database user. However, under normal conditions only the TeamForge site process itself needs to access the database.

It is OK for this token to have the same value as `DATABASE_USERNAME`, because they are running in separate PostgreSQL processes.
{{site.data.alerts.hr_shaded}}

## REPORTS_ENABLE_REPORT_GENERATION
The `REPORTS_ENABLE_REPORT_GENERATION` token is used to enable or disable the **Reports** tab in the UI.

**Values**: true or false

**Default**: true or false

**Comments**
Datamart is enabled by adding the 'datamart' service to the HOST_\<hostname>token. The service is disabled if datamart is not added. The default value of the REPORTS_ENABLE_REPORT_GENERATION token is based on this service.
{{site.data.alerts.hr_shaded}}

## REQUIRE_PASSWORD_SECURITY {#REQUIRE_PASSWORD_SECURITY}
The `REQUIRE_PASSWORD_SECURITY` token, if set to true, enforces password security policy for the site.

**Values**: true or false

**Default**: true

**Comments**:
This token can be useful when an organization's security policy prohibits users from entering passwords without any restrictions. You can also set the `PASSWORD_CONTROL_EFFECTIVE_DATE` token with a date from which the password policy would be enforced. For more information, see [PASSWORD_CONTROL_EFFECTIVE_DATE][siteoptiontokens.html#PASSWORD_CONTROL_EFFECTIVE_DATE].
{{site.data.alerts.hr_shaded}}

## REQUIRE_RANDOM_ADMIN_PASSWORD
The `REQUIRE_RANDOM_ADMIN_PASSWORD` token restricts users from setting a random admin password.

**Values**: true or false.

**Default**: True (SaaS), false (BTF)

**Comments**:
This token, when set to `true`, checks for a valid mail id in the `ADMIN_EMAIL` token.
{{site.data.alerts.hr_shaded}}

## REQUIRE_USER_PASSWORD_CHANGE {#REQUIRE_USER_PASSWORD_CHANGE}
The `REQUIRE_USER_PASSWORD_CHANGE` token determines if the user password needs to be changed during the first login instance.

**Values**: true or false.

**Default**: true

**Comments**:
Setting this token to `true` makes the new system force users to change password during first login and false otherwise.
{{site.data.alerts.hr_shaded}}

## RUNTIME_LOG_DIR
The `RUNTIME_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's runtime environment is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/runtime`
{{site.data.alerts.hr_shaded}}

## SAFE_DOWNLOAD_MODE {#SAFE_DOWNLOAD_MODE}

Use this token to enforce downloading and saving of documents, attachments and files locally using the "Save" dialog box instead of inline views.

**Values**: true, false, none, all, html

You can set this token to "none" "all" or "html" that will force download of nothing, everything, or just html documents respectively.

**Default**: none
{{site.data.alerts.hr_shaded}}

## SCM_DEFAULT_SHARED_SECRET
The `SCM_DEFAULT_SHARED_SECRET` token allows SCM Integrations to securely communicate with the TeamForge Application Server.

**Values**: 
* Alpha-numeric
* Special characters like '~!@#$%^&*'
* 16-24 byte length

**Default**: 
The default value is automatically generated during runtime.
{{site.data.alerts.hr_shaded}}

## SCM_SOAP_TIMEOUT
The `SCM_SOAP_TIMEOUT` token is used to specify the connection timeout of the SCM soap requests between the APP and SCM servers.

**Values**: Integer (Milliseconds)

**Default**: 300000
{{site.data.alerts.hr_shaded}}

## SCM_USER_ENCRYPTED_PASSWORD {#SCM_USER_ENCRYPTED_PASSWORD}
The `SCM_USER_ENCRYPTED_PASSWORD` token is used to store the encrypted scmviewer password.

**Values**: 
* Alpha-numeric
* Special characters like '~!@#$%^&*'

**Default**: 
The default value will be in the encrypted format. See [password_util.sh][passwordutil] for more information.
{{site.data.alerts.hr_shaded}}

## SEARCH_LOG_DIR
The `SEARCH_LOG_DIR` token specifies the path where information about the activity of the TeamForge site's Lucene search component is written.

**Values**: Path specification

**Default**: `{__LOG_DIR__}/james`
{{site.data.alerts.hr_shaded}}

## SEARCH_MAX_FILE_SIZE
The `SEARCH_MAX_FILE_SIZE` token sets an upper limit to the size of files that are indexed for search.

**Values**: Integer (bytes)

**Default**: 10M

**Comments**: 
A value of zero or less specifies that there is no limit, which is the same as the default behavior without the token.
{{site.data.alerts.hr_shaded}}

## SEARCH_SUPPRESS_ARCHIVE_SUB_DOCS
The `SEARCH_SUPPRESS_ARCHIVE_SUB_DOCS` token prevents archive files from being indexed for search.

Archive files include `zip`, `gzip`, `tar`, and similar file types. They also include document files that are stored in archive format, such as `docx` files from Microsoft Word 2007.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## SECURE_REDIRECTS {#SECURE_REDIRECTS}

This token which is _false_ by default, if set to _true_, redirects your CTF instance to the allowed hostname(s) as specified in the `site-options.conf` token [ALLOWED_HOSTS][siteoptiontokens.html#ALLOWED_HOSTS].

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## SERVICE_MONITOR_RETRIES {#SERVICE_MONITOR_RETRIES}

Number of retries of monit before restarting the service. Default value of this token is `0`.

**Values**: Integer

**Default**: 0

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## SESSION_COOKIES_ONLY
the `SESSION_COOKIES_ONLY` token restricts the persistence of all cookies to the user's current session.

If `SESSION_COOKIES_ONLY=true`, then all cookies created during the user session expire automatically when the user closes their browser. If it is `false`, the cookie expires according to the system logic for that particular cookie.

**Values**: true or false

**Default**: false

**Comments**: 
This token can be useful when an organization's security policy prohibits cookies that persist across user sessions.
{{site.data.alerts.hr_shaded}}

## SESSION_TIMEOUT
Use this token to set the user session timeout duration for newly created Application Server/Integration Server sessions.

**Values**: A positive value in the range of 1-1440.

**Default**: 
The default value of the `SESSION_TIMEOUT` token is 30 minutes (for security reasons). You may change this to any value in the range of 1-1440 (minutes). However, you must create runtime for the changes to take effect.

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## SOAP_ANONYMOUS_SHARED_SECRET
The `SOAP_ANONYMOUS_SHARED_SECRET` token allows users to have an anonymous login to the TeamForge site through SOAP.

**Values**: String (possibly encrypted)

**Default**: None

**Comments**: 
The token must be configured to a non-empty value if users need to have an anonymous login to the site through SOAP. A value must be provided if site-wide reporting is enabled.
{{site.data.alerts.hr_shaded}}

## SOAP_ARTIFACT_LIST_LIMIT
The `SOAP_ARTIFACT_LIST_LIMIT` token is used to limit the number of artifacts returned via SOAP calls.

**Values**: Integer

**Default**: -1

This means that the artifact list retrieved via SOAP is unlimited.

**Comments**: 
In TeamForge releases earlier than 6.1.1, SOAP calls returned everything that was asked for, and that is the default behavior in TeamForge 6.1.1 as well. However, sites with performance and stability issues (OutOfMemory errors) in returning a large number of artifacts can now limit the number using this token. Changing this value requires a recreate-runtime and thus a site restart.

{% include important.html content="Increasing the number of artifacts beyond the optimal 20,000 - 25,000 range might cause a heap dump." %}
{{site.data.alerts.hr_shaded}}

## SSL_CERT_FILE {#SSL_CERT_FILE}
The `SSL_CERT_FILE` specifies the path where the TeamForge site's Secure Socket Layer certificate is stored.

**Values**: Path specification

**Default**: None
{{site.data.alerts.hr_shaded}}

## SSL_CHAIN_FILE {#SSL_CHAIN_FILE}
The `SSL_CHAIN_FILE` token specifies the path where the TeamForge site's SSL certficate chain file is stored.

**Values**: Path specification

**Default**: None
{{site.data.alerts.hr_shaded}}

## SSL_CIPHER_SUITE
The `SSL_CIPHER_SUITE` token disables some of the less secure methods.

**Values**: SSLCipherSuite method

**Default**: 

```shell
ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-DSS-AES128-GCM-SHA256:kEDH+AESGCM:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA:ECDHE-ECDSA-AES128-SHA:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA:ECDHE-ECDSA-AES256-SHA:DHE-RSA-AES128-SHA256:DHE-RSA-AES128-SHA:DHE-DSS-AES128-SHA256:DHE-RSA-AES256-SHA256:DHE-DSS-AES256-SHA:DHE-RSA-AES256-SHA:AES128-GCM-SHA256:AES256-GCM-SHA384:AES128-SHA256:AES256-SHA256:AES128-SHA:AES256-SHA:AES:CAMELLIA:DES-CBC3-SHA:!aNULL:!eNULL:!EXPORT:!DES:!RC4:!MD5:!PSK:!aECDH:!EDH-DSS-DES-CBC3-SHA:!EDH-RSA-DES-CBC3-SHA:!KRB5-DES-CBC3-SHA
````
{{site.data.alerts.hr_shaded}}

## SSL_PROTOCOL
The `SSL_PROTOCOL` token disables some of the less secure methods.

**Values**: SSLProtocol method

**Default**: all -SSLv3 -SSLv2
{{site.data.alerts.hr_shaded}}

## SSL_KEY_FILE {#SSL_KEY_FILE}
The `SSL_KEY_FILE` specifies the path where the TeamForge site's RSA private key is stored when Secure Socket Layer encryption is in effect.

**Values**: Path specification

**Default**: None
{{site.data.alerts.hr_shaded}}

## SUBVERSION_BRANDING_URI
The `SUBVERSION_BRANDING_URI` token specifies the path component of the data repository URL.

**Values**: BDB or FSFS

**Default**: BDB
{{site.data.alerts.hr_shaded}}

## SVN_AUTHNZ_TIMEOUT
The `SVN_AUTHNZ_TIMEOUT` token allows you to set the timeout value (in seconds) for the mod_authnz_ctf module.

**Values**: Timeout value in number of seconds.

**Default**: 60
{{site.data.alerts.hr_shaded}}

## SYSTEM_EMAIL
The `SYSTEM_EMAIL` token specifies a valid email address for the system administrator responsible for this site.

* System administrators can use this email address to set up outage alerts and other notifications.
* The mail account specified must be hosted on a separate server from the TeamForge site server.
* The SYSTEM_EMAIL, ADMIN_EMAIL, and JAMES_POSTMASTER_EMAIL tokens can specify the same address.

**Values**: Email address specification

**Default**: `root@{__APPLICATION_HOST__}`

{% include important.html content="In TeamForge 6.x, the sender name and address for system-generated emails is taken from the value of the `SYSTEM_EMAIL` token. Therefore, changing the admin user's full name or email address does not affect the sender details of system-generated emails. This is different from TeamForge 5.x, in which the sender name and address for system-generated emails is derived from the admin user's full name and email address." %}
{{site.data.alerts.hr_shaded}}

## USE_BROWSER_CACHE_PASSWORD
The `USE_BROWSER_CACHE_PASSWORD` token restricts the storage of password in the browser when you login to the site.

**Values**: true/false

**Default**: true
{{site.data.alerts.hr_shaded}}

## USE_EXTERNAL_USER_AUTHENTICATION {#USE_EXTERNAL_USER_AUTHENTICATION}
The `USE_EXTERNAL_USER_AUTHENTICATION` token specifies whether users can be authenticated through a separate system, such as OpenLDAP.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## USE_STATIC_SENDER_EMAIL
<!-- https://forge.collab.net/sf/go/artf269719 -->
The `USE_STATIC_SENDER_EMAIL` token, if set to `true`, assigns the `Return-Path` parameter in the TeamForge notification email header with a `noreply@<user's email domain>` email ID. This prevents Out of Office replies from being posted to artifacts and discussion forums.

On the other hand, the `USE_STATIC_SENDER_EMAIL` token, if set to `false`, assigns the `Return-Path` parameter in the TeamForge notification email header with the email ID of the user (for example, tom@forge.collab.net) whose action triggers the notification email. In this case, Out of Office replies are posted to artifacts and discussion forums. If the user is a Site Administrator, the `Return-Path` parameter in the TeamForge notification email header is assigned with the email ID `root@<TeamForge domain name>`.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## USER_ACCOUNT_RESTRICTED
The `USER_ACCOUNT_RESTRICTED` token determines whether newly created users are "restricted" or "unrestricted" users by default.

* Restricted users can access only public projects and projects of which they are members.
* Unrestricted users can access all projects except private projects of which they are not members.

**Values**: true or false

**Default**: true
{{site.data.alerts.hr_shaded}}

## USER_MONITORING_REMOVE_ENABLED {#USER_MONITORING_REMOVE_ENABLED}
Set the `USER_MONITORING_REMOVE_ENABLED` token to `true`, if you want to enable the feature that lets you remove one or more users from monitoring selected TeamForge objects.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## USER_NEED_PERMISSION_TO_VIEW_FULL_USER_DETAILS
The `USER_NEED_PERMISSION_TO_VIEW_FULL_USER_DETAILS` token restricts users from viewing other users' organization information.

**Values**: true or false

**Default**: false
{{site.data.alerts.hr_shaded}}

## USERS_WITH_NO_EXPIRY_PASSWORD
The `USERS_WITH_NO_EXPIRY_PASSWORD` token specifies the users for whom there is no expiry of password. The token is enabled by default.

**Values**: Specify the usernames (for the user accounts) for which there is no expiry of password.

**Default**: USERS_WITH_NO_EXPIRY_PASSWORD=admin,nobody,system,scmviewer,scmadmin
{{site.data.alerts.hr_shaded}}

## USER_RESOURCE_CACHE_MAX_SIZE_LIMIT {#USER_RESOURCE_CACHE_MAX_SIZE_LIMIT}

Specifies the maximum size limit for user resource cache.

**Values**: Integer

**Default**: 16000

{% include installupgrade/teamforgereload.html %}
{{site.data.alerts.hr_shaded}}

## USER_SYNC_CRON_EXP {#USER_SYNC_CRON_EXP}
Specifies the CRON expression to synchronize user information for every N minute(s) between baseline and TeamForge databases. 

**Values**: 1, 2, .... N (minutes)

**Default**: 1 minute
{{site.data.alerts.hr_shaded}}

## Using Multi-line Blocks for Site Options
The multi-line block configuration is generally used by old SFEE sites. To define a `site-options.conf` token with a multi-line block value, you need to follow a certain syntax.

* Declare the token name with the value `START_MULTILINE_BLOCK`. Syntax: `<TOKEN_NAME>=START_MULTILINE_BLOCK`
* Specify the multi-line values beneath the token.
* Complete the multi-line block with `END_MULTILINE_BLOCK` after all the multi-line values are specified. Syntax: `END_MULTILINE_BLOCK`

**Example**:

```shell
SOURCEFORGE_CONFIGURATION_PROPERTIES_APPEND=START_MULTILINE_BLOCK
email.suppress.project_member_added=true
email.suppress.scm_user_password_synchronized=true
END_MULTILINE_BLOCK
````
{{site.data.alerts.hr_shaded}}

## WEBR_ADMIN_USER {#WEBR_ADMIN_USER}

Specifies the user name of [TeamForge Webhooks-based Event Broker][webhooks-event-broker] Administrator.

**Values**: webradmin, webradministrator, ....

{{site.data.alerts.hr_shaded}}

## WEBR_ADMIN_PASSWORD {#WEBR_ADMIN_PASSWORD}

Specifies the password of [TeamForge Webhooks-based Event Broker][webhooks-event-broker] Administrator.

**Value**: abc, abc123, ....

{{site.data.alerts.hr_shaded}}

## WEBR_HTTP_BINDNAME {#WEBR_HTTP_BINDNAME}
<!-- Artifact artf394921 : Doc update : two new webr site options tokens -->
WEBR is, by default, bound to port 3000 and https. However, you can bind the WEBR service to http and to any other port of choice. Use the WEBR_HTTP_BINDNAME token to bind WEBR to any http port of choice. 

Here's an example of how to bind WEBR to port 3009.

```shell
WEBR_HTTP_BINDNAME=:3009
WEBR_HTTP_BINDNAME=localhost:3009
````
{{site.data.alerts.hr_shaded}}

## WEBR_INIT_JSFILE {#WEBR_INIT_JSFILE}
<!-- https://forge.collab.net/sf/go/artf394874#3 -->
Use this token to load an initial Javascript (JS) file to the WEBR's native JS virtual machine. The initial JS file configured via this token is executed first before the subscription script. 

The use case is to load a script to the JS VM that any script can have access to. For example, you can load a script that has a few variable definitions and make the variables commonly available to all other scripts.

Here's an example. 

```shell
WEBR_INIT_JSFILE=./initialJSfile.js
````
**An Illustration**

1. Create an `init.js` file in current directory with the following content:
   ```js
   var custname = "umakanthan";
   var othername = $inmessage.Name;
   ````
2. Add the WEBR_INIT_JSFILE token to the `site-options.conf` file as:
   ```shel
   WEBR_INIT_JSFILE=./init.js
   ````
3. Create a subscription with the following subscription script:
   ```shell
   $outmessage = 'My name is Uma,'+ custname + ' ' + othername;
   ````
4. Send a message to the Sync event with following payload:
   ```json
   {
   	"Name": "uma111"
   }
   ````

   Here's the response you get:

   ```shell
   My name is Uma, umakanthan uma111
   ````

   {% include note.html content="The init code is run just after creating the $inmessage and other internal variables. So these should be accessible inside the init script." %}

{{site.data.alerts.hr_shaded}}   


{% include links.html %}