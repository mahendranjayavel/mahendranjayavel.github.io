---
title: Installation Requirements
keywords: teamforge installation upgrade requirements, ports, hardware requirements, software requirements, Phusion Passenger, Nginx
tags: [ctf_20.2, ctf_20.1, ctf_20.0, ctf_19.3, ctf_19.2, ctf_19.1, ctf_19.0, ctf_18.3, installation, upgrade, integration, getting_started, authentication, baseline, event_broker]
sidebar: teamforge_sidebar
permalink: requirements.html
last_updated: Jul 10, 2020
summary: Here's what it takes to install and run TeamForge and other integrations supported by TeamForge.
---
## TeamForge Hardware Requirements {#tfhardwarereq}

The following table lists the CPU, RAM and JVM Heap Size recommendations for Small, Medium, Large and Extra-large sites.

<div><table class="table">

<thead align="left" class="thead">
<tr class="row">
<th>&nbsp;</th>
<th>Small</th>
<th>Medium</th>
<th>Large</th>
<th>X-Large</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="row">
<td>Users</td>
<td>100</td>
<td>500</td>
<td>1000-5000</td>
<td>10000+</td>
</tr>
<tr class="row">
<td>CPU</td>
<td>Octa-core</td>
<td>12-core</td>
<td>&gt; 12-core</td>
<td>&gt; 16-core</td>
</tr>
<tr class="row">
<td>RAM</td>
<td>16GB</td>
<td>24GB</td>
<td>32GB</td>
<td>32GB</td>
</tr>
<tr class="row">
<td>Jboss JVM Heap Size</td>
<td>1.5GB</td>
<td>3GB</td>
<td>6GB</td>
<td>&gt; 8GB</td>
</tr>
<tr class="row">
<td rowspan="2">Elasticsearch JVM Heap Size</td>
<td>2GB</td>
<td>2GB</td>
<td>2GB</td>
<td>2GB</td>
</tr>
<tr class="row">
<td colspan="4">You must have adequate RAM to accomodate the JVM heap requirements of Elasticsearch in addition to the JVM heap requirements of other components such as Jboss, integrated applications, and so on.</td>
</tr>
<tr class="row">
<td colspan="5">200 GB (or more) hard drive. The required hard drive capacity depends on the estimated amount of document and file release uploads.</td>
</tr>
</tbody>
</table>
</div>

The following table highlights the factors that can impact TeamForge performance. Numbers are indicative. Anything more than the prescribed numbers may impact the performance.

<div>
<table class="table">
<thead align="left" class="thead">
<tr class="row">
<th>&nbsp;</th>
<th>Small</th>
<th>Medium</th>
<th>Large</th>
<th>X-Large</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="row">
<td>Artifacts</td>
<td>15000</td>
<td>70000</td>
<td>100000</td>
<td>100000</td>
</tr>
<tr class="row">
<td>Flex Fields</td>
<td>25</td>
<td>50</td>
<td>100</td>
<td>100</td>
</tr>
<tr class="row">
<td>Projects</td>
<td>20</td>
<td>80</td>
<td>500</td>
<td>500</td>
</tr>
<tr class="row">
<td>Integrations</td>
<td>0-1</td>
<td>0-2</td>
<td>0-2</td>
<td>0-2</td>
</tr>
<tr class="row">
<td>Integrated Applications</td>
<td>0-2</td>
<td>0-3</td>
<td>3+</td>
<td>3+</td>
</tr>
</tbody>
</table>
</div>

{% include important.html content="On Medium, Large, and X-Large sites, it is highly recommended that you install the TeamForge Application, Database, and SCM services on separate 64-bit servers based on the usage pattern." %}

## Gerrit Hardware Requirements {#gerrithardwarereq}

The following table lists the CPU, RAM and Gerrit JVM Heap Size recommendations for Small, Medium, and Large sites.

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
For X-Large setup, see [Gerrit Performance Cheat Sheet](downloads/Gerrit-Performance-Tuning-Cheat-Sheet.pdf).
{% endunless %}


<!-- Use this for pdf output -->
{% unless site.output == "web" %}
For X-Large setup, see <a href="https://docs.collab.net/teamforge203/downloads/Gerrit-Performance-Tuning-Cheat-Sheet.pdf">Gerrit Performance Cheat Sheet</a>.
{% endunless %}

<div><table class="table">

