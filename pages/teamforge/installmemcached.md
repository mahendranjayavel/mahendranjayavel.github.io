---
title: Install Memcached
keywords: memcached, caching with memcached, mod_authnz_ctf, authentication, authorization
tags: [ctf_20.2, ctf_20.0, installation, authentication]
sidebar: teamforge_sidebar
permalink: installmemcached.html
last_updated: Jul 13, 2020
toc: no
summary: Memcached caches Subversion (SVN) authentication and authorization information and serves the mod_authnz_ctf module's authentication and authorization requests thereby reducing the number of SOAP calls, which in turn results in less load on the TeamForge Application Server.
---

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">
* See this [wiki page](https://en.wikipedia.org/wiki/Memcached) for more information about Memcached.
* Memcached can run on the TeamForge Application Server or on a separate server (in case Subversion is on a separate server). This document assumes that you install Memcached on the TeamForge Application Server that also hosts Subversion.
</div>
</div>

## Do This on the TeamForge Application Server

1. Install Memcached.

   Add the `subversion-caching` identifier to the `SERVICES` token. For example:

   ```shell
   localhost:SERVICES=ctfcore ctfcore-database mail etl ctfcore-datamart search subversion codesearch cliserver gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter subversion-caching
   ````

   It is also possible to use an externally managed Memcached server. To use an externally managed Memcached server, add the `subversion-caching` service to the `SERVICES` token as shown below:
   ```shell
   localhost:SERVICES=ctfcore ctfcore-database mail etl ctfcore-datamart search subversion codesearch cliserver gerrit gerrit-database binary binary-database reviewboard reviewboard-database reviewboard-adapter
   myexternalmemcachedserver:SERVICES=subversion-caching
   ````
   Where, `myexternalmemcachedserver` hosts the Memcached service.


2. Configure the OPTIONS key in the Memcached configuration file (`/etc/sysconfig/memcached`) and start Memcached.
   
   The OPTIONS key in the memcached configuration file is used to set additional options during Memcached startup. Add the -l <ip-addr> flag to have Memcached listen to <ip_addr>. This is an important option to consider as there is no other way to secure the installation. Binding to an internal or firewalled network interface is recommended.
   
   ```shell
   vi /etc/sysconfig/memcached
   ````

   {% include important.html content="Remove the -l flag from the OPTIONS key to have Memcached listen to the server's default IP address or host name, including the 'localhost'." %}

3. {% include installupgrade/deploy_services_without_note.html %}


{% include links.html %}