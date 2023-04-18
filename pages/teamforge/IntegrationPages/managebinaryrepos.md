---
title: Manage Binary Repositories
keywords: binary, repository, create, delete, link, maven
tags: [ctf_19.2, binaries, source_code]
sidebar: teamforge_sidebar
permalink: managebinaryrepos.html
last_updated: Jul 24, 2019
summary: With TeamForge—Nexus integration enabled, you can create one or more binary repositories and link them to your project.
---

## Create a Binary Artifact Repository

{% include note.html content="Before you can create a repository for binary artifacts, a site administrator must set up TeamForge-Nexus integration and add one or more binary servers to your TeamForge site." %}

1. Click **BINARIES** from the **Project Home** menu.
2. Select **Create Nexus3 Repository** from **Create Repository** drop-down list. You are redirected to Nexus 3 application.
   {% include important.html content="TeamForge-Nexus 3 integration does not support creating a repository from within TeamForge **Binaries** page." %}
3. Create the repository from within the Nexus 3 application.

The binary repository is created.

## Link Binary Artifact Repository to Project

You can link existing binary artifact repositories, if any, to your project.

{% include note.html content="Earlier, only project admins can link the repository to a project. From TeamForge 18.2, any user with the permission to create repositories can link the repository to a project." %}

1. Click **BINARIES** from the **Project Home** menu.
2. Click **Link Existing Repository**.
3. Select a repository from the list of binary repositories and click **Link to Project**.


## Delete a Binary Artifact Repository

You must have the required permission to delete binary repositories. As a project admin, you can use the delete option only to unlink the repository from a project. If you want to delete a repository from the Nexus, login as a Nexus admin.

1. Click **BINARIES** from the **Project Home** menu.
2. In the list of the repositories, select the repository you want to delete and click **Delete**. The following confirmation message appears: 
   ```shell
   This repository will no longer be accessible. Your site administrator can relink it later. Are you sure you want to unlink this repository?
   ````
3. Click **OK** to delete.

The repository is deleted.

{% include note.html content="This deletion dissociates the repository from your project; only the Site Admin can reinstate the repository." %}

{{site.data.alerts.hr_shaded}}
#### Related Links

* [TeamForge Binary Integration Overview][managebinaries]
* [Install Nexus][installnexus]
* [Install the TeamForge-Nexus Integration Plugin][installnexusplugin]
* [TeamForge-Binary Integration FAQs][binaries-faqs]

{% include links.html %}