<thead align="left" class="thead">
<tr class="row">
<th>&nbsp;</th>
<th>Small</th>
<th>Medium</th>
<th>Large</th>
</tr>
</thead>
<tbody class="tbody">
<tr class="row">
<td>Fetch requests per day</td>
<td>100k</td>
<td>500k</td>
<td>1 Million</td>
</tr>
<tr class="row">
<td>CPU</td>
<td>4-core</td>
<td>16-core</td>
<td>32-core</td>
</tr>
<tr class="row">
<td>RAM</td>
<td>8GB</td>
<td>16GB</td>
<td>32GB</td>
</tr>
<tr class="row">
<td>Gerrit JVM Heap Size</td>
<td>4GB</td>
<td>12GB</td>
<td>28GB</td>
</tr>
<tr class="row">
<td colspan="4">200GB (or more) hard disk. The required hard disk capacity depends on the number and size of repositories.</td>
</tr>
</tbody>
</table>
</div>

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
{% include important.html content="These numbers are indicative. Adjust your hardware based on your Gerrit server's usage. To better understand Gerrit hardware requirements and performance tuning possibilities, see [Gerrit Performance Cheat Sheet](downloads/Gerrit-Performance-Tuning-Cheat-Sheet.pdf)." %}
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
{% include important.html content="These numbers are indicative. Adjust your hardware based on your Gerrit server's usage. To better understand Gerrit hardware requirements and performance tuning possibilities, see [Gerrit Performance Cheat Sheet](https://docs.collab.net/teamforge203/downloads/Gerrit-Performance-Tuning-Cheat-Sheet.pdf)." %}
{% endunless %}

<!-- ## EventQ Hardware Requirements {#eventqhardwarereq}

{% include important.html content="EventQ services can be collocated with TeamForge on the same physical server. If you do so, compare the hardware requirements for both TeamForge and EventQ and settle for the best possible hardware resources for your setup. It's always recommended to install EventQ on its own server for optimal scalability and performance." %}

### Single Host Installation Setup

This section outlines the hardware requirements for installing TeamForge EventQ services on a single server. The single-host installation places all three TeamForge EventQ services (`App Server`, `MQ Server`, and `DB Server`) on a single operating system. This configuration is designed for trials and moderate load, while the multi-host installation setup is provided as a first step toward scaling your TeamForge EventQ instance.

Prepare for installation by setting up:
* Host running {{site.data.identifiers.rhel_centos_past}} or {{site.data.identifiers.rhel_centos_now}}
* User credentials with sudo privileges on the host

| Description  | Services | CPU | RAM | Storage |
|---|------|-----|-----|---------|
|Single host setup with all EventQ services on the same server | App, DB and MQ servers | Quad-core 2.5 GHz | 8 GB| 74 GB |

### Multi-host Installation Setup

For high load instances or when performance is critical, install TeamForge EventQ services on separate servers or virtual machines.

Multi-host installation originates on a single server and installs core services and the TeamForge EventQ application on that first server (the `App Server`). Then, the installer remotely installs the database service on a second server (the `DB Server`) and the message queue service on a third server (the `MQ Server`).

Prepare for a multi-host installation by setting up:
* Empty hosts running RHEL or CentOS {{site.data.identifiers.rhel_centos_past}} or {{site.data.identifiers.rhel_centos_now}}
* User credentials with sudo privileges on all three hosts
* ssh routes from the App server host to the other two hosts

The following are minimum resource requirements:

| Description  | Service | CPU | RAM | Storage | Bandwidth |
|---|------|-----|-----|---------|------|
| EventQ App Server | App | Quad-core 2.5 GHz | 4 GB| 16 GB | 1 Gbps to DB Server |
| MongoDB DB Server | DB | Quad-core 2.5 GHz | 4 GB| 50 GB | 1 Gbps to App Server |
| AMQP Message Queue Server | MQ | Quad-core 2.5 GHz | 4 GB| 16 GB | NA | -->

## Baseline Hardware Requirements {#baselinehardwarereq}

It’s highly recommended that you install the TeamForge Baseline services on a separate server as the baseline process can consume considerable CPU and database resources. 

The following table lists the hardware requirements of the Baseline Server:

