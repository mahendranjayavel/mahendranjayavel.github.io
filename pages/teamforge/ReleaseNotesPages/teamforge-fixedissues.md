---
title: What's Fixed in TeamForge 22.1?
keywords: release, notes, fixed, issues, bug, fixes
tags: [release_notes]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforge-fixedissues.html
last_updated: Dec 07, 2022
summary: Here's a list of few noteworthy issues fixed in TeamForge 22.1.
---

<!-- See CRI 22.1 List: https://forge.collab.net/sf/go/artf421181  -->

In addition to fixing a few security vulnerabilities, the following issues were also fixed in TeamForge 22.1. 

* Fixed the discrepancy between the Last Status Change dates on the artifact (as found in the UI) and on the exported Excel sheet. 
* Fixed an issue that rendered the attachment in an artifact (the source artifact) inaccessible when you delete the other artifact which was cloned from the source artifact.
<!-- https://forge.collab.net/sf/sfmain/do/go/artf421683 -->
* Added a cron job to delete unused messages (with msg_status as DELIVERED) at regular intervals (every one hour) in the WEBR tables. A corresponding log entry will be posted to `webr/service.log`. 
* Fixed an issue with the TeamForge Desktop application that caused the date in user-defined date fields to change even when the user was only changing the other fields.
* Fixed an issue that rendered the SOAP service unavailable after TeamForge server restart. 
* Restored the horizontal scroll bar to scroll the Documents folder tree structure horizontally. 
* Fixed an issue with the Documents module that prevented users from viewing the default reviewers list.
* Fixed the post upgrade ETL failure issue found on TeamForge 22.0 sites that use Oracle 19C. 
* Fixed an issue with the `GET /documents/{docid}/versions/{versionid}/download` API call that prevented users from downloading a specific document version. 
* Fixed an issue with the `PATCH /ctfrest/tracker/v1/fields/{fieldId}` API call that prevented users from creating new field values.
* Fixed an issue with the `GET /users` API call that returned the list of users even if the call was not having a valid authorization token.
* Fixed an issue that prevented users from creating Baseline Definitions if the repository has no tags.
* Fixed a UI issue to properly align the **Automatically adjust Remaining and Actual Effort** field in the UI.
* Fixed the jssecacert-related issue that caused ETL job failures.
* Fixed the FRS download count discrepancy. The download count now includes the downloads done via the CLI as well. 
* Changed the **Status** label in the **Associations** tab as **Status Type/Status** to avoid ambiguities.
* Updated the FRS module so that file download count is now tracked at the file level.
* Fixed the Baselines view permission issue that prevented users with the right permissions from viewing Baselines that are in DRAFT status.
* Upgraded NPM to version 6.13.4 to fix security vulnerabilities.
* Fixed a UI issue that prevented users from scrolling through the list of reviews in the Review Board.
* Fixed security vulnerabilities in the following areas:
  * Jenkins integration plugin
  * WebConnect
  * Jquery-related
  * Apache Struts-related

**TeamForge SCM—Bug Fixes**

* Fixed the Pentest issue reported—Stored XSS on Create File/Folder in Git repository.
* Fixed the duplicate user name issue with the **Add protected branch role** modal. 
* Git LFS-enabled repositories—fixed the authentication issue during `git push` on Windows clients with SSH protocol.
* Fixed a text formatting issue to show the Git committer name properly in the **Source Code > Changes** tab. 

{% include links.html %}