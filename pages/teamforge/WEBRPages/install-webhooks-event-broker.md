---
title: Install the TeamForge Webhooks-based Event Broker
keywords: webhooks, event broker
tags: [ctf_20.0, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: install-webhooks-event-broker.html
last_updated: Jan 23, 2020
summary: This page walks you through the installation procedure for TeamForge Webhooks-based Event Broker (WEBR).
---
## Install WEBR
The Webhooks-based Event Broker is installed by default when you install or upgrade TeamForge {{site.data.identifiers.teamforge}}. In other words, you don't have to run the `yum install teamforge-webr` command separately.

For more information, see TeamForge {{site.data.identifiers.teamforge}} install and upgrade instructions.

## Call Back URLs and WEBR/TeamForge Restart
<!-- Artifact artf394594 : [DOC TASK]When WEBR service is restarted/stopped, CTF should also be restarted -->

Call back URLs registered with WEBR are lost when you restart WEBR. This means, a TeamForge/Jboss restart must follow immediately after you stop or restart WEBR.

<!-- <div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">
* From TeamForge 19.3, TeamForge Webhooks-based Event Broker is installed automatically when you install/upgrade TeamForge. In other words, you don't have to run the command `yum install teamforge-webr` separately.
* You should have the TeamForge installation respository configured as part of the TeamForge installation. 
</div>
</div>

Do this on the TeamForge Application Server to install the Webhooks-based Event Broker. 

1. Run this command:

   ```shell
   yum install teamforge
   ````

2. Add the Webhooks-based Event Broker services (`webr` and `webr-database`) to the **host:SERVICES** token in `site-options.conf` file. 

   For example:
   ```
   host:SERVICES=ctfcore ctfcore-database ctfcore-datamart search mail etl binary reviewboard reviewboard-database reviewboard-adapter cliserver webr webr-database
   ````
3. {% include installupgrade/deploy_services_without_note.html %} -->


{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Webhooks-based Event Broker Overview][webhooks-event-broker-overview]
* [TeamForge-Jenkins Integration Using TeamForge Webhooks-based Event Broker][teamforge-jenkins-integration]
* [TeamForge-JIRA Integration Using TeamForge Webhooks-based Event Broker][teamforge-jira-integration]
* [TeamForge-TestLink Integration Using TeamForge Webhooks-based Event Broker][teamforge-testlink-integration]

{% include links.html %}



