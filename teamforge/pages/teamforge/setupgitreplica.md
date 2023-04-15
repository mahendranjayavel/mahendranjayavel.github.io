---
title: Set up Git Replica Servers
keywords: git, replica
tags: [ctf_22.1, ctf_21.3, ctf_20.2, git_gerrit, integration, source_code, installation, upgrade, replica]
sidebar: teamforge_sidebar
permalink: setupgitreplica.html
last_updated: Dec 07, 2022
layout: "page_without_h3_in_toc"
summary: On sites distributed across multiple geographic locations, Git Replica Servers are local and remote mirror servers that can provide up-to-date copies of the central repositories. If set up, Git Replica Servers can address load balancing and fetch performance issues. You can set up one or more Git Replica Servers (also referred to as slave or mirror servers) with TeamForge 8.1 and later.
---
## Set up a Git Replica Server

* A Git Replica Server has one and only one `master` Git server.
* It's not possible to set up both Git master and slave on the same server. However, you can have multiple master and slave servers in your TeamForge environment.
* Git replication servers can be set up with TeamForge 8.1 or later only.

You can have your master Git integration server installed on the TeamForge Application Server or on a separate server dedicated to Git/SCM integration.

{% include image.html file="setupgitreplicaserver01.png" caption="TeamForge and Git (master) on the Same Server" %}

{% include image.html file="setupgitreplicaserver02.png" caption="TeamForge and Git (master) on Separate Servers" %}

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">

* Make sure you have upgraded your Git integration to TeamForge-Git v8.4.6 or later.
* Have the master Git integration server's `externalSystemId` handy.
  
  Open the `/opt/collabnet/gerrit/etc/gerrit.config` file on the master Git integration server and note down the `externalSystemId` from the **[teamforge]** section.

  Alternatively, log on to the TeamForge Application Server as a Site Administrator, click **Admin > Integrations > SCM Integrations**, select the master Git integration server, click **Edit** and look for a token such as `exsy####`, for example `exsy1002`, in the browser URL. This is the external system ID of your Git integration server.

* Open the TeamForge Application Server's `site-options.conf` file and keep the values of the following tokens handy.

  ```conf
  SCM_DEFAULT_SHARED_SECRET=
  ````

  Note down the values of the following tokens if and only if obfuscation is enabled (`OBFUSCATION_ENABLED=true`):

  ```conf
  OBFUSCATION_ENABLED=
  OBFUSCATION_KEY=
  OBFUSCATION_PREFIX=
  ```
* Note down the value of the `AUTO_DATA` token. 
</div>
</div>

1. {% include installupgrade/install_rhel_centos_now.html %}
2. Check your basic networking setup. See [Set up Networking][setupnetworking] for more information.
3. {% include installupgrade/yum_upgrade.html %}
4. Reboot the server.

   ```linux
   reboot
   ````

{% unless site.output == "pdf" %}
5. {% include installupgrade/installrepoconfig.html %}
{% endunless %}

{% unless site.output == "web" %}
5. [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}

6. Install the Git packages.

   ```linux
   yum install teamforge-git
   ````

7. Set up the `site-options.conf` tokens for the Git Replica Server.

   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````

   {% capture cap2 %}
   It is assumed that:<br>

   {% include inline_image.html file="status-success-small.png" %} `my.app.domain.com` is the Fully Qualified Domain Name (FQDN) of your TeamForge Application Server.<br><br>
   {% include inline_image.html file="status-success-small.png" %} `my.git.domain.com` is the Fully Qualified Domain Name (FQDN) of your Git Integration Server.<br><br>
   {% include inline_image.html file="status-success-small.png" %} `my.gitreplica.domain.com` is the Fully Qualified Domain Name (FQDN) of your Git Replica Server.
   {% endcapture %}
   {% include callout.html type="primary" content=cap2 %}

   1. Set up the `SERVICES` tokens.

      ```conf
      my.gitreplica.domain.com:SERVICES=gerrit gerrit-database
      my.app.domain.com:SERVICES=ctfcore ctfcore-database ctfcore-datamart etl search subversion binary binary-database
      ````

      Note: Make sure you do not have the `gerrit gerrit-database` services to the `my.app.domain.com:SERVICES` token in the `/opt/collabnet/teamforge/etc/site-options.conf` file of the Git replica server. 

   2. Turn on the SSL for your site by editing the relevant variables in the `site-options.conf` file. To generate the SSL certificates, see [Generate SSL Certificates][generatesslcerts].

      ```conf
      SSL=on
      SSL_CERT_FILE=
      SSL_KEY_FILE=
      SSL_CHAIN_FILE=
      ````

      * The SSL_CHAIN_FILE is optional.
      * If you use certificates that are generated in-house, self-signed, or signed by a non-established Certificate Authority, they must be registered with each client system that will connect to the TeamForge server.
      * For the setup discussed in this topic, add the certificate of `my.app.domain.com` to the JVM of `my.git.domain.com` and `my.gitreplica.domain.com`. In addition, add the certificate of `my.gitreplica.domain.com` to the JVM of `my.git.domain.com`. [Click here][sslforintegrations] for more information.
   
   3. Set the gerrit replication server mode.

      ```conf
      GERRIT_REPLICATION_MODE=slave
      ````

   4. Set the external system ID of the master Git integration server.

      ```conf
      GERRIT_REPLICATION_MASTER_EXTERNAL_SYSTEM_ID=exsy####
      ````

   5. Set the obfuscation related tokens.
   6. Save the `site-options.conf` file.

8. {% include installupgrade/deploy_services_without_note.html %}

Now, the gerrit service is running in replica mode. You can now find the newly created Git Replica Server listed on TeamForge Application Server by accessing the following url: `http://<TF_HOST>/sf/sfmain/do/listSystems`.

