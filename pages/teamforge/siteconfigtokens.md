---
title: TeamForge Services and Domain Configuration Tokens
keywords: site-options.conf, site option tokens
tags: [ctf_20.0, ctf_19.2, installation, upgrade, site-options.conf, config_files, site_admin_tasks, security]
sidebar: teamforge_sidebar
permalink: siteconfigtokens.html
last_updated: Jan 19, 2020
toc: true
layout: "page_without_h3_in_toc"
summary: Use the host:SERVICES and the host:PUBLIC_FQDN tokens to define the services and domain names of your TeamForge site respectively. You can also have unique service-specific FQDNs for services such as Subversion, Git, mail, Codesearch and so on.
---

## host:SERVICES

The `host:SERVICES` token is used to define the TeamForge services running on a host. 

The syntax for defining the services running on a TeamForge host is:

```shell
<hostname>:SERVICES = list of services separated by space
````
Where `<hostname>` can be `localhost` or the server name as returned by the `hostname` command on the console. The latter is recommended as this allows reuse of the same ``site-options.conf`` file across all servers in a distributed setup. Here's a few examples.

### Example—Default Single-server Setup
```shell
localhost:SERVICES=ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch subversion
````

### Example—Single-server Setup with Git Integration
```shell
localhost:SERVICES=ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch subversion gerrit gerrit-database
````

### Example—Single-server Setup with Review Board Integration
```shell
localhost:SERVICES=ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch subversion reviewboard reviewboard-database 
````

### Example—Three-server Setup with Git and Binary Integration
```shell
server01:SERVICES=ctfcore etl mail search codesearch binary binary-database
server02:SERVICES=subversion gerrit
server03:SERVICES=ctfcore-database ctfcore-datamart gerrit-database
````

### Example—Distributed Setup with Multiple Git Integration Servers
```shell
server01:SERVICES=ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch binary binary-database
server02:SERVICES=subversion
server-03:SERVICES=gerrit gerrit-database
server-04:SERVICES=gerrit gerrit-database
````

## host:PUBLIC_FQDN {#hostpublic_fqdn} 
The `host:PUBLIC_FQDN` token is used to define the domain name of your TeamForge site. Assign a public FQDN (optional, but strongly recommended). Make sure there is a DNS A or CNAME record for this FQDN. Here's a few examples.

```shell
server01:PUBLIC_FQDN = teamforge.example.com
server02:PUBLIC_FQDN = scm.example.com
````

<!-- Artifact artf394570 : [doc] self signed certs to include SAN -->
{% include important.html content="It is typical of browser clients not to trust self-signed SSL certificates that do not have the Subject Alternatine Name (SAN) configuration. Configuring the PUBLIC_FQDN token in TeamForge is necessary to have SAN/DNS entries configured in the self-signed SSL certificate you generate." %}

<!-- https://forge.collab.net/sf/go/artf301286#6 -->
<!-- {% include note.html content="You cannot have a separate PUBLIC_FQDN for EventQ." %} -->

### Service-specific FQDNs {#servicespecificfqdns}

Installing TeamForge with service-specific FQDNs (instead of machine-specific host/domain names) is highly recommended so that you will be able to change the system landscape at a later point in time without having any impact on the URLs (in other words, end users do not have to notice or change anything). Service-specific FQDNs come in handy when you want to get started with a single server and later distribute TeamForge across multiple servers as you scale up.

For example, you can create FQDNs specifically for services such as Subversion, Git, mail, Codesearch and so on.
* All such service-specific FQDNs must belong to a single sub domain and it is recommended to create a new sub domain for TeamForge.
* A wildcard SSL cert is required if you are using service-specific FQDNs. SNI SSL cert cannot be used.
* When no custom SSL-certificates are provided, a self-signed wildcard cert is generated for the sub domain.
* When a custom SSL-certificate is provided, the CN of the certificate is verified to be a wildcard CN.

<!-- https://forge.collab.net/sf/go/artf304560#2 -->
{% include note.html content="TeamForge has no support for having service-specific FQDN for Review Board." %}

### Services and Domain Configuration Examples

* Here's an example to illustrate the Services and FQDN tokens in a single-server setup with unique service-specific FQDNs for ctfcore, subversion, gerrit and mail.

  ```shell
  # host:SERVICES token
  localhost:SERVICES = ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch reviewboard reviewboard-database reviewboard-adapter binary binary-database cliserver webr webr-database subversion gerrit gerrit-database

  # host:PUBLIC_FQDN token
  localhost:PUBLIC_FQDN = app.forge.collab.net

  # Service-specific FQDNs
  localhost:ctfcore:PUBLIC_FQDN = ctf.forge.collab.net
  localhost:subversion:PUBLIC_FQDN = svn.forge.collab.net
  localhost:gerrit:PUBLIC_FQDN = git.forge.collab.net
  localhost:mail:PUBLIC_FQDN = mail.forge.collab.net
  ````

  In this single server setup, all these domain names point to a single server. However, when services are later distributed across multiple servers, all it takes to avoid an end user impact is to adjust these domain names to point to different servers.

* Here's an example to illustrate the Services and FQDN tokens in a two-server distributed setup with unique service-specific FQDNs for Subversion and Git.
<!-- https://forge.collab.net/sf/go/artf391846#2 -->

  ```shell
  # host:SERVICES tokens
  apphost:SERVICES = ctfcore ctfcore-database ctfcore-datamart etl mail search codesearch reviewboard reviewboard-database reviewboard-adapter binary binary-database cliserver webr webr-database gerrit-database
  svngithost:SERVICES = subversion gerrit

  # host:PUBLIC_FQDN tokens
  apphost:PUBLIC_FQDN=my.app.domain.com
  svngithost:PUBLIC_FQDN=my.app.domain.com

  # Service-specific FQDNs for Subversion and Git
  svngithost:subversion:PUBLIC_FQDN=svn.app.domain.com
  svngithost:gerrit:PUBLIC_FQDN=git.app.domain.com
  ````

  Where: 
  * `apphost` is the TeamForge Application Server.
  * `svngithost` is the SCM Server that hosts Subversion and Git.



{% include links.html %}