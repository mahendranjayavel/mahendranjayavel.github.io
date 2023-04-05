---
title: EventQ End of Life 
keywords: events
tags: [ctf_20.0, site_admin_tasks, installation, upgrade]
sidebar: teamforge_sidebar
last_updated: Jan 29, 2020
permalink: eventqendoflife.html
folder: teamforge
summary: EventQ is no longer supported and is completely removed from TeamForge starting from TeamForge 20.0. If you have been using EventQ on your site, you must consider a few things when you upgrade to TeamForge 20.0 or later.
---

EventQ as a TeamForge service is no longer supported from TeamForge 20.0. In case you have been using EventQ, there are a few things you must keep in mind when you upgrade to TeamForge 20.0 or later. 

* All the reports (for example, some of the Activity Reports) that use EventQ datastore are deprecated.
* All EventQ-enabled integrations such as integrations with Jira, Jenkins and so on are deprecated. As an alternative, you can create integrations via the TeamForge Webhooks-based Event Broker (WEBR). 
* All EventQ related site option tokens are deprecated.
* Do not discard your EventQ data. Back up your EventQ database before you upgarde.

## Are you Upgrading to TeamForge 20.0 (or Later)?
If you have been using EventQ and if you are upgrading to TeamForge 20.0 (or later):
1. Undeploy EventQ services before you upgrade your TeamForge services (before you do `yum install teamforge`).
<!-- Artifact artf395002 : [Doc]teamforge undeploy eventq,rabbitmq,redis before upgrading -->
   ```shell
   teamforge undeploy -s eventq
   teamforge undpeloy -s rabbtimq
   teamforge undeploy -s redis
   ````
2. Remove all the EventQ service identifiers (`eventq`, `redis`, `rabbitmq`) from the `site-options.conf` except `mongodb` before running the `teamforge provision` command. 
   
   The `teamforge provision` command fails in case your `site-options.conf` file has any of the EventQ service identfiers (except `mongodb`, which is allowed).

   You must have `mongodb` included in the `site-options.conf` to avoid issues during the data migration phase of the `teamforge provision`. 

   For example, here's a sample `host:SERVICES` token when you upgrade to TeamForge on a new hardware with all services on the same server. 

   ```shell
   server-01:SERVICES = ctfcore ctfcore-database ctfcore-datamart service-monitor mail etl search codesearch subversion cliserver gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter baseline baseline-database baseline-post-install webr webr-database `mongodb`
   ````

## Post Upgrade Task
1. Post upgrade to TeamForge 20.0 or later, you must remove the EventQ packages. 
   ```shell
   yum erase CN-eventq CN-eventq-runtime CN-rabbitmq CN-redis
   ````
2. Delete the EventQ application from the list of integrated applications.
   <!-- Artifact artf394428 : Doc task for artf394427 -->
   1. Select **My Workspace > Admin**.
   2. Select **Projects > Integrated Apps**.
   3. Select **EventQ** and click **Force Delete**. 



{% include links.html %}
