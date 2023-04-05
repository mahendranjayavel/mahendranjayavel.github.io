---
title: Known Issues in TeamForge 22.1
keywords: known, issues, late, breaking, workaround, work, around
tags: [release_notes]
sidebar: teamforge_sidebar
folder: teamforge
permalink: teamforge-known.html
last_updated: Dec 07, 2022
summary: The following noteworthy issues, including any workarounds we may have, are known to exist in the TeamForge 22.1 release. These issues would be resolved in an upcoming release.
---

<!-- artf421451 : Misalignment of Created In and Updated On columns on sorting -->
* The **Created In** and **Updated On** column headers of the Baselines View page are misaligned as soon as you sort the table by those columns.
<!-- https://forge.collab.net/sf/go/artf422083 -->
* The `git clone` scp command, which includes a new `-O` option, would fail with the following error if used with some of the older OpenSSH clients. 
  
  `unknown option -- O`

  Run the git clone scp command without the `-O` option. You can also upgrade your client if you want to run the git clone scp command with the `-O` option.


{% include links.html %}
