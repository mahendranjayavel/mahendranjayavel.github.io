---
title: Install All Services on a Single RHEL/CentOS Server
keywords: dedicated installation, single server setup
tags: [ctf_20.2, ctf_20.0, ctf_19.3, ctf_19.1, ctf_19.0, installation]
sidebar: teamforge_sidebar
permalink: allinoneserver_rhel_centos.html
last_updated: Aug 6, 2020
layout: "page_without_h3_in_toc"
summary: The easiest way to install TeamForge is to install it on a single server, dedicated to TeamForge taking the default configuration settings.
---

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

<!-- Installation Setup  -->

## Single Server Setup

You can install TeamForge on both {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}. In this [single server setup][plan_your_installation_upgrade.html#singleordistributed], all the following [TeamForge services][plan_your_installation_upgrade.html#teamforgeservices] are installed on a single RHEL/CentOS server.

### TeamForge Application Server (server-01)

* TeamForge Application Server (ctfcore)
* Database Server (ctfcore-database and ctfcore-datamart)
* Mail Server (mail)
* Code Search Server (codesearch)
* ETL Server (etl)
* Git Integration Server (gerrit and gerrit-database)
* Review Board (reviewboard, reviewboard-database and reviewboard-adapter)[^1]
* Binary (binary and binary-database)
* SCM Integration Server (subversion)
* Search Server (search).
* CLI Server (cliserver)
* TeamForge Baseline (baseline, baseline-database, baseline-post-install)[^2]
* TeamForge Webhooks-based Event Broker (webr webr-database)
* Service Monitor (service-monitor)

<!-- Installation Setup  -->

<!-- Installation Steps -->

## Do This Step by Step on the TeamForge Application Server (server-01)

1. Install {{site.data.identifiers.rhel_centos_now}} or {{site.data.identifiers.rhel_centos_past}} and log on as root.
   {% capture rhnetwork %}
   {% include inline_image.html file="status-success-small.png" %} The host must be registered with the Red Hat Network if you are using Red Hat Enterprise Linux.<br><br>
   {% include inline_image.html file="status-success-small.png" %} See the [{{site.data.identifiers.rhel_centos_now}} Installation Guide](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/index.html) or [RHEL {{site.data.identifiers.rhel_centos_past}} Installation Guide](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/6/html/Installation_Guide/index.html) for help.<br><br>
   {% include inline_image.html file="status-success-small.png" %} Delete the python-crypto package if you are installing TeamForge on {{site.data.identifiers.rhel_centos_past}}. `yum erase python-crypto`
   {% endcapture %}
   {% include callout.html type="primary" content=rhnetwork %}
   
2. Check your networking setup. See [Set up Networking][setupnetworking] for more information.

{% unless site.output == "pdf" %}
3. {% include installupgrade/installrepoconfig.html %}
{% endunless %}

{% unless site.output == "web" %}
3. [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

4. Install the TeamForge application packages.
   
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

   Install the Baseline packages.
   ```shell
   yum install teamforge-baseline
   ````   
   
{% unless site.output == "pdf" %}
5. Set up your site's master configuration file.
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````
   ### host:SERVICES Token
   ```shell
   server-01:SERVICES=ctfcore ctfcore-database service-monitor search mail codesearch etl ctfcore-datamart subversion gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter cliserver baseline baseline-database baseline-post-install webr webr-database
   ````
   {% include note.html content="You may remove the identifiers of components you do not want. For example, remove `baseline baseline-database baseline-post-install` if you are not planning to install the TeamForge Baseline tool. See [TeamForge services](plan_your_installation_upgrade.html#teamforgeservices) for more information." %}

   ### host:PUBLIC_FQDN Token
   ```shell
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````

   Save the `site-options.conf` file. 

   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): {% include installupgrade/site_options_config.html %}

{% endunless %}

{% unless site.output == "web" %}
5. Set up your site's master configuration file.
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````
   ### host:SERVICES Token
   ```shell
   server-01:SERVICES=ctfcore ctfcore-database service-monitor search mail codesearch etl ctfcore-datamart subversion gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter cliserver baseline baseline-database baseline-post-install webr webr-database
   ````
   {% include note.html content="You may remove the identifiers of components you do not want. For example, remove `baseline baseline-database baseline-post-install webr webr-database` if you are not planning to install the TeamForge Baseline and Webhooks-based Event Broker tools. See [TeamForge services](plan_your_installation_upgrade.html#teamforgeservices) for more information." %}

   ### host:PUBLIC_FQDN Token
   ```shell
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````

   Save the `site-options.conf` file. 

   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): [Set up Your Site's Master Configuration File][for_pdf_site_options_config].
{% endunless %}

6. {% include installupgrade/deploy_services_with_note.html %}

7. {% include installupgrade/verify_installation.html %}

{% include installupgrade/postinstalltasks.html %}

<!-- Installation Steps -->

{{site.data.alerts.hr_shaded}}
[^1]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}. 
[^2]: It's highly recommended that you install the [TeamForge Baseline][baseline-overview] services on a separate server as the baselining process can consume considerable CPU and database resources. For more information, see [Install TeamForge in a Distributed Setup][distributed_install_rhel_centos].


{% include links.html %}