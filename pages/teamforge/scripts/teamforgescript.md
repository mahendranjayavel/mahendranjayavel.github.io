---
title: The teamforge.py Script
keywords: teamforge, script, provision, deploy, undeploy, components, services, backup, restore, back up, start, stop, restart, snapshot, bootstrap, initialize
tags: [ctf_20.1, ctf_19.0, ctf_18.3, installation, upgrade, scripts, backup_restore, site-options.conf]
sidebar: teamforge_sidebar
permalink: teamforgescript.html
last_updated: Apr 23, 2019
summary: Use the teamforge.py script to deploy and undeploy services, start and stop services, verify the status of services, verify the application environment, bootstrap or migrate data, back up and restore data and do much more.
---

## Overview

Use the `teamforge` script wherever applicable as it subsumes the functions of the following legacy TeamForge scripts:
* `bootstrap-data.sh`
* `bootstrap-data.py`
* `bootstrap-reporting-data.sh`
* `bootstrap-reporting-data.py`
* `create-runtime.py`
* `collabnet`
* `migrate.py`
* `post-install.py`
* `snapshot.py`

{% capture cap1 %}
{% include inline_image.html file="status-success-small.png" %} Starting from TeamForge 17.8, `/opt/collabnet/teamforge/bin/teamforge` has been linked to `/usr/bin`. You can simply run the `teamforge` command from any path.
{% endcapture %}
{% include callout.html type="primary" content=cap1 %}

Run the `teamforge` script with the following syntax:

```shell
teamforge [command] [-s serviceName] [other parameters]
````

For example, the following command displays the status of all the services:

```shell
teamforge status
````
## TeamForge components and services

### Components

TeamForge comprises of a set of components such as ctfcore, subversion, james, and so on. Some components are always required to be installed, while some are optional. By delivering these components over multiple RPMs, we make sure that users do not have to install everything all the time. Though this is valuable, RPMs alone prove insufficient to manage the components and their inter-dependencies.
* Some components do not have a physical representation but are configuration-only.
* RPM dependencies are restricted to the local machine only; however, in a distributed installation, dependencies between components must be tracked across servers.

In addition to the physical componentization (using RPMs), there is also a need for a logical componentization of TeamForge.

### Services

Services represent a logical component of TeamForge. Such a logical component may either be a feature, which the user explicitly opts to install (for example, Review Board) or a technical component (for example, Apache and Logrotate), which other services depend on. Services come with additional metadata, which makes it possible to track and manage dependencies to a more fine-grained level.
* Deployment dependencies specify which other services need to be deployed locally.
* Provided Endpoints specify which network endpoints the service offers.
* Required Endpoints specify which network endpoints the service depends on.

In general, services are more fine-grained than RPMs and it is common to have a single RPM containing multiple services.

### Service Life Cycle

A service can be in one of the following states:
* `Uninstalled`: A service is uninstalled if the RPM that contains it is not installed. Uninstalled services do not exist as far as TeamForge is concerned.
* `Undeployed`: The RPM containing the service is installed, but the service has not been deployed yet. Deployment is also referred to as "creating the runtime", but is specific to one service.
* `Dependencies unavailable`: The service itself might be available, but at least one of its deployment dependencies is not in "Available" state.
* `Available`: Service is fully functional.

Services that manage data have the following additional states:
* `Not bootstrapped`: Data structures have not been initialized yet.
* `Not migrated`: Data structures are initialized, but data needs to be migrated.

Services that have a daemon have the following additional states:
* `Dependencies unavailable`: The service itself might be available, but at least one of its deployment dependencies is not in "Available" state.
* `Ports Blocked`: The service is impeded from starting up because at least one of the ports it needs is in use by a different process.
* `Stopped`: Service is an auto start-type service, yet is stopped.
* `Inactive`: Service is a demand start-type service and is stopped.
* `Starting`: Service is in the process of starting up.
* `Available`: Service is running and healthy according to its health check.
* `Unhealthy`: Service is running but unhealthy according to its health check.
* `Dead`: Service is supposed to be running, but the process disappeared.
* `Doomed`: Service is technically running, but it will never work properly because some part of it failed to initialize properly.
* `Stopping`: Service is in the process of stopping.

