---
title: Install or Upgrade the TeamForge—Nexus Integration Plugin
keywords: nexus, binary
tags: [ctf_21.1, ctf_21.0, ctf_20.3, ctf_20.2, ctf_20.1, ctf_20.0, ctf_19.3, installation, upgrade, binaries, ctf_19.2, integration]
sidebar: teamforge_sidebar
permalink: installnexusplugin.html
last_updated: Jun 11, 2021
summary: Once you have your Nexus server set up, install the TeamForge-Nexus integration plugin.
---

TeamForge—Nexus 2 integration is no longer supported by TeamForge 19.2 and later. If you have TeamForge—Nexus 2 integration, [Upgrade to Nexus 3][installnexus.html#upgradenexus2to3] and integrate TeamForge and Nexus 3.

You must keep the following information handy before installing the TeamForge—Nexus integration plugin:
* **Nexus absolute path**—This is the path to the directory where you have Nexus installed. In other words, the path to the directory where you have your Nexus files unzipped. For example, `/nexus-3.29.2-02-unix/sonatype-work/nexus3` (Nexus 3).
* **TeamForge host URL**—The URL to access TeamForge. For example, http://ctf.cloud.collab.net.
* TeamForge administrator user name and password.
* **Nexus Application Name**—The name given to your Nexus integration. In other words, the name found in the Nexus integrated application configuration file.
* **Nexus Application Prefix**—The prefix chosen for Nexus. In other words, the prefix found in the Nexus integrated application configuration file.
* **Nexus URL**: The fully qualified Nexus URL.

## Install and Configure the TeamForge-Nexus 3 Integration Plugin {#installtfnexus3plugin}

1. Log on to the Nexus server.
2. Stop Nexus if it's running.
   * Linux:
     ```linux
     ./bin/nexus stop
     ````
   * Windows:
     ```msdos
     \bin\nexus stop
     ```
3. Download the TeamForge—Nexus 3 integration plugin. 

   <!-- https://forge.collab.net/sf/go/artf415661#15 -->
   TeamForge—Nexus {{site.data.identifiers.nexus3}} integration plugin—[Download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/CTF-Nexus-3-Integration-Plugin/{{site.data.identifiers.nexus3-plugin-version}}/CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip) the `CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip` file.   

4. Unzip the `CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip` file.
   * Linux:
     ```linux
     cd <nexus-install-directory>/nexus/system
     unzip CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip
     ````
   * Windows: Use a utility such as WinRAR.
5. Install the TeamForge-Nexus 3 integration plugin.
   ```shell
   sudo java -jar <nexus-install-directory>/nexus/system/CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}/installer.jar -enable
   ````
6. Enter the Nexus absolute path and TeamForge host URL when prompted.
7. Start Nexus.
   * Linux:
     ```linux
     cd <nexus-install-directory>
     ./bin/nexus start
     ````
   * Windows:
   ```msdos
   cd <nexus-install-directory>
    \bin\nexus start
    ````
8. Log on to Nexus 3 as a Site Administrator.
9. Click **Realms** under the **Security** section on the **Administration** menu.
10. Select **TF Authentication Realm** and **TF Authentication Token Realm** from the available list of realms.
    {% include image.html file="nexus-3-authentication.png" %}
11. Add them to the list of active realms and click **Save**.
    {% include image.html file="nexus-3-authentication-2.png" %}    
12. Once Nexus is up and running, upload the Nexus IAF descriptors to TeamForge.
```shell
java -jar <nexus-install-directory>/nexus/system/CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}/installer.jar -installxml
````
   Enter the TeamForge Host URL, TeamForge admin user name and password, Nexus application name, Nexus application prefix and Nexus URL when prompted.

## Upgrade the TeamForge—Nexus 3 Integration Plugin {#upgradetfnexus3plugin}
<!-- Artifact artf394560 : Nexus 3 integration creating custom privileges -->
You must upgrade your TeamForge—Nexus 3 integration plugin to `CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip` if you are upgrading to TeamForge {{site.data.identifiers.teamforge}}.   

1. Download the TeamForge—Nexus 3 integration plugin.

   TeamForge—Nexus {{site.data.identifiers.nexus3}} integration plugin—[Download](https://mvn.collab.net/nexus/content/repositories/binaries-integration/com/collabnet/CTF-Nexus-3-Integration-Plugin/{{site.data.identifiers.nexus3-plugin-version}}/CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip) the `CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip` file.  

2. Unzip the `CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip` file.
   * Linux:
     ```linux
     cd <nexus-install-directory>/nexus/system
     unzip CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}.zip
     ````
   * Windows: Use a utility such as WinRAR.
3. Install the TeamForge-Nexus 3 integration plugin.
   ```shell
   sudo java -jar <nexus-install-directory>/nexus/system/CTF-Nexus-3-Integration-Plugin-{{site.data.identifiers.nexus3-plugin-version}}/installer.jar -enable
   ````
4. Log on to Nexus 3 as a Site Administrator.
5. Click **Realms** under the **Security** section on the **Administration** menu.
6. Select **TF Authentication Realm** and **TF Authentication Token Realm** from the **Active** list of realms, move them to the **Available** list of realms and move them back to the **Active** list of realms.

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Binary Integration Overview][managebinaries]
* [Install Nexus][installnexus]
* [Manage Binary Repositories][managebinaryrepos]
* [TeamForge-Binary Integration FAQs][binaries-faqs]


{% include links.html %}	
