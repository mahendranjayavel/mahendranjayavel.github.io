---
title: Install Review Board
keywords: install review board, review board
tags: [ctf_20.2, installation, site_admin_tasks, review_board]
sidebar: teamforge_sidebar
permalink: install_review_board.html
last_updated: Nov 23, 2022
layout: "page_without_h3_in_toc"
summary: Install Review Board on your site before you can make it available as an integrated application to project managers on your TeamForge site.
---

{% capture rbinstall %}
{% include inline_image.html file="status-success-small.png" %} You can install the Review Board application (`reviewboard`) on the TeamForge Application Server or on a separate server of its own.<br><br>
{% include inline_image.html file="status-success-small.png" %} Review Board database (`reviewboard-database`) can be installed on the TeamForge PostgreSQL Database Server on sites with database running on a separate server.<br><br>
{% include inline_image.html file="status-success-small.png" %} To install Review Board successfully, ensure that other repositories such as EPEL (Extra Packages for Enterprise Linux) are disabled apart from the CollabNet and Operating System repositories.<br><br>
{% include inline_image.html file="status-success-small.png" %} This procedure is for those who are installing the Review Board for the first time.<br><br>
{% include inline_image.html file="status-success-small.png" %} In this scenario, both TeamForge and Review Board use PostgreSQL.<br><br>
{% include inline_image.html file="status-success-small.png" %} TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.<br><br>
{% include inline_image.html file="status-success-small.png" %} Installing Review Board needs root privileges. You must log on as root or use a root shell to install Review Board.
{% endcapture %}
{% include callout.html type="primary" content=rbinstall %}

<!-- https://forge.collab.net/sf/go/artf304560#2 -->
{% include important.html content="TeamForge has no support for having service-specific FQDN for Review Board." %}

{{site.data.alerts.hr_shaded}}

## Install Review Board on the TeamForge Application Server

In this setup, you install Review Board on the TeamForge Application Server (server-01) that already has TeamForge installed on it. 