Once you have set up one or more Git Replica Servers, you can replicate repositories.

## Upgrade Git Replica Servers

{% include important.html content="When upgrading TeamForge-Git integration servers, it is important that Git master and slave servers are upgraded to the same version of  TeamForge-Git integration. On sites with Git Replica Servers, you must upgrade the Git Replica Servers first and then upgrade the master Git servers. For more information about upgrading master Git servers, see TeamForge upgrade instructions." %}

To upgrade existing Git Replica Servers:

1. Log on to the Git Replica Server and move the existing TeamForge repository from `/etc/yum.repos.d`.
2. Remove the `collabnet-teamforge-internal-repo.rpm`.

   ```shell
   yum erase collabnet-teamforge-internal-repo rpm
   ```

{% unless site.output == "pdf" %}
3. {% include installupgrade/installrepoconfig_second.html %}
{% endunless %}

{% unless site.output == "web" %}
3. [Configure the TeamForge installation repository][for_pdf_installrepoconfig].
{% endunless %}
4. Refresh your repository cache.

   ```shell
   yum clean all
   ````

5. Upgrade the Git packages.

   ```linux
   yum install teamforge-git
   ````

6. {% include installupgrade/deploy_services_without_note.html %}

## Replicate Repositories with Git Replica Servers {#replicategitrepo}

It is assumed that you already have one or more Teamforge projects that consists of one or more Git repositories that you want to replicate.

1. To start replicating a repository--go to the TeamForge project--select the Git repository you want to replicate, select the **Settings** tab and then select the **Replicas** tab.
   {% include image.html file="replicatab.png" %}

   This page lists the available Git Replica Servers.
2. From the list of Replica Servers, click the **Add** button of one or more Replica Servers to have the server(s) replicate the selected repository.
   {% include image.html file="replicatab01.png" %}
3. Click **Save**.
4. Push a commit and verify if it's replicated on the Replica Servers.

## Remove a Git Replica Server

1. Go to **Admin > Integrations**, select the Git replica server, and click **Delete**.

   This removes the replica server configured for the Git repositories from the UI.

   {% include image.html file="22.0-git-replica-01.png" %}

## Re-add a Git Replica Server

1. To add the git replica server again, you must remove the server from UI by clicking **Delete** from **Admin > Integrations** page.
2. Comment out or remove the slave section of the `/opt/collabnet/gerrit/etc/gerrit.config` file.

   ```conf
         [plugin "teamforge-slave"]
             metricsPrefix = teamforge
             allowGroup = Administrators
             replicaId = replica1001
   ````

3. Provision TeamForge services.

   ```conf
   teamforge provision
   ````

   The re-added replica server has no repositories configured for replication. You must configure repository replication again for the repositories you want. For more information, see [Replicate Repositories with Git Replica Servers][setupgitreplica.html#replicategitrepo].

#### Related Links

* [Restore the Git Replica Servers by Bootstrapping][gitgerrit-faqs.html#restorereplica]
* [How do I use a replicated Git repository from the client?][gitgerrit-faqs.html#usereplicaongitclient]
* [Replicate a Subversion Repository][replicatearepository]

{% include links.html %}
