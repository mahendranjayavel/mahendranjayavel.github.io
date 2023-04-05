---
title: TeamForge Baseline - An Overview
keywords: what is a baseline, baseline overview
tags: [ctf_20.2, baseline, ctf_20.1, ctf_18.2, ctf_18.3, ctf_19.0, getting_started, project_admin_tasks, role_based_access_control, license]
sidebar: teamforge_sidebar
last_updated: Jul 17, 2020
permalink: baseline-overview.html
folder: teamforge
summary: A Baseline in TeamForge represents a snapshot of selected configuration items from a given TeamForge project at a given point in time. Such a baseline includes key data that describes or helps identify the configuration items in the same state as it existed at the time of creation of the baseline. You can create a Baseline when you accomplish specific milestones in your project or when you release or deliver a product. 
---

## What is a Baseline Definition?

A **Baseline Definition** is a set of inclusion or filter criteria based on TeamForge components such as Tracker Artifacts, Documents, Source Code Repositories (only Git and Subversion are supported), File Releases, and Binaries (only Nexus binaries are supported) of a given TeamForge project. 

## What is a Project Baseline Definition?

A **Project Baseline Definition** is a set of inclusion or filter criteria for a given TeamForge project based on components such as Tracker Artifacts, Documents, Source Code Repositories (only Git and Subversion are supported), File Releases, and Binaries (only Nexus binaries are supported). A TeamForge project can have only one Project Baseline Definition, which can be modified when required.

## What is a Project Baseline?

A **Project Baseline** is a baseline created on a project at a given point in time. Once you have Project Baselines created, you can kick start new projects from Project Baselines and proceed from when and where the Project Baselines were created in the past. Project Baselines are typically created using Project Baseline Definitions. You can create as many as Project Baselines as required.

## What is an External Baseline? {#externalbaseline}

{% capture includeexternalbaselines %}
{% include inline_image.html file="status-success-small.png" %} An "External Baseline" is a Baseline or a Project Baseline that is part of one TeamForge project and used in the Baseline, the Baseline Definition, or the Project Baseline Definition created in another TeamForge project.  <br><br>
{% include inline_image.html file="status-success-small.png" %} Only approved External Baselines or Project Baselines can be included in a Baseline or a Baseline Definition or a Project Baseline Definition. <br><br>
{% include inline_image.html file="status-success-small.png" %} An External Baseline is just referenced, but not copied into the Baseline or the Baseline Definition or the Project Baseline Definition in which it is included.<br><br>
{% include inline_image.html file="status-success-small.png" %} A new section "External Baselines" has been added in [Create Baseline][create-baseline], [Create Definition][create-baseline-def], and [Project Baseline Definition][project-baseline-definition] pages.
{% endcapture %}
{% include callout.html type="primary" content=includeexternalbaselines %}

## What is a Baseline Package?

A **Baseline Package** is a downloadable package of physical project artifacts such as Tracker Artifacts, Documents, and so on generated from an approved Baseline or a Project Baseline. Once generated, you can download and share the package with your stakeholders.

## Is there a separate license for the Baseline tool in TeamForge?

Yes, Baseline has its own license in TeamForge. You must have both **ALM** and **Baseline** licenses to create and work with the Baseline tool in TeamForge. For more information, see [TeamForge License][teamforgelicense].

## What is a Configuration Item? {#configurationitem}

A **Configuration item** is a project artifact that can be uniquely identified.

Typically, a Baseline in TeamForge can include the following configuration items:

* Tracker Artifacts
* Documents
* Source Code Repositories (from Git/Subversion repositories, identified by Tags)
* File Releases
<!-- Artifact artf317297 : Support for Raw repo type in Nexus 3 while creating TF project from project baseline -->
* Binaries (only Nexus `Maven2` and `Raw` formatted Proxy, Hosted and Group types of repositories are supported)

## Hard-links Between Baselines and Configuration Items {#baselineshardlinks}
<!-- [artf413862] Hardlinks—Allow users to delete Documents & FRS that are part of a baseline -->
* Hard-linking of baselined documents and FRS, introduced in TeamForge 20.1, is now well-rounded to allow deletion of baselined documents and FRS without any restrictions whatsoever. 
* With TeamForge 20.2 (and later), you can delete a baselined document (including its versions) and File Release (FRS package).
* When documents and FRS are baselined, a hard-link is established between the baseline and the configuration items (documents and FRS), which lets you delete the documents and FRS packages without breaking the baselines that include them.
* However, you cannot delete documents and FRS packages included as part of baselines created with TeamForge 20.0 or earlier.

## What are the permissions associated with the Baseline tool? {#baselinepermissions}

Here's a list of Baseline-specific permissions. You can set up site-wide, project-level or global roles in TeamForge with the following permissions.

<table>

<tr>
<th>Baseline Permissions</th>
<th>User Actions</th>
</tr>

<tr>
<td><b>BASELINE ADMIN</b></td>
<td markdown="1">
Users with this permission can:

* Manage custom attributes
* Manage custom statuses
* Manage workflow status transition
* Manage field inclusions
</td>
</tr>