{% unless site.output == "pdf" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. 
   
   For more information, see: {% include installupgrade/installrepoconfig.html %}
{% endunless %}

{% unless site.output == "web" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. For more information, see [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

2. Install Review Board.
   ```shell
   yum install teamforge
   ````

3. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the `SERVICES` token of the TeamForge Application Server.
   ```shell
   server-01:SERVICES=ctfcore ctfcore-database mail search codesearch etl ctfcore-datamart subversion gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter cliserver
   ````

4. {% include installupgrade/deploy_services_without_note.html %}

5. If SCM is installed on a separate box, run the following script to authenticate a scmviewer user against a TeamForge Subversion repository for creating a new review request.
   ```shell
   /opt/collabnet/teamforge/runtime/scripts/svn-auth.py --repo-path=https://<scm_domain>/svn/repos/<repo_dir_name>
   ````
   You should now have a Review Board instance ready to work with TeamForge.

{{site.data.alerts.hr_shaded}}

## Install Review Board with Database on a Separate Server

You can install the Review Borad database on the TeamForge Database Server on sites with a dedicated Database Server. In this setup, you install TeamForge and Review Board on a two-server distributed setup with database services running on a separate server. 

### Install Review Board services on the TeamForge Application Server (server-01)

{% unless site.output == "pdf" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. 
   
   For more information, see: {% include installupgrade/installrepoconfig_second.html %}
{% endunless %}

{% unless site.output == "web" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. For more information, see [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

2. Install Review Board.
   ```shell
   yum install teamforge
   ````
3. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the SERVICES token as required.
   
   ```shell
   server-01:SERVICES = ctfcore mail search codesearch cliserver etl subversion gerrit binary binary-database reviewboard reviewboard-adapter
   server-02:SERVICES = ctfcore-database ctfcore-datamart gerrit-database reviewboard-database
   ````

4. Do this on sites without internet access.
   1. Contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) and get the `python-modules-sources.zip` file.
   2. Unzip the `python-modules-sources.zip` file to `/opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources`.
      ```shell
      unzip python-modules-sources.zip -d /opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources
      ````

5. {% include installupgrade/deploy_services_without_note.html %}


### Provision the Database Server (server-02) with reviewboard-database Added to It

{% unless site.output == "pdf" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. 
   
   For more information, see: {% include installupgrade/installrepoconfig_third.html %}
{% endunless %}

{% unless site.output == "web" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. For more information, see [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

2. Install Review Board.
   ```shell
   yum install teamforge
   ````

3. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the SERVICES token as required.
   
   ```shell
   server-01:SERVICES = ctfcore mail search codesearch cliserver etl subversion gerrit binary binary-database reviewboard reviewboard-adapter cliserver
   server-02:SERVICES = ctfcore-database ctfcore-datamart gerrit-database reviewboard-database
   ````
3. {% include installupgrade/deploy_services_without_note.html %}


### Do This on the TeamForge Application Server (server-01)

If SCM is installed on a separate box, run the following script to authenticate a scmviewer user against a TeamForge Subversion repository for creating a new review request.

```shell
/opt/collabnet/teamforge/runtime/scripts/svn-auth.py --repo-path=https://<scm_domain>/svn/repos/<repo_dir_name>
````
You should now have a Review Board instance ready to work with TeamForge.

{{site.data.alerts.hr_shaded}}

## Install Review Board on a Separate Server

In this setup, you install TeamForge and Review Board on a two-server distributed setup with Review Board services running on a separate server.

### Provision the TeamForge Application Server (server-01) with reviewboard-adapter Added to It

{% unless site.output == "pdf" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. 
   
   For more information, see: {% include installupgrade/installrepoconfig_fourth.html %}
{% endunless %}

{% unless site.output == "web" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. For more information, see [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

2. Install Review Board.
   ```shell
   yum install teamforge
   ````

3. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the SERVICES token as required.
   
   ```shell
   server-01:SERVICES = ctfcore ctfcore-database ctfcore-datamart gerrit-database mail search codesearch cliserver etl subversion gerrit binary binary-database reviewboard-adapter cliserver
   server-02:SERVICES = reviewboard reviewboard-database
   ````
4. {% include installupgrade/deploy_services_without_note.html %}


### Install Review Board Services on the Review Board Server (server-02)

{% unless site.output == "pdf" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. 
   
   For more information, see: {% include installupgrade/installrepoconfig_fifth.html %}
{% endunless %}

{% unless site.output == "web" %}
1. If you have TeamForge installed, you should have the TeamForge installation repository configured already. For more information, see [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

2. Install Review Board.
   ```shell
   yum install teamforge
   ````

3. Make sure that `reviewboard`, `reviewboard-database` and `reviewboard-adapter` identifiers have been added to the SERVICES token as required.
   
   ```shell
   server-01:SERVICES = ctfcore ctfcore-database ctfcore-datamart gerrit-database mail search codesearch cliserver etl subversion gerrit binary binary-database reviewboard-adapter cliserver
   server-02:SERVICES = reviewboard reviewboard-database
   ````

4. Do this on sites without internet access.
   1. Contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) and get the `python-modules-sources.zip` file.
   2. Unzip the `python-modules-sources.zip` file to `/opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources`.
      ```shell
      unzip python-modules-sources.zip -d /opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources
      ````
5. {% include installupgrade/deploy_services_without_note.html %}

6. Reinitialize TeamForge on the Review Board Server. 
   ```shell
   teamforge reinitialize
   ````

7. If SCM is installed on a separate box, run the following script to authenticate a scmviewer user against a TeamForge Subversion repository for creating a new review request.
   ```shell
   /opt/collabnet/teamforge/runtime/scripts/svn-auth.py --repo-path=https://<scm_domain>/svn/repos/<repo_dir_name>
   ````
   You should now have a Review Board instance ready to work with TeamForge.

{{site.data.alerts.hr_shaded}}

## Post Install Tasks

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