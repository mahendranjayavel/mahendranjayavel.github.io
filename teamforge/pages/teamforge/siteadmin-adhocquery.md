---
title: Query the TeamForge Database (Ad Hoc Database Query)
keywords: ad hoc, database, query 
tags: [site_admin_tasks]
sidebar: teamforge_sidebar
permalink: siteadmin-adhocquery.html
last_updated: Jun 23, 2020
summary: You can query the database if you are a site administrator or have been given access to System Tools by another site administrator.
---
You can raise a database query using the **Admin > System Tools > Ad Hoc Database Query** page.

{% include note.html content="This feature is not available for sites that use the Oracle database." %}

In the **Ad Hoc Database Query** page, select a data store, `Operational Datastore` or `Datamart` or `Baseline` or `WEBR`, type the "select" query and click **Run Query**. 

{% include image.html file="siteadmin-adhoc-database-query.png" caption="Ad Hoc Database Query against selected database" %}

For security reasons, the `sfuser` and `password_history` tables of the operational datastore are restricted for ad hoc querying from the **Admin > System Tools > Ad Hoc Database Query** page. Alternatively, use the following views, `sfuser_view` and `password_history_view`, for retrieving all other data but passwords.

{% include note.html content="The results of your query may be limited or your query session may timeout as per the settings in the `site-options.conf` file." %}

You can submit read-only queries of the format: 

```shell
SELECT [FROM][WHERE][GROUP BY] [HAVING] [ORDER BY]
````

You can use the following special keywords while drafting the query:

* "\d" or "show tables" - To list all the tables.
* "\d \<table name\> - To view the description of a specific table.
* "select * from \<table name\> - To view all the contents of a specific table.


{% include links.html %}