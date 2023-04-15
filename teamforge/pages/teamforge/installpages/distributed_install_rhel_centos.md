---
title: Install TeamForge in a Distributed Setup
keywords: multihost, distributed installation
tags: [ctf_20.2, ctf_20.0, ctf_19.3, ctf_19.1, ctf_19.0, ctf_18.3, installation]
sidebar: teamforge_sidebar
permalink: distributed_install_rhel_centos.html
last_updated: Aug 6, 2020
layout: "page_without_h3_in_toc"
summary: Distributed setup with TeamForge, Database (including Datamart), Review Board, SCM (Subversion and Git), Code Search and Baseline installed on separate servers.
---

{% include inline_image.html file="status-success-small.png" %} In this [distributed setup][plan_your_installation_upgrade.html#singleordistributed], [TeamForge services][plan_your_installation_upgrade.html#teamforgeservices] are distributed across six servers, server-01 through server-06 as illustrated in the following table.<br><br> 
{% include inline_image.html file="status-success-small.png" %} You can install TeamForge on both {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}. In this distributed setup, all the following services are installed on {{site.data.identifiers.rhel_centos_now}} servers.


| server-01 | server-02 | server-03 | server-04 | server-05   | server-06 |
| TeamForge Application Server | TeamForge Database Server | Review Board Server | SCM Server | Code Search Server | Baseline Server |
|------------------------------|---------------------------|---------------|---------------------|------------|--------------------|-----------------|
| ctfcore  | ctfcore-database | reviewboard[^1] | subversion | codesearch | baseline[^2] |
| mail     | ctfcore-datamart |          | gerrit |          | baseline-post-install[^3] |
| etl      | gerrit-database |          |  |          | baseline-database |
| search   | binary-database |          |          |          |       |
| reviewboard-adapter[^4] | reviewboard-database |          |          |          |      |
| binary | webr-database | | | | |
| cliserver | | | | | |
| webr| | | | | |
| service-monitor| | | | | |

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

## Prepare the Servers for TeamForge Installation (server-01 through server-06)

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

1. Install the TeamForge application packages on the TeamForge Application Server (server-01).
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

   Install the Baseline packages on the TeamForge Application Server (server-01), if you are installing TeamForge Baseline.
   ```shell
   yum install teamforge-baseline
   ````  

2. Install the database packages and the Baseline packages on the TeamForge Database Server (server-02) based on the following conditions:

   * On sites without TeamForge Baseline, run this command to install the database packages on the TeamForge Database server (server-02).
 
     ```
     yum install teamforge-database
     ````

   * On sites with TeamForge Baseline, if you're installing TeamForge Baseline on a separate server (server-07), run this command to install both the Baseline packages and the database packages on the TeamForge Database server (server-02).
   
     ```
     yum install teamforge-baseline
     ````

3. Install Review Board packages on the Review Board Server (server-03).

   ```shell
   yum install teamforge
   ````

5. Install SCM packages on the SCM Server (server-04).
   ```shell
   yum install teamforge-scm teamforge-git
   ````

6. Install the Code Search packages on the Code Search Server (server-05).
   ```shell
   yum install teamforge-codesearch
   ````
7. Install the Baseline packages on the Baseline Server (server-06).
   ```shell
   yum install teamforge-baseline
   ````

## Set up Your Site's Master Configuration File

1. Do this on the TeamForge Database Server (server-02).
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````

   ### host:SERVICES Token
   ```shell
   server-01:SERVICES=ctfcore service-monitor search mail etl binary reviewboard-adapter cliserver webr 
   server-02:SERVICES=ctfcore-database ctfcore-datamart gerrit-database binary-database reviewboard-database webr-database
   server-03:SERVICES=reviewboard
   server-04:SERVICES=subversion gerrit
   server-05:SERVICES=codesearch
   server-06:SERVICES=baseline baseline-post-install baseline-database
   ````

   ### host:PUBLIC_FQDN Token
   ```shell
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````

   Save the `site-options.conf` file.

   {% unless site.output == "pdf" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): {% include installupgrade/site_options_config.html %}
   {% endunless %}

   {% unless site.output == "web" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): [Set up Your Site's Master Configuration File][for_pdf_site_options_config].
   {% endunless %}

2. Provision the Database Server (server-02).
   ```shell
   teamforge provision
   ````

2. Copy the `/opt/collabnet/teamforge/etc/site-options.conf` file from the TeamForge Database Server (server-02) to the `/opt/collabnet/teamforge/etc/` directory of all other servers.

## Provision Services on All the Servers

1. {% include installupgrade/deploy_services_with_note.html %}

   {% include inline_image.html file="status-success-small.png" %} You must provision services in a particluar sequence. Usually you start with the Database Server, followed by the Application Server and then by other servers such as SCM, Review Board and Code Search servers.<br><br>
   {% include inline_image.html file="status-success-small.png" %} The TeamForge installer derives this sequence from your `site-options.conf` file and shows you the order of provisioning servers when you try to provision one of the distributed servers. Follow the exact sequence as instructed.

### Provisioning Sequence without Baseline

   1. Provision the Application Server (server-01).
   2. Provision the SCM server (server-05).
   3. Provision the Review Board Server (server-03).
   5. Provision the Code Search Server (server-06).

### Provisioning Sequence with Baseline

   1. Provision the Application Server (server-01).
   2. Provision the Baseline Server (server-07).
   3. Copy the `/opt/collabnet/teamforge/etc/site-options.conf` file from the TeamForge Baseline Server (server-07) to the `/opt/collabnet/teamforge/etc/` directory of all other servers.
   4. Provision the Database Server (server-02) again.
   5. Provision the Application Server (server-01) again.
   6. Provision the SCM server (server-05).
   7. Provision the Review Board Server (server-03).
   8. Provision the Code Search Server (server-05).

{% include installupgrade/reinitialize_teamforge.html %}

## Verify TeamForge Installation

1. {% include installupgrade/verify_installation.html %}

{% include installupgrade/postinstalltasks.html %}

{{site.data.alerts.hr_shaded}}
[^1]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
[^2]: It's highly recommended that you install the [TeamForge Baseline][baseline-overview] services on a separate server as the baselining process can consume considerable CPU and database resources.
[^3]: Synchronizes the user information between the baseline database and TeamForge database.
[^4]: `reviewboard-adapter` must always be installed on the TeamForge Application Server.

{% include links.html %}