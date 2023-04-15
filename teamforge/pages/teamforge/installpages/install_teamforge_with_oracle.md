---
title: Install TeamForge with Oracle Database
keywords: multi, multihost, multi-host, distributed installation, oracle
tags: [ctf_20.2, ctf_20.0, ctf_19.3, ctf_19.1, ctf_19.0, installation, oracle]
sidebar: teamforge_sidebar
permalink: install_teamforge_with_oracle.html
last_updated: Aug 6, 2020
layout: "page_without_h3_in_toc"
summary: Distributed setup with TeamForge and Oracle Database (including Datamart) installed on separate servers.
---

{% include inline_image.html file="status-success-small.png" %} In this [distributed setup][plan_your_installation_upgrade.html#singleordistributed], [TeamForge and Oracle database services][plan_your_installation_upgrade.html#teamforgeservices] are distributed across two servers, server-01 and server-02 as illustrated in the following table.<br><br> 
{% include inline_image.html file="status-success-small.png" %} You can install TeamForge on both {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}. In this distributed setup, all the following services are installed on {{site.data.identifiers.rhel_centos_now}} servers.

| server-01                    | server-02                 | 
| TeamForge Application Server | Oracle Database Server    | 
|------------------------------|---------------------------|
| ctfcore  | ctfcore-database |
| mail     | ctfcore-datamart |
| etl      | |
| search   |  |
| codesearch | |
| gerrit | |
| gerrit-database | |
| subversion | |
| reviewboard[^1] | |
| reviewboard-database | |
| reviewboard-adapter[^2] | |
| binary | |
| binary-database | |
| cliserver | |
| service-monitor | |

{% include important.html content="Baseline services are not supported in TeamForge setup with Oracle database." %}

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

## Prepare the Servers for TeamForge Installation (server-01 through server-02)

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

   {% capture noreporeqd %}
   {% include inline_image.html file="status-success-small.png" %} You need not configure the TeamForge installation repository on the Oracle Database Server.
   {% endcapture %}
   {% include callout.html type="primary" content=noreporeqd %}

## Install the TeamForge Services

1. Install the TeamForge application services on the TeamForge Application Server (server-01).
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

2. Install the Review Board services on the TeamForge Application Server (server-01).

   ```shell
   yum install teamforge
   ````
3. [Download](http://www.oracle.com/technetwork/database/features/instant-client/index-097480.html) the corresponding version of Oracle client and run the following command on the TeamForge Application Server (server-01).
   ```shell
   yum localinstall <path to oracle client rpm>
   ````
<!-- 4. Install EventQ services on the EventQ Server (server-03).
   ```shell
   yum install teamforge-eventq (run this command only on RHEL/CentOS 6.x)
   yum install CN-eventq CN-eventq-runtime CN-mongodb CN-rabbitmq
   ```` -->

## Set up the Oracle Database Server (server-02) {#setuporacledbserver}

1. Install Oracle {{site.data.identifiers.oracle_server}}.
   
   {% include note.html content="Make sure your database uses UTF8 or AL32UTF8 encoding. This is needed to support users in Asian languages. See this [Oracle knowledge base article](http://oracle.ittoolbox.com/documents/popular-q-and-a/changing-the-character-set-of-an-oracle-database-1601#)." %}

2. Log on to the Oracle Database Server as a system administrator with `SYSDG` privilege and run the following query.
   ```SQL
   alter system set parallel_threads_per_cpu=4;
   ````
3. Log in as an Oracle user and create the site database user and permissions.

   To use an Oracle database for your TeamForge data, set up the Oracle database and tell the TeamForge installer how to handle it.

   ### TeamForge Database Setup

   {% include note.html content="Make sure your database uses UTF8 or AL32UTF8 encoding. This is needed to support users in Asian languages. See this [Oracle knowledge base article](http://oracle.ittoolbox.com/documents/popular-q-and-a/changing-the-character-set-of-an-oracle-database-1601#)." %}

   1. Connect to your Oracle database.
      ```SQL
      SQL> connect <adminusername>@<db_name>/<adminpassword> as sysdba
      ````
   2. Create the database user and password you will use to connect from TeamForge to Oracle.
      ```SQL
      SQL> create user <sf user> identified by <sf passwd> default tablespace <your tablespace> temporary tablespace <temporary tablespace>;
      ````
   3. Grant permissions to the user that you just created.
      ```SQL
      SQL> grant unlimited tablespace to <sf user>;
      SQL> grant create snapshot to <sf user>;
      SQL> grant create cluster to <sf user>;
      SQL> grant create database link to <sf user>;
      SQL> grant create procedure to <sf user>;
      SQL> grant create sequence to <sf user>;
      SQL> grant create trigger to <sf user>;
      SQL> grant create type to <sf user>;
      SQL> grant create view to <sf user>;
      SQL> grant query rewrite to <sf user>;
      SQL> grant alter session to <sf user>;
      SQL> grant create table to <sf user>;
      SQL> grant create session to <sf user>;
      SQL> grant create any synonym to <sf user>;
      SQL> exit
      ````
   4. Create the database read-only user that you will use to connect from TeamForge.
      ```SQL
      SQL> create user <database_readonly_user> identified by <database_readonly_password> default tablespace <your tablespace> temporary tablespace <temporary tablespace>;
      ````
   5. Grant the required permissions to the read-only user that you just created.
      ```SQL
      SQL> grant create session to <database_readonly_user>;
      SQL> exit
      ````
   6. Connect to your Oracle database as <sf user>.
      ```SQL
      SQL> connect <sf user>@<db_name>/<sf passwd>
      ````
   7. Grant the 'create synonym' permission on TeamForge database to the read-only user that you just created.
      ```SQL
      SQL> begin
      for i in (select table_name from user_tables) loop 
      execute immediate 'grant select on '|| i.table_name||' to <database_readonly_user>'; 
      execute immediate 'create synonym <database_readonly_user>.'||i.table_name||' for '||i.table_name||''; 
      end loop; 
      end;
      
      SQL> exit
      ````
   
   ### TeamForge Datamart Setup

   {% include note.html content="Make sure your database uses UTF8 or AL32UTF8 encoding. This is needed to support users in Asian languages. See this [Oracle knowledge base article](http://oracle.ittoolbox.com/documents/popular-q-and-a/changing-the-character-set-of-an-oracle-database-1601#)." %}

   1. Connect to your Oracle database.
      ```SQL
      SQL> connect <adminusername>@<db_name>/<adminpassword> as sysdba
      ````
   2. Create the datamart user you will use to connect from TeamForge.
      ```SQL
      SQL> create user <reports_database_user> identified by <reports_database_password> default tablespace <your tablespace> temporary tablespace <temporary tablespace>;
      ````
   3. Grant permissions to the user that you just created.
	  ```SQL
	  SQL> grant unlimited tablespace to <reports_database_user>;
	  SQL> grant create snapshot to <reports_database_user>;
	  SQL> grant create cluster to <reports_database_user>;
	  SQL> grant create database link to <sreports_database_user>;
	  SQL> grant create procedure to <reports_database_user>;
	  SQL> grant create sequence to <reports_database_user>;
	  SQL> grant create trigger to <reports_database_user>;
	  SQL> grant create type to <reports_database_user>;
	  SQL> grant create view to <reports_database_user>;
	  SQL> grant query rewrite to <reports_database_user>;
	  SQL> grant alter session to <reports_database_user>;
	  SQL> grant create table to <reports_database_user>;
	  SQL> grant create session to <reports_database_user>;
	  SQL> grant create any synonym to <reports_database_user>;
	  SQL> exit
	  ````
	  {% include note.html content="Replace <reports_database_user> with the datamart username specified in the site-options.conf and <reports_database_password> with the database password specified in site-options.conf." %}
   4. Create the datamart read-only user that you will use to connect from TeamForge.
      ```SQL
      SQL> create user <reports_readonly_user> identified by <reports_readonly_password> default tablespace <your tablespace> temporary tablespace <temporary tablespace>;
      ````
   5. Grant the required permissions to the read-only user that you just created.
      ```SQL
      SQL> grant create session to <reports_readonly_user>;
      SQL> exit
      ````
      {% include note.html content="The TeamForge installer creates the tables and default values for you." %}
   6. Connect to your Oracle database as <reports_database_user>.
      ```SQL
      SQL> connect <reports_database_user>@<db_name>/<reports_database_password>
      ````
   7. Grant the 'create synonym' permission on TeamForge datamart to the read-only user that you just created. SQL> begin
      ```SQL
      for i in (select table_name from user_tables) loop 
      execute immediate 'grant select on '|| i.table_name||' to <reports_readonly_user>'; 
      execute immediate 'create synonym <reports_readonly_user>.'||i.table_name||' for '||i.table_name||''; 
      end loop; 
      end;

      SQL> exit
      ````
4. Log on to the TeamForge Application Server and copy the Oracle Datamart setup script from `/opt/collabnet/teamforge/runtime/scripts/` to the `/tmp` directory of the Oracle Database Server (server-02).
   ```shell
   scp /opt/collabnet/teamforge/runtime/scripts/datamart-oracle-setup.sh <username>@<server-02>:/tmp
   ````
5. Copy the Oracle Datamart setup script to `/u1` directory.
   ```shell
   mkdir /u1
   cp /tmp/datamart-oracle-setup.sh /u1
   ````
6. Create the reporting user and schema.
   
   {% include tip.html content="Skip this step if you have already set up the datamart as discussed earlier. Your responses to the `datamart-oracle-setup.sh` script's prompts must match the values of the equivalent variables of the TeamForge Application Server's `site-options.conf` file." %}

   ```shell
   cd /u1
   sh datamart-oracle-setup.sh
   ````


## Set up the TeamForge Application Server (server-01)
Log on to the TeamForge Application Server (server-01), set up the `site-options.conf` file, and provision the services. 

1. Rename the sample Oracle site configuration file in the `/opt/collabnet/teamforge/etc/` directory.
   ```shell
   cd /opt/collabnet/teamforge/etc/
   cp site-options-oracle.conf site-options.conf
   ````
2. Set up your site's master configuration file. 
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````

   ### host:SERVICES Token
   ```conf
   server-01:SERVICES=ctfcore service-monitor mail etl search subversion codesearch cliserver gerrit gerrit-database  binary binary-database reviewboard reviewboard-database reviewboard-adapter
   server-02:SERVICES=ctfcore-database ctfcore-datamart
   ````
 
   ### host:PUBLIC_FQDN Token
   ```conf
   server-01:PUBLIC_FQDN=my.app.domain.com
   ````

   ### Configure the Oracle Database Tokens {#oraclesiteoptiontokens}
   Configure the Oracle database name, usernames and passwords as configured on the Oracle Database Server.
   * Database type is `oracle` (`DATABASE_TYPE=oracle`)
   * Database service name is the host name of the Oracle Database Server (for example, `DATABASE_SERVICE_NAME=cu349.maa.collab.net`)
   * Reports database service name is the host name of the server where the datamart is (for example, `REPORTS_DATABASE_SERVICE_NAME=cu349.maa.collab.net`)

   ```conf
   DATABASE_TYPE=oracle

   # Adjust usernames/passwords to match what has been configured on the database server.
   DATABASE_USERNAME=ctfuser
   DATABASE_PASSWORD=ctfpwd
   DATABASE_READ_ONLY_USER=ctfrouser
   DATABASE_READ_ONLY_PASSWORD=ctfropwd
   DATABASE_NAME=orcl
   DATABASE_SERVICE_NAME=
​
   # Adjust usernames/passwords to match what has been configured on the database server.
   REPORTS_DATABASE_USERNAME=ctfrptuser
   REPORTS_DATABASE_PASSWORD=ctfrptpwd
   REPORTS_DATABASE_NAME=orcl
   REPORTS_DATABASE_READ_ONLY_USER=ctfrptrouser
   REPORTS_DATABASE_READ_ONLY_PASSWORD=ctfrptropwd
   REPORTS_DATABASE_SERVICE_NAME=
   ````

   Save the `site-options.conf` file.
   
   {% unless site.output == "pdf" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): {% include installupgrade/site_options_config_oracle.html %}
   {% endunless %}

   {% unless site.output == "web" %}
   For further customization of your site configuration (SSL settings, password policy settings, PostgreSQL settings, LDAP settings and so on): [Set up Your Site's Master Configuration File][for_pdf_site_options_config_oracle].
   {% endunless %}

3. {% include installupgrade/deploy_services_with_note.html %}

## Verify TeamForge Installation

1. {% include installupgrade/verify_installation.html %}

{% include installupgrade/postinstalltasks.html %}

{{site.data.alerts.hr_shaded}}
[^1]: TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board_os76}} on {{site.data.identifiers.rhel_centos_now}} and Review Board {{site.data.identifiers.review_board_os610}} on {{site.data.identifiers.rhel_centos_past}}.
[^2]: `reviewboard-adapter` must always be installed on the TeamForge Application Server.

{% include links.html %}