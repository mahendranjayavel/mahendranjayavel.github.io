---
title: pasql-reporting-wrapper
keywords: postgres backend
tags: [datamart, postgres, scripts, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: psql-reporting-wrapper.html
last_updated: Mar 14, 2018
summary: The psql-reporting-wrapper script is used to connect to the datamart. 
---
**Usage**

```shell
sudo [RUNTIME_DIR]/scripts/psql-reporting-wrapper
````

**Comments**

* Run this script as a sudo user.
* Run this script with the postgres backend.
* You have full write access to the database for executing queries.

{% include note.html content="This script is not supported in the Oracle backend." %}

{% include links.html %}