---
title: Upgrade TeamForge on New Hardware in a Distributed Multi-host Setup
keywords: new hardware, multi-host, multihost, upgrade
tags: [ctf_21.1, ctf_21.0, ctf_20.2, ctf_20.0, ctf-19.3, ctf_19.0, upgrade, site_admin_tasks, backup_restore]
sidebar: teamforge_sidebar
permalink: new_hardware_upgrade_multi_host.html
last_updated: Jul 06, 2021
layout: "page_without_h3_in_toc"
summary: You can upgrade TeamForge on new hardware in a distributed multi-host setup.
---

In this [distributed setup][plan_your_installation_upgrade.html#singleordistributed], [TeamForge services][plan_your_installation_upgrade.html#teamforgeservices] are distributed across multiple servers as illustrated in the following table.

| server-01                     | server-02                  | server-03      | server-04            | server-05   | server-06           |
| TeamForge Application Server | TeamForge Database Server | Review Board Server | SCM Server | Code Search Server | Baseline Server |
|------------------------------|---------------------------|---------------|---------------------|------------|--------------------|
| ctfcore  | ctfcore-database | reviewboard[^1] | subversion | codesearch | baseline[^2] |
| mail     | ctfcore-datamart |       | gerrit |          | baseline-post-install[^3] |
| etl      | gerrit-database |        |  |          | baseline-database |
| search   | binary-database |        |          |          |       |
| reviewboard-adapter[^4] | reviewboard-database |          |          |          |          |
| binary | webr-database | | | | |
| cliserver | | | | | |
| webr | | | | | |
| service-monitor | | | | | |


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

{% include installupgrade/onehop.html %}

<!-- Installation Dos and Don'ts -->

{% include installupgrade/teamforge-license-211-and-later.html %}

{% include installupgrade/cvseol-upgrade.html %}

{% include installupgrade/eventqendoflife.html %}

{% include installupgrade/chmodsubversionbaserepo.html %}   

## Prepare the New Servers for TeamForge Installation (server-01 through server-07)

1. Install {{site.data.identifiers.rhel_centos_now}} and log on as root.
   {% capture rhnetwork %}
   {% include inline_image.html file="status-success-small.png" %} The host must be registered with the Red Hat Network if you are using Red Hat Enterprise Linux.<br><br>
   {% include inline_image.html file="status-success-small.png" %} See the [{{site.data.identifiers.rhel_centos_now}} Installation Guide](http://docs.redhat.com/docs/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/index.html) for help.
   {% endcapture %}
   {% include callout.html type="primary" content=rhnetwork %}
   
2. Check your networking setup. See [Set up Networking][setupnetworking] for more information.

{% unless site.output == "pdf" %}
3. {% include installupgrade/installrepoconfig_upgrade.html %}
{% endunless %}

{% unless site.output == "web" %}
3. [Configure the TeamForge installation repository][for_pdf_installrepoconfig_upgrade].
{% endunless %}

## Install the TeamForge Services

1. Install TeamForge application services on the TeamForge Application Server (server-01).
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
   
    3. Install the baseline packages on the TeamForge Application Server (server-01), if you are installing TeamForge Baseline.
       ```shell
       yum install teamforge-baseline
       ````
   
2. Install the database and baseline packages on the TeamForge Database Server (server-02).

   ```shell
   yum install teamforge-baseline
   ````
   {% include important.html content="The `yum install teamforge-baseline` command installs both the database and baseline packages. In case you don't install the TeamForge Baseline, you must use the `yum install teamforge-database` command to install the database packages." %}

3. Install Review Board services on the Review Board Server (server-03).

   ```shell
   yum install teamforge
   ````

4. Install SCM services on the SCM Server (server-04).
   ```shell
   yum install teamforge-scm teamforge-git
   ````

5. Install the Code Search service on the Code Search Server (server-05).
   ```shell
   yum install teamforge-codesearch
   ````

6. Install the Baseline packages on the Baseline Server (server-06).
   ```shell
   yum install teamforge-baseline
   ````

## Back up and Restore TeamForge Database, Data Directories and site-options.conf
See [Back up and Restore TeamForge Database, Data Directories and site-options.conf][backupandrestore.html#backupteamforge].

## Back up and Restore Review Board Database and Data Directories
See [Back up and Restore Review Board][backupandrestore.html#backuprb].

## Disable OID While Upgrading to TeamForge 22.0 or later

Do this on the Database Server (server-02) if you are upgrading from TeamForge 21.2 or earlier to TeamForge 22.0 or later. 

TeamForge 22.0 supports PostgreSQL {{site.data.identifiers.postgres_short}}. As a result, you must run the `/opt/collabnet/teamforge/dist/scripts/disable_oid_pg_upgrade13.py` script to disable the object identifiers (OIDs) before provisioning TeamForge services.

```shell
/opt/collabnet/teamforge/dist/scripts/disable_oid_pg_upgrade13.py
```` 

## Import the SSL Certs to the Java Keystore
<!-- [artf417891] Doc changes needed for upgrade CTF on new hardware to support OS centos/rhel8 -->
Do this on the TeamForge Application Server (server-01). 

1. Locate the Java keystore. 
   
   This is `PATH_TO_JAVA/jre/lib/security/cacerts`. For example, this may be `/usr/local/j2sdk1.4.2_10/jre/lib/security/cacerts`.
2. Locate the Java keytool utility.

   This is `PATH_TO_JAVA/bin/keytool` For example, `/usr/local/j2sdk1.4.2_10/bin/keytool`.
3. Import the certificate into the keystore.
   
   ```shell
   PATH_TO_JAVA/bin/keytool -import -keystore PATH_TO_JAVA/jre/lib/security/cacerts -file <server>.crt -alias <server>
   ````
   {% include note.html content="Any value is accepted for server in -alias <server>." %}

## Set up the site-options.conf File

1. Log on to the new TeamForge Database Server (server-02) and copy the backed up `site-options.conf` file to the TeamForge installer directory.
   ```shell
   cp /tmp/site-options.conf /opt/collabnet/teamforge/etc/
   ````

2. Do this on the TeamForge Database Server (server-02).
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
   
   {% include tip.html content="Remove server-06 in case you are not installing TeamForge Baseline." %}
 
   ### host:PUBLIC_FQDN Token
   ```shell
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````

   Save the `site-options.conf` file.

   {% unless site.output == "pdf" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): {% include installupgrade/site_options_config_upgrade.html %}
   {% endunless %}

   {% unless site.output == "web" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): [Set up Your Site's Master Configuration File][for_pdf_site_options_config_upgrade].
   {% endunless %}

3. {% include installupgrade/deploy_services_with_note.html %}   

4. Copy the `/opt/collabnet/teamforge/etc/site-options.conf` file from the TeamForge Database Server (server-02) to the `/opt/collabnet/teamforge/etc/` directory of all other servers.

   {% include important.html content="Copy the SSL certificate file, SSL chain file, and the TeamForge site's private RSA key file from the TeamForge Application Server (from the path as specified in the `site-options.conf` tokens [SSL_CERT_FILE][siteoptiontokens.html#SSL_CERT_FILE], [SSL_CHAIN_FILE][siteoptiontokens.html#SSL_CHAIN_FILE], and [SSL_KEY_FILE][siteoptiontokens.html#SSL_KEY_FILE]) to Subversion, Gerrit, and Baseline servers." %}

## Provision Services on All the Servers

{% include installupgrade/openjdk.html %}

1. {% include installupgrade/deploy_services_with_note.html %}

   {% include inline_image.html file="status-success-small.png" %} You must provision services in a particluar sequence. Usually you start with the Database Server, followed by the Application Server and then by other servers such as SCM, Review Board and Code Search servers.<br><br> 
   {% include inline_image.html file="status-success-small.png" %} The TeamForge installer derives this sequence from your `site-options.conf` file and shows you the order of provisioning servers when you try to provision one of the distributed servers. Follow the exact sequence as instructed.

### Provisioning Sequence without Baseline

   1. Provision the Application Server (server-01)
   2. Provision the SCM server (server-04) 
   3. Provision the Review Board Server (server-03)
   4. Provision the Code Search Server (server-05)

### Provisioning Sequence with Baseline

   1. Provision the Application Server (server-01)
   2. Provision the Baseline Server (server-06)
   3. Copy the `/opt/collabnet/teamforge/etc/site-options.conf` file from the TeamForge Baseline Server (server-07) to the `/opt/collabnet/teamforge/etc/` directory of all other servers.
   4. Provision the Database Server (server-02) again
   5. Provision the Application Server (server-01) again
   6. Provision the SCM server (server-04) 
   7. Provision the Review Board Server (server-03)
   9. Provision the Code Search Server (server-05)

### Delete Existing Elastic Search Indexes While Upgrading to TeamForge 22.0 or later

TeamForge 22.0 uses Elastic Search 7.16.3 to address the Log4j dependent vulnerabilities. As a result, you must delete the existing Elastic Search indexes as they might not be compatible with Elastic Search 7.16.3. The Elastic Search service would fail in this case. Use the `/opt/collabnet/teamforge/runtime/scripts/delete_es_nodes.py` script to delete the existing indexes. You must restart the Elastic Search service after deleting the old indexes. For more information, see TeamForge upgrade instructions.

While the existing `ELASTICSEARCH_JAVA_OPTS` token is still supported to configure the JAVA_OPTS values, the following tokens have been added to configure the minimum and maximum heap size for Elastic Search.
* ELASTICSEARCH_MIN_HEAP_SIZE=-Xms2g
* ELASTICSEARCH_MAX_HEAP_SIZE=-Xmx2g

In other words, in TeamForge 21.2 and earlier, you just had to configure `ELASTICSEARCH_JAVA_OPTS=-Xms2g -Xmx2g -Dlog4j2.formatMsgNoLookups=true`. 

Whereas, in TeamForge 22.0 and later, you must configure:
* ELASTICSEARCH_MIN_HEAP_SIZE=-Xms2g
* ELASTICSEARCH_MAX_HEAP_SIZE=-Xmx2g
* ELASTICSEARCH_JAVA_OPTS=-Dlog4j2.formatMsgNoLookups=true   

{% include installupgrade/reinitialize_teamforge.html %}

## Finishing Tasks
<!-- 1. {% include installupgrade/cvssyncpermissions.html %} -->
* {% include installupgrade/verify_installation_upgrade.html %}

{% include installupgrade/postupgradetasks.html %}

{{site.data.alerts.hr_shaded}}
[^1]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
[^2]: It's highly recommended that you install the [TeamForge Baseline][baseline-overview] services on a separate server as the baselining process can consume considerable CPU and database resources.
[^3]: Synchronizes the user information between the baseline database and TeamForge database.
[^4]: `reviewboard-adapter` must always be installed on the TeamForge Application Server.

{% include links.html %}