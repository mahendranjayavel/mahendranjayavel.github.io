---
title: TeamForge Maven Deploy Plugin
keywords: binary, repository, create, delete, link, maven
tags: [ctf_20.0, ctf_19.3, ctf_19.2, binaries, source_code, webr]
sidebar: teamforge_sidebar
permalink: configuremavenplugin.html
last_updated: Feb 11, 2020
summary:  The Digital.ai TeamForge Maven Deploy Plugin can be configured to post binary artifact deployment information to TeamForge via the Webhooks-based Event Broker (WEBR) for end-to-end traceability.
---

<!-- {% include important.html content="Migrate the existing binary artifact data from EventQ's MongoDB database to TeamForge database if you have been using EventQ to notify TeamForge with binary artifact data in TeamForge 19.2 or earlier. See [Migrate Binary Artifact Data][configuremavenplugin.html#migratemavenplugindata]." %} -->

<div class="panel panel-info">
<div class="panel-heading">Before You Begin</div>
<div class="panel-body" markdown="1">

Before you begin with the configuration of the TeamForge Maven Deploy Plugin, generate the TeamForge Webhook URL by running the [`create_webhook_event.py`][create_webhook_event_py] script. 

</div>
</div>


## Configure the Digital.ai TeamForge Maven Deploy Plugin {#configuremavendeployplugin}

<!-- {% include note.html content="TeamForge EventQ is being deprecated. Once you configure the Digital.ai TeamForge Maven Deploy Plugin, the binary artifact deployment notifications are no longer sent to TeamForge EventQ." %} -->

To configure the Digital.ai TeamForge Maven Deploy Plugin:

1. Replace the standard deploy plugin with Digital.ai TeamForge Maven Deploy Plugin in your POM.xml.

   ```xml
   <pluginRepositories>
   <pluginRepository>
     <id>collabnet</id>
     <name>Collabnet Public Repo</name>
     <url>http://mvn.collab.net/nexus/content/groups/public/</url>
   </pluginRepository>
   </pluginRepositories>
   <plugins>
   ....
     <plugin>
       <groupId>org.apache.maven.plugins</groupId>
       <artifactId>maven-deploy-plugin</artifactId>
       <version>2.8.2</version>
       <configuration>
         <skip>true</skip>
       </configuration>
     </plugin>
     <plugin>
       <groupId>net.collab.maven.deploy</groupId>
       <artifactId>collabnet-deploy-maven-plugin</artifactId>
       <version>19.3</version>
       <extensions>true</extensions>
       <executions>
         <execution>
           <id>default-deploy</id>
           <phase>deploy</phase>
           <goals>
             <goal>deploy</goal>
           </goals>
         </execution>
       </executions>
       <configuration>
         <skipTeamForgeNotification>false</skipTeamForgeNotification>
         <ctfWebhookUrl>https://localhost:3000/inbox/v4/BinaryCustomData/1001</ctfWehookUrl>
         <associatedBuildNumber>${env.BUILD_NUMBER}</associatedBuildNumber>
         <associatedJobName>${env.JOB_NAME}</associatedJobName>
         <skipLinkToBinaries>true</skipLinkToBinaries>         
       </configuration>
     </plugin>
   </plugins>
   ````   
   
   {% include important.html content="Make sure the \<skip> tag is set to `true` to prevent more than one Nexus notification for a single Nexus artifact deployment. If \<skip> is not set to true, notifications are sent by both the `maven-deploy-plugin` and the `collabnet-deploy-maven-plugin` for a single binary artifact." %}

   The following table lists the available configuration items.

   <table>
    <tr>
      <th>Configuration Parameter</th>
      <th>Description</th>
      <th>Mandatory</th>
      <th>Default Value</th>
      <th>Example</th>
    </tr>
    <tr>
      <td>ctfWebhookUrl</td>
      <td>TeamForge Webhook URL.</td>
      <td>Yes</td>
      <td>None</td>
      <td>https://localhost:3000/inbox/v4/BinaryCustomData/1001</td>
    </tr>
    <tr>
      <td>associatedBuildNumber</td>
      <td>Specify to the env variable depending on your build system process. Set to ${env.BUILD_NUMBER} for Jenkins.</td>
      <td>Yes</td>
      <td>None</td>
      <td>${env.BUILD_NUMBER}</td>
    </tr>
    <tr>
      <td>associatedJobName</td>
      <td>Specify to the env variable depending on your build system process. Set ${env.JOB_NAME} for Jenkins.</td> 
      <td>Yes</td>
      <td>None</td>
      <td>${env.JOB_NAME}</td>
    </tr>
    <tr>
      <td>skipLinkToBinaries</td>
      <td>Set to true to download binary artifact from traceability view. If set to false, redirects to the download location of binary artifact.</td> 
      <td>No</td>
      <td>true</td>
      <td>true</td>
    </tr>
    <tr>
      <td>skipTeamForgeNotification</td>
      <td>Set to true to disable notification.</td> 
      <td>No</td>
      <td>false</td>
      <td>false</td>
    </tr>
    <tr>
      <td>component</td>
      <td>Used to identify a specific binary artifact as a component in a larger application.</td> 
      <td>No</td>
      <td>None</td>
      <td>An ALM platform has several components such as an application server, an indexer, an SCM integration server and so on. These components have their own build process. This property is used to uniquely identify such components in TeamForge Webhooks-based Event Broker. </td>
    </tr>
    <tr>
      <td>componentOf</td>
      <td>Associated with the 'component' parameter to store the details of the component.</td> 
      <td>No</td>
      <td>None</td>
      <td>SCM as a component of Teamforge.</td>
    </tr>
   </table>

2. Set up the Nexus credentials in the `settings.xml` file. 

   You may find this file in the Maven home directory. For example, in the following illustration, your distribution management section has a repository id as `local-nexus` (as configured earlier in the POM.xml file):
   ```xml
   <settings>
    <servers>
     <server>
      <id>local-nexus</id>
      <username>your_ctf_username</username>
      <password>xxxxxxxx</password>
     </server>     
    </servers>
   </settings>
   ````
  
