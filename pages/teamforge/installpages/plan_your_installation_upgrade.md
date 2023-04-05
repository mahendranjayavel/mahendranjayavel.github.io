---
title: Plan Your Installation / Upgrade
keywords: plan, planning, services
tags: [ctf_21.1, ctf_21.0, ctf_20.3, ctf_20.2, ctf_20.1, ctf_19.0, ctf_18.3, installation, upgrade, getting_started, backup_restore]
sidebar: teamforge_sidebar
permalink: plan_your_installation_upgrade.html
last_updated: Jun 3, 2021
layout: "page_without_h3_in_toc"
summary: Plan your installation or upgrade setup, hardware and software requirements and so on before you begin.
---

## TeamForge Services {#teamforgeservices}

Before you plan your installation or upgrade, let us understand TeamForge and its services. 

A TeamForge site consists of a core TeamForge application and several tightly integrated services that support it. In addition, you can integrate TeamForge with other third party applications such as Nexus, Jenkins, Jira and so on. Some of the TeamForge services are mandatory and some are optional. You can install the services, all in one single server, or distribute them across two or more servers.

* The core TeamForge application provides the Web interface that users see, and the API that other applications can interact with. It also includes the file system where some user content is stored, such as wiki pages.
* The site database is where most of the user-created content is stored and accessed. Documents, discussion posts, tracker artifacts, project administration settings: all that sort of thing lives in the database.
* The source control server ties any number of Subversion or Git/Gerrit repositories into the TeamForge site.
* The Extract Transform and Load (ETL) server pulls data from the site database and populates the datamart to generate charts and graphs about how people are using the site.
The datamart (Reports DB) is an abstraction of the site database, optimized to support the reporting functionality.
* Baseline is a TeamForge capability that lets you create snapshot of selected configuration items from a given TeamForge project at a given point in time. For more information, see [TeamForge Baseline][baseline-overview].
* TeamForge Webhooks-based Event Broker, which is also referred to as the integration broker, is a webhooks-based message broker that pushes the messages of specific events received from a Publisher to a Subscriber. For more information, see [TeamForge Webhooks-based Event Broker][webhooks-event-broker-overview].

Here's a list of available TeamForge services.

| Service | Mandatory/Optional | Old Name | Description |
|---------|--------------------|----------|-------------|
| ctfcore | Mandatory | app | Main TeamForge application server |
| search | Mandatory | indexer | Indexing and searching |
| mail | Mandatory | NA (added in TeamForge 17.1) | Email server |
| ctfcore-database | Mandatory | database | Operational database |
| ctfcore-database-mirror | Optional | NA | Mirror of operational database |
| codesearch | Mandatory | codesearch | Code Search |
| etl | Optional | etl | ETL for Datamart |
| ctfcore-datamart | Mandatory if and only if you install `etl` | datamart | Datamart database |
| cliserver | Mandatory | NA | CLI Server |
| subversion | Optional | subversion | SVN Version Control |
| gerrit | Optional | gerrit | Git/Gerrit Version Control |
| gerrit-database | Mandatory if and only if you install `gerrit` | NA (added in TeamForge 17.1) | Database for Git/Gerrit. In a distributed setup, add this identifier to the server where you want to run Gerrit database.<br><br> In a distributed setup with multiple Git integration servers, add this identifier to all the servers that run the Git databases. For more information, see [host:SERVICES][siteconfigtokens] token. |
| binary | Optional | Optional | Artifact repository integration |
| binary-database | Mandatory if and only if you install `binary` | binary | Database for artifact repository integration. Binary app (binary) and database (binary-database) have to be installed on the same server. |
| reviewboard | Optional | reviewboard | Review Board code review tool |
| reviewboard-database | Mandatory if and only if you install `reviewboard` | NA (added in TeamForge 17.1) | Database for Review Board. In a distributed setup, add this identifier to the server where you want to run Review Board database. |
| reviewboard-adapter |	Mandatory if and only if you install `reviewboard` | NA |	Adapter for reviewboard to copy `ctfrbevents.jar`. In a distributed setup, `reviewboard-adapter` must always be installed on the TeamForge Application Server. |
| baseline | Optional | NA | Baseline service. In a distributed setup, add this identifier to the server where you want to run the Baseline application. |
| baseline-database | Mandatory if and only if you install `baseline` | NA | Baseline database service. In a distributed setup, add this identifier to the server where you want to run the Baseline database. |
| baseline-post-install | Mandatory if and only if you install `baseline` | NA | Baseline service that is used to synchronize user information between the Baseline and TeamForge databases. |
| webr | Mandatory. The WEBR application is installed by default when you install or upgrade to TeamForge. | NA | Webhooks-based Event Broker service that is used to push the messages of specific events received from a Publisher to a Subscriber. |
| webr-database | Mandatory. | NA | Database service for the TeamForge Webhooks-based Event Broker. |

