---
title: What's New in TeamForge 22.1?
keywords: release notes
tags: [release_notes]
sidebar: teamforge_sidebar
permalink: teamforge-new.html
last_updated: Dec 07, 2022
layouts: "pagefaqs"
summary: TeamForge 22.1 has a lot of new features and enhancements. Here's a list of a few release-defining new features in TeamForge 22.1.
---

## Release Information

* **Released on**: Dec 07, 2022
* **GA Version**: 22.1.411

## Support for Review Board {{site.data.identifiers.review_board_os76}}

TeamForge 22.1 supports integration with Review Board {{site.data.identifiers.review_board_os76}}. Review Board {{site.data.identifiers.review_board_os76}} supports new capabilities, performance improvements, and fixes to some of the existing defects and security vulnerabilities. For more information, see [Review Board 4.0.6 Release Notes](https://www.reviewboard.org/docs/releasenotes/reviewboard/4.0.6/).

## Support for Nexus {{site.data.identifiers.nexus3}}

TeamForge 22.1 supports integration with Nexus {{site.data.identifiers.nexus3}}. Nexus {{site.data.identifiers.nexus3}} supports new capabilities, performance improvements, and fixes to some of the existing defects and security vulnerabilities. For more information, see [Nexus Repository 3.41.1 Release Notes](https://help.sonatype.com/repomanager3/product-information/release-notes/2022-release-notes/nexus-repository-3.41.0---3.41.1-release-notes).

## Compliance with Section 508 Standards

* The following TeamForge 22.1 modules are verified to comply with Section 508 standards for 1194.22 Web-based intranet and internet information and applications:
  * Trackers
  * Documents
  * Baselines
* Supported Standards: A, C, D, G, H, K, L, N
* For more information, see [www.section508.gov](https://www.section508.gov/).

## File Releases (FRS)—Download Count for Files

TeamForge 22.1 lets you track the number of downloads for each file under **File Releases> Package > Release** within the FRS module. This helps you understand the number of downloads and then take an informed decision on whether to retain or delete a file based on the number of downloads.

![FRS File Downloads Count](images/frsfiledownloadcount.png)

## Fixed in Release and Reported in Release as Multi-select Fields

* You can now select multiple releases for the **Fixed in Release** and **Reported in Release** fields.
* Projects often have several maintenance/release branches and if there is an issue, it might affect one or more releases (branches), and the fix would typically apply to several releases. Having the ability to select multiple releases helps with the clear definition of the release content.

  ![multi select fields](images/multiselectfields.png)

## Tracker Dependency Updates Within Change Log  

* Artifact dependency updates such as adding or removing parent or child artifact are now added to the artifact's **Change Log** tab.
* The dependency change log includes information such as the user who updated the dependency, the time when the update was done, and a brief description of the old and new dependency values.
* This change log can come in handy for auditing purposes.
  
  ![dependency change log](images/dependencychangelog.png)  


## Export Associations in Trackers

You can now export artifact associations from the following pages:

* Tracker list view
* Planning Folder list view
* Tracker table report

  ![export tracker associations](images/exportassociations.png)  

## Show Annotations in Source Code > Tags view

You can now view annotations for tags in the **Source Code > Tags** **List View** tab.

* Annotation provides a more detailed description of a tag
* Annotation helps developers better understand a tag

  ![annotations](images/annotations.png)  

## Git Integration 22.1.0-3.3.11

TeamForge 22.1 supports integration with Git 3.3.11.

## Install / Upgrade

TeamForge 22.1 supports {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}.

{% include links.html %}
