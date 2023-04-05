---
title: TeamForge—JIRA Integration Using the Webhooks-based Event Broker
keywords: webhooks, event broker
tags: [ctf_20.0, ctf_19.3, ctf_19.0, ctf_18.3, install, upgrade, webhooks, site_admin_tasks, integration, event_broker, webr]
sidebar: teamforge_sidebar
permalink: teamforge-jira-integration.html
last_updated: Nov 20, 2020
summary: TeamForge Webhooks-based Event Broker supports TeamForge-JIRA integration. A new JIRA integration plugin version 1.1 is used to integrate TeamForge with JIRA using the TeamForge Webhooks-based Event Broker.
---

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">

Before you begin with the installation and the configuration of the TeamForge—JIRA integration plugin, generate the TeamForge Webhook URL using the [`create_webhook_event.py`][create_webhook_event_py] script. 

</div>
</div>


## JIRA Version Information

The following table provides the supported JIRA product versions and the version of the new TeamForge-JIRA integration plugin. 

<table border="1">
  <col width="50">
  <col width="200">
  <tr><th bgcolor="#8F8C8B"><font color="#FFFFFF">Supported JIRA Versions</font></th><th bgcolor="#8F8C8B"><font color="#FFFFFF">Compatible Plugin</font></th></tr>
  <tr><td>JIRA {{site.data.identifiers.jira}}</td><td width="400px">TeamForge-JIRA-adapter-1.1</td></tr>
</table>

## Configure the JIRA Integration Plugin to Notify the TeamForge Webhooks-based Event Broker {#configurejiraforwebr}

This method of integration is based on the new TeamForge-JIRA integration plugin version 1.1 and is recommended for on-premises installation of JIRA. The TeamForge-JIRA integration via TeamForge Webhooks-based Event Broker brings associations and traceability between JIRA, TeamForge, and various tools supported by TeamForge Webhooks-based Event Broker.

Within JIRA, all the SCM related activities for the particular JIRA issue are tracked and displayed under the _TeamForge_ tab on the JIRA issue page.

{% include image.html file="JIRA_associations_list.png" %}

The **TeamForge** tab provides a summary of associations and also the details of a full listing of associations. This is a listing of immediate associations, activities with direct relationships to the JIRA issue at hand. To explore the chain of associations, click the **Trace** button. The traceability chain that includes commits, builds, reviews, deploys, and other XDS-based integration is displayed. On the **Trace Associations** page, clicking any node lights up all the association paths to that node. In addition, a small pop-up appears with details about the node in context. You can use **SET AS TARGET** button to expand the associations from the selected point. Another function exists to **SEE** more details about the node, opening a new browser tab.

{% include image.html file="jira_trace.png" %}

The TeamForge-JIRA plugin 1.1 is packaged as a JIRA "add-on". Once installed and configured, the add-on supplies issue tracker "work item" metadata to TeamForge. The TeamForge-JIRA plugin 1.1 needs configuration on a per project basis in JIRA, such that JIRA (many) to TeamForge (one) project mappings are established. It is therefore required to configure the TeamForge URL and the TeamForge credentials for each JIRA project. Once this configuration is done, the JIRA integration plugin will create and manage the needed sources.

### Install the JIRA Integration Plugin