These service identifiers are used in the `site-options.conf` file's `host:SERVICES` token. For more information, see [host:SERVICES][siteconfigtokens] token.

In addition, installing TeamForge with service-specific FQDNs (instead of machine-specific host/domain names) is highly recommended so that you will be able to change the system landscape at a later point in time without having any impact on the URLs (in other words, end users do not have to notice or change anything). For example, you can create FQDNs specifically for services such as Subversion, Git, mail, Codesearch and so on. For more information, see [Service-specific FQDNs][siteconfigtokens].

## Single Server or Distributed Setup? {#singleordistributed}

If you are installing TeamForge, are you planning to install on a single server or distribute TeamForge services across two or more servers? How are you going to distribute the services?

In the default setup, all services run on the same server as the main TeamForge application. But in practice, only the TeamForge application needs to run on the TeamForge application server. The other services can share that server or run on other servers, in almost any combination. 

Assess your own site's particular use patterns and resources to decide how to distribute your services, if at all. For example, if you anticipate heavy use of your site, you will want to consider running the site database, the source control service, or the reporting engine on separate hardware to help balance the load. For examples on how to distribute TeamForge services, see [host:SERVICES][siteconfigtokens] token.

{% capture distributeservices %}
In a distributed setup, it is highly recommended to have dedicated servers for TeamForge database and SCM services, as these are the most sought after services in TeamForge. If you are installing [TeamForge Baseline][baseline-overview], it is always recommended to install it on a separate server.
{% endcapture %}
{% include callout.html type="primary" content=distributeservices %}

When you distribute your services on multiple servers, you must do some configuration to handle communication between the services. Verify your basic networking setup. See [Set Up Networking for TeamForge][setupnetworking].

## PostgreSQL or Oracle? {#postgresororacle}

<!--PostgreSQL is installed automatically when you install TeamForge. If you intend to use Oracle, CollabNet recommends that you let the installer run its course, make sure things work normally, and then set up your Oracle database and switch over to it.-->

PostgreSQL {{site.data.identifiers.postgres_long}} is installed automatically when you install TeamForge {{site.data.identifiers.teamforge}}. If you intend to use Oracle, CollabNet recommends that you let the installer run its course, make sure things work normally, and then set up your Oracle database and switch over to it.

If you want to use Oracle as your database, consider the following points:
* TeamForge {{site.data.identifiers.teamforge}} supports Oracle server {{site.data.identifiers.oracle_server}} and Oracle client {{site.data.identifiers.oracle_client}}.
* Oracle express edition is not supported for both client and server.
* Review Board {{site.data.identifiers.review_board}} was tested with PostgreSQL {{site.data.identifiers.postgres_long}} only. Review Board with Oracle was not tested. 
* Git integration works only with PostgreSQL. The Git integration uses PostgreSQL even if your TeamForge site uses Oracle.

