---
title: Upgrade Review Board
keywords: upgrade review board, review board
tags: [ctf_20.2, ctf_19.3, upgrade, site_admin_tasks, review_board]
sidebar: teamforge_sidebar
permalink: upgrade_review_board.html
last_updated: Nov 23, 2022
layout: "page_without_h3_in_toc"
summary: Use these instructions to upgrade Review Board to a latest build.
---

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">
* TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
* This procedure is for those who have Review Board already and are upgrading Review Board to a latest build on {{site.data.identifiers.rhel_centos_past}} or {{site.data.identifiers.rhel_centos_now}}.
* You may choose to upgrade Review Board on the same server or on a new server.
* In this scenario, both TeamForge and Review Board use PostgreSQL.
* To install Review Board successfully, ensure that other repositories such as EPEL (Extra Packages for Enterprise Linux) are disabled apart from the CollabNet and Operating System repositories.
* Upgrading Review Board needs root privileges. You must log on as root or use a root shell to upgrade Review Board.
</div>
</div>

## Back up and Restore the Review Board Database and Data Directories {#backuprb}

If Review Board and TeamForge are co-hosted on the same server, the Review Board database and data directories should have been backed up already when you backed up TeamForge. So, it is not necessary to take a back up of the Review Board database and data directories again. However, you must back up Review Board if you have Review Board on a separate server outside of the TeamForge Application Server. 

1. Back up the `/opt/collabnet/teamforge/var/pgsql` and `/opt/collabnet/teamforge/var/reviewboard/data` directories from the Review Board Server that hosts the Review Board database service (`reviewboard-database`) in case you have Review Board on a separate server outside of the TeamForge Application Server.

   ```shell
   mkdir -p /tmp/backup_dir
   cd /opt/collabnet/teamforge/var
   tar -zcvf /tmp/backup_dir/reviewboard_pgsql.tgz pgsql/{{site.data.identifiers.postgres_past_short}}
   tar -zcvf /tmp/reviewboard_data.tgz reviewboard
   ````

2. Copy the `/tmp/reviewboard_pgsql.tgz` and `reviewboard_data.tgz` files to the `/tmp` directory of the new server if you are upgrading Review Board on a new hardware.

   ```shell
   scp /tmp/reviewboard_pgsql.tgz username@newRBbox:/tmp
   scp /tmp/reviewboard_data.tgz username@newRBbox:/tmp
   ````

## Upgrade Review Board

<!-- https://forge.collab.net/sf/go/artf304560#2 -->
{% include note.html content="TeamForge 18.1 and later has no support for having [service-specific FQDN][siteconfigtokens] for Review Board." %}

1. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the `SERVICES` token of the TeamForge Application Server (server-01).
   ```shell
   server-01:SERVICES=ctfcore ctfcore-database mail search codesearch etl ctfcore-datamart subversion gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter cliserver
   ````
   {% capture assumption %}
   It is assumed that the Review Board is running on the TeamForge Application Server. In case you have a separate Review Board Server, add the `reviewboard` and `reviewboard-database` identifiers to the Review Board server's `SERVICES` token.
   {% endcapture %}
   {% include callout.html type="primary" content=assumption %}


{% unless site.output == "pdf" %}
2. {% include installupgrade/installrepoconfig_upgrade.html %}
{% endunless %}

{% unless site.output == "web" %}
2. [Configure the TeamForge installation repository][for_pdf_installrepoconfig_upgrade].
{% endunless %}

   {% include tip.html content=" If you have TeamForge installed, you would have the installation repository already configured." %}

3. Upgrade Review Board.
   ```shell
   yum install teamforge
   ````

4. Restore the Review Board database and data directories (on the new server where you plan to have the Review Board database).
   
   ```shell
   cd /opt/collabnet/teamforge/var/
   tar -zxvf /tmp/reviewboard_pgsql.tgz
   tar -zxvf /tmp/reviewboard_data.tgz
   ````   

5. {% include installupgrade/deploy_services_without_note.html %}

6. If SCM is installed on a separate box, run the following script to authenticate a scmviewer user against a TeamForge Subversion repository for creating a new review request.
    ```shell
    python ./svn-auth.py --repo-path=https://<scm_domain>/svn/repos/<repo_dir_name>
    ````

## Post Upgrade Tasks

* [Add Review Board to Projects][iaf-reviewboard-add]
<!-- https://forge.collab.net/sf/go/artf304542#3 -->
* [Users are not getting email notifications for review requests and reviews. What should I do?][reviewboard-faqs.html#rbemailsettings]
* [Review Board deployment fails on sites that use a self-signed certificate. What should I do?][reviewboard-faqs.html#cert-verification-cfg]

### Bootstrap Review Board Post Install or Upgrade
<!-- Adding this section for the defect https://forge.collab.net/sf/go/artf303737#5 -->
Use the following instructions if you want to bootstrap Review Board (drop Review Board database tables and recreate them again) for some reason post installation or upgrade.

1. Log on to the server that hosts the Review Board. 
2. Select **My Workspace > Admin**. 
3. Select **Projects > Integrated Apps**.
4. Select **Review Board** and click **Delete**.
5. Stop TeamForge.
   ```shell
   teamforge stop
   ````
6. Start the TeamForge database services. 
   ```shell
   teamforge start -s postgres
   ````
7. Bootstrap the Review Board database.
   ```shell
   teamforge bootstrap -s reviewboard-database-postgres
   ````
8. Bootstrap the Review Board. 
   ```shell
   teamforge bootstrap -s reviewboard
   ````
9. {% include installupgrade/start_teamforge.html %}

{% include links.html %}