## Parameters

teamforge.py script accepts the following command line parameters:

<dl class="dl">
<dt class="dt dlterm">
[-s | --service]
</dt>
<dd class="dd" markdown="1">
Use the *-s* parameter to selectively act on a specific service or component such as selectively start, stop, bootstrap, backup and restore a specific service. For example, the following command gets you the status of Jboss:
```shell
teamforge status -s jboss
````
</dd>
<dt class="dt dlterm">
[-f | --site_options_file]
</dt>
<dd class="dd">
Use the <span class="keyword parmname">-f</span> parameter to pass the
<span class="ph filepath">site-options.conf</span> file's path as a command line
parameter (default is <span class="ph filepath">/opt/collabnet/teamforge/etc/site-options.conf</span>).
</dd>
<dt class="dt dlterm">
[--skip-verification]
</dt>
<dd class="dd">
Pass this parameter if you want to skip environment verification.
</dd>
<dt class="dt dlterm">
[-y | --yes]
</dt>
<dd class="dd">
Pass this parameter if you want to skip confirmation prompts.
</dd>
<dt class="dt dlterm">
[-p | --path]
</dt>
<dd class="dd" markdown="1">
The path to the backup or restore directory. Used with the `teamforge backup` and `teamforge restore` commands.
</dd>
</dl>


## Commands

The `teamforge` script can perform the following actions:


<dl>
<dt markdown="1">
status
</dt>
<dd markdown="1">
Show status of all services. Use the `-s` parameter to know the status of a specific service.
</dd>
<dt markdown="1">
bootstrap
</dt>
<dd markdown="1">
Bootstrap data (re-create data structures). Use the `-s` parameter to selectively bootstrap a specific component. Suppose, you did not have SVN on your TeamForge site and if you add SVN while upgrading to TeamForge 16.10 or later. You can now selectively bootstrap SVN alone.
</dd>
<dt markdown="1">
deploy
</dt>
<dd markdown="1">
Deploy service(s).
</dd>
<dt markdown="1">
migrate
</dt>
<dd markdown="1">
Migrate data to latest schema.
</dd>
<dt markdown="1">
provision
</dt>
<dd markdown="1">
Provision/reprovision the server. The `provision` command performs tasks such as creating the runtime, starting and stopping services, bootstrapping (fresh install) or migrating (upgrade) data, deploying services, setting file permissions, setting SELinux permissions, initializing services and so on.
</dd>
<dt markdown="1">
undeploy
</dt>
<dd markdown="1">
Undeploy service(s).
</dd>
<dt markdown="1">
start
</dt>
<dd markdown="1">
Start service(s).
</dd>
<dt markdown="1">
stop
</dt>
<dd markdown="1">
Stop service(s).
</dd>
<dt markdown="1">
kill
</dt>
<dd markdown="1">
Terminates service(s) forcefully.
</dd>
<dt markdown="1">
verify
</dt>
<dd markdown="1">
Verify environment.
</dd>
<dt markdown="1">
show-endpoints
</dt>
<dd markdown="1">
Show endpoints
</dd>
<dt markdown="1">
show-dependencies
</dt>
<dd markdown="1">
Show deployment dependencies
</dd>
<dt markdown="1">
reinitialize
</dt>
<dd markdown="1">
Reinitializes all the TeamForge services
</dd>
<dt markdown="1">
apply-permissions
</dt>
<dd markdown="1">
Applies the TeamForge file system permissions when you restore the TeamForge data in a new server while upgraing to a latest TeamForge version.
</dd>
<dt markdown="1">
snapshot
</dt>
<dd markdown="1">
Dumps relevant diagnostic information to the console (stdout) for each deployed service.
</dd>
<dt markdown="1">
info
</dt>
<dd markdown="1">
Displays a summary of TeamForge configuration.
</dd>
<dt markdown="1">
check-data-integrity
</dt>
<dd markdown="1">
Verifies the integrity of the data defined in the service manifest.
</dd>
<dt markdown="1">
update-data-integrity
</dt>
<dd markdown="1">
Updates the calculated checksums for the data defined in the manifest.
</dd>
<dt markdown="1">
await-dependencies
</dt>
<dd markdown="1">
Waits for dependencies to become available.
</dd>
<dt markdown="1">
apply-selinux
</dt>
<dd markdown="1">
Applies selinux policies.
</dd>
<dt markdown="1">
unload-selinux
</dt>
<dd markdown="1">
Unloads selinux policies.
</dd>
<dt markdown="1">
logs
</dt>
<dd markdown="1">
Tails log files.
</dd>
<dt markdown="1">
backup
</dt>
<dd markdown="1">
Back up TeamForge data. The **-p** parameter is mandatory. For more information, see [Back up and Restore TeamForge Data Using the teamforge.py Script][teamforgescript.html#teamforgebackup].
</dd>
<dt markdown="1">
restore
</dt>
<dd markdown="1">
Restore TeamForge data. The **-p** parameter is mandatory. For more information, see [Back up and Restore TeamForge Data Using the teamforge.py Script][teamforgescript.html#teamforgebackup].
</dd>
</dl>

### teamforge reload {#reload}

The `teamforge reload` command comes in handy when you want to quickly bring up the site after modifying some of the frequently-used `site-options.conf` tokens. Certain site-options.conf tokens, when modified, require stopping, deploying, restarting and initializing certain services. Instead of restarting the whole site, the `teamforge reload` command, depending on the tokens that are modified, restarts only the services that need a restart, while keeping the site up for other services.

The following table lists the tokens with which you can use the `teamforge reload` command and the services that are restarted when you change those tokens. 

| When you modify these tokens... | This is what `teamforge reload` does...  |
|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| `PGSQL_SHARED_BUFFERS=`<br> `PGSQL_WORK_MEM=`<br> `PGSQL_FSYNC=`<br> `PGSQL_COMMIT_DELAY=`<br> `PGSQL_COMMIT_SIBLINGS=`<br> `PGSQL_EFFECTIVE_CACHE_SIZE=`<br> `PGSQL_RANDOM_PAGE_COST=`<br> `PGSQL_MAINTENANCE_WORK_MEM=`<br>`PGSQL_LOG_MIN_DURATION=`<br> | 1. Stop PostgreSQL.<br> 2. Deploy PostgreSQL.<br> 3. Start PostgreSQL. |
| `JAMES_GATEWAY_HOST=`<br> `JAMES_GATEWAY_PORT=`<br> `PHOENIX_JAVA_OPTS=`<br> | 1. Stop Phoenix.<br> 2. Deploy Mail.<br> 3. Start Phoenix.<br> 4. Initialize Mail. |
| `ETL_JOB_TRIGGER_TIME`=<br> `ETL_JAVA_OPTS`=<br> | 1. Stop ETL.<br> 2. Deploy ETL.<br> 3. Start ETL.<br> 4. Initialize ETL. |
| `ENABLE_SERVICE_MONITORING=`<br> `SERVICE_MONITOR_RETRIES=`<br> `MONIT_CHECK_INTERVAL=`<br> | 1. Stop Monit (service-monitor).<br> 2. Deploy Monit (service-monitor).<br> 3. Start Monit (service-monitor). |
| `SESSION_TIMEOUT=`<br> `JBOSS_JAVA_OPTS=`<br> `MAX_WWW_CLIENTS=`<br> `USER_RESOURCE_CACHE_MAX_SIZE_LIMIT=`<br> `ADHOC_QUERY_RESULTS_LIMT=`<br> `ADHOC_QUERY_CONNECTION_TIMEOUT=`<br> `PASSWORD_EXPIRY_PERIOD=`<br> `PASSWORD_DISABLE_PERIOD=`<br> `PASSWORD_WARNING_PERIOD=`<br> `PASSWORD_DELETE_PERIOD=`<br> `PASSWORD_CONTROL_EFFECTIVE_DATE=`<br> | 1. Stop Jboss.<br> 2. Deploy Jboss and ctfcore-app.<br> 3. Start Jboss.<br> 4. Initialize the ctfcore-app service. |

<!-- Commenting out the following Troubleshooting section as this issue appears to have been fixed per Hussain. -->
<!-- ## Troubleshooting
### Deploy Error While Upgrading TeamForge

The following error message might show up when you run the `teamforge provision` command during TeamForge upgrades.
```shell
/opt/collabnet/teamforge/service/legacy-runtime/hooks/runtime-option-defaults/tomcat/00-scm-server-check.py failed: No module named constants
````

