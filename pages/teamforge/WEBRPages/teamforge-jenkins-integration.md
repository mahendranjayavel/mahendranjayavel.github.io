---
title: TeamForge—Jenkins Integration Using the Webhooks-based Event Broker
keywords: webhooks, event broker
tags: [ctf_21.1, ctf_20.0, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: teamforge-jenkins-integration.html
last_updated: Jul 05, 2021
summary: TeamForge Webhooks-based Event Broker supports TeamForge—Jenkins integration. Jenkins integration plugin is used to integrate TeamForge with Jenkins using TeamForge Webhooks-based Event Broker.
---
It is assumed you have Jenkins {{site.data.identifiers.jenkins}} installed and this topic discusses how to configure the Jenkins integration plugin to integrate Jenkins with TeamForge. 

## Configure Jenkins Integration Plugin to Notify the Webhooks-based Event Broker {#configurejenkinsforwebr}

The Jenkins integration plugin {{site.data.identifiers.jenkins_integration_plugin}} for TeamForge {{site.data.identifiers.teamforge}}—Jenkins {{site.data.identifiers.jenkins}} integration—if configured—can notify the TeamForge's native Webhooks-based Event Broker (WEBR) about the build data. 

**CollabNet Jenkins Plugin's Features**

<!-- * Notify EventQ when builds complete. The CollabNet Plugin must be installed once on each Jenkins server you wish to connect to TeamForge/EventQ. -->
* Notify TeamForge Webhooks-based Event Broker when builds complete.
* Authenticate users from TeamForge. If set up as the "Build & Test" application, it can even use Single Sign-On.
* Authorization from TeamForge, including the ability to set permissions in Jenkins based on roles in your TeamForge project.
* Upload the build log or workspace artifacts to the TeamForge Documents.
* Upload workspace artifacts to the TeamForge File Release System, as a post-build publishing task or as a build promotion task.
* Open/update/close TeamForge Tracker artifacts based on the Jenkins build status.
* Upload workspace artifacts to the Lab Management Project Build Library. (Requires CollabNet Lab Management).

  [Click here to download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/ctf/ctf-jenkins-plugin/2.0.8/CollabNet-2.0.8.hpi) or know more about the requirements for installing the latest CollabNet plugin.

EventQ has been completely removed in TeamForge 20.0. Hence, you must configure Jenkins to notify the TeamForge Webhooks-based Event Broker (WEBR) for TeamForge—Jenkins integration.

<!-- {% include important.html content="If you use native Webhooks-based Event Broker, the build information will not appear on the Activity Stream and the build related reports will not work. For this reason, if you want to have the Jenkins plugin notify the EventQ (instead of the Webhooks-based Event Broker) about the build data, see [Configuring Jenkins Adapter to notify EventQ][eventq_adapters.html#configurejenkinsjob]." %} -->

Use the following instructions to have the Jenkins integration plugin notify the native Webhooks-based Event Broker.

1. [Download the TeamForge—Jenkins integration plugin](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/ctf/ctf-jenkins-plugin/2.0.8/CollabNet-2.0.8.hpi) {{site.data.identifiers.jenkins_integration_plugin}}. 
2. Select **Manage Jenkins > Manage Plugins > Advanced**. 
3. Click **Choose File** from the **Upload Plugin** section, browse and select the plugin file.
4. Restart your Jenkins server.
5. Configure an Individual Jenkins Job to notify the TeamForge Webhooks-based Event Broker.
   1. As a privileged Jenkins user, locate the job you wish to report build data to TeamForge Webhooks-based Event Broker and navigate to its configuration page.
   2. Add a post-build action to **Notify TeamForge/EventQ when a build completes**.
      {% include image.html file="171_configuring_jenkins_plugin_02.png" %}
   3. Select the **Notify TeamForge** check box.
      {% include image.html file="webr-notification-params.png" %}
   4. Enter the TeamForge **WebHook URL** to which the build data will be sent, [Username][siteoptiontokens.html#WEBR_ADMIN_USER], and [Password][siteoptiontokens.html#WEBR_ADMIN_PASSWORD] in the respective fields.
      {% include note.html content="You can obtain TeamForge Webhook URL by running the [`create_webhook_event.py`][create_webhook_event_py] script." %}
   5. By default, the **Optional TeamForge Association View** check box is selected. If required, you can override the global configuration by entering the TeamForge URL and user credentials.
      {% include image.html file="171_configuring_jenkins_plugin_01.png" %}
   6. Save the job configuration.
   7. Run a build to test the new configuration and verify configuration. Information and errors will be reported to your Jenkins log and to the build console.

      {% include warning.html content="DO NOT select the **Notify EventQ** option as EventQ has been completely removed from TeamForge 20.0 and later." %}


<!-- 1. If you are integrating TeamForge and Jenkins for the first time:
   1. Log on to the Jenkins Server as a previliged Jenkins user, navigate to **Manage Jenkins > Manage Plugins > Available**.
   2. Select the latest CollabNet Plugin and install the plugin.
   3. Restart your Jenkins server.
   4. Go to step 3.

2. Existing TeamForge-Jenkins integrations that use CollabNet Plugin v2.0.4 (or earlier):
   1. Log on to the Jenkins Server as a privileged Jenkins user, navigate to **Manage Jenkins > Manage Plugins > Updates**.
   2. Select the latest CollabNet Plugin and install the plugin. -->
<!--    3. [Migrate Jenkins Data][teamforge-jenkins-integration.html#migratejenkinsdata] from EventQ's MongoDB database to TeamForge database and proceed to step 4. --> 

<!-- 3. Existing TeamForge-Jenkins integrations that use EventQ Jenkins Adapter v2.0 (or earlier) plugin:
   1. Log on to the Jenkins Server as a privileged Jenkins user, navigate to **Manage Jenkins > Manage Plugins > Installed**.
   2. Select the EventQ Jenkins Adapter v2.0 and click **Uninstall**.
   3. Select the _Available_ tab.
   4. Select the latest CollabNet Plugin and install the plugin.
   5. [Download](downloads/migrate_jenkins_plugin.sh) the `migrate_jenkins_plugin.sh` script and save it to `<JENKINS_HOME_DIRECTORY>/jobs/`.
      {% include tip.html content="Jenkins default home directory is _/var/lib/jenkins/_." %}
   6. Change ownership of the `migrate_jenkins_plugin.sh` file.
      ```shell
      chmod 755 migrate_jenkins_plugin.sh
      ````
   7. Run the `migrate_jenkins_plugin.sh` script.
      ```shell
      ./migrate_jenkins_plugin.sh
      ````
   8. [Migrate Jenkins Data][teamforge-jenkins-integration.html#migratejenkinsdata] from EventQ's MongoDB database to TeamForge database and proceed to step 4. -->

<!-- ## Migrate the Existing Jenkins Data from EventQ to TeamForge {#migratejenkinsdata}

If you have configured the new Jenkins integration plugin v2.0.6 to notify the TeamForge-based Webhooks Event Broker, you need to migrate the Jenkins data from EventQ's MongoDB database to TeamForge database, after upgrading to {{site.data.identifiers.teamforge}}. 

To migrate the Jenkins data from EventQ's MongoDB to TeamForge database:

This migration process is two-fold:

1. Extract the existing Jenkins data from EventQ's MongoDB database and generate an SQL file based on the database option chosen.
2. Execute the generated SQL file on the TeamForge database (Postgres/Oracle).

### Extract Jenkins Data from EventQ MongoDB

1. [Download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/eventq-migration/jenkins/1.0/jenkins-1.0.jar) the Jenkins plugin **jenkins-1.0.jar**.

2. Run this command to execute the migration script.

   ```shell
   java -jar jenkins-1.0.jar -migrate
   ````
3. Enter the MongoDB hostname as **localhost** or just press **ENTER** for **localhost** to be taken as default host name.
   {% include note.html content="The migration script will be successful only if MongoDB is installed on the same machine from which the script is executed." %}

4. Enter the MongoDB port number or just press **ENTER** for **27017** to be taken as default port number.

5. Enter the MongoDB database name for EventQ.

6. Enter the MongoDB username and password.

7. For `Does TeamForge use Oracle Database [y/n]:`, press **y** if you use Oracle. Press **n** if you use PostgreSQL.

   The migration script is executed and generates the `jenkins_data_migration.sql` file.

   {% include image.html file="jenkins_migration.png" %}

### Execute the SQL File on PostgreSQL/Oracle Database

{% include warning.html content="If an error occurs while executing the SQL file, it will rollback the entire transaction. You must re-execute the file again." %}

* To execute the SQL file on PostgreSQL Database:

  1. Log on to your TeamForge Server.

  2. Run this command to import the migrated data.

     ```shell
     sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper <filepath of `jenkins_data_migration.sql`> 
     ````

     OR 
     
     ```shell
     cat <filepath of `jenkins_data_migration.sql`> | sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper 
     ````

* To execute the SQL file on Oracle Database:

  1. Log on to your Oracle database.

  2. Run this command to import the migrated data.
     
     ```shell
     @<filepath of `jenkins-data-migration.sql`>
     ```` -->

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Webhooks-based Event Broker Overview][webhooks-event-broker-overview]
* [Install the TeamForge Webhooks-based Event Broker][install-webhooks-event-broker]
* [TeamForge-JIRA Integration Using TeamForge Webhooks-based Event Broker][teamforge-jira-integration]
* [TeamForge-TestLink Integration Using TeamForge Webhooks-based Event Broker][teamforge-testlink-integration]

{% include links.html %}