The efficiency of your database can have an impact on your users' perception of the site's usability. If your site uses a PostgreSQL database (which is the default), you may want to consider tuning it to fit your specific circumstances. The default settings are intended for a small-to-medium site running on a single server. See [What are the right PostgreSQL settings for my site?][database-faqs.html#postgres_settings] for recommendations from CollabNet's performance team on optimizing PostgreSQL for different conditions.

## Integrations

TeamForge supports integration with a wide array of third party applications such as Nexus, Jira and so on. As a customer, you may or may not always want (or have) all of TeamForge's supported integrated applications. It's also quite possible that some of the integrated applications may not always run on all the platforms supported by TeamForge. To accommodate a wider audience, by default, TeamForge install and upgrade instructions include steps to integrate such third party applications with TeamForge. 

However, use your discretion to ignore and skip such steps if they are not relevant to your site. See [TeamForge Installation Requirements][requirements] to understand what it takes to run TeamForge {{site.data.identifiers.teamforge}} with integrations.

**Do you have `UserFilter` in your Gerrit Quality Gates/Review Rules?**
See: [How to verify if you can upgrade to TeamForge—Git integration 20.1 or later?][userfilterremoval.html#workflowreadiness]

{% include installupgrade/onehop.html %}

## Gerrit Upgrade from Version 2.16 to 3.2

Skip this section if you are upgrading from TeamForge 20.3 to 21.0. This is valid if and only if you are upgrading from TeamForge 20.2 or earlier to TeamForge 21.0. 

TeamForge 20.3 and later support Gerrit 3.2—a major upgrade that skips two Gerrit versions—[3.0](https://www.gerritcodereview.com/3.0.html) and [3.1](https://www.gerritcodereview.com/3.1.html) and includes the following note-worthy changes:
* TeamForge 20.3 (and later) Gerrit is not data-compatible with Gerrit 2.16 or earlier (in other words, not data-compatible with TeamForge 20.0 or earlier). Intermediate data migration to Gerrit 2.16 happens when you upgrade from TeamForge 20.0 or earlier to TeamForge 20.3 (or later). This means that data migration during upgrade takes more than usual time to complete. 
* TeamForge 20.3 (and later) Gerrit is not index-compatible with any previous version. All open reviews are reindexed offline when you upgrade from TeamForge 20.0 or earlier to TeamForge 20.3 (or later). This means that data migration during upgrade takes more than usual time to complete.
* [Orphaned draft comments are cleaned up](https://www.gerritcodereview.com/3.2.html#schema-changes) when you upgrade to TeamForge 20.3 (or later). It is recommended to schedule and run the following Git garbage collection (Git GC) command directly on the `All-Users` project before you upgrade to TeamForge 20.3 (or later). 
  ```shell
  ssh -p 29418 [admin]@[git-server] gerrit gc All-Users --aggressive --show-progress
  ````
* Git Protocol v2 is now default
* `ReviewDB` and Gerrit GWT UIs are no longer available
* For more information about Git protocol v2, see the [documentation for Git Protocol v2](https://git-scm.com/docs/protocol-v2/en).
* `ReviewDB` removal means that the database backend for changes, accounts, groups and projects (`ReviewDb`) is removed and this metadata is now stored in git (“NoteDb”). As `NoteDb` is being used by TeamForge 19.0 and later, this change is seamless for the users.
* However, the Gerrit GWT UI has more visible consequences. The GWT-related UI plugin functionality had to be ported—either to the new Gerrit Polymer UI or to the TeamForge UI.

Noteworthy Changes
: The Gerrit UI has a new look and feel with the new Gerrit Polymer UI replacing the GWT UI. 
: The Gerrit UI no longer has the history protection tab. This functionality is now available via the TeamForge Code Browser UI.
: Gerrit internal repositories are exposed at the integration level in TeamForge.
: Microsoft Internet Explorer 11 is no longer supported in Gerrit UI.

## Hardware and Backup

If you aren't the person who first installed your current TeamForge site (or maybe, even if you are), it's essential to catalog the hosts where your services are running and to know what configuration has been applied to them.

While upgrading to a latest TeamForge version, you can choose to upgrade on the same hardware or on new hardware. In general, it is good to have a backup plan in place. Same hardware upgrades need no backup. However, it's recommended to take a back up as a measure of caution. See [Back up and Restore TeamForge][backupandrestore] for more information.

## TeamForge License Framework

The TeamForge license framework has been revamped in TeamForge 21.1. 

The new TeamForge license model consists of the following license types:

* TeamForge ALM
* TeamForge ALM Essentials
* TeamForge SCM

Here's the list of changes to the new TeamForge license model.

* The `Version Control`, `Collaboration`, and `Trackers` license types are no longer available in TeamForge 21.1 and later
* The `ALM` and `Baselines` license types are bundled together and are being offered as the new `TeamForge ALM` license
* The `SCM` license type has been renamed as `TeamForge SCM`

When you migrate from TeamForge 21.0 or earlier to TeamForge 21.1 or later:

* Existing ALM licenses are migrated to the new TeamForge ALM license
* Existing SCM licenses are migrated to TeamForge SCM
* All other types of licenses such as Baselines, Version Control, Tracker, and Collaboration are deleted

For more information, see [TeamForge License][teamforgelicense].

{% unless site.output == "pdf" %}
## Other Dos and Don'ts

{% include installupgrade/install_dos_and_donts.html %}
{% endunless %}

{% include links.html %}