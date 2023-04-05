---
title: TeamForge Binary Integration Overview
keywords: binary, repository, binaries, artifactory, nexus, maven
tags: [binaries, authentication, integration, installation, release_notes, ctf_18.2, ctf_19.3]
sidebar: teamforge_sidebar
permalink: managebinaries.html
last_updated: Feb 18, 2020
summary: An important aspect of the end-to-end development lifecycle is the creation and storage of software packages that are often binary artifacts. In the Java world, these are usually reusable jars that are used by other projects. Binary artifact repository managers are software systems that manage, version, and store binary artifacts. Example of such repository manager is Sonatype Nexus.
---

Here is an overview of integrating TeamForge, a complete ALM suite, with binary repository managers.

## What is a binary artifact repository?
A binary artifact repository stores binary artifacts along with the metadata in a defined directory structure, conceptually similar to a source code repository. The metadata describes the binary software artifact and includes information such as dependencies, versioning, and build promotions. Maven is the widely used tool for dependency management, especially for Java projects. Maven represents dependencies in an XML file called Project Object Model (POM). Other tools can use similar approaches to store documentation archives, source archives, Flash libraries and applications, and Ruby libraries.

## How does a binary artifact repository manager help?
Some of the advantages of using a binary artifact repository manager are:

* **Dependency management**: Nexus can act as a Maven repository. Maven is a widely used Java dependency management and build tool.
* **Efficient builds**: With the help of a binary artifact repository manager, you can save the download time from public repositories as the artifacts once downloaded are cached locally.
* **Predictability and release stability**: Once published onto a release repository, the binary artifact and metadata do not change. It ensures predictable and repeatable builds.
* **Control and audit**: If you want to standardize libraries that are used in your software, the binary artifact repository helps track the versions of your software components. Also it enables you to audit the licenses of your third-party components used in your software.
* **Promotes collaboration**: The binary artifact repository enables you to share components with other teams.

## How to integrate TeamForge with Nexus? {#integratenexus}

{{site.data.identifiers.teamforge}} supports integration only with Nexus 3. If you have TeamForge-Nexus 2 integration, [upgrade to Nexus 3][installnexus.html#upgradenexus2to3] and integrate TeamForge and Nexus 3. For more information, see:
* [Install Nexus][installnexus]
* [Install and Configure the TeamForge—Nexus 3 Integration Plugin][installnexusplugin.html#installtfnexus3plugin]

{% include important.html content="TeamForge—Nexus integration is not supported in SUSE Linux platform. See [TeamForge Installation Requirements][requirements]." %}

TeamForge supports integration with Nexus {{site.data.identifiers.nexus3}} in both ALM and SCM modes.

To integrate Nexus with TeamForge:
1. Download and install the Nexus OSS. To set up the Nexus 3 server, see [Install Nexus][installnexus].
2. Download and install the TeamForge—Nexus integration plugin. To install the TeamForge—Nexus 3 integration plugin, see [Install the TeamForge-Nexus Integration Plugin][installnexusplugin].
   
   You must have a Nexus instance running before you install the TeamForge-Nexus integration plugin. If you are upgrading from an earlier version of the plugin, ensure that the old plugin is completely removed from the directory and the new plugin is unzipped on the same directory before you restart the Nexus instance.

   You need to have the following information handy before you start off with the installation:
   * Installation path of the running Nexus instance.
   * TeamForge host's URL.
   * TeamForge site administrator credentials.
   * A suitable name for your Nexus instance; the Binaries Application in TeamForge refers to this name.
3. Change your build system and use the [CollabNet supplied Maven deploy plugin][configuremavenplugin] for end-to-end traceability from requirements to source code all the way to deployed binary artifacts.

**Accessing Nexus through TeamForge**: You have to introduce a TeamForge project context in Nexus and allow authentication to use TeamForge credentials for logging into Nexus directly. Accessing Nexus through the TeamForge project toolbar provides you with Single Sign-on (SSO). It logs you into Nexus automatically with the project context. You can allow RBAC (Role Based Access Control) using TeamForge roles.

## Authentication Policies

<table style="width:100%">
<tr>
<th>Nexus</th>
</tr>
<tr>
<td markdown="1">
Your site administrator can enable the integration with the following two authentication mechanisms:

* TeamForge and native Nexus login (default)
* TeamForge only

In both the cases, you can use your TeamForge credentials to log on to Nexus. If your Site Administrator has used the default setup, you can use your pre-existing Nexus credentials.

**Roles and Permissions**

Following are the two administrative privileges in Nexus:

* Nexus Admin (Site Admin in TeamForge will be a Nexus Admin)
* Project admin (permissions to create, update, and delete binary artifact repositories.)

For all the other users, privileges are based on the TeamForge RBAC setup.
</td>
</tr>
</table>

## Known Limitations with TeamForge—Nexus 3 Integration {#limitations}

Here's a list of known limitations of TeamForge—Nexus 3 integration.

* Unlike Nexus 2 users, Nexus 3 users cannot create binary repositories from the TeamForge **Binaries** page. When they do so, they are redirected to the Nexus 3 Repository Manager in Nexus Application, to let them create binary repositories.
  
* A TeamForge user cannot be configured as an anonymous user in Nexus as TeamForge users are not available in the Nexus database.

* TeamForge broadcast messages and license notifications are not visible in Sonatype Nexus pages in TeamForge. This is due to a limitation with the TeamForge&mdash;Nexus integration plugin.

* When the TeamForge Project administrator changes the existing binary permissions for a user, the changes will not immediately take place due to the cache implementation in Nexus to improve the performance of session handling. Due to this limitation, when a user tries to create a new Nexus repository, he will get the permission denied error. Hence the user must wait for the changes to take effect. However, the user can view the changes immediately on a standalone Nexus application by restarting his session on it.

{{site.data.alerts.hr_shaded}}
#### Related Links

* [Install Nexus][installnexus]
* [Install the TeamForge-Nexus Integration Plugin][installnexusplugin]
* [Manage Binary Repositories][managebinaryrepos]
* [TeamForge-Binary Integration FAQs][binaries-faqs]

{% include links.html %}