This happens if the runtime folder is not found in `/opt/collabnet/teamforge/`. 

In such cases, run the following command:
```shell
find /opt/collabnet/teamforge/dist/lib/multiplatform/python/ -name *.pyc -exec rm -f {} +
```` -->

## Back up and Restore TeamForge Data Using the teamforge.py Script {#teamforgebackup}
<!-- Artifact artf301054 : Doc task for "artf298538 : teamforge backup, restore commands" -->

Use the `teamforge.py` script's `backup` and `restore` commands to back up and restore TeamForge data.

### Back up and Restore TeamForge
If you are upgrading to a latest TeamForge version, it is still recommended to follow the [usual backup and restore procedure][backupandrestore]. Use the `teamforge.py` script's `backup` and `restore` commands if you want to back up a particular service such as SVN and restore it on a new server (when you intend to move a specific service from one server to another, typically to move the service to a dedicated server of its own).

If you are backing up TeamForge as a whole, you must stop all the TeamForge services but PostgreSQL before running the `teamforge backup`  and `teamforge restore` commands.

1. To back up TeamForge data:
   ```shell
   teamforge stop
   teamforge start -s postgres
   teamforge backup -p <path to the directory where the data is backed up>
   ````
2. Compress the backed up data and copy it to the target server where you want to restore the data.
3. To restore TeamForge data:
   ```shell
   teamforge stop
   teamforge start -s postgres
   teamforge restore -p <path to the directory where you have the data to be restored>
   ````
4. {% include installupgrade/deploy_services_without_note.html %}

### Back up and Restore a Specific Service
1. To back up a specific service (such as SVN):
   ```shell
   teamforge backup -s <serviceName> -p <path to the directory where the data is backed up>
   ````
   For example:
   ```shell
   teamforge backup -s svn -p /tmp/svnbackup
   ````   
2. Compress the backed up data and copy it to the target server where you want to restore the data. 
3. To restore a specific service's data:
   ```shell
   teamforge restore -s <serviceName> -p <path to the directory where you have the data to be restored>
   ````
   For example:
   ```shell
   teamforge restore -s svn -p /tmp/svnbackup
   ````     
4. {% include installupgrade/deploy_services_without_note.html %}     

### Did You Back up symlinked Directories?
<!-- https://forge.collab.net/sf/go/artf301278#20 -->
Do this if and only if you had backed up and restored symlinked directories.

1. Move the `svnroot`, `cvsroot` and `sf-svnroot` directories from `/opt/collabnet/teamforge/var/scm` to the root directory.

   ```shell
   cd /opt/collabnet/teamforge/var/scm
   mv svnroot cvsroot sf-svnroot /
   ````
2. Create symlinks to the root directory.
   ```shell
   ln -s /sf-svnroot .
   ln -s /svnroot .
   ln -s /cvsroot .
   ````
3. Provision TeamForge. 
   ```shell
   teamforge provision -y
   ````
4. Apply the TeamForge file system permissions.
   ```shell
   teamforge apply-permissions
   ````


## Logging

The `teamforge` script writes entries to `/opt/collabnet/teamforge/log/runtime/runtime.log` file.


{% include links.html %}