<!-- ## Migrate the Binary Artifact Data from EventQ to TeamForge {#migratemavenplugindata}

After configuring the CollabNet Maven Deploy Plugin, you must migrate the binary artifact data from EventQ's MongoDB database to TeamForge database post upgrade to TeamForge {{site.data.identifiers.teamforge}}. 

Before migrating the binary artifact data from EventQ to TeamForge, create the `config.properties` file with the following tokens in the `/tmp` directory and keep it handy.

```shell
#Default Mongo DB host is "localhost"
MONGO_DB_HOST=localhost

#Default Mongo DB port is "27017"
MONGO_DB_PORT=27017

MONGO_DB_NAME=eventq
MONGO_DB_USERNAME=eventq

#Enter (y)es or (n)o for CTF_USES_ORACLE_DB
CTF_USES_ORACLE_DB=n

#If CTF_USES_ORACLE=(y)es, enter ORACLE_SID
ORACLE_SID=

CTF_HOST_NAME=<TeamForge host name or domain name>
CTF_PORT=5432

#If CTF_USES_ORACLE=(n)o, enter CTF_DB_NAME
CTF_DB_NAME=teamforge
CTF_DB_USERNAME=teamforge
````

To migrate the existing binary artifact data:

1. Extract the existing binary artifact data from EventQ's MongoDB database and generate an SQL file based on the TeamForge database you have (Postgres/Oracle).
2. Execute the generated SQL file on the TeamForge database (Postgres/Oracle).

### Extract Binary Artifact Data from EventQ MongoDB

1. [Download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/eventq-migration/collabnet-deploy-maven-plugin/1.0/collabnet-deploy-maven-plugin-1.0.jar) the CollabNet Maven deploy plugin **collabnet-deploy-maven-plugin-1.0.jar**.

2. Run this command to execute the migration script.

   ```shell
    java -jar collabnet-deploy-maven-plugin-1.0.jar -m -f /tmp/config.properties
   ````
   {% include note.html content="The migration script will be successful only if MongoDB is installed on the server the script is being executed." %}

3. Enter the MongoDB password and TeamForge database password, when prompted.

   The migration script is executed and generates the `collabnet_deploy_maven_plugin_data_migration.sql` file.

   {% include image.html file="maven_plugin_migration.png" url="http://docs.collab.net/teamforge221/images/maven_plugin_migration.png" %}

### Execute the SQL File on the PostgreSQL/Oracle Database

{% include warning.html content="If an error occurs while executing the SQL file, the entire transaction is rolled back. You must re-execute the file." %}

* To execute the SQL file on PostgreSQL Database:

  1. Log on to TeamForge Server.

  2. Run this command to import the migrated data.

     ```shell
     sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper <filepath of `collabnet_deploy_maven_plugin_data_migration.sql`> 
     ````

     OR 
     
     ```shell
     cat <filepath of `collabnet_deploy_maven_plugin_data_migration.sql`> | sudo /opt/collabnet/teamforge/runtime/scripts/psql-wrapper 
     ````

* To execute the SQL file on Oracle Database:

  1. Log on to your Oracle database.

  2. Run this command to import the migrated data.
     
     ```shell
     @<filepath of `collabnet_deploy_maven_plugin_data_migration.sql`>
     ```` -->

{% include links.html %}