---
title: Install TeamForge with an External PostgreSQL Server
keywords: external postgres server, install, AWS, RDS, Aurora
tags: [ctf_20.2, ctf_20.0, ctf_19.3, ctf_19.1, ctf_19.0, installation, getting_started, postgres, datamart]
sidebar: teamforge_sidebar
permalink: dbdm-on-nonctfmanaged-postgresserver.html
last_updated: Aug 6, 2020
layout: "page_without_h3_in_toc"
summary: You can install TeamForge with its database installed separately on an external PostgreSQL server such as AWS RDS/Aurora.
---
You can install TeamForge with its database installed separately on an external PostgreSQL server such as AWS RDS/Aurora. These instructions are for installing TeamForge in a three-server distributed setup with TeamForge on a separate server. All database services are hosted on a second server, which is an external PostgreSQL server not directly managed by TeamForge.

{% include inline_image.html file="status-success-small.png" %} You can install TeamForge on both {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}.<br><br>
{% include inline_image.html file="status-success-small.png" %} In this [distributed setup][plan_your_installation_upgrade.html#singleordistributed], [TeamForge services][plan_your_installation_upgrade.html#teamforgeservices] are distributed across two servers, server-01 and server-02 as illustrated in the following table. It is assumed that server-02 is an externally managed PostgreSQL server.<br><br>


| server-01                     | server-02     | 
| TeamForge Application Server  | External Database Server |
|-------------------------------|---------------|
| ctfcore                       | gerrit-database          |
| mail                          | reviewboard-database     |
| search                        | binary-database          |
| codesearch                    | ctfcore-database         |
| etl                           | ctfcore-datamart         |
| gerrit                        |                          |
| reviewboard[^1]               |                          |
| reviewboard-adapter[^2]       |                          |
| subversion                    |                          |
| binary                        |                          |
| cliserver                     |                          |
| service-monitor               |                          |


<!-- Installation Dos and Don'ts -->

{% unless site.output == "pdf" %}
## Dos and Don'ts
<div markdown="1" class="panel panel-default">
<div class="panel-body" markdown="1">
{% include installupgrade/install_dos_and_donts.html %}
</div>
</div>
{% endunless %}

{% unless site.output == "web" %}
<h2>Dos and Don'ts</h2>
Before you begin, see [Installation Dos and Don'ts][for_pdf_installdosdonts].
{% endunless %}

<!-- Installation Dos and Don'ts -->

## Prepare the Server for TeamForge Installation (server-01)

1. Install {{site.data.identifiers.rhel_centos_now}} and log on as root.
   {% capture rhnetwork %}
   {% include inline_image.html file="status-success-small.png" %} The host must be registered with the Red Hat Network if you are using Red Hat Enterprise Linux.<br><br>
   {% include inline_image.html file="status-success-small.png" %} See the [{{site.data.identifiers.rhel_centos_now}} Installation Guide](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/index.html) for help.
   {% endcapture %}
   {% include callout.html type="primary" content=rhnetwork %}
   
2. Check your networking setup. See [Set up Networking][setupnetworking] for more information. 

{% unless site.output == "pdf" %}
3. {% include installupgrade/installrepoconfig.html %}
{% endunless %}

{% unless site.output == "web" %}
3. [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

## Install TeamForge Services

1. Install TeamForge and Review Board services on the TeamForge Application Server (server-01).
   
   ```shell
   yum install teamforge
   ````

   Install Monit.

   {% include important.html content="If you haven't already installed the latest version of the Monit application, download it [here](https://dl.fedoraproject.org/pub/epel/7/x86_64/Packages/m/monit-5.30.0-1.el7.x86_64.rpm)." %}

   1. Download Monit for


      * RHEL 8.x from the EPEL repository.

        ```
        wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-8.noarch.rpm
        rpm -ivh epel-release-latest-8.noarch.rpm
        ```

      * RHEL/CentOS 7.x from the EPEL repository.

        ```
        wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
        rpm -ivh epel-release-latest-7.noarch.rpm
        ```

    2. Install Monit.

        ```
        yum install monit
        ```   

## Prepare the External Database Server for TeamForge Installation

1. Log on to the Database Server and create the TeamForge database, datamart, Gerrit database, Binary database and Review Board database. Note down the following credentials that are required to set up the TeamForge `site-options.conf` tokens later in the process.

   * Database name (DATABASE_NAME)
   * Database username (DATABASE_USERNAME)
   * Database password (DATABASE_PASSWORD)
   * Database read-only username (DATABASE_READ_ONLY_USER)
   * Database read-only password (DATABASE_READ_ONLY_PASSWORD)
   * Reports database name (REPORTS_DATABASE_NAME)
   * Reports database username (REPORTS_DATABASE_USERNAME)
   * Reports database password (REPORTS_DATABASE_PASSWORD)
   * Reports database read-only username (REPORTS_DATABASE_READ_ONLY_USER)
   * Reports database read-only password (REPORTS_DATABASE_READ_ONLY_PASSWORD)
   * Gerrit database password (GERRIT_DATABASE_PASSWORD)
   * IAF database name (IAF_DBNAME)
   * IAF database username (IAF_DBUSER)
   * IAF database password (IAF_DBPASS)
   * Review Board database name (REVIEWBOARD_DATABASE_NAME)
   * Review Board database username (REVIEWBOARD_DATABASE_USER)
   * Review Board database password (REVIEWBOARD_DATABASE_PASSWORD)

2. Create users and grant access rights.
   * **Access rights for read-only users**: LOGIN,NOCREATEDB,NOCREATEROLE,NOSUPERUSER
   * **Access rights for other users**: LOGIN,CREATEDB,NOCREATEROLE,NOSUPERUSER

{% unless site.output == "pdf" %}
3. {% include installupgrade/installrepoconfig_second.html %}
{% endunless %}

{% unless site.output == "web" %}
3. [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

4. Install TeamForge database services on the External PostgreSQL Server (server-03)
   ```shell
   yum install teamforge-database
   ````

## Set up Your Site's Master Configuration File

1. Do this on the TeamForge Application Server (server-01).
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````

   ### host:SERVICES Token
   ```shell
   server-01:SERVICES=ctfcore service-monitor mail etl search subversion codesearch cliserver gerrit binary reviewboard reviewboard-adapter
   server-02:SERVICES=ctfcore-database ctfcore-datamart gerrit-database binary-database reviewboard-database
   ````
 
   ### host:PUBLIC_FQDN Token
   ```shell
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````
   
   ### Set up the Following Site Option Tokens

   * DATABASE_NAME=
   * DATABASE_USERNAME=
   * DATABASE_PASSWORD=
   * DATABASE_READ_ONLY_USER=
   * DATABASE_READ_ONLY_PASSWORD=
   * REPORTS_DATABASE_NAME=
   * REPORTS_DATABASE_USERNAME=
   * REPORTS_DATABASE_PASSWORD=
   * REPORTS_DATABASE_READ_ONLY_USER=
   * REPORTS_DATABASE_READ_ONLY_PASSWORD=
   * GERRIT_DATABASE_PASSWORD=
   * IAF_DBNAME=
   * IAF_DBUSER=
   * IAF_DBPASS=
   * REVIEWBOARD_DATABASE_NAME=
   * REVIEWBOARD_DATABASE_USER=
   * REVIEWBOARD_DATABASE_PASSWORD=

   Save the `site-options.conf` file. 

   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): {% include installupgrade/site_options_config.html %}

2. Copy the `/opt/collabnet/teamforge/etc/site-options.conf` file from the TeamForge Application Server to the `/opt/collabnet/teamforge/etc/` directory of the database server.

## Provision Services on All the Servers

1. {% include installupgrade/deploy_services_with_note.html %}

{% include inline_image.html file="status-success-small.png" %} You must provision services in a particluar sequence. Usually you start with the Database Server, followed by the Application Server and then by other servers.<br><br> 
{% include inline_image.html file="status-success-small.png" %} The TeamForge installer derives this sequence from your `site-options.conf` file and shows you the order of provisioning servers when you try to provision one of the distributed servers. Follow the exact sequence as instructed.

1. Provision the Database Server (server-02).
2. Provision the Application Server (server-01).

## Verify TeamForge Installation

1. {% include installupgrade/verify_installation.html %}

{% include installupgrade/postinstalltasks.html %}

{{site.data.alerts.hr_shaded}}
[^1]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
[^2]: `reviewboard-adapter` must always be installed on the TeamForge Application Server.

{% include links.html %}