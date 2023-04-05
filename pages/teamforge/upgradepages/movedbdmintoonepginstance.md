---
title: Create a Single Cluster for Both Database and Datamart
keywords: PostgreSQL, cluster, reports database port
tags: [ctf_18.3, upgrade, site_admin_tasks, postgres, datamart]
sidebar: teamforge_sidebar
permalink: movedbdmintoonepginstance.html
last_updated: Jul 15, 2019
summary: The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server has been deprecated in TeamForge 17.11. 
---

The ability to run separate PostgreSQL instances for TeamForge database and datamart on the same server has been deprecated in TeamForge 17.11. In addition, the `REPORTS_DATABASE_PORT` token has been deprecated in TeamForge 18.3. If you have the TeamForge database and datamart on separate PostgreSQL instances on the same server, follow these instructions to create a dump of both the database and datamart and load them into one PostgreSQL instance on the same server.

* During TeamForge installation, the `REPORTS_DATABASE_PORT` token should no longer be used to assign a separate port for datamart.
* If you have the TeamForge database and datamart running on separate PostgreSQL instances on the same server, create a dump of both the database and datamart and load them into the same PostgreSQL instance.

{% include note.html content="The following instructions assume that you are upgrading from TeamForge 17.8 (with database and datamart on separate ports) to TeamForge 18.3 (or later) on a new hardware." %} 

1. Do this on the existing TeamForge Application Server where the database and datamart runs on two separate ports.
   1. Make a dump file of your site database.
      ```shell
      su - postgres
      /usr/bin/pg_dumpall > /var/lib/pgsql/9.x/backups/teamforge_data_backup.dmp
      exit
      mkdir /tmp/backup_dir
      cp /var/lib/pgsql/9.x/backups/teamforge_data_backup.dmp /tmp/backup_dir/
      ````
   2. Make a dump of your datamart.
      ```shell
      /usr/bin/pg_dumpall -p <reports_database_port> > /var/lib/pgsql/9.x/backups/teamforge_reporting_data_backup.dmp
      ````

2. Do this on the new TeamForge server.
   1. Recreate the runtime environment (do not provision TeamForge directly).

      {% include installupgrade/dumpandload.html %}

      ```shell
      teamforge deploy
      ````

   2. Reload the site database.
      ```shell
      su - postgres
      /usr/bin/psql < /tmp/backup_dir/teamforge_data_backup.dmp
      exit
      ````
      
   3. Reload the datamart.
      ```shell
      su - postgres -c "/usr/bin/psql -p <reports_database_port> < /tmp/backup_dir/teamforge_reporting_data_backup.dmp"
      ````

3. {% include installupgrade/deploy_services_without_note.html %}

{% include links.html %}