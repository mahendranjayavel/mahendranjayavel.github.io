---
title: Install/Upgrade Dos and Don'ts
output: pdf
keywords: 
sidebar: teamforge_sidebar
permalink: for_pdf_installdosdonts.html
last_updated: Dec 11, 2019
search: exclude
summary: Here's a list of dos, don'ts and points to remember when you install or upgrade TeamForge.
---
### Dos

* Understand TeamForge installation [requirements][requirements] and [plan your installation or upgrade][plan_your_installation_upgrade].
* Get your [TeamForge license][teamforgelicense] key and keep it handy.
* Verify your basic networking setup before installing or upgrading TeamForge. See [Set Up Networking for TeamForge][setupnetworking].
* Look for new or modified `site-options.conf` tokens and update your `site-options.conf` file as required during the upgrade process. See [Site Options Change Log][siteoptionschangelog].
* Set up a TeamForge Stage Server before you upgrade your Production Server.
* Stop TeamForge services on all servers in a distributed setup while upgrading to TeamForge {{site.data.identifiers.teamforge}}.
* Uninstall hot fixes and add-ons, if any, before you start the TeamForge {{site.data.identifiers.teamforge}} upgrade procedure.
* <!-- (See: https://forge.collab.net/sf/go/artf300770) -->As a result of changes to the logging framework in Java 9, the `PrintGCDetails` and `PrintGCTimeStamps` logging options are no longer supported. Remove these options from the following tokens while upgrading to TeamForge 18.1 or later. TeamForge provision fails otherwise.
  * JBOSS_JAVA_OPTS
  * PHOENIX_JAVA_OPTS
  * INTEGRATION_JAVA_OPTS
  * ETL_JAVA_OPTS
  * ELASTICSEARCH_JAVA_OPTS

### Don'ts

* Do not customize your operating system installation. Select only the default packages list.
* While upgrading TeamForge, whether in place or on new hardware, always reuse the old `site-options.conf` file and make changes as necessary. **Do not** try to start with a new `site-options.conf` file. Reusing the old `site-options.conf` avoids many potential problem, particularly around the management of usernames and passwords.
* Do not manually modify TeamForge-managed site option tokens such as the `AUTO_DATA` token. See [AUTO_DATA][siteoptiontokens.html#auto_data] for more information.
* <!-- https://forge.collab.net/sf/go/artf302825#8 -->If you are creating symlinks, note that you must create symlinks only to the TeamForge data directory (`/opt/collabnet/teamforge/var`). You should not create symlinks to TeamForge application directories (such as `/opt/collabnet`).

### Points to Remember

* Installing or upgrading TeamForge needs root privileges. You must log on as root or use a root shell to install or upgrade TeamForge.
* SSL is enabled by default and a self-signed certificate is auto-generated. However, you can use a few `site-options.conf` tokens to adjust this behavior. To generate the SSL certificates, see [Generate SSL Certificates][generatesslcerts].
* For the ETL service to run as expected in a distributed TeamForge installation, all servers must have the same time zone.
* If you have Git integration on a separate server, both TeamForge and Git servers must have their time and date synchronized. Similarly, If Subversion is on a separate server, both TeamForge and Subversion servers must have their time and date synchronized.
<!-- * While you can run both EventQ and TeamForge on the same server, CollabNet recommends such an approach only for testing purposes. It's always recommended to run EventQ on a separate server for optimal scalability. -->
* It's highly recommended that you install the [TeamForge Baseline][baseline-overview] services on a separate server as the baselining process can consume considerable CPU and database resources. For more information, see [Install TeamForge in a Distributed Setup][distributed_install_rhel_centos].   
* No backup is required for same hardware upgrades. However, you can create a backup as a measure of caution. See [Back up and Restore TeamForge][backupandrestore] for more information.
* Always use compatible JDBC drivers meant for specific database versions. See [JDBC Drivers Reference](https://help.pentaho.com/Documentation/5.2/0D0/160/010) for more information. Also see: [Why do ETL jobs fail post TeamForge upgrade?][database-faqs.html#etl_fails_post_upgrade].
* You can run the initial load job any time after the installation of TeamForge. We recommend that you run it before you hand over the site to the users. For more information, see [ETL Initial Load Jobs][database-faqs.html#etl_initial_load_jobs].
* SOAP50 APIs and event handlers are no longer supported in TeamForge 16.10 and later. Use the latest TeamForge SOAP/REST APIs. 
* TeamForge {{site.data.identifiers.teamforge}} installer expects the system locale to be `LANG=en_US.UTF-8`. TeamForge create runtime (`teamforge provision`) fails otherwise.
* Installing TeamForge with service-specific FQDNs (instead of machine-specific host/domain names) is highly recommended so that you will be able to change the system landscape at a later point in time without having any impact on the URLs (in other words, end users do not have to notice or change anything). For example, you can create FQDNs specifically for services such as Subversion, Git, mail, Codesearch and so on. For more information, see [Service-specific FQDNs][siteconfigtokens.html#servicespecificfqdns].
* All such service-specific FQDNs must be long to a single sub domain and it is recommended to create a new sub domain for TeamForge.
* If you are using service-specific FQDNs:
  * A wildcard SSL cert is required. SNI SSL cert cannot be used.
  * When SSL is enabled and no custom SSL-certificates are provided, a self-signed wildcard cert is generated for the sub domain.
  * When SSL is enabled and a custom SSL-certificate is provided, the CN of the certificate is verified to be a wildcard CN.
<!-- https://forge.collab.net/sf/go/artf301286#6 -->
<!-- * You cannot have a separate PUBLIC_FQDN for EventQ. -->
* The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server is being deprecated in TeamForge 17.11. If you have TeamForge database and datamart on separate PostgreSQL instances on the same server and if you are upgrading on a new hardware, you must [Create a Single Cluster for Both Database and Datamart][movedbdmintoonepginstance] while upgrading to TeamForge {{site.data.identifiers.teamforge}} or later.
* While upgrading TeamForge-Git integration servers, it is important that Git master and slave servers are upgraded to the same version of TeamForge-Git integration. On sites with Git Replica Servers, you must upgrade the Git Replica Servers first and then upgrade the master Git servers.
<!-- * EventQ is not installed by default when you install TeamForge 19.0 or later. However, you can install EventQ seprately, if required. EventQ installation instructions are included in the TeamForge installation/upgrade instructions, which you can ignore if not required for your setup.  --> 
* From TeamForge 19.3, TeamForge Webhooks-based Event Broker is installed automatically when you install/upgrade TeamForge. In other words, you don't have to run the command `yum install teamforge-webr` separately.
* Call back URLs registered with WEBR are lost when you restart WEBR. This means, a TeamForge/Jboss restart must follow immediately after you stop or restart WEBR.
* TeamForge supports [Monit](https://mmonit.com/monit/) for monitoring services and recovering failed services. Monit is installed on the TeamForge Application server to monitor the health of services and restart the services when they fail. Monit log file is located at `/opt/collabnet/teamforge/log/monit/monit.log`.   


{% include links.html %}