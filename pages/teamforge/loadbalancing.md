---
title: TeamForge Load Balancing Setup 
keywords: HAProxy, load balancing
tags: [ctf_20.2, ctf_20.0, ctf_19.3, ctf_19.0, system_admin_tasks, installation, upgrade]
sidebar: teamforge_sidebar
last_updated: Aug 6, 2020
permalink: loadbalancing.html
folder: teamforge
toc: no
summary: Installing TeamForge in a Load Balancing setup ensures distribution of processing load between multiple servers. The HAProxy Server hosts the HAProxy services that are required for the load balancing function.
--- 

* In this setup, TeamForge services have been distributed across several servers to distribute the load across several servers. 
* The hardware/software requirements for running TeamForge in a load balancing setup remain the same as that of the usual setup. See [TeamForge Requirements][requirements].
* [HAProxy](http://www.haproxy.org/) can be installed on a server with single core CPU and at least 1GB of RAM.
* [Monit](https://mmonit.com/monit/) is required on all servers to monitor services such as HAProxy and TeamForge applications.

### HAProxy

HAProxy is one of the efficient and reliable solutions that offers load balancing services. For more information, see [HAProxy Documentation](http://www.haproxy.org/#docs).

This setup uses the HAProxy server as the termination point for all requests to the TeamForge application and its related components. The HAProxy will be
configured to handle all requests to the backend servers.

The HAProxy Server is hereinafter referred to as `haproxy.company.domain.com`.

#### Domain Names
With this load balancing setup, there is no requirement to allocate additional user-facing domain names for the servers. Each service is described based on the FQDN of the server on which it runs. HAProxy will proxy the requests to the relevant back-end servers.

This HAProxy deployment model is implemented to support the scenario of federating services across multiple servers without impacting existing URLs to those services.

#### Configuring HAProxy
HAProxy can have its configuration generated automatically by TeamForge. CollabNet recommends deploying HAProxy as the load balancing / front-end proxy by configuring it as a TeamForge node.


In this setup:

* The TeamForge Application Server hosts the core TeamForge application service, `ctfcore`, and other services such as `service-monitor`, `cliserver`, `reviewboard-adapter`, `mail`, `search`, `etl`, `binary`, `reviewboard`, `reviewboard-database`, `binary-database`, `ctfcore-datamart`, `ctfcore-database`, `gerrit-database`, `webr` and `webr-database`.
* The HAProxy Server hosts the HAProxy services.
* Services such as `subversion`, `gerrit`, `codesearch` and `baseline` are hosted on separate servers. 
* Place the license file which you intend to use (`sflicense.txt`) in the `/opt/collabnet/teamforge/var/etc/` directory. This saves you from having to restart the servers when the license is applied at a later point in time.
  ```
  The license must be applicable to both the servers in the cluster.
  ```
* Unless self-signed certificates are acceptable, provide custom SSL certificates using the following TeamForge `site-options.conf` tokens:

  ```
  SSL_CERT_FILE=/etc/ssl/certs/server.crt
  SSL_KEY_FILE=/etc/ssl/certs/server.key

  # Optional - only needed if an intermediate cert is needed
  # SSL_CHAIN_FILE=/etc/ssl/certs/intermediate.crt
  ````

### Service Monitor

TeamForge supports [Monit](https://mmonit.com/monit/) for monitoring services and recovering failed services. Monit is installed on the TeamForge Application and HAProxy servers to monitor the health of services and restart the services when they fail.

Monit log file is located at `/opt/collabnet/teamforge/log/monit/monit.log`. 

### System Landscape {#systemlandscape}
The following TeamForge `site-options.conf` snippet illustrates the system landscape for this setup being discussed in this topic:

```
################################################################################################################

#HAProxy cluster and PUBLIC_FQDN
haproxy-cluster:CLUSTER_SERVICES=haproxy-ctfcore service-monitor haproxy-stats haproxy-subversion haproxy-mail haproxy-gerrit haproxy-binary haproxy-reviewboard haproxy-webr
haproxy.company.domain.com:CLUSTER=haproxy-cluster
haproxy-cluster:PUBLIC_FQDN=hafqdn.company.domain.com
haproxy-cluster:haproxy-ctfcore:BACKEND = ctfapp.company.domain.com
haproxy-cluster:haproxy-mail:BACKEND = ctfapp.company.domain.com
haproxy-cluster:haproxy-binary:BACKEND = ctfapp.company.domain.com
<!-- haproxy-cluster:haproxy-cvs:BACKEND = ctfapp.company.domain.com -->
haproxy-cluster:haproxy-reviewboard:BACKEND = ctfapp.company.domain.com
haproxy-cluster:haproxy-subversion:BACK END = svn.company.domain.com
haproxy-cluster:haproxy-gerrit:BACKEND = gerrit.company.domain.com
haproxy-cluster:haproxy-webr:BACKEND = ctfapp.company.domain.com

###############################################################################################################

#ctfcore-cluster and PUBLIC_FQDN
ctfapp.company.domain.com:SERVICES=ctfcore service-monitor cliserver reviewboard-adapter mail search etl binary reviewboard reviewboard-database binary-database ctfcore-datamart ctfcore-database gerrit-database webr webr-database
ctfapp.company.domain.com:PUBLIC_FQDN=hafqdn.company.domain.com
ctfapp.company.domain.com:mail:PUBLIC_FQDN=hafqdn-mail.company.domain.com
ctfapp.company.domain.com:binary:PUBLIC_FQDN=hafqdn-binary.company.domain.com
ctfapp.company.domain.com:webr:PUBLIC_FQDN=hafqdn-webr.company.domain.com

################################################################################################################

#Gerrit Box
gerrit.company.domain.com:SERVICES=gerrit
gerrit.company.domain.com:PUBLIC_FQDN=hafqdn.company.domain.com
gerrit.company.domain.com:gerrit:PUBLIC_FQDN=hafqdn-gerrit.company.domain.com

#Subversion Box
svn.company.domain.com:SERVICES=subversion
svn.company.domain.com:PUBLIC_FQDN=haqatest.maa.collab.net
svn.company.domain.com:subversion:PUBLIC_FQDN=hafqdn-subversion.company.domain.com

ENABLE_SERVICE_MONITORING=true

#others
codesearch.company.domain.com:SERVICES=codesearch

baseline.company.domain.com:SERVICES=baseline baseline-database baseline-post-install

################################################################################################################
```
Where:

| Cluster/Server | Description | Hosted Services |
|---------------------|-------------|-----------------|
|`haproxy.company.domain.com` | The HAProxy cluster | `haproxy-ctfcore` <br> `service-monitor` <br> `haproxy-stats` <br> `haproxy-subversion` <br> `haproxy-mail` <br> `haproxy-gerrit` <br> `haproxy-binary` <br> `haproxy-reviewboard` <br> `haproxy-eventq` <br> `haproxy-webr` |
|`ctfapp.company.domain.com` | The CTF Core cluster |`ctfcore` <br> `service-monitor` <br> `cliserver` <br> `reviewboard-adapter` <br> `mail` <br> `search` <br> `etl` <br> `binary` <br> `reviewboard` <br> `reviewboard-database` <br> `binary-database` <br> `ctfcore-datamart` <br> `ctfcore-database` <br> `gerrit-database` <br> `webr` <br> `webr-database` |
|`svn.company.domain.com` | The Subversion server | `subversion` |
|`gerrit.company.domain.com` | The Gerrit server | `gerrit` |
|`codesearch.company.domain.com` | The Codesearch server | `codesearch` |
|`baseline.company.domain.com` | The Baseline server | `baseline` <br> `baseline-database` <br> `baseline-post-install` |


## Install TeamForge in a Load Balancing Setup

For the distributed setup discussed earlier, the installation process has to be done in the following sequence:
1. Set up the TeamForge Application Server, provision TeamForge and copy the site-options.conf file to all other servers.
2. Set up the HAProxy Server and provision TeamForge.
3. Set up the Baseline Server, provision TeamForge and copy the site-options.conf file to all other servers. 
4. Provision the TeamForge Application and HAProxy servers again. 
5. Set up the Subversion Server.
6. Set up the Gerrit Server.
7. Set up the Codesearch Server.

### Prepare the Servers
It is assumed that you have all the servers required for TeamForge Load Balancing installation prepped up with the required OS: {{site.data.identifiers.rhel_centos_past}} or {{site.data.identifiers.rhel_centos_now}}.

### Set up the TeamForge Application Server 

1. Configure the TeamForge installation repository.
   
   {% include installupgrade/installrepoconfig.html %}

2. Install the TeamForge application packages.

   ```
   yum install teamforge
   ```

   If you are installing TeamForge {{site.data.identifiers.teamforge}} on {{site.data.identifiers.rhel_centos_past}}, contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) to get the `python-modules-sources-el8.zip` file and unzip it to `/opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources`.
   <!-- https://forge.collab.net/sf/go/artf318790 -->
   <!-- https://forge.collab.net/sf/go/artf392772 -->
   ```shell
   unzip python-modules-sources-el8.zip -d /opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources
   ````

3. Install the Baseline packages if you are installing TeamForge Baseline.

   ```
   yum install teamforge-baseline
   ```

4. Install Monit.

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

5. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

6. Provision services. 
   ```
   teamforge provision
   ```

### Copy the `site-options.conf` File

Once you configure the `site-options.conf` file in the TeamForge Application Server, you can copy it to the `/opt/collabnet/teamforge/etc/` directory of all the servers. 

### Set up the HAProxy Server

1. Configure the TeamForge installation repository.
  
   {% include installupgrade/installrepoconfig_second.html %}


2. Install the TeamForge application packages.
   ```
   yum install teamforge CN-haproxy
   ```

   If you are installing TeamForge {{site.data.identifiers.teamforge}} on {{site.data.identifiers.rhel_centos_past}}, contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) to get the `python-modules-sources-el8.zip` file and unzip it to `/opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources`.
   <!-- https://forge.collab.net/sf/go/artf318790 -->
   <!-- https://forge.collab.net/sf/go/artf392772 -->
   ```shell
   unzip python-modules-sources-el8.zip -d /opt/collabnet/teamforge/service/reviewboard/resources/SOURCES/python-modules-sources
   ````
   
3. Install Monit.

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

4. Provision services. 
   ```
   teamforge provision
   ```

### Set up the Baseline Server

1. Configure the TeamForge installation repository.

   {% include installupgrade/installrepoconfig_third.html %}


3. Install the TeamForge Baseline application packages.
   ```
   yum install teamforge-baseline -y
   ```

4. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

5. Provision services. 
   ```
   teamforge provision
   ```
6. Copy the site-options.conf file from the Baseline Server to all other servers. 

7. Provision the TeamForge Application and HAProxy servers again. 


### Set up the Subversion Server

1. Configure the TeamForge installation repository.

   {% include installupgrade/installrepoconfig_fourth.html %}


2. Install the TeamForge application packages.
   ```
   yum install teamforge-scm -y
   ```

3. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

4. Provision services. 
   ```
   teamforge provision
   ```

### Set up the Git Server

1. Configure the TeamForge installation repository.
  
   {% include installupgrade/installrepoconfig_fifth.html %}


2. Install the Git packages.
   ```
   yum install teamforge-git -y
   ```

3. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

4. Provision services. 
   ```
   teamforge provision
   ```

### Set up the Codesearch Server

1. Configure the TeamForge installation repository.
   
   {% include installupgrade/installrepoconfig_sixth.html %}


2. Install the TeamForge Codesearch application packages.
   ```
   yum install teamforge-codesearch -y
   ```

3. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

4. Provision services. 
   ```
   teamforge provision
   ```

<!-- ### Set up the EventQ Server

1. Configure the TeamForge installation repository. 

   {% include installupgrade/installrepoconfig_seventh.html %}

2. Install the TeamForge EventQ application packages.
   ```
   yum install teamforge-eventq (run this command only on RHEL/CentOS 6.x)
   yum install teamforge CN-eventq collabnet-nginx collabnet-passenger
   ```

3. Modify the `/etc/hosts` entries and add the FQDNS, all pointing to the HAProxy server's IP address.

4. Provision services. 
   ```
   teamforge provision
   ``` -->

## Troubleshooting

* What do I do if the HAProxy connections to https frontend reaches the maximum number of connections (which is 10000 by default)?

  Increase the number to a higher value (like HAPROXY_MAX_CONNECTIONS=15000) in the `site-options.conf` on the HAProxy server and provision TeamForge again. This is to buy time to identify the root cause of the real problem.

  Possible issue: Check the clients (like Gerrit, Jenkins, Nexus, etc) from the network and look out for the stale/long running connections (they may be appearing as incomplete requests) and fix/close those connections.

* How do I enable keep alive in HAProxy?

  Set `HAPROXY_HTTP_MODE_OPTION=http-keep-alive` in the `site-options.conf` in HAProxy server and provision TeamForge.

{% include links.html %}