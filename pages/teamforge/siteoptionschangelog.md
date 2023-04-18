---
title: Site Options Change Log
keywords: change history, site-options.conf
tags: [ctf_20.2, ctf_20.1, ctf_20.0, ctf_19.3, ctf_19.0, ctf_18.3, ctf_18.2, installation, upgrade, site-options.conf, config_files]
sidebar: teamforge_sidebar
permalink: siteoptionschangelog.html
last_updated: Jul 17, 2020
summary: Change log of site-options.conf tokens.
---

## TeamForge 22.0 {#tf220}

New Tokens
: [ELASTICSEARCH_MIN_HEAP_SIZE][siteoptiontokens.html#esminheap]
: [ELASTICSEARCH_MAX_HEAP_SIZE][siteoptiontokens.html#esmaxheap]

Changed Tokens
: [ELASTICSEARCH_JAVA_OPTS][siteoptiontokens.html#elasticsearch]
## TeamForge 20.2
Obsolete Tokens
<!-- artf415114 -->
* LINUX_USERNAME_MODE_ENABLED 

## TeamForge 20.1
Modified Tokens
: [PGSQL_LOG_MIN_DURATION][siteoptiontokens.html#pgsqllogminduration]


## TeamForge 20.0 {#tf200}

New Tokens
: [HAPROXY_HTTP_REUSE_OPTION][siteoptiontokens.html#HAPROXY_HTTP_REUSE_OPTION]
: [WEBR_HTTP_BINDNAME][siteoptiontokens.html#WEBR_HTTP_BINDNAME]
: [WEBR_INIT_JSFILE][siteoptiontokens.html#WEBR_INIT_JSFILE]
: [BASELINE_LIQUIBASE_LOGLEVEL][siteoptiontokens.html#BASELINE_LIQUIBASE_LOGLEVEL]

## TeamForge 19.3 {#tf193}

New Tokens
: [MAX_DOCUMENTS_DOWNLOAD_SIZE][siteoptiontokens.html#MAX_DOCUMENTS_DOWNLOAD_SIZE]
: [MAX_DOCUMENTS_DOWNLOAD_LIMIT][siteoptiontokens.html#MAX_DOCUMENTS_DOWNLOAD_LIMIT]

## TeamForge 19.2 {#tf192}

### New Tokens

* [BASELINE_COMPARE_ROOT_FOLDER][siteoptiontokenS.html#BASELINE_COMPARE_ROOT_FOLDER]

### Obsolete Tokens

* SSL

## TeamForge 19.0 {#tf190}

### New Tokens

* [ALLOWED_HOSTS][siteoptiontokens.html#ALLOWED_HOSTS]
* [SECURE_REDIRECTS][siteoptiontokens.html#SECURE_REDIRECTS]
* [BASELINE_CACHE_ENABLED][siteoptiontokens.html#BASELINE_CACHE_ENABLED]
* [BASELINE_BULKDATA_BATCHSIZE][siteoptiontokens.html#BASELINE_BULKDATA_BATCHSIZE]
* [BASELINE_BULKDATA_WORKER][siteoptiontokens.html#BASELINE_BULKDATA_WORKER]
* [BASELINE_LOG_FILE][siteoptiontokens.html#BASELINE_LOG_FILE]
* [BASELINE_LOG_MAX_SIZE][siteoptiontokens.html#BASELINE_LOG_MAX_SIZE]
* [BASELINE_LOG_MAX_AGE ][siteoptiontokens.html#BASELINE_LOG_MAX_AGE]
* [BASELINE_LOG_MAX_BACKUP][siteoptiontokens.html#BASELINE_LOG_MAX_BACKUP]
* [BASELINE_LOG_MAX_COMPRESS][siteoptiontokens.html#BASELINE_LOG_MAX_COMPRESS]
* [BASELINE_FILE_STORAGE][siteoptiontokens.html#BASELINE_FILE_STORAGE]
* [POSTINSTALL_LOG_FILE][siteoptiontokens.html#POSTINSTALL_LOG_FILE]
* [BINARIES_ENDPOINT_URL][siteoptiontokens.html#BINARIES_ENDPOINT_URL]
* [NEXUS2_DEFAULT_PATH][siteoptiontokens.html#NEXUS2_DEFAULT_PATH]
* [NEXUS3_SEARCH_PATH][siteoptiontokens.html#NEXUS3_SEARCH_PATH]
* [NEXUS3_REPOSITORIES_PATH][siteoptiontokens.html#NEXUS3_REPOSITORIES_PATH]
* [NEXUS3_SCRIPT_PATH][siteoptiontokens.html#NEXUS3_SCRIPT_PATH]
* [NEXUS3_COMPONENTS_PATH][siteoptiontokens.html#NEXUS3_COMPONENTS_PATH]
* [WEBR_ADMIN_USER][siteoptiontokens.html#WEBR_ADMIN_USER]
* [WEBR_ADMIN_PASSWORD][siteoptiontokens.html#WEBR_ADMIN_PASSWORD]

## TeamForge 18.3

### New Tokens

* [POSTINSTALL_LOG_LEVEL][siteoptiontokens.html#POSTINSTALL_LOG_LEVEL]
* [USER_SYNC_CRON_EXP][siteoptiontokens.html#USER_SYNC_CRON_EXP]
* [BASELINE_PSQL_MAX_CONN][Siteoptiontokens.html#BASELINE_PSQL_MAX_CONN]
* [BASELINE_CTF_MAX_CONN][siteoptiontokens.html#BASELINE_CTF_MAX_CONN]
* [BASELINE_LOG_LEVEL][siteoptiontokens.html#BASELINE_LOG_LEVEL]
* [BASELINE_CACHE_EXPIRE_TIME][siteoptiontokens.html#BASELINE_CACHE_EXPIRE_TIME]
* [BASELINE_CACHE_PURGE_TIME][siteoptiontokens.html#BASELINE_CACHE_PURGE_TIME]
* [BASELINE_POST_INSTALL_PORT][siteoptiontokens.html#BASELINE_POST_INSTALL_PORT]
* [NEXUS_TYPE][siteoptiontokens.html#NEXUS_TYPE]
* [ENABLE_GO_PROFILING][siteoptiontokens.html#ENABLE_GO_PROFILING]
* [COMPARE_LIMIT][siteoptiontokens.html#COMPARE_LIMIT]

### Obsolete Tokens

The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server and the `REPORTS_DATABASE_PORT` token have been deprecated. 
  * During TeamForge installation, the `REPORTS_DATABASE_PORT` token should no longer be used to assign a separate port for datamart.
  * If you have the TeamForge database and datamart running on separate PostgreSQL instances on the same server, create a dump of both the database and datamart and load them into the same PostgreSQL instance. For more information, see [Create a single cluster for both Database and Datamart][movedbdmintoonepginstance].


## TeamForge 18.2

### New Tokens

* [JAMES_DKIM_VERIFICATION][siteoptiontokens.html#JAMES_DKIM_VERIFICATION]
* [JAMES_DKIM_SELECTOR][siteoptiontokens.html#JAMES_DKIM_VERIFICATION]
* [JAMES_DKIM_SIGNINGDOMAIN][siteoptiontokens.html#JAMES_DKIM_SIGNINGDOMAIN]
* [JAMES_DKIM_KEY_TYPE][siteoptiontokens.html#JAMES_DKIM_KEY_TYPE]


## TeamForge 18.1

### New Tokens

* [GERRIT_USER_EMAIL][siteoptiontokens.html#gerrituseremail]
* [BROWSER_NO_CACHE][siteoptiontokens.html#browsernocache]

### Unsupported *_JAVA_OPTS Token Options 
<!-- (See: https://forge.collab.net/sf/go/artf300770) -->TeamForge 18.1 (and later) supports Java 9. As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens before upgrading to TeamForge 18.1.
* JBOSS_JAVA_OPTS
* PHOENIX_JAVA_OPTS
* INTEGRATION_JAVA_OPTS
* ETL_JAVA_OPTS
   
## TeamForge 17.11

### Obsolete Tokens
* ENABLE_CACHING_WITH_MEMCACHED
* MEMCACHED_SERVER_HOST
* MEMCACHED_SERVER_PORT
* MEMCACHED_SERVER_TTL
* SSL_CA_CERT

### subversion-caching service

A new TeamForge service, `subversion-caching`, has been added in TeamForge 17.11. Add this service to the `SERVICES` token of the TeamForge `site-options.conf` file to have Memcached installed. For more information, see [Install Memcached][installmemcached]. With this change, the following tokens are no longer supported:
* ENABLE_CACHING_WITH_MEMCACHED
* MEMCACHED_SERVER_HOST
* MEMCACHED_SERVER_PORT
* MEMCACHED_SERVER_TTL

### Separate Ports for Database and Datamart on the Same Server

The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server has been deprecated.

* During TeamForge installation, the `REPORTS_DATABASE_PORT` token should no longer be used to assign a separate port for datamart on the server that also runs the TeamForge database. The following warning shows up if you use the `REPORTS_DATABASE_PORT` token with a custom port number (other than the default value, which is 5432).

  ``` shell
  Using two separate Postgres clusters for database and datamart on the same machine is deprecated. Consider deploying the two clusters on two machines or using a single cluster for both databases.
  ````
* If you have the TeamForge database and datamart running on separate PostgreSQL instances on the same server:
  * **New Hardware Upgrade**: If you are upgrading on a new hardware, it is highly recommended to create a dump of both the database and datamart and load them into the same PostgreSQL instance. For more information, see [Create a single cluster for both Database and Datamart][movedbdmintoonepginstance].
  * **Same Hardware Upgrade**: If you are upgrading on the same hardware, you may still choose to use the `REPORTS_DATABASE_PORT` and have the database and datamart running on two separate PostgreSQL instances. However, support for `REPORTS_DATABASE_PORT` token may end in one of the future TeamForge releases, when you may have to dump and load both the database and datamart on the same PostgreSQL instance anyway.


## TeamForge 17.8

### Obsolete tokens
* JAMES_ACCEPTED_RELAYS
* REPORTS_LIFECYCLE_METRICS

## TeamForge 17.4

### Obsolete Tokens
* GERRIT_FORCE_HISTORY_PROTECTION
* ORC_HOSTNAME[^1]
* ORC_SSL_CA_CERT_FILE
* ORC_PORT
* ORC_PROXIED_PATH
* ORC_PROTOCOL
* ORCHESTRATE_ENABLED
* POSTGRES_INTERFACE_IP
* POSTGRES_INTERFACE

### New Tokens
* [LISTEN_IP][siteoptiontokens.html#listen_ip]

### Default Values for site-options.conf Tokens

Default values have been assigned to the following `site-options.conf` tokens and are therefore removed from the default TeamForge 17.4 `site-otpions-default.conf` file.

{% include warning.html content="If you are upgrading from TeamForge 17.1 (or earlier) to TeamForge 17.4 (or later) and if you have been using your own values for the following tokens, you must make sure you use the same values in your site-options.conf file post upgrade to TeamForge 17.4." %}

```shell
# CTF Core
SCM_ADMIN_PASSWORD=$auto$
IAF_DBPASS=$auto$
SCM_DEFAULT_SHARED_SECRET=$auto$
SOAP_ANONYMOUS_SHARED_SECRET=$auto$

# Database
DATABASE_USERNAME=teamforge
DATABASE_NAME=teamforge
DATABASE_PASSWORD=$auto$
DATABASE_READ_ONLY_USER=teamforge_reader
DATABASE_READ_ONLY_PASSWORD=$auto$

# Datamart
REPORTS_DATABASE_USERNAME=teamforge_datamart
REPORTS_DATABASE_NAME=teamforge_datamart
REPORTS_DATABASE_PASSWORD=$auto$
REPORTS_DATABASE_READ_ONLY_USER=teamforge_datamart_reader
REPORTS_DATABASE_READ_ONLY_PASSWORD=$auto$

# ETL
ETL_SOAP_SHARED_SECRET=$auto$

# Gerrit
GERRIT_DATABASE_PASSWORD=$auto$

# RabbitMQ
RABBITMQ_APP_ADMIN_USER=guest
RABBITMQ_APP_ADMIN_PASSWORD=$auto$
RABBITMQ_APP_CTF_USER=ctf
RABBITMQ_APP_CTF_PASSWORD=$auto$
RABBITMQ_APP_SERVICES_USER=eventq
RABBITMQ_APP_SERVICES_PASSWORD=$auto$
RABBITMQ_PERMISSION_PUBLISHER=permission_publisher
RABBITMQ_PERMISSION_PUBLISHER_PASSWORD=$auto$

# Mongo
MONGODB_APP_DATABASE_NAME=eventq
MONGODB_ADMIN_DATABASE_NAME=admin
MONGODB_APP_ADMIN_USER=admin
MONGODB_APP_ADMIN_PASSWORD=$auto$
MONGODB_APP_BACKUP_USER=backup
MONGODB_APP_BACKUP_PASSWORD=$auto$
MONGODB_APP_SERVICES_USER=eventq
MONGODB_APP_SERVICES_PASSWORD=$auto$

# HAProxy
HAPROXY_STATS_PASSWORD=$auto$

# Binary
IAF_DBNAME=iafdb
IAF_DBUSER=iafdbusr

# James Admin (for management interface)
JAMES_ADMIN_USER=admin
JAMES_ADMIN_PASSWORD=$auto$
````

## TeamForge 17.1
### Obsolete Tokens

* BDCS_ADMIN_PASSWORD
* BDCS_ADMIN_USERNAME
* BDCS_HOST
* BDCS_SSL
* BDCS_TOMCAT_PORT
* BDCS_SDK_SEARCH_LIMIT_MAX
* BDCS_SSL_CERT_FILE
* BDCS_SSL_KEY_FILE
* BDCS_SSL_CA_CERT_FILE
* BDCS_SSL_CHAIN_FILE
* BDCS_SCAN_SOURCE_DIR_ROOT
* BDCS_INSTALL_PATH
* BDCS_PGSQL_HOME_DIR_ROOT
* BDCS_PGSQL_PORT
* BDCS_TOMCAT_MX_IN_MB
* BDCS_TOMCAT_SHUTDOWN_PORT

### New Tokens

* ELASTICSEARCH_JAVA_OPTS

## TeamForge 16.10

### Obsolete Tokens

* SSH_TUNNEL_ENABLED
* SELINUX_SETUP
* SELINUX_ENABLED

### New Tokens

* DISABLE_REMOTE_PUBLISHING

## TeamForge 16.7

### Obsolete Tokens

* TeamForge 16.7 installer automatically sets `JAVA_HOME` during installation or upgrade. Therefore, the `JAVA_HOME` site options token, if added to your `site-options.conf` file, must be removed while upgrading to TeamForge 16.7 and later.
* The `DEDICATED_INSTALL` token is no longer supported. CollabNet recommends removing this token from the `site-options.conf` file. However, this token is ignored (has no effect whatsoever) if you continue to have it in your `site-options.conf` file post upgrade to TeamForge 16.7 and later.
* Debug settings can be done via the `JAVA_OPTS` tokens (such as JBOSS_JAVA_OPTS and ETL_JAVA_OPTS). Hence, the following tokens are no longer supported:
  * JBOSS_DEBUG
  * PHOENIX_DEBUG
  * ETL_DEBUG
  * INTEGRATION_DEBUG
  * ETL_DEBUG_PORT
  * JBOSS_DEBUG_PORT
  * INTEGRATION_DEBUG_PORT
  * PHOENIX_DEBUG_PORT
* The SITE_DIR and DATA_DIR tokens are no longer supported. Starting from TeamForge 16.7 (and later) SITE_DIR and DATA_DIR are unconditionally set to `/opt/collabnet/teamforge` and `/opt/collabnet/teamforge/var` respectively during runtime creation.
* The MODPAGESPEED_ENABLED token is no longer supported.
* SSL certificates are validated by default. Hence, VALIDATE_SSL_CERTS token is no longer supported. If in use, remove this token from the `site-options.conf` file post upgrade to TeamForge 16.7 and later.
* While the SSL_CA_CERT_FILE token is still supported, it has been removed from the `site-options-default.conf` file as it is only needed for add-ons. References to this token have been removed from TeamForge documentation as well.

### New Tokens

* ALLOW_CASE_INSENSITIVE_LOGIN
* HTTP_MAX_PARAMETERS
* ENABLE_SITE_NEWS
* LOGROTATE_ARCHIVE_COUNT
* MAX_PASSWORD_LENGTH

## TeamForge 8.2 

### Obsolete Tokens
* PERFORCE_CLIENT_DIR
* PERFORCE_GROUP
* PERFORCE_LICENSE_FILE
* PERFORCE_LOG_DIR
* PERFORCE_PORT
* PERFORCE_REPOSITORY_BASE
* PERFORCE_SERVICE_CMD
* PERFORCE_USER
* HELP_AVAILABILITY
* REMOTE_HELP_URL
* EXTERNAL_TOMCAT_INSTALL_DIR
* INTEGRATION_BUILTIN_TOMCAT
* ETL_BUILTIN_TOMCAT
* CEE_COMPATIBLE

### New Tokens
* ENABLE_CACHING_WITH_MEMCACHED
* MEMCACHED_SERVER_HOST
* MEMCACHED_SERVER_PORT
* MEMCACHED_SERVER_TTL

## TeamForge 8.0

### New Tokens
* NOTIFY_SITE_ADMINS_FOR_SITE_ACTIVITIES
* BINARY_SETUP_TYPE

{{site.data.alerts.hr_shaded}}

[^1]: EventQ installation is being taken care of by the TeamForge installer. Remove the ORC_* tokens from the `site-options.conf` file while upgrading to TeamForge 17.4 or later.

{% include links.html %}