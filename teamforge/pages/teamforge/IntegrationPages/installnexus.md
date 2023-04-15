---
title: Install Nexus 
keywords: nexus, binary
tags: [installation, upgrade, binaries, ctf_18.2, ctf_20.1, ctf_21.1]
sidebar: teamforge_sidebar
permalink: installnexus.html
last_updated: Jun 11, 2021
summary: TeamForge supports only Nexus 3 integration. This page walks you through the installation procedure for Nexus 3 and upgrade procedure from Nexus 2 to Nexus 3. 
---

## Installing Nexus 3

Nexus comes bundled with a Jetty instance that listens to all configured IP addresses on a host (0.0.0.0) and runs on port 8081 by default.

Installing Nexus is straightforward. Unzip the Nexus bundle in a directory and start Nexus.

{% include important.html content="Though Nexus can be installed on Mac OS, CollabNet does not support Nexus integration on Mac OS." %}

The following instructions are for installing Nexus as a standalone server and integrating it with TeamForge.

1. Log on to the Nexus server.
2. Download the Nexus zip file. TeamForge supports integration with Nexus {{site.data.identifiers.nexus3}}. For instructions, see [Nexus 3 Installation](https://help.sonatype.com/repomanager3/installation).
3. Unzip the content to a directory of your choice.

   {% capture cap1 %}
   You can find two directories, a directory that contains Nexus installation files and folders (hereinafter referred to as `<nexus-install-directory>`) and a Nexus work directory (hereinafter referred to as `<nexus-work-directory>`).
   <br><br>
   {% include inline_image.html file="status-success-small.png" %} `<sonatype-work>` is the default Nexus work directory. As a notation, `<nexus-work-directory>` is used in place of `<sonatype-work>` in this document.<br><br>
   {% include inline_image.html file="status-success-small.png" %} Make sure you have full access permissions on all Nexus folders.
   {% endcapture %}
   {% include callout.html type="primary" content=cap1 %}
4. Open the command prompt and start Nexus.
   * Linux:

     1. Change to `<nexus-install-directory>`.

        ```linux
        cd <nexus-install-directory>
        ````     
     2. Start Nexus.

        ```linux
        ./bin/nexus start
        ````
   * Windows:

     1. Change to `<nexus-install-directory>`.

        ```msdos
        cd <nexus-install-directory>
        ````    
     2.  Start Nexus.

         ```msdos
         \bin\nexus start
         ````

5. Verify if Nexus is running by accessing the URL: `<nexus host name>:port/index.html`.

   Default port is 8081. In case you have multiple Nexus instances, modify the **application-port** property in `/<nexus-work-directory>/nexus3/etc/nexus.properties` file for Nexus 3.

<!-- Artifact artf413434 : Update the nexus installation document for CTF release 20.1 -->

6. Do this if and only if you are installing Nexus 3.21.2 or later and if you have TeamForge Baselines installed for baselining Nexus repositories.
   Add the `nexus.scripts.allowCreation=true` property on a new line to the `/<nexus-work-directory>/nexus3/etc/nexus.properties` file.
   
7. Stop Nexus.
   * Linux:
     ```linux
     ./bin/nexus stop
     ````
   * Windows:
   ```msdos
   \bin\nexus stop
   ````

## Upgrade Nexus 2 to Nexus 3 {#upgradenexus2to3}

{% include note.html content="TeamForge—Nexus 2 integration is no longer supported from TeamForge 19.2. If you have TeamForge—Nexus 2 integration, [upgrade to Nexus 3][installnexus.html#upgradenexus2to3] and integrate TeamForge and Nexus 3. For more information on TeamForge&mdash;Nexus 3 integration, see [Installing and Configuring TeamForge-Nexus 3 Integration Plugin][installnexusplugin.html#installtfnexus3plugin]." %}

This section discusses the migration and post migration steps of Nexus 2 to Nexus 3 migration.

{% include important.html content="It is assumed that you're running Nexus version 2.14.8 that uses Java 8." %}

1. Upgrade your Nexus 2 server to Nexus 3 following the instructions. See [Upgrading Nexus](https://help.sonatype.com/repomanager3/upgrading).
2. Do this if and only if you are installing Nexus 3.21.2 or later and if you have TeamForge Baselines installed for baselining Nexus repositories.

   Add the `nexus.scripts.allowCreation=true` property on a new line to the `/<nexus-work-directory>/nexus3/etc/nexus.properties` file.

3. Log on to the Nexus 3 server as a Site Administrator.
4. Click **Realms** from the **Administration > Security** menu.
5. Select **TF Authentication Realm** and **TF Authentication Token Realm** from the available list of realms.

   {% include note.html content="Both the **TF Authentication Realm** and **TF Authentication Token Realm** will get listed in the available list of realms, only if you have already installed the TeamForge-Nexus 3 plugin. For installing the TeamForge-Nexus 3 plugin, see [Installing the TeamForge-Nexus 3 Integration Plugin][installnexusplugin.html#installtfnexus3plugin]." %}
   
   {% include image.html file="nexus-3-authentication.png" %}

6. Add them to the list of active realms and click **Save**.
   
   {% include image.html file="nexus-3-authentication-2.png" %}    

7. Copy `teamforgeProjectConfiguration` folder from Nexus 2 to Nexus 3.

   * If you have installed Nexus 3 on the same server where Nexus 2 services are running:

     ```shell
     cp -r <nexus-work-directory>/nexus/conf/teamforgeProjectConfiguration <nexus-work-directory>/nexus3/etc/
     ````

   * If Nexus 2 and Nexus 3 are installed on separate servers:

     ```shell
     scp -r user@<nexus-work-directory>/nexus/conf/teamforgeProjectConfiguration user@<nexus-work-directory>/nexus3/etc/
     ````

8. Copy the values of the **TIME_TO_HOLD_USER_CACHE** and **TIME_TO_HOLD_PERMISSION_CACHE** properties from the Nexus 2 `ctf_nexus.properties` file to that of Nexus 3.

   * Location of the `ctf_nexus.properties` file in Nexus 2:

     ```shell
     <nexus-work-directory>/nexus/conf/      
     ````

   * Location of the `ctf_nexus.properties` file in Nexus 3:

     ```shell
     <nexus-work-directory>/nexus3/etc/
     ````

9. **Do this step on the TeamForge Application Server**. Run the `nexus3_upgrade.py` script with the required arguments (see below command—run the command with `sudo` if required) to update the repository path and the IAF server name of Nexus 2 (against the Binary database) with that of Nexus 3.

   ```shell
   /opt/collabnet/teamforge/runtime/scripts/nexus3_upgrade.py nexus2_app_name nexus3_app_name nexus3_repo_host_url
   ````

   where,

   * **nexus2_app_name**: Integrated Application Framework (IAF) server name of Nexus 2
   * **nexus3_app_name**: Integrated Application Framework (IAF) server name of Nexus 3
   * **nexus3_repo_host_url**: Repository path of Nexus 3

10. Restart Nexus 3.

    ```shell
    <nexus_3_app_dir>/bin/nexus restart
    ````

11. Delete the Nexus 2 application integrated with TeamForge.   

    1. Log on to TeamForge as a Site Administrator.

    2. Select **My Workspace > Admin**.

    3. Select **Integrated Apps** from the **Projects** menu.

    4. Select the **Binaries** tab.

    5. Select the Nexus 2 integrated app that you want to delete.

    6. Click **Delete** or **Force Delete**.

#### Key Points to Note When You Integrate TeamForge with Nexus 3

{% capture teamforgewithnexus3 %}

{% include inline_image.html file="status-success-small.png" %} Clicking a repository link from the **Binaries** page shows the repository in the Nexus application page on a separate browser tab. <br><br>
{% include inline_image.html file="status-success-small.png" %} Clicking **Create Repository** from the **Binaries** page redirects you to the Nexus application to create the repository. <br><br>
{% include inline_image.html file="status-success-small.png" %} The **Include Traceability** function is not supported any longer. <br><br>
{% include inline_image.html file="status-success-small.png" %} All the users with permission to create binary repositories can link repositories. <br><br>
{% include inline_image.html file="status-success-small.png" %} You can create new repositories, update or delete existing repositories and do other repository management activities only from within the Nexus application (with TeamForge's RBAC). <br><br>
{% include inline_image.html file="status-success-small.png" %} Roles and permissions are mapped/created automatically during the Nexus 2 to Nexus 3 migration and during repository creation. <br><br>
{% include inline_image.html file="status-success-small.png" %} You can link TeamForge to different types of Nexus repositories such as Maven, Docker, NuGet, and so on and so forth. <br><br>
{% include inline_image.html file="status-success-small.png" %} You can link the repository groups from Nexus to TeamForge from the **Binaries** page. 

{% endcapture %}
{% include callout.html type="primary" content=teamforgewithnexus3 %}

{{site.data.alerts.hr_shaded}}
#### Related Links

* [Install the TeamForge-Nexus Integration Plugin][installnexusplugin]
* [Manage Binary Repositories][managebinaryrepos]
* [TeamForge Binary Integration Overview][managebinaries]
* [TeamForge-Binary Integration FAQs][binaries-faqs]

{% include links.html %}