Use the TeamForge-JIRA plugin 1.1 to notify TeamForge of updates to JIRA issues and to vizualize the associations between JIRA and other tools. The TeamForge-JIRA plugin 1.1 must be installed once on each JIRA server you wish to connect to TeamForge. Install the TeamForge-JIRA plugin 1.1 using the JIRA add-on Manager. Refer to the [Atlassian Marketplace](https://marketplace.atlassian.com/plugins/net.collab.orchestrate.trackerlistener/versions) for supported versions.

**Install the TeamForge-JIRA Associations Add-on**

1. As a privileged JIRA user, navigate to **Administration > Manage apps > Find new apps**.
   {% include image.html file="174_removeprojectmapping01.png" %}

2. Search the marketplace for the **TeamForge Associations** add-on for JIRA. Type 'TeamForge Associations' and search.
   {% include image.html file="searchthemarketplace.png" %}

3. Click **Install**.
   {% include image.html file="searchthemarketplace01.png" %}

**Upgrade the TeamForge-JIRA Associations Add-on**

New versions of the TeamForge-JIRA associations add-on will be visible in the **Manage apps** section (**Administration > Manage apps > Manage apps**).

### Configure the JIRA Integration Plugin 

Configure "TeamForge Associations" to notify _TeamForge Webhooks-based Event Broker_ about JIRA issues.

<!-- {% include important.html content="Migrate the existing JIRA data from EventQ's MongoDB database to TeamForge database if you have been using EventQ-based TeamForge—JIRA integration in TeamForge 18.3 or earlier. See [Migrate JIRA Data][teamforge-jira-integration.html#migratejiradata]." %}
 -->

1. Configure the add-on from the **Project settings** page to notify TeamForge about the JIRA issues.
   1. Select **Projects** from JIRA Administration menu.
      {% include image.html file="jira-admin-menu.png" %}

   2. Select your project from the list of projects on the **Administration** page.
      {% include image.html file="jira-projects-list.png" %}
      
   3. Select **TeamForge** on the **Project settings** page.

      {% include image.html file="jira_tfsetup_page_webr.png" %}

   4. Enter TeamForge URL in the **TeamForge URL** field.

   5. Enter valid TeamForge login credentials in the **Username** and **Password** fields.

      {% include note.html content="The user whose credentials are provided must have API permissions in TeamForge, or the user should be a `Project Admin`." %}

   6. Enter the Webhook URL in the **Webhook URL** field.

      {% include note.html content="You can generate the TeamForge Webhook URL using the [`create_webhook_event.py`][create_webhook_event_py] script." %}

   7. Click **Save** to save the configuration.

      {% include image.html file="jira_tfsetup_saveconfig_webr.png" %}

      Once the configuration is saved, JIRA issues are pushed to the configured Webhook URL.

      {% include image.html file="jira_tfsetup_savedconfig_webr.png" %}

   
**Sync Existing JIRA Issues into TeamForge**

To associate TeamForge objects to existing JIRA issues, click **Sync Issues**.

This step bootstraps JIRA issue data from the current project into the TeamForge. Note that this process may take several minutes (even hours) to complete, depending on the number of issues in the JIRA project.

{% include note.html content="You can synchronize the JIRA issues only once for each configuration." %}

{% include image.html file="jira_tfsetup_syncissues_webr.png" %} 

<br>
**Edit TeamForge-JIRA Mapping Configuration**

Click **Edit** to modify current configuration, if required.

<br>
**Delete Configured TeamForge Mapping from JIRA Project**

Click **Delete** if you wish to completely dissociate the JIRA project from the configured TeamForge mapping.

{% include warning.html content="Deleting TeamForge mapping abandons all existing association data. The JIRA project can be mapped to another project subsequently, but existing associations are lost. Do this if you were testing the integration using a production JIRA project but now wish to remove any test association data." %}

## Associate JIRA Issues to Version Control Commits

{% capture associateJIRAissues %}
Associations between JIRA<sup>&#174;</sup> issues and TeamForge-aware version control commits can be created via commit message references. Commits to TeamForge project repositories and external repositories that have been configured in TeamForge are also supported.
{% endcapture %}
{% include callout.html type="primary" content=associateJIRAissues %}

**Creating Associations**

1. Using your desired terminal or IDE, instantiate a version control commit to a repository of your choice.
2. In the commit message, make reference to JIRA ID(s) to which you wish to associate the commit surrounded by square brackets.<br><br>
   <u>Sample Commit Messages</u>
   ```Shell
   “[DEMO-123] This commit message will result in an association between
   JIRA issue DEMO-123 and this commit.”

   “[DEMO-123, DEMO-124] Here I’m associating two JIRA issues with project
   identifiers DEMO.” 
   ````

**Viewing Associations inside JIRA**

1. Navigate to the desired JIRA issue details page.
2. Click the **TeamForge** tab.
3. A list of immediate associations appears. In other words, these objects are directly associated to the JIRA issue in context.
4. Click **Trace** to view the first three levels of the traceability chain.
   {% capture traceability %}
   {% include inline_image.html file="status-success-small.png" %} All activities are mapped chronologically. <br>
   {% include inline_image.html file="status-success-small.png" %} Lines indicate direct associations.<br>
   {% include inline_image.html file="status-success-small.png" %} Use the "+" icon to explore further levels of traceability.
   {% endcapture %}
   {% include callout.html type="primary" content=traceability %}

{% include image.html file="JIRA_associations_list.png" %}   

## Remove TeamForge Mappings

{% capture removetfprojmapping %}
As a JIRA site administrator, you can disable active TeamForge mappings for one or more or all the JIRA projects (**Administration > Manage apps > TeamForge Associations**), if you want to prevent a JIRA server that's mirrored into a staging/testing environment from triggering events back to TeamForge (when there are changes to issues in JIRA projects that are mapped to TeamForge) thereby polluting the production TeamForge event data store.
{% endcapture %}
{% include callout.html type="primary" content=removetfprojmapping %}

Use this feature to disable all production JIRA-TeamForge mappings in stage environments and then test the TeamForge Associations add-on by creating a new mapping between a staging JIRA server and TeamForge server.

1. Log on to the JIRA server as a site administrator.
2. Select **JIRA Administration > Manage apps**.
   {% include image.html file ="174_removeprojectmapping01.png" %}
3. Select **TeamForge Associations > Manage**.
   {% include image.html file = "174_removeprojectmapping02.png" %}
4. Select one or more projects from the list to remove the TeamForge-JIRA mapping.
   {% include tip.html content="You can select the **Select All** checkbox to select all the projects." %}
5. Click **Remove**.
   A confirmation message is displayed.
   {% include image.html file="174_removeprojectmapping03.png" %}
6. Click **Remove** to delete the mapping.

<!-- ## Migrate Existing JIRA Data from EventQ to TeamForge {#migratejiradata}

If you configure the new JIRA integration plugin 1.1 to notify TeamForge, you must migrate the JIRA data from EventQ's MongoDB database to TeamForge database, after upgrading to {{site.data.identifiers.teamforge}}. 

To migrate the JIRA data from EventQ's MongoDB to TeamForge database:

This migration process is two-fold:

1. Extract the existing JIRA data from EventQ's MongoDB database and generate an SQL file based on the database option chosen.
2. Execute the generated SQL file on the TeamForge database (Postgres/Oracle).

### Extract JIRA Data from EventQ MongoDB

1. [Download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/eventq-migration/jira/1.0/jira-1.0.jar) the JIRA plugin **jira-1.0.jar**.

2. Run this command to execute the migration script.

   ```shell
   java -jar jira-1.0.jar -migrate
   ````
3. Enter the MongoDB hostname as **localhost** or just press **ENTER** for **localhost** to be taken as default host name.
   {% include note.html content="The migration script will be successful only if MongoDB is installed on the same machine from which the script is executed." %}

4. Enter the MongoDB port number or just press **ENTER** for **27017** to be taken as default port number.

5. Enter the MongoDB database name for EventQ.

6. Enter the MongoDB username and password.

7. For `Does TeamForge use Oracle Database [y/n]:`, press **y** if you use Oracle. Press **n** if you use PostgreSQL.

   The migration script is executed and generates the `jira_data_migration.sql` file.

   {% include image.html file="jira_migration.png" %}

### Execute the SQL File on PostgreSQL/Oracle Database

{% include warning.html content="If an error occurs while executing the SQL file, the entire transaction is rolled back. You must re-execute the file." %}

* To execute the SQL file on PostgreSQL database:

  1. Log on to your TeamForge Server.

  2. Run this command to import the migrated data.

     ```shell
     sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper <filepath of `jira_data_migration.sql`> 
     ````

     OR 
     
     ```shell
     cat <filepath of `jira_data_migration.sql`> | sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper 
     ````

* To execute the SQL file on Oracle Database:

  1. Log on to your Oracle database.

  2. Run this command to import the migrated data.
     
     ```shell
     @<filepath of `jira_data_migration.sql`>
     ```` -->

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Webhooks-based Event Broker Overview][webhooks-event-broker-overview]
* [Install the TeamForge Webhooks-based Event Broker][install-webhooks-event-broker]
* [TeamForge-Jenkins Integration Using TeamForge Webhooks-based Event Broker][teamforge-jenkins-integration]
* [TeamForge-TestLink Integration Using TeamForge Webhooks-based Event Broker][teamforge-testlink-integration]

{% include links.html %}