<table>
<tr>
<th>Description</th>
<th>Service</th>
<th>CPU</th>
<th>RAM</th>
<th>Storage</th>
</tr>
<tr>
<td>Baseline Application and Database Server</td>
<td width="100px">Application and Database</td>
<td width="100px">4-core</td>
<td width="100px">8GB</td>
<td width="400px">Directly proportional to the number and size of baselines created. Typically, baseline packages can be large in size. It's recommended to scale the storage according to your site's requirements.</td>
</tr>
</table>

## TeamForge Webhooks Event Broker Hardware Requirements {#webhookseventbroker}

TeamForge Webhooks-based Event Broker can be installed on the same server on which TeamForge is installed. 

The following table lists the hardware requirements for the Webhooks-based Event Broker:

<table>
<tr>
<th>Description</th>
<th>Service</th>
<th>CPU</th>
<th>RAM</th>
</tr>
<tr>
<td rowspan="3">TeamForge Webhooks Event Broker Application & Database Server</td>
<td width="100px" rowspan="3">Application & Database</td>
<td width="100px">2-core</td>
<td width="400px">4GB (Upto 100 messages/sec)</td>
</tr>
<tr>
<td width="100px">4-core</td>
<td width="400px">8GB (Between 100 - 400 messages/sec)</td>
</tr>
<tr>
<td width="100px">8-core</td>
<td width="400px">16GB (Above 400 messages/sec)</td>
</tr>
</table>

## TeamForge Software Requirements {#tfsoftwarereq}

TeamForge {{site.data.identifiers.teamforge}} supports the following platforms:
* {{site.data.identifiers.rhel_centos_past}}
* {{site.data.identifiers.rhel_centos_now}}

  <div class="well well-sm" markdown="1">
  * Do not customize your operating system installation. Select only the default packages list.
  * Red Hat Enterprise Linux servers must have access to the Red Hat Network or equivalent (satellite server, spacewalk, or RHN proxy).
  </div>

Here's a list of a few noteworthy software that are installed by default when you install TeamForge {{site.data.identifiers.teamforge}}:
* Apache HTTPD Server {{site.data.identifiers.apache_httpd_server}}
* JBoss {{site.data.identifiers.jboss_wildfly}}
* OpenJDK {{site.data.identifiers.openjdk}}[^1]
* Tomcat {{site.data.identifiers.tomcat}}
* PhantomJS {{site.data.identifiers.phantomjs}}
* Elasticsearch {{site.data.identifiers.elasticsearch}}
* Highcharts {{site.data.identifiers.highcharts}}
* Subversion
<!-- Artifact artf395499 : [DOC] Subversion upgraded to 1.10.2 but remains at 1.8.19 in EL6 -->
  * {{site.data.identifiers.subversion_rhel7_rhel8}} on {{site.data.identifiers.rhel_centos_past}}
  * {{site.data.identifiers.subversion_rhel7_rhel8}} on {{site.data.identifiers.rhel_centos_now}}
