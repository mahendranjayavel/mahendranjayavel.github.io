---
title: Back up and Restore TeamForge
keywords: back up, restore, backup
tags: [ctf_20.0, ctf_19.3, ctf_19.0, ctf_18.3, backup_restore, upgrade, postgres, datamart]
sidebar: teamforge_sidebar
permalink: backupandrestore.html
last_updated: Jan 11, 2020
summary: Save a copy of your TeamForge site's data to a location from where you can quickly retrieve it to your TeamForge site.
---

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">
* The following instructions, though applicable in general to any PostgreSQL version, assume that you run a TeamForge version that runs on PostgreSQL {{site.data.identifiers.postgres_past_short}}, which you want to back up. Replace {{site.data.identifiers.postgres_past_short}} with the PostgreSQL version you run, if required.
* If you are upgrading by installing TeamForge {{site.data.identifiers.teamforge}} on new hardware, then you'll need the backed-up site data to complete the upgrade.
* If you are upgrading your site on the same hardware, then you won't need to back up but you should create a backup anyway, as a measure of caution.
</div>
</div>

## Back up and Restore TeamForge Database, Data Directories and site-options.conf {#backupteamforge}

1. Log on to the TeamForge server that you want to back up.

2. SOAP 50 is no longer supported. Back up all your custom event handlers and remove all the event handler JAR files before starting your TeamForge upgrade process.
   {% include tip.html content="Do this on the TeamForge Application Server." %}
   1. Go to **My Workspace** > **Admin**.
   2. Click **System Tools** from the **Projects** menu.
   3. Click **Customizations**.
   4. Select the custom event handler and click **Delete**.
      {% include tip.html content="Post upgrade, you can add custom event handlers again from the backup while making sure that you don't have SOAP50 (deprecated) library used." %}

3. {% include installupgrade/stop_teamforge_on_all_servers_distributed.html %}

4. Back up your site data.

   1. Back up the `/opt/collabnet/teamforge/var` directory.
      {% include tip.html content="Do this on both the TeamForge Application and Database servers in case you have them running on two separate servers." %}
      ```shell
      mkdir -p /tmp/backup_dir
      cp -Rpfv /opt/collabnet/teamforge/var /tmp/backup_dir
      ````

   2. Back up the `/opt/collabnet/gerrit` directory if you have Git integration.
      {% include tip.html content="Do this on the server that hosts the TeamForge—Git integration services." %}
      ```shell
      mkdir /tmp/backup_dir/gerrit
      cp -Rpfv /opt/collabnet/gerrit/ /tmp/backup_dir/gerrit
      ````
<!--    3. Back up the EventQ YAML files and directories if you have EventQ installed.
      {% include tip.html content="Do this on the server that hosts the TeamForge EventQ services." %}
      ```shell
      cp -Rpfv /opt/collabnet/eventq/config/*.yml /opt/collabnet/mongodb /opt/collabnet/rabbitmq /tmp/backup_dir
      ```` -->
   3. Compress your backup data.
      ```shell
      cd /tmp
      tar czvf backup.tgz backup_dir
      ````

5. Back up the SSH keys, if any.

6. Back up your SSL certificates and keys, if any.

7. If you are upgrading TeamForge on new hardware, copy the backed up data and the `site-options.conf` file to the new server.
   ```shell
   scp /tmp/backup.tgz username@newbox:/tmp
   scp /opt/collabnet/teamforge/etc/site-options.conf username@newbox:/tmp
   ````
   
8. Restore the TeamForge data.

   1. Log on to the server where you want to restore the data and unpack the `backup.tgz` file.
      ```shell
      cd /tmp
      tar xzvf backup.tgz
      ````
   2. Restore the database and data directories.
      ```shell
      cp -Rpfv /tmp/backup_dir/var /opt/collabnet/teamforge/
      ````
   3. Restore the Git data directories on the server that hosts TeamForge—Git integration.
      ```shell
      cp -Rpfv /tmp/backup_dir/gerrit/gerrit/etc /opt/collabnet/gerrit
      cp -Rpf /tmp/backup_dir/gerrit/gerrit/.ssh /opt/collabnet/gerrit
      cp -Rpf /tmp/backup_dir/gerrit/gerrit/bin /opt/collabnet/gerrit
      cp -Rpf /tmp/backup_dir/gerrit/gerrit/index /opt/collabnet/gerrit      
      mv /opt/collabnet/gerrit/box-<gerrit source server hostname> /opt/collabnet/gerrit/box-<TeamForge 19.1 gerrit server hostname>       
      ````       
      here, `<gerrit source server hostname>` refers to the hostname of the server on which gerrit was hosted. 

<!--    4. Restore the EventQ YAML files and data directories on the server that hosts EventQ.
      ```shell
      yes | cp -Rf /tmp/backup_dir/*.yml /opt/collabnet/eventq/config/
      yes | cp -Rf /tmp/backup_dir/mongodb /opt/collabnet
      yes | cp -Rf /tmp/backup_dir/rabbitmq /opt/collabnet
      ```` -->

## Back up and Restore the Review Board Database and Data Directories {#backuprb}

If Review Board and TeamForge are co-hosted on the same server, the Review Board database and data directories should have been backed up already when you backed up TeamForge. So, it is not necessary to take a back up of the Review Board database and data directories again. However, you must back up Review Board if you have Review Board on a separate server outside of the TeamForge Application Server. 

1. Back up the `/opt/collabnet/teamforge/var/pgsql` and `/opt/collabnet/teamforge/var/reviewboard/data` directories from the Review Board Server that hosts the Review Board database service (`reviewboard-database`) in case you have Review Board on a separate server outside of the TeamForge Application Server.

   ```shell
   mkdir -p /tmp/backup_dir
   cd /opt/collabnet/teamforge/var
   tar -zcvf /tmp/backup_dir/reviewboard_pgsql.tgz pgsql/{{site.data.identifiers.postgres_past_short}}
   tar -zcvf /tmp/reviewboard_data.tgz reviewboard
   ````

2. Copy the `/tmp/reviewboard_pgsql.tgz` and `reviewboard_data.tgz` files to the `/tmp` directory of the new server if you are upgrading Review Board on a new hardware.

   ```shell
   scp /tmp/reviewboard_pgsql.tgz username@newRBbox:/tmp
   scp /tmp/reviewboard_data.tgz username@newRBbox:/tmp
   ````

3. Restore the Review Board database and data directories (on the new server where you plan to have the Review Board database).
   
   ```shell
   cd /opt/collabnet/teamforge/var/
   tar -zxvf /tmp/reviewboard_pgsql.tgz
   tar -zxvf /tmp/reviewboard_data.tgz
   ````

{{site.data.alerts.hr_shaded}}
#### Related Links
[Back up and Restore TeamForge Data Using the teamforge.py Script][teamforgescript.html#teamforgebackup]

{% include links.html %}