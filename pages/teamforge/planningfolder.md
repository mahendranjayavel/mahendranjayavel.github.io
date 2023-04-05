---
title: Planning Folder Overview
keywords: planning folder
tags: [project_admin_tasks, planning_folder, boards]
sidebar: teamforge_sidebar
permalink: planningfolder.html
last_updated: Mar 15, 2018
summary: A planning folder is a way to organize work into feasible chunks and monitor its progress. As a project admin or as a user with the appropriate permissions, create and populate all the planning folders you need to capture the work you are planning.
---
When you've thought through your plan, express it in one or more planning folders.
  {% include tip.html content="It often makes sense to set up planning folders _after_ you have outlined and analyzed the features you plan to deliver. See [Define the Scope of Your Project][scope]." %}

For your agile projects, you have the option to create planning folders specific to iterations and releases, or you can create generic planning folders which you may customize later. When you've thought about the general categories the work falls into, you are ready to create planning folders that reflect those ideas.

A planning folder can represent:

* A set of tasks, such as Iteration 3, or "Initial infrastruture development". 
* A period of time, such as "April", or "Q2-2010".
* A phase of development, such as "Testing" or "Deployment".
* A component of the product, such as "Chapter 12" or "Rear stabilizer".

Navigate to **Project Home > Trackers** page and click the _All_ tab under the _Planning Folders_ section to see the statuses of the planning folders.

{% include image.html file="planningfoldertree.png" %}

Planning folder with "Freeze" status (introduced in TeamForge 18.1):

{% include image.html file="planningfolder-status-freeze-2.png" %}

When you've set up your planning folders, you have four views available to work with them:

{% include image.html file="listplantrack01.png" %}

* **LIST**: The list view.
* **PLAN**: The planning board view.
* **TASK**: The task board view.
* **KANBAN**: The kanban board view.

#### Related Links

* [What is a planning folder?][planningfolder-faqs.html#whatisaplanningfolder]
* [Manage Statuses for a Planning Folder][planningfolderstatus]

## Ranking in Planning Folders

The ranking logic has been revamped in TeamForge 17.11 to improve the overall Planning Folder performance. This new ranking logic is applied to artifacts inside planning folders while you upgrade to TeamForge 17.11, due to which data migration can take longer than usual while upgrading to TeamForge 17.11. The time taken for data migration is proportional to the number of artifacts available inside individual planning folders. You can use the following queries to find out the total number of artifacts and the the total number of artifacts that are inside planning folders.

* The following query can get you the total number of artifacts:

```shell
select count(id) as total_artifacts from artifact;
````

* The following query can get you the total number of artifacts that are inside planning folders:

```shell
select count(a.id) as artifacts_with_pf from artifact a, item i where a.id = i.id and i.planning_folder_id like 'plan%' and i.is_deleted <> '1';
````

CollabNet's Performance Lab test results show that it takes 11 minutes approximately to migrate (apply the new ranking logic) a site that with 245K artifacts in total, of which around 46K artifacts were placed inside planning folders.

{% include note.html content="With this new light weight ranking function, the hidden URL, which was used by project administrators to reset ranks for a given project, is no longer supported." %}

{% include links.html %}