* Git/Gerrit {{site.data.identifiers.git_gerrit}}
* Review Board {{site.data.identifiers.review_board}}[^2]
* PostgreSQL Server {{site.data.identifiers.postgres_long}}
* PostgreSQL JDBC Driver {{site.data.identifiers.postgres_JDBC_driver}}
* Oracle Server {{site.data.identifiers.oracle_server}}
* Oracle Client {{site.data.identifiers.oracle_client}}
* Oracle JDBC Driver {{site.data.identifiers.oracle_JDBC_driver}}

  <div class="well well-sm" markdown="1">
  PostgreSQL {{site.data.identifiers.postgres_long}} is installed by default when you install TeamForge {{site.data.identifiers.teamforge}}. However, you can use Oracle if you want to. See [PostgreSQL or Oracle?][plan_your_installation_upgrade.html#postgresororacle] for more information.
  </div>

TeamForge {{site.data.identifiers.teamforge}} supports the following browsers:
* Google Chrome {{site.data.identifiers.google_chrome}}
* Mozilla Firefox {{site.data.identifiers.mozilla_firefox}}
* Microsoft Internet Explorer {{site.data.identifiers.microsoft_ie}}
* Microsoft Edge {{site.data.identifiers.msedge}}

  <div class="well well-sm" markdown="1">
    * Microsoft Internet Explorer 10 and earlier are not actively tested and supported.<br>
    * TeamForge user interfaces are best viewed at screen resolution of at least 1280 x 800 (or more) pixels.
  </div>
<!-- * Yum Package Manager {{site.data.identifiers.yum_package_manager}} -->

<!-- ## EventQ Software Requirements {#eventqsoftwarereq}

* SSH and SFTP clients are required, i.e. openssh-client. To test for this dependency, on the target server, issue the command: `sftp localhost`.
* `createrepo` package is required by the disconnected mode installation. To test for this dependency, on the target server, issue the command: `createrepo --version`.
* EventQ has a number of other open source software (such as Nginx, Redis and so on) dependencies, all of which are installed as part of the installation process. The following software services and their dependencies are installed:

  | [Nginx](http://nginx.org/) | Installed on EventQ App Server |
  | [Phusion Passenger](https://www.phusionpassenger.com/) | Installed on EventQ App Server |
  | [Redis](http://www.redis.io/) | Installed on EventQ App Server |
  | [MongoDB](http://www.mongodb.org/) | Installed on EventQ DB Server |
  | [RabbitMQ](http://www.rabbitmq.com/) | Installed on EventQ DB Server |

  {% include important.html content="In case you have an already existing instance of MongoDB and RabbitMQ, you may choose to use it instead of installing these services again. Make sure you have the required versions, though." %} -->

## Supported Integrations {#supportedintegrations}

TeamForge {{site.data.identifiers.teamforge}} supports the following integrations:

* SubversionEdge {{site.data.identifiers.subversion_edge}}
* ViewVC {{site.data.identifiers.viewvc}}
* Nexus 3 ({{site.data.identifiers.nexus3}})[^3]  
* Jira {{site.data.identifiers.jira}}
* TestLink {{site.data.identifiers.testlink}}
* Jenkins {{site.data.identifiers.jenkins}} 

## Port Requirements {#portreq}

### TeamForge Port Requirements {#tfportreq}

TeamForge components listen on a number of operating system ports. However, only a small subset must be exposed externally to enable users to access TeamForge services. Any port that is not absolutely needed must be closed.

You can select your open ports in one of these ways:
* Use the firewall configuration GUI tool that comes with your operating system. It's usually launched with a command like `system-config-selinux`.
* Open the `/etc/sysconfig/iptables` file and manually specify your open ports.

#### Ports Open to the Internet

Open the following operating system level ports. All other ports must be firewalled off to maintain security.

{% include important.html content="Do not open port 7080 or port 8080 to the Internet. These ports are only for communications between the TeamForge application and the source code integration service, when those two site components are running on separate boxes." %}

<table class="table" markdown="1">
<thead>
<th>Port</th>
<th>Description</th>
</thead>
<tr>
<td>22 (SSH)</td>
<td>Port 22 is the default port for the secure shell (SSH). This is required for basic SSH administrative functionality<!--  and for CVS, as all CVS transactions occur over SSH -->. 
If all Teamforge repositories are in SVN (the default for Teamforge), then this port should be closed to the public and only accessible to the system administrators. <br /><br />

If you have to expose SSH to the Internet, the best way to protect it is to require SSH keys and not allow password authentication, and do not permit root logins over SSH. If you must use local authentication for SSH, enforce regular password changes and password complexity.

{% include note.html content="If you have to expose SSH internally, limit access to the port to a bastion host if you can; otherwise limit it to specific trusted hosts or subnets." %}</td>
</tr>
<tr>
<td>25 (SMTP)</td>
<td>Port 25 is the default port for SMTP (email). TeamForge discussion forums include mailing list functionality that allows users to send email to the TeamForge server. 
The James mail server included with TeamForge listens on port 25 to accept this mail for processing.
</td>
</tr>
<tr>
<td>80 (http)</td>
<td>Port 80 is the default port for Web data transfer. We strongly recommend that you set up SSL and use port 80 only to redirect to port 443.
</td>
</tr>
<tr>
<td>443 (https)</td>
<td>Port 443 is the default port for encrypted Web data transfer (https). 
The Apache web server should be configured to encrypt all data so that it cannot be compromised by a third party with malicious intent. Apache can be configured to force all traffic to be sent over https, even when a request is sent via port 80 (http). <br /><br />
TeamForge can help you take care of this, if you tell it to. See Set up SSL for your TeamForge site for details.</td>
</tr>
<tr>
<td>29418 (Gerrit SSH)</td>
<td>Port 29418 is the default port which should be open for Gerrit SSH.</td>
</tr>
</table>

<!-- #### Ports for Internal Use Only

Open the `REPORTS_DATABASE_PORT`, if you are granting direct access to the datamart from specific IPs using the `REPORTS_DB_ACCESS_HOSTS` site-options.conf token.

{% include warning.html content="The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server has been deprecated in TeamForge 17.11. For more information, see [Create a Single Cluster for Both Database and Datamart][movedbdmintoonepginstance]." %} -->

#### Ports to be Open in a Firewall Environment for TeamForge {{site.data.identifiers.teamforge}}

In the following table, `Source Server` is where the data is coming from and `Target Server` is where the data is going to.

<table class="table" markdown="1">
<thead>
<th></th>
<th>Source Server</th>
<th>Target Server</th>
<th>Port to Be Open on the Target Server</th>
<th>Remarks</th>
</thead>
<tr>
<td>Apache</td>
<td>All</td>
<td>TeamForge App</td>
<td>80 or 443</td>
<td>443 for SSL</td>
</tr>
<tr>
<td>TeamForge Database</td>
<td>TeamForge App</td>
<td>TeamForge Database</td>
<td>5432</td>
<td></td>
</tr>
<tr>
<td>SVN Integration</td>
<td>All</td>
<td>SVN</td>
<td>80 or 443</td>
<td>443 for SSL</td>
</tr>
<tr>
<td>Git Integration</td>
<td>All</td>
<td>Git</td>
<td>80 or 443</td>
<td>443 for SSL</td>
</tr>
<tr>
<td>Git SSH</td>
<td>All</td>
<td>Git</td>
<td>29418</td>
<td></td>
</tr>
<tr>
<td>Search</td>
<td>TeamForge App</td>
<td>Search</td>
<td>2099</td>
<td></td>
</tr>
<tr>
<td>Binaries</td>
<td>TeamForge App</td>
<td>Binaries</td>
<td>8500</td>
<td></td>
</tr>
<tr>
<td>Reports DB</td>
<td>TeamForge App</td>
<td>Reports DB</td>
<td>5432 or 5632</td>
<td>5432 is used by default as Reports DB is co-hosted with TeamForge database. 5632 can be used if you want Reports DB on a separate port.</td>
</tr>
<tr>
<td>Reports ETL</td>
<td>TeamForge App</td>
<td>Reports ETL</td>
<td>7010</td>
<td></td>
</tr>
<tr>
<td>Code Search (Elasticsearch)</td>
<td>All</td>
<td>Code Search (Elasticsearch)</td>
<td>9200</td>
<td></td>
</tr>
</table>

<!-- ### EventQ Port Requirements {#eventqportreq}

#### Ports Used by TeamForge EventQ Services {#eventq_proxy_port_settings} -->

<!-- The EventQ service is designed to run proxied behind TeamForge's web server. The default configuration works for situations where EventQ and TeamForge are intended to run on the same machine. However, if you intend to install EventQ on a separate host, the TeamForge site options token `ORC_HOSTNAME` must be uncommented and changed from localhost to the desired hostname. Please read [TeamForge-EventQ Proxy Settings] for a complete list of proxy configuration options and make any needed changes in TeamForge's `site-options.conf` file before installation begins.

{% include important.html content="Understand the following port requirements to avoid conflicts during installation. Note that the HTTP/HTTPS port listed below is EventQ's internal, non-proxied port. Once proxied, EventQ will be accessible through TeamForge's HTTP(S) hostname and port." %} -->

<!-- <table class="table" markdown="1">
<thead>
<th>Port</th>
<th>Service</th>
<th>Host</th>
</thead>
<tr>
<td>8844</td>
<td>HTTP/HTTPS</td>
<td>App Server</td>
</tr>
<tr>
<td>6379</td>
<td>Redis</td>
<td>App Server</td>
</tr>
<tr>
<td>27017</td>
<td>MongoDB</td>
<td>DB Server</td>
</tr>
<tr>
<td>28017</td>
<td>MongoDB</td>
<td>DB Server</td>
</tr>
<tr>
<td>5672</td>
<td>RabbitMQ</td>
<td>MQ Server</td>
</tr>
<tr>
<td>15672</td>
<td>RabbitMQ Management Console</td>
<td>MQ Server</td>
</tr>
</table>

#### Ports to be Open in a Firewall Environment for EventQ

The following use cases detail TeamForge EventQ's firewall/routing requirements. By default, end-user web access is proxied through the primary TeamForge web server. TeamForge EventQ adapters supply data using the MQ layer and therefore need access to the MQ server (default port 5672). There are also private access requirements between the various installed services as detailed below.

In the following table, `Source Server` is where the data is coming from and `Target Server` is where the data is going to.

<table class="table" markdown="1">
<thead>
<tr>
<th>Source Server</th>
<th>Target Server</th>
<th>Ports to Be Open on the Target Server</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>App server</td>
<td>TeamForge server</td>
<td>443/80</td>
<td>App communication with TeamForge server</td>
</tr>
<tr>
<td>TeamForge server</td>
<td>App server</td>
<td>8844</td>
<td>TeamForge communication with App server</td>
</tr>
<tr>
<td>TeamForge EventQ Adapters</td>
<td>MQ server</td>
<td>5672</td>
<td>Message communication between Adapters and MQ server</td>
</tr>
<tr>
<td>App server</td>
<td>MQ server</td>
<td>5672</td>
<td>App communication with MQ server</td>
</tr>
<tr>
<td>TeamForge server</td>
<td>MQ server</td>
<td>5672</td>
<td>TeamForge communication with MQ server</td>
</tr>
<tr>
<td>App server</td>
<td>MQ server</td>
<td>15672</td>
<td>App administration of MQ server</td>
</tr>
<tr>
<td>App server</td>
<td>DB server</td>
<td>27017</td>
<td>App server communication with DB server</td>
</tr>
<tr>
<td>App server</td>
<td>MQ server</td>
<td>22</td>
<td>App ssh to MQ server, installation only</td>
</tr>
<tr>
<td>App server</td>
<td>DB server</td>
<td>22</td>
<td>App ssh to DB server, installation only</td>
</tr>
</tbody>
</table> -->

### Ports to be Open in a Firewall Environment for Baseline {#baselineports}

In the following table, `Source Server` is where the data is coming from and `Target Server` is where the data is going to.

<table class="table" markdown="1">
<thead>
<tr>
<th>Source Server</th>
<th>Target Server</th>
<th>Ports to Be Open on the Target Server</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>Baseline Application</td>
<td>TeamForge Database</td>
<td>5432</td>
<td>Baseline Application communication with TeamForge database server</td>
</tr>
<tr>
<td>Baseline Application</td>
<td>Baseline Database</td>
<td>5432</td>
<td>Baseline Application communication with Baseline database server</td>
</tr>
<tr>
<td>TeamForge Application</td>
<td>Baseline Application</td>
<td>9191</td>
<td>Baseline Application communication with TeamForge Application</td>
</tr>
<tr>
<td>TeamForge Application</td>
<td>Baseline Post Install Application</td>
<td>9192</td>
<td>Baseline Post Install Application communication with TeamForge Application</td>
</tr>
</tbody>
</table>

### Ports to be Open in a Firewall Environment for TeamForge Webhooks-based Event Broker {#webrports}

In the following table, `Source Server` is where the data is coming from and `Target Server` is where the data is going to.

<table class="table" markdown="1">
<thead>
<tr>
<th>Source Server</th>
<th>Target Server</th>
<th>Ports to Be Open on the Target Server</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>TeamForge Webhooks-based Event Broker Application</td>
<td>TeamForge Webhooks-based Event Broker Database</td>
<td>5432</td>
<td>TeamForge Webhooks-based Event Broker application communication with its database server</td>
</tr>
<tr>
<td>Publisher Application</td>
<td>TeamForge Webhooks-based Event Broker Application</td>
<td>3000</td>
<td>Publisher application communication with TeamForge Webhooks-based Event Broker application</td>
</tr>
<tr>
<td>Subscriber Application</td>
<td>TeamForge Webhooks-based Event Broker Application</td>
<td>Subscriber port (Unknown)</td>
<td markdown="1">
Subscriber application communication with TeamForge Webhooks-based Event Broker application
{% include note.html content="Subscriber ports should be accessible in a Firewall environment." %}
</td>
</tr>
</tbody>
</table>


{{site.data.alerts.hr_shaded}}

[^1]: TeamForge 19.2 and later used OpenJDK (it no longer uses Oracle JRE). It is recommended to remove the  `JAVA_HOME` token, if added to your `site-options.conf` file. TeamForge uses the default `JAVA_HOME` which is set to the OpenJDK path. 
[^2]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
[^3]: CollabNet releases new versions of integration plugins from time to time. It is recommended to upgrade your TeamForge-Nexus integration plugins whenever a new version is available.


{% include links.html %}