<tr>
<td><b>CREATE/VIEW BASELINE</b></td>
<td markdown="1">
Users with this permission can:

* Create a new baseline definition
* Create a new baseline
* View baseline definitions and baselines
* Search for baseline definitions and baselines
* Compare baselines
</td>
</tr>

<tr>
<td><b>PACKAGE GENERATION</b></td>
<td>
Users with this permission can generate package(s) from approved item level or project baselines.
</td>
</tr>

<tr>
<td><b>PACKAGE DOWNLOAD</b></td>
<td markdown="1">
Users with this permission can download baseline packages generated from approved item level or project baselines.

</td>
</tr>

<tr>
<td><b>CREATE PROJECT BASELINE</b></td>
<td>Users with this permission can create a project baseline.</td>
</tr>

<tr>
<td><b>PROJECT BASELINE DEFINITION</b></td>
<td markdown="1">
Users with this permission can:

* Create a new project baseline definition
* Update an existing project baseline definition
</td>
</tr>

<tr>
<td><b>VIEW ONLY</b></td>
<td markdown="1">
Users with this permission can: 

* Search for baseline definitions and baselines
* View baseline definitions and baselines
* Compare baselines
<!-- https://forge.collab.net/sf/go/artf396686 -->
* Export approved item level or project baselines to Excel.
* Export the diff of two baselines to Excel.
</td>
</tr>

<tr>
<td><b>BASELINE REVIEW</b></td>
<td markdown="1">
Users with this permission can:

* Review a baseline
* Approve a baseline
* Reject a baseline
</td>
</tr>

<!-- Artifact artf396075 : [Doc Task]artf395756 : A new permission "DELETE/VIEW BASELINE" should be available for selection to assign to a given role -->
<tr>
<td><b>DELETE/VIEW BASELINE</b></td>
<td markdown="1">Users with this permission can:

* Search for baselines
* View baselines
* Compare baselines
* Delete Open and Rejected (meta status) baselines. 
</td>
</tr>

<!-- [artf415450] Documentation for artf415198 : Delete a Baseline Definition -->
<tr>
<td><b>DELETE/VIEW BASELINE DEFINITION</b></td>
<td markdown="1">Users with this permission can:

* Search for baseline definitions
* View baseline definitions
* Delete baseline definitions
</td>
</tr>
</table>

## How would you create a Baseline in TeamForge?

Baseline creation in TeamForge involves the following steps:

**1. Create baseline definitions**
     
  You can create a baseline definition by defining the filter criteria for Tracker Artifacts, Documents, Source Code Repositories, File Releases, and Binaries. Baseline definitions can be used while creating the baseline. You can also edit a baseline definition at any point in time. For more information, see [Create Baseline Definitions][create-baseline-def].

**2. Create baselines**

  You can create a new baseline using an existing baseline definition or without a definition. Baselines become immutable after their creation. For more information, see [Create Baselines][create-baseline].

**3. Review baselines**
     
  You can review the baseline once it is created. During the review cycle, the baselines can either be approved or rejected. For more information, see [Review Baselines][baseline-review-approval-workflow].

**4. Compare baselines**

  You can compare two baselines created in distinct timelines to view the difference between them. For more information, see [Compare Baselines][compare-baselines].

**5. Create baseline packages**

  You can create one or more baseline packages from approved baselines. As baseline package creation takes a long time, it runs as a backend process. The baseline database server takes care of the package creation. For more information, see [Generate and Download Baseline Packages][generate-baseline-package].
  
  {% include image.html file="baseline-workflow-2.png" %}


## How would I install Baseline?

Baseline services can be installed when you install TeamForge. For more information on Baseline hardware requirements, see [Baseline Hardware Requirements][requirements.html#baselinehardwarereq].

It's highly recommended that you install the TeamForge Baseline services on a separate server as the baseline process can consume considerable CPU and database resources. For more information, see [Install TeamForge in a Distributed Setup][distributed_install_rhel_centos].


## How to enable Baseline for projects?

The Baseline tool is enabled by default for any new project created after you install Baseline on your site. However, you must enable Baseline for old projects that were created before Baseline installation.

To add the Baseline tool to an existing TeamForge project: 

1. Log on to TeamForge and select a project from the **My Workspace** menu.
2. Select **Project Admin > Tools** from the **Project Home** menu. 
3. Select the **Baselines** check box and click **Save**. 

   {% include image.html file="enable-baseline.png" caption="Enable Baselines for projects created before Baseline installation" %}

   A new tool, **Baselines**, is added to the **Project Home** menu.

   {% include image.html file="baseline-in-projectadmin.png" caption="Baselines tool added to the Project Home menu" %}

To use TeamForge Baselines, a TeamForge user must have the Baseline license and the required baseline permissions to perform various functions. 

For example, a user with the **VIEW ONLY** permission can view baselines and baseline definitions, search for baselines and baseline definitions, and compare baselines. For more information about baseline permissions, see [What are the permissions associated with the Baseline tool?][baseline-overview.html#baselinepermissions]


{% include links.html %}