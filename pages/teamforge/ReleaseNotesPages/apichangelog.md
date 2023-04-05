---
title: REST API Change Log—TeamForge 22.1
sidebar: teamforge_sidebar
tags: [REST, extend_teamforge, ctf_22.1]
permalink: apichangelog.html
last_updated: Dec 07, 2022
summary: Here's what's new with the TeamForge 22.1 REST APIs as compared to TeamForge 22.0.  
---

* Fixed an issue with the `GET /documents/{docid}/versions/{versionid}/download` API call that prevented users from downloading a specific document version. 
* Fixed an issue with the `PATCH /ctfrest/tracker/v1/fields/{fieldId}` API call that prevented users from creating new field values.
* Fixed an issue with the `GET /users` API call that returned the list of users even if the call was not having a valid authorization token.

{{site.data.alerts.hr_shaded}}
#### Related Links
{% include apidoclinks.html %}


{% include links.html %}