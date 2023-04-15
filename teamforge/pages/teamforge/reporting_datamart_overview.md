---
title: Advanced Reporting and Datamart Access
keywords: advanced reporting and datamart access
tags: [ctf_20.0, ctf_18.3, project_admin_tasks, project_member_tasks, datamart, reports, etl]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Jan 30, 2020
layouts: "pagefaqs"
permalink: reporting_datamart_overview.html
summary: Using external reporting and OLAP tools, query the datamart directly and generate reports. The database schema diagrams provide the means to create advanced query scripts to extract required information from the datamart.
---

Accessing the datamart for reporting provides more analytical data than is provided by the TeamForge user interface options. The external tool must connect directly to the datamart and is then granted read-only permission to all data in the datamart.

 {% include note.html content="It is recommended that you limit the access to the datamart to a limited set of trusted users." %}


## Datamart Schemas

The `Users`, `SCM`, and `Tracker` schemas are documented here for use in queries to the datamart. The datamart uses a "Star Schema" design for tables.

### User Schema

Query the user schema to obtain useful information in the user database tables detailed here in a schema diagram.

User schema contains user login information; TeamForge captures one fact row for each user that is logged in during the day.

 {% include image.html file="user-schema-image-new.png" %}

#### Description of User Schema

 * **etl_job**
   Used to track the ETL run status. There is one record per ETL run for a job, for example, Tracker ETL or User ETL. `etl_job`has a 1-to-many relationship with `audit_dimension` since a job may update more than one fact table. All report generation queries must "join" the `etl_job` table with the condition `etl_job.status=1`, thereby discarding data from incomplete ETL runs.

 * **audit_dimension**
   Holds metadata about fact table records. There is one record per fact table for an ETL run.

 * **date_dimension**
   Conformed dimension used for all transaction times.

 * **user_dimension**
   Used for string user attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_super_user`, `status`, and `license_type` are the SCD-2 fields.

 * **activity_dimension**
   Conformed dimension that stores the activity or transaction names for various activities being tracked.

 * **user_transaction_fact**
   A fact-less fact table with user data of "daily" granularity.

#### Sample Queries

You can obtain useful user information by querying the user database, and further refine the results by using filters on the "date", "user type" (admin or non), "status", and "license type" fields. For example:

 * Number of users who are logged in, by day, over a period of time:

   ```shell
   SELECT c.date_of_trans as Date, count(distinct(b.id)) as NumUsers            
   FROM user_transaction_fact a, user_dimension b, date_dimension c, etl_job d            
   WHERE a.user_key=b.user_key and a.trans_date_key=c.date_key and a.job_key=d.job_key                
   and d.status=1 and c.date_of_trans >= '2012-12-17' and c.date_of_trans <= '2012-12-21'            
   GROUP BY c.date_of_trans
   ```

 * List of users who have logged in:

   ```shell  
   SELECT c.date_of_trans as Date, b.username as UserName
   FROM user_transaction_fact a, user_dimension b, date_dimension c, etl_job d
   WHERE a.user_key=b.user_key and a.trans_date_key=c.date_key and a.job_key=d.job_key
   and d.status=1 and c.date_of_trans >= '2012-12-17' and c.date_of_trans <= '2012-12-21'
   GROUP BY c.date_of_trans, b.username
   ````

### SCM Schema

Query the SCM schema to obtain useful commit information in the SCM tables detailed here in a schema diagram.

 {% include image.html file="scm-schema-image-new.png" %}

#### Description of SCM Schema

 * **etl_job**
   Used to track the ETL run status. There is one record per ETL run for a job, for example, Tracker ETL or User ETL. `etl_job` has a 1-to-many relationship with `audit_dimension` since a job may update more than one fact table. All report generation queries must "join" the `etl_job` table with the condition `etl_job.status=1`, thereby discarding data from incomplete ETL runs.

 * **audit_dimension**
   Holds metadata about fact table records. There is one record per fact table for an ETL run.

 * **date_dimension**
   Conformed dimension used for all transaction times.

 * **activity_dimension**
   Conformed dimension that stores the activity or transaction names for various activities being tracked.

 * **user_dimension**
   Used for string user attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_super_user`, `status`, and `license_type` are the SCD-2 fields.

 * **project_dimension**
   Used for storing project attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_deleted` and `project_access_level` are the SCD-2 fields.

 * **repository_dimension**
   Used for storing repository attributes and is a "slowly changing dimension of type 1."

 * **scm_transaction_fact**
   The fact table for SCM activities with "transaction" granularity. TeamForge inserts a row in this table for every SCM activity that it processes in a transaction.

     * TeamForge object id , if available.
     * Number of files added, deleted, modified, moved, copied, if applicable.

#### Sample Queries

You can obtain useful SCM information by querying the SCM database. For example:

 * Number of SCM commits, sorted by date:

   ```shell
   select b.date_of_trans as Date, 
            count(a.scm_transaction_fact_key) as NumCommits
            from scm_transaction_fact a, date_dimension b
            where a.trans_date_key=b.date_key
            group by b.date_of_trans
   ````

 * Number of SCM commits, with quarterly trend:

   ```shell
   select 'Q'||b.quarter as Quarter, 
            count(a.scm_transaction_fact_key) as NumCommits
            from scm_transaction_fact a, date_dimension b
            where a.trans_date_key=b.date_key
            group by b.quarter 
    ````

 * List of users who made commits.

   ```shell
   select b.username as UserName, 
            count(a.scm_transaction_fact_key) as NumCommits
            from scm_transaction_fact a, user_dimension b
            where a.user_key=b.user_key
            group by b.username
    ````

 * Project-wise commit data:

   ```shell
   select b.id as ProjectId, b.title as ProjectName, 
            count(a.scm_transaction_fact_key) as NumCommits
            from scm_transaction_fact a, project_dimension b
            where a.project_key=b.project_key
            group by b.id, b.title
   ````

 * Commits by date, in a specific project:

   ```shell
   select c.date_of_trans as Date, b.id as ProjectId, b.title as ProjectName, 
            count(a.scm_transaction_fact_key) as NumCommits
            from scm_transaction_fact a, project_dimension b, date_dimension c
            where a.project_key=b.project_key and a.trans_date_key=c.date_key
              and b.id='proj1008'
            group by c.date_of_trans, b.id, b.title
   ````

### Tracker Schema

Query the tracker schema to obtain useful information in the tracker database tables detailed here in a schema diagram.

TeamForge constructs the state or field values of the artifact during each update. The schema addresses both activity queries and total count queries.

TeamForge includes information for the activities in fixed fields, default artifact fields, and flex fields. This information includes artifact `create`, `move`, `update` for fixed-value changes, `delete`, `open_to_close`, and `close_to_open`.

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[![Tracker Schema](images/artifact-schema-image-new1.png)](images/artifact-schema-image-new1.png)
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
{% include image.html file="artifact-schema-image-new1.png" %}
{% endunless %}

#### Description of Tracker Schema

* **etl_job**
  Used to track the ETL run status. There is one record per ETL run for a job, for example, Tracker ETL or User ETL. `etl_job` has a 1-to-many relationship with audit_dimension since a job may update more than one fact table. All report generation queries must "join" the `etl_job` table with the condition `etl_job.status=1`, thereby discarding data from incomplete ETL runs.

* **audit_dimension**
  Holds metadata about fact table records. There is one record per fact table for an ETL run.

* **date_dimension**
  Conformed dimension used for all transaction times.

* **user_dimension**
  Used for string user attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_super_user`, `status`, and `license_type` are the SCD-2 fields.

* **project_dimension**
  Used for storing project attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_deleted` and `project_access_level` are the SCD-2 fields.

* **pf_dimension**
  The planning folder dimension for storing planning folder attributes. Use this table to generate reports without planning folder hierarchy.

* **pf_bridge**
  A table for the planning folder hierarchy containing end-of-day status. `pf_bridge` is a "slowly changing dimension of type 2 (SCD-2)." You must limit queries to a given parent planning folder while joining with the `pf_bridge` table.Use `pf_bridge` to generate reports around planning folder hierarchy by joining with parent tables such as `artifact_daily_snapshot_fact` or `artifact_transaction_fact`.

  Joining `pf_bridge` with `artifact_transaction_fact` generates correct results only if end-of-day in queries is set to "12:00 a.m.". While formulating queries with `pf_bridge`, please note:

  * `parent` and `child` fields — Contain values from `pf_dimension.pf_key;` a depth of 0 indicates self.

  * `leaf` field — Is true if the child is a leaf node, otherwise false. Every planning folder will have an entry here with a depth of 0; every parent planning folder will have entries for all of its children, recursively, up to the leaf node of all branches.

  * `effective_from` and `effective_till` fields — Indicate the period when the parent-child relationship is correct, and can be used in queries to get the hierarchy for a specified time period.

 * **tracker_dimension**
   Used for storing tracker attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_deleted` is the changing field that act as a filter for reports.

 * **artifact_dimension**
   Used for storing artifact data and is a "slowly changing dimension of type 1."

 * **group_dimension**
   Used for holding values of the TeamForge tracker field "group". `group_dimension` has values for all artifacts from all Trackers.

 * **status_dimension**
   Used for holding values of the TeamForge tracker field "status". The `status_value_class` field represents the meta-status of an artifact and has values "Open" and "Close". `status_dimension` has values for all artifacts from all Trackers.

 * **category_dimension**
   Used for holding values of the TeamForge tracker field "category". `category_dimension` has values for all artifacts from all Trackers.

 * **customer_dimension**
   Used for holding values of the TeamForge tracker field "customer". `customer_dimension` has values for all artifacts from all Trackers.

 * **release_dimension**
   Used for holding values of the TeamForge tracker fields "Reported in Release" and "Fixed in Release". `release_dimension` has values for all artifacts from all Trackers.

 * **artifact_transaction_fact**
   Every change in fixed or default artifact field values, or to project or tracker artifacts, results in a row inserted to `artifact_transaction_fact`. Changes to flex-field values, adding comments, attachments, and so on do not add a row to the table. The `artifact_dimension.date_last_modified` field has the time in the source tracker at the time of the `ETL run.artifact transaction fact` can be used to generate reports around activities such as create, update, delete and move, and for intra-day reports. `artifact_transaction_fact` has a "transaction" granularity.

 * **artifact_daily_snapshot_fact**
   An aggregate table that holds the daily snapshot data or end-of-day status. `artifact_daily_snapshot_fact` can be used to generate reports for artifact close & re-open counts. It is recommended to use this table for end-of-day reports as it has fewer rows compared to `artifact_transaction_fact`. `artifact_daily_snapshot_fact` has a "daily" granularity.

 * **team_dimension**
   A dimension for holding values of Teams. This is a "slowly changing dimension of type 2 (SCD-2)". Use this table to generate reports without team hierarchy.

 * **team_membership_dimension**
    This is more or less a factless fact table that holds the changes in terms of Team memberships. This is a "slowly changing dimension of type 2 (SCD-2)".

 * **team_bridge**
   A table for handling team hierarchy containing end-of-day status. team_bridge is a "slowly changing dimension of type 2 (SCD-2)." You must limit queries to a given parent team while joining with the `team_bridge` table. Use `team_bridge` to generate reports around team hierarchy (ex: a report on all artifacts assigned to Team 1 and its child teams) by joining with parent tables such as `artifact_daily_snapshot_fact` or `artifact_transaction_fact`.

   Joining `team_bridge` with `artifact_transaction_fact` generates correct results only if end-of-day in queries is set to "12:00 a.m.". While formulating queries with `team_bridge`, please note:

     * `parent_surrogate_id` and `child_surrogate_id` fields — Contain values from `team_dimension.surrogate_id;` a depth of 0 indicates self.

     * `leaf` field — Is true if the child is a leaf node, otherwise false. Every team will have an entry here with a depth of 0; every parent team will have entries for all of its children, recursively, up to the leaf node of all branches .

     * `effective_from` and `effective_till` fields — Indicate the period when the parent-child relationship is correct, and can be used in queries to get the hierarchy for a specified time period.

         {% include note.html content="`team_dimension` is a `slowly changing dimension of type 2`. So, make sure that the JOIN clause in queries that join team_bridge and team_dimension includes the date and time as well." %}

 * **flex_field_dimension**
   Used for storing information about flex fields and is a "slowly changing dimension of type 2 (SCD-2)".

 * **flex_field_value_dimension**
   Used for storing information about flex field values and is a "slowly changing dimension of type-2 (SCD-2)".
 
 * **artifact_dependency_dimension**
   Used for storing relationship between artifacts and is a "slowly changing dimension of type-2 (SCD-2)".

 * **artifact_dependency_bridge**
   A table for the artifacts hierarchy containing end-of-day status. This is a "slowly changing dimension of type-2 (SCD-2). Use this table to generate reports around artifact hierarchy.

 * **artifact_flex_fields**
   A table to bind the flex field updates on artifacts into a well formed XML, which stores the 'field key', 'value' and 'type' of the flex field.


**Schema diagram for XML to non-XML conversion**

<!-- Use this for web output -->
{% unless site.output == "pdf" %}
[![Schema for XML to non-XML conversion](images/17-4-artifact-schema-image-new2.png)](images/17-4-artifact-schema-image-new2.png)
{% endunless %}

<!-- Use this for pdf output -->
{% unless site.output == "web" %}
{% include image.html file="17-4-artifact-schema-image-new2.png" %}
{% endunless %}


#### Description of Schema used for XML to non-XML Conversion

 * **flex field dimension**
  Used for storing information about flex fields and is a "slowly changing dimension of type 2 (SCD-2)".

 * **flex field value dimension**
  Used for storing information about flex field values and is a "slowly changing dimension of type-2 (SCD-2)".

 * **artifact flex fields**
   A table to bind the flex field updates on artifacts into a well formed XML, which stores the 'field key', 'value' and 'type' of the flex field.

 * **artifact daily snapshot fact**
   An aggregate table that holds the daily snapshot data or end-of-day status. `artifact_daily_snapshot_fact` can be used to generate reports for artifact close & re-open counts. It is recommended to use this table for end-of-day reports as it has fewer rows compared to `artifact_transaction_fact`. `artifact_daily_snapshot_fact` has a "daily" granularity.

 * **artifact transaction fact**
   Every change in fixed or default artifact field values, or to project or tracker artifacts, results in a row inserted to `artifact_transaction_fact`. Changes to flex-field values, adding comments, attachments, and so on do not add a row to the table. The `artifact_dimension.date_last_modified` field has the time in the source tracker at the time of the ETL run. `artifact transaction fact` can be used to generate reports around activities such as create, update, delete and move, and for intra-day reports. `artifact_transaction_fact` has a "transaction" granularity.

 * **tracker dimension**
   Used for storing tracker attributes and is a "slowly changing dimension of type 2 (SCD-2)." `is_deleted` is the changing field that act as a filter for reports.

 * **ss_flex_fields_bridge**
   A table to hold details about single select flex field assigned to an artifact. To get the details of the assigned artifact, the "ss_flex_fields_bridge" table must be joined with the "artifact_transaction_fact" table and the "artifact_dimension" table.

 * **user_flex_fields_bridge**
   A table to hold details about user flex field assigned to an artifact. To get the details of the assigned artifact, the "user_flex_fields_bridge" table must be joined with the "artifact_transaction_fact" table and the "artifact_dimension" table.

 * **text_flex_fields_bridge**
   A table to hold details about text flex field assigned to an artifact. To get the details of the assigned artifact, the "text_flex_fields_bridge" table must be joined with the "artifact_transaction_fact" table and the "artifact_dimension" table.

 * **date_flex_fields_bridge**
   A table to hold details about date flex field assigned to an artifact. To get the details of the assigned artifact, the "date_flex_fields_bridge" table must be joined with the "artifact_transaction_fact" table and the "artifact_dimension" table.

 * **ms_flex_fields_bridge**
   A table to hold details about multi select flex field assigned to an artifact. To get the details of the assigned artifact, the "ms_flex_fields_bridge" table must be joined with the "artifact_transaction_fact" table and the "artifact_dimension" table.


#### Sample Queries

You can obtain useful tracker information by querying the tracker database. For example:

* Number of artifacts created in a tracker, sorted by date:

  ```shell
  SELECT b.date_of_trans, count(a.artifact_key) 
            FROM artifact_transaction_fact a, date_dimension b, tracker_dimension c 
            WHERE a.trans_date_key=b.date_key and a.tracker_key=c.tracker_key 
            and a.activity='Create' and c.title='Tracker-1' 
            and b.date_of_trans >= '2011-10-31' and b.date_of_trans <= '2011-11-07' 
            GROUP BY b.date_of_trans 
            ORDER BY b.date_of_trans
  ````

 * Number of artifacts created in a tracker, sorted by date and priority:

   ```shell
   SELECT b.date_of_trans, d.title as Tracker, 'P'||a.priority as Priority,c.id ArtifactId 
            FROM artifact_transaction_fact a, date_dimension b, artifact_dimension c, tracker_dimension d 
            WHERE a.trans_date_key=b.date_key and a.artifact_key=c.artifact_key and a. tracker_key=d.tracker_key 
            and a.activity='Create' and d.title='Tracker-1' 
            and b.date_of_trans >= '2011-10-31' and b.date_of_trans <= '2011-11-07' 
            ORDER BY b.date_of_trans, d.title, Priority
   ````

 * Number of artifacts created on a particular day in a particular planning folder:

   ```shell
   SELECT b.date_of_trans, c.id ArtifactId, c.title 
            FROM artifact_transaction_fact a, date_dimension b, artifact_dimension c, pf_dimension d, pf_bridge e  WHERE a.trans_date_key=b.date_key and a.artifact_key=c.artifact_key and a.pf_key=e.child 
            and d.pf_key=e.parent and a.activity='Create' and d.title='Pf-1' 
            and '2011-10-31' >= e.effective_from and '2011-10-31' < e.effective_till 
            and b.date_of_trans = '2011-10-31' 
            ORDER BY b.date_of_trans
   ````

 * Number of closed tracker artifacts, sorted by day:

   ```shell
   SELECT b.date_of_trans, count(a.artifact_key) 
            FROM artifact_daily_snapshot_fact a, date_dimension b, tracker_dimension c 
            WHERE a.trans_date_key=b.date_key and a.tracker_key=c.tracker_key and a.closed_today_flag='true' 
            and c.title='Tracker-1' and b.date_of_trans >= '2011-10-31' and b.date_of_trans <= '2011-11-07' 
            GROUP BY b.date_of_trans 
            ORDER BY b.date_of_trans
   ```` 

 * List of artifacts in the "Open" state, sorted by day:

   ```shell
   SELECT a.date_of_trans, c.id, c.title 
            FROM date_dimension a inner join artifact_daily_snapshot_fact b 
            on a.date_of_trans >= date(b.effective_from) and a.date_of_trans < date(b.effective_till) 
            inner join artifact_dimension c on b.artifact_key=c.artifact_key 
            inner join status_dimension d on b.status_key=d.status_key 
            WHERE d.status_value_class='Open' and a.date_of_trans >= '2011-10-31' 
            and a.date_of_trans <= '2011-11-02' 
            ORDER BY a.date_of_trans
   ````

 * List of artifacts assigned to a team (including child teams) on a given day:

   ```shell
   select ad.id as artifact_id
           from artifact_transaction_fact fact 
           inner join date_dimension dd on (dd.date_of_trans + 1) between fact.effective_from and fact.effective_till
           inner join team_dimension child_td on child_td.team_key = fact.team_key
           inner join team_bridge tb on tb.child_surrogate_id = child_td.surrogate_id and 
                 (dd.date_of_trans + 1) between tb.effective_from and tb.effective_till
           inner join team_dimension parent_td on tb.parent_surrogate_id = parent_td.surrogate_id and 
                 (dd.date_of_trans + 1) between parent_td.effective_from and parent_td.effective_till
           inner join artifact_dimension ad on ad.artifact_key = fact.artifact_key
           inner join etl_job ej on ej.job_key = fact.job_key and ej.status = 1
           where dd.date_of_trans = '2015-01-01' and parent_td.id = 'team1002'
           order by artifact_id
   ````

## Datamart Access Using External Tools {#datamartaccesswithexternaltools}

Use external tools to directly query the PostgreSQL or Oracle datamarts to access more TeamForge data than is available through options on the TeamForge user interface.

### Accessing the Datamart

You can use OLAP or GUI tools to query your datamart directly to procure all the TeamForge data that is relevant to your analysis.

The external tool must be in the same network as the datamart to ensure fast access with a direct connection to the database. On the TeamForge host machine, you must enable `REPORTS_DATABASE_HOST` for remote access.

 {% include note.html content="You only have read access; the datamart does not allow writes." %}

### Enabling the Datamart for Access

You must enable the datamart for direct queries and re-start the site. Once enabled, all data in the datamart can be queried using external tools.


### Enable TeamForge (PostgreSQL Datamart) for Queries from External Tools

You must enable, then re-start TeamForge so that you can use an external tool to query the datamart directly.

You cannot use external reporting tools to connect directly to a datamart if you have a single-box installation using localhost:SERVICES.

 1. Edit the `site-options.conf` file. Set `REPORTS_DB_ACCESS_HOSTS` to the IP address or IP address range (CIDR address) from which the tool will establish connection to the datamart. Specify multiple IPs as a comma-separated list. For example: `REPORTS_DB_ACCESS_HOSTS = 10.0.0.2,10.2.1.0/24`.

    {% include note.html content="If the TeamForge site is not within your network and a Network Address Translation (NAT) is configured, then specify the NAT's external facing IP in the token.  If you have used an `advanced` installation method to install TeamForge, you must also manually add the IP addresses to the pg_hba.conf file." %}

 2. In `site-options.conf` file, set `REPORTS_DATABASE_READ_ONLY_USER` and `REPORTS_DATABASE_READ_ONLY_PASSWORD` with your user and password.

 3. On the TeamForge host machine, enable `REPORTS_DATABASE_HOST` for remote access.

 4. Provision services.

    ```shell
    teamforge provision
    ````

    {% include note.html content="TeamForge 17.4 (and later) installer expects the system locale to be LANG=en_US.UTF-8. TeamForge `provision` command fails otherwise." %}

You can now enable trusted users to establish connections by providing them with values of options `REPORTS_DATABASE_HOST`, `REPORTS_DATABASE_READ_ONLY_USER`, and `REPORTS_DATABASE_READ_ONLY_PASSWORD`.


### Enable TeamForge (Oracle Datamart) for Queries from External Tools

You must enable, then restart TeamForge so that you can use an external tool to query the datamart directly.

You can use external reporting tools to connect directly to a datamart only if you do not have a single-box installation using `localhost:SERVICES`.

 1. In `site-options.conf` file, set `REPORTS_DATABASE_READ_ONLY_USER` and `REPORTS_DATABASE_READ_ONLY_PASSWORD` with your user and password.

 2. On the TeamForge host machine, enable `REPORTS_DATABASE_HOST` for remote access.

 3. Provision services.

    ```shell
    teamforge provision
    ````

    {% include note.html content="TeamForge 17.4 (and later) installer expects the system locale to be LANG=en_US.UTF-8. TeamForge `provision` command fails otherwise." %}

You can now enable trusted users to establish connections by providing them with values of options `REPORTS_DATABASE_HOST`, `REPORTS_DATABASE_READ_ONLY_USER`, and `REPORTS_DATABASE_READ_ONLY_PASSWORD`.


### Common Errors While Connecting to PostgreSQL or Oracle Datamarts

You may encounter these errors while configuring your datamart to allow queries from external tools.

#### PostgreSQL Database Access Error

This error in a PostgreSQL datamart is because TeamForge is not granting access to your IP address.

```shell
Error: psql: FATAL: no pg_hba.conf entry for host "111.111.111.111", user "test", database "datamart"
````
**Solution**: Have the TeamForge administrator grant access to your IP address.


#### PostgreSQL Authentication Error

```shell
Error: psql: FATAL: password authentication failed for user "test"
````

**Solution**: Specify the correct user name and password.


#### PostgreSQL Connection Error

```shell
Error: psql: could not connect to server: Connection refused. Is the server running on host "<datamart-host>" and accepting TCP/IP connections on port 5632?
````

**Solution**:

 * Check the host and port numbers; the database must be running on host "datamart-host" and accept TCP/IP connections on port 5632.

 * Check if remote access is enabled on TeamForge; the Teamforge administrator can enable the required access.


#### Oracle Connection Error

This error in an Oracle datamart occurs when some connection parameters are set incorrectly.

```shell
Error: ORA-12505, TNS:listener does not currently know of SID given in connect descriptor.
````

**Solution**: Check and set your connection parameters appropriately.


### Query PostgreSQL Datamart Based on Flex Fields

Create query scripts to query and extract the required information from the PostgreSQL datamart. Make sure these scripts are available to any user (including users with read-only permission) who wants to execute these scripts. This topic lists the functions and sample queries for a few specific use cases.

 {% capture querypostgresql %}
 
 **Important:** <br><br>

 {% include inline_image.html file="status-success-small.png" %} Log into TeamForge as a Reporting user and run the queries. Note that this is a one-time process. <br><br>
 {% include inline_image.html file="status-success-small.png" %} Use the following flex field functions by joining the flex_field_dimension, artifact_flex_field and artifact_transaction_fact (or) artifact_daily_snapshot_fact tables as it depends on the XML data and flex field key generated by the platform.
  
 {% endcapture %}
 {% include callout.html type="primary" content=querypostgresql %}

#### Common script used across all flex field functions

 ```shell
    CREATE OR REPLACE FUNCTION array_search(needle anyelement, haystack anyarray) 
      RETURNS integer AS 
    $BODY$ 
        SELECT i 
          FROM generate_subscripts($2, 1) AS i 
         WHERE $2[i] = $1 
      ORDER BY i 
    $BODY$ 
      LANGUAGE sql STABLE 
      COST 100; 
 ````

#### Function for Date Flex Fields

**Input Arguments**

  * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

  * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

<u>Date flex field values</u>

  ```shell 
  CREATE OR REPLACE FUNCTION get_artifact_date_value(artifact_xml xml, field_key integer) 
    RETURNS character varying AS 
  $BODY$ 
  DECLARE 
  field_value_key varchar(9055) default ''; 
   BEGIN 
   SELECT cast((xpath('/fields/field/@val',artifact_xml)) [(array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml))::text[]))] as varchar) into field_value_key; 
   Return field_value_key; 
   END; 
  $BODY$ 
    LANGUAGE plpgsql VOLATILE 
    COST 100; 
  ````

<!-- #### Function for Text Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field tables)`.

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

 <u>Text flex field values</u>

  ```shell
  CREATE OR REPLACE FUNCTION replacen(artifact_xml1 xml) 
    RETURNS text AS 
  $BODY$ 
   select replace ((select replace(artifact_xml1::varchar(3000),'<!','&lt;!')),']>',']&gt;') 

  $BODY$ 
    LANGUAGE sql STABLE 
    COST 100; 

   
  CREATE OR REPLACE FUNCTION get_artifact_text_value(artifact_xml xml, field_key integer) 
    RETURNS character varying AS 
  $BODY$ 
   DECLARE 
    field_value_key varchar(9055) default '';  
   BEGIN  
   SELECT cast((xpath('/fields/field/@val',replacen(artifact_xml)::xml)) [(array_search(field_key::text,(xpath('/fields/field/@key',replacen(artifact_xml)::xml))::text[]))] as varchar) into field_value_key; 
   Return field_value_key; 
   END; 
   $BODY$ 
     LANGUAGE plpgsql VOLATILE 
     COST 100;
  ```` -->

#### Function for Single-select Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

<u>Values selected or stored in single-select flex field</u>

  ```shell
  CREATE OR REPLACE FUNCTION get_artifact_select_value(artifact_xml xml, field_key integer) 
    RETURNS character varying AS 
 $BODY$ 
  DECLARE 
   field_value_key varchar(9055) default ''; 
  singleSelectValues varchar(9055) default ''; 
  BEGIN 
   SELECT cast((xpath('/fields/field/@val',artifact_xml)) [(array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml))::text[]))] as varchar) into field_value_key; 
   Select value into singleSelectValues  from flex_field_value_dimension where flex_field_value_key::text = (field_value_key::text); 

  Return singleSelectValues; 
  END; 
 $BODY$ 
   LANGUAGE plpgsql VOLATILE 
   COST 100;
  ````

#### Function for Multi-select Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

 * Specific value(s) stored in the field or the keyword 'ALL' for retrieving all values stored in multi-select flex field.

 * Logical conditional operator. Possible values are 'ALL' or 'ANY'. The argument value of 'ALL' performs a search equivalent to the 'AND' condition and the value of 'ANY' performs a search equivalent to the 'OR' condition.


**Output Arguments**

<u>Values selected or stored in multi-select flex field</u>

```shell
  -----First Execute Inner Function------
-------Inner function start------  
CREATE OR REPLACE FUNCTION get_artifact_multiselect_values_any(artifact_xml xml, field_key integer, selectedfields text[])
RETURNS text AS
$BODY$
DECLARE
fieldValues text;
multiFieldValues text default '';
splitfield text[];
splitfield2 text[];
loop1 integer DEFAULT 1;
 loop2 integer DEFAULT 1;
arrayLength integer DEFAULT 1;
 arrayLength2 integer DEFAULT 1;
multifield text DEFAULT '';
filteredField text Default '';
BEGIN
 Select cast((xpath('/fields/field/@val',artifact_xml))
[array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml)::text[]))]
 as varchar(9055)) into fieldValues;
Select array_length(regexp_split_to_array(fieldValues, ','),1) into arrayLength;
Select regexp_split_to_array(fieldValues, ',') into splitfield;
IF arrayLength IS NOT NULL THEN
        FOR loop1 IN 1..arrayLength LOOP
        Select value into multiFieldValues from flex_field_value_dimension where flex_field_value_key = splitfield[loop1]::integer;
        multifield := concat(multifield,',',multiFieldValues);
        EXIT WHEN loop1 > arrayLength; 
        END LOOP;


        multifield := rtrim(multifield,'" ');
        multifield := ltrim(multifield,',');

Select array_length(regexp_split_to_array(array_to_string(selectedFields,','), ','),1) into arrayLength2;
Select regexp_split_to_array(array_to_string(selectedFields,','), ',') into splitfield2;
IF selectedFields = Array['ALL'] THEN
filteredField:=multifield;
Return filteredField;
ELSE
FOR loop2 IN 1..arrayLength2 LOOP
IF   multifield ~ splitfield2[loop2] THEN
      filteredField := concat(splitfield2[loop2],',',filteredField);
END IF;
EXIT WHEN loop2 > arrayLength2; 
END LOOP;
END IF;
END IF;
filteredField := rtrim(filteredField,'" ');
filteredField := rtrim(filteredField,',');
Return filteredField;
 END;  
$BODY$
LANGUAGE plpgsql VOLATILE
COST 100; 
-------Inner function end------


CREATE OR REPLACE FUNCTION get_artifact_multiselect_value(artifact_xml xml, field_key integer,selectedfields text[],condition character varying)
  RETURNS text as
  $BODY$
  DECLARE
   fieldValues text;
   loop1 integer default 1;
   
   loop2 integer default 1;
  arrayLength1 integer default 1;
  arrayLength2 integer default 1;
  arrayLength3 integer default 1;
  multiFieldValues text default '';
  multifield text DEFAULT '';
  returnvalues text DEFAULT '';
    i integer default 1;
    j integer default 1;
     v_array1 text[]; 
     v_array2 text[]; 
     v_array3 text[];
     results text Default '' ;
     filteredField text Default '';
     count integer default 0;  
   BEGIN
       Select cast((xpath('/fields/field/@val',artifact_xml))[array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml)::text[]))]
       as varchar(9055)) into fieldValues;
       Select array_length(regexp_split_to_array(fieldValues, ','),1) into arrayLength1;
       Select regexp_split_to_array(fieldValues, ',') into v_array1; 
  IF arrayLength1 IS NOT NULL THEN
       FOR  loop1 in 1..arrayLength1 LOOP
       select value into multiFieldValues from  flex_field_value_dimension where flex_field_value_key=v_array1[loop1]::integer;
       multifield := concat(multifield,',',multiFieldValues);
       EXIT WHEN loop1 > arrayLength1;
       multifield := rtrim(multifield,'" ');
       multifield := ltrim(multifield,',');
       END LOOP;
       Select array_length(regexp_split_to_array(multifield, ','),1) into arrayLength2;
       Select regexp_split_to_array(multifield, ',') into v_array2;
       Select array_length(regexp_split_to_array(array_to_string(selectedfields,','), ','),1) into arrayLength3;
       Select regexp_split_to_array(array_to_string(selectedfields,','), ',') into v_array3;

             IF (UPPER(condition)=UPPER('ALL')) THEN
                  IF selectedFields = Array['ALL'] THEN 
                       results:=multifield;
                  ELSE
          IF (v_array2 is not  null AND v_array3 is not null) THEN 
               FOR i in 1..arrayLength3 LOOP
                FOR j in 1..arrayLength2 LOOP
                     IF (v_array3[i]= v_array2[j]) THEN 
                   filteredField := concat(v_array3[i],',',filteredField);
                   
                   count=count+1;
                   EXIT;
                     END IF;
          
               END LOOP;
                 END LOOP;
          ELSE
             results = false;
                 
                END IF;
                IF (count=arrayLength3) THEN
                results=filteredField;
                ELSE 
                results='';
                END IF;
             END IF;
           ELSE 
      
            select get_artifact_multiselect_values_any(artifact_xml,field_key,selectedfields) into returnvalues;
                IF returnvalues IS NOT NULL THEN 
                    results=returnvalues;
                ELSE 
                     results='';
                END IF;
      
           END IF;
  END IF;
  results := rtrim(results,'" ');
  results := rtrim(results,',');
 RETURN(results);
 END;  
$BODY$
LANGUAGE plpgsql VOLATILE
COST 100;
````
       
#### Function for Multi-user Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

 * Specific value(s) stored in the field or the keyword 'ALL' for retrieving all values stored in multi-select flex field.

 * Logical conditional operator. Possible values are 'ALL' or 'ANY'. The argument value of 'ALL' performs a search equivalent to the 'AND' condition and the value of 'ANY' performs a search equivalent to the 'OR' condition.

**Output Arguments**

<u>Values selected or stored in multi-user flex field</u>

```shell
     -----First Execute Inner Function------

 ------Inner function start---
CREATE OR REPLACE FUNCTION get_artifact_user_values_any(artifact_xml xml, field_key integer, selectedfields text[]) 
  RETURNS text AS 
$BODY$ 
DECLARE 
fieldValues text; 
multiFieldValues text default ''; 
splitfield text[]; 
splitfield2 text[]; 
loop1 integer DEFAULT 1; 
 loop2 integer DEFAULT 1; 
arrayLength integer DEFAULT 1; 
 arrayLength2 integer DEFAULT 1; 
multifield text DEFAULT ''; 
filteredField text Default ''; 
BEGIN  
 Select cast((xpath('/fields/field/@val',artifact_xml)) 
[array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml)::text[]))] 
 as varchar(9055)) into fieldValues; 
Select array_length(regexp_split_to_array(fieldValues, ','),1) into arrayLength; 
Select regexp_split_to_array(fieldValues, ',') into splitfield; 
IF arrayLength IS NOT NULL THEN
   FOR loop1 IN 1..arrayLength LOOP 
      Select full_name into multiFieldValues from user_dimension where user_key = splitfield[loop1]::integer; 
      multifield := concat(multifield,',',multiFieldValues); 
      EXIT WHEN loop1 > arrayLength; 
   END LOOP; 
      multifield := rtrim(multifield,'" '); 
      multifield := ltrim(multifield,','); 

     Select array_length(regexp_split_to_array(array_to_string(selectedFields,','), ','),1) into arrayLength2; 
     Select regexp_split_to_array(array_to_string(selectedFields,','), ',') into splitfield2; 
      IF selectedFields = Array['ALL'] THEN 
      filteredField:=multifield;
      Return filteredField;
      ELSE 
          FOR loop2 IN 1..arrayLength2 LOOP 
          IF   multifield ~ splitfield2[loop2] THEN 
        filteredField := concat(splitfield2[loop2],',',filteredField); 
          END IF; 
          EXIT WHEN loop2 > arrayLength2; 
          END LOOP; 
      END IF; 
END IF;
filteredField := rtrim(filteredField,'" '); 
filteredField := rtrim(filteredField,','); 
Return filteredField; 
 END;  
$BODY$ 
  LANGUAGE plpgsql VOLATILE 
  COST 100; 
 
 ------Inner Function End-----

create or replace FUNCTION get_artifact_user_value(artifact_xml xml, field_key integer,selectedfields text[],condition character varying)
   RETURNS text as
  $BODY$
  DECLARE
   fieldValues text;
   loop1 integer default 1;
   
   loop2 integer default 1;
  arrayLength1 integer default 1;
  arrayLength2 integer default 1;
  arrayLength3 integer default 1;
  multiFieldValues text default '';
  multifield text DEFAULT '';
  returnvalues text DEFAULT '';
    i integer default 1;
    j integer default 1;
     v_array1 text[]; 
     v_array2 text[]; 
     v_array3 text[];
     results text Default '' ;
     filteredField text Default '';
     count integer default 0;  
   BEGIN
       Select cast((xpath('/fields/field/@val',artifact_xml))[array_search(field_key::text,(xpath('/fields/field/@key',artifact_xml)::text[]))]
       as varchar(9055)) into fieldValues;
       Select array_length(regexp_split_to_array(fieldValues, ','),1) into arrayLength1;
       Select regexp_split_to_array(fieldValues, ',') into v_array1; 
  IF arrayLength1 IS NOT NULL THEN
       FOR  loop1 in 1..arrayLength1 LOOP
       select full_name into multiFieldValues from  user_dimension where user_key=v_array1[loop1]::integer;
       multifield := concat(multifield,',',multiFieldValues);
       EXIT WHEN loop1 > arrayLength1;
       multifield := rtrim(multifield,'" ');
       multifield := ltrim(multifield,',');
       END LOOP;
       Select array_length(regexp_split_to_array(multifield, ','),1) into arrayLength2;
       Select regexp_split_to_array(multifield, ',') into v_array2;
       Select array_length(regexp_split_to_array(array_to_string(selectedfields,','), ','),1) into arrayLength3;
       Select regexp_split_to_array(array_to_string(selectedfields,','), ',') into v_array3;

             IF (UPPER(condition)=UPPER('ALL')) THEN
                  IF selectedFields = Array['ALL'] THEN 
                       results:=multifield;
                  ELSE
          IF (v_array2 is not  null AND v_array3 is not null) THEN 
               FOR i in 1..arrayLength3 LOOP
                FOR j in 1..arrayLength2 LOOP
                     IF (v_array3[i]= v_array2[j]) THEN 
                   filteredField := concat(v_array3[i],',',filteredField);
                   
                   count=count+1;
                   EXIT;
                     END IF;
          
               END LOOP;
                 END LOOP;
          ELSE
             results = false;
                 
                END IF;
                IF (count=arrayLength3) THEN
                results=filteredField;
                ELSE 
                results='';
                END IF;
             END IF;
           ELSE 
      
            select get_artifact_user_values_any(artifact_xml,field_key,selectedfields) into returnvalues;
                IF returnvalues IS NOT NULL THEN 
                    results=returnvalues;
                ELSE 
                     results='';
                END IF;
      
           END IF;
  END IF;
  results := rtrim(results,'" ');
  results := rtrim(results,',');
 RETURN(results);
 END;  
$BODY$
LANGUAGE plpgsql VOLATILE
COST 100;
````

#### Sample Use Cases and Queries

 {% include note.html content="Flex field Name, Value, Tracker title and so on that are used in the filtering conditions are case-sensitive. See Case 7 below for building a case-insensitive search using upper() or lower()functions." %}

**Use Case 1: Filter Date and Text Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Date flex field named 'CreatedDate' that has a value of '2015-09-02 00:00:00'.

 * Text flex field named 'Text102' with part of its value containing the pattern 'soft'.

 * Tracker title is 'Tracker101'.

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system. The date passed as input should be of the format `YYYY-MM-DD HH24:MI:SS`." %}

**Sample Query**

```shell
select 
  t.Date as Date,
  t.Project as Project,
  t.Tracker as Tracker,
  t.Planing_folder as Planing_folder,
  'P'||t.Priority as Priority,
  count(distinct t.artifact_key) 
from 

(            select     b.date_of_trans as Date,
        e.title as Project,c.title as Tracker, 
        d.title as Planing_folder,
        'P'||a.priority as Priority,
        get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) as TextFlexField,
        a.artifact_key
from 
        artifact_transaction_fact a, 
        date_dimension b, 
        artifact_flex_fields ff, 
        tracker_dimension c, 
        pf_dimension d, 
        project_dimension e ,
        flex_field_dimension ffd
where 
        a.trans_date_key=b.date_key 
        and ff.artifact_flex_fields_key = a.flex_fields_key 
        and a.tracker_key=c.tracker_key 
        and a.pf_key=d.pf_key 
        and a.project_key=e.project_key 
        and a.tracker_key=ffd.tracker_key
        and e.title='Project SCD-2 Test'
        and ffd.name in ('Text102')
        and c.title in ('Tracker101') 
        and get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) like 'soft%'

union  

    select    b.date_of_trans as Date,
        e.title as Project,c.title as Tracker, 
        d.title as Planing_folder,
        'P'||a.priority as Priority,
        regexp_split_to_table(get_artifact_date_value(ff.flex_fields, ffd.flex_field_key),E',') as DateFlexField,
        a.artifact_key
  
from 
        artifact_transaction_fact a, 
        date_dimension b, 
        artifact_flex_fields ff, 
        tracker_dimension c, 
        pf_dimension d, 
        project_dimension e ,
        flex_field_dimension ffd
where 
        a.trans_date_key=b.date_key 
        and ff.artifact_flex_fields_key = a.flex_fields_key 
        and a.tracker_key=c.tracker_key 
        and a.pf_key=d.pf_key 
        and a.project_key=e.project_key 
        and a.tracker_key=ffd.tracker_key
        and e.title='Project SCD-2 Test'
        and ffd.name in ('CreatedDate')
        and c.title in ('Tracker101') 
        and  get_artifact_date_value(ff.flex_fields, ffd.flex_field_key)='2015-09-02 00:00:00') as t
group by 1,2,3,4,5 
order by 1,2,3,4,5;
````

**Use Case 2: Filter Single-select Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'FSS1'
 * Value selected or stored: 'S1'
 * Tracker title: 'Tracker2'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
select
    b.date_of_trans as Date,
    pd.title as Project,
    td.title as Tracker,
    d.title as Planning_folder,
    'P'||a.priority as Priority ,
    get_artifact_select_value(aff.flex_fields,ffd.flex_field_key) as SingleSelectFlexField,
    count(distinct a.artifact_key) TotalArtifacts 
from
    artifact_transaction_fact a,
    date_dimension b,
    artifact_flex_fields aff,
    project_dimension pd ,
    tracker_dimension td,
    pf_dimension d, 
    flex_field_dimension ffd 
where 
    a.trans_date_key=b.date_key 
    and a.flex_fields_key=aff.artifact_flex_fields_key
    and a.tracker_key=td.tracker_key
    and a.project_key=pd.project_key
    and td.tracker_key=ffd.tracker_key
    and a.pf_key=d.pf_key 
    and pd.title='ProjectTestFunctionSCD-2'
    and td.title in ('Tracker2')
    and ffd.name='FSS1'
    and get_artifact_select_value(aff.flex_fields,ffd.flex_field_key)='S1' 
    --and date(a.effective_from)<=date(now()) and date(a.effective_till)>'2012-04-01' 
group by 1,2,3,4,5,6
order by 1,2,3,4,5,6;
````

**Use Case 3: Filter Text Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'Text101'
 * Value contains: 'hello'
 * Tracker name: 'Tracker101'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
select
     b.date_of_trans as Date,
    e.title as Project,
    c.title as Tracker, 
    d.title as Planing_folder,
    'P'||a.priority as Priority,
    get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) as TextFlexField,
    count(distinct a.artifact_key) Artifacts
from 
    artifact_transaction_fact a, 
    date_dimension b, 
    artifact_flex_fields ff, 
    tracker_dimension c, 
    pf_dimension d, 
    project_dimension e ,
    flex_field_dimension ffd
where 
    a.trans_date_key=b.date_key 
    and ff.artifact_flex_fields_key = a.flex_fields_key 
    and a.tracker_key=c.tracker_key 
    and a.pf_key=d.pf_key 
    and a.project_key=e.project_key 
    and a.tracker_key=ffd.tracker_key
    and e.title='Project SCD-2 Test'
    and ffd.name = 'Text101'
    and c.title in ('Tracker101') 
    and get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) like 'hello%' 
    --and date(a.effective_from)<=date(now()) and date(a.effective_till)>'2012-04-01' 
group by 1,2,3,4,5,6 
order by 1,2,3,4,5,6;
````

**Use Case 4: Filter Date Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

* Flex field name: 'CreatedDate'
* Value: '2015-09-02 00:00:00'
* Tracker name: 'Tracker101'

  {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
select
    b.date_of_trans as Date,
    e.title as Project,
    c.title as Tracker, 
    d.title as Planing_folder,
    'P'||a.priority as Priority,
    regexp_split_to_table(get_artifact_date_value(ff.flex_fields, ffd.flex_field_key),E',') as DateFlexField,
    count(distinct a.artifact_key)
  
from 
    artifact_transaction_fact a, 
    date_dimension b, 
    artifact_flex_fields ff, 
    tracker_dimension c, 
    pf_dimension d, 
    project_dimension e ,
    flex_field_dimension ffd
where 
        a.trans_date_key=b.date_key 
        and ff.artifact_flex_fields_key = a.flex_fields_key 
        and a.tracker_key=c.tracker_key 
        and a.pf_key=d.pf_key 
        and a.project_key=e.project_key 
        and a.tracker_key=ffd.tracker_key
        and e.title='Project SCD-2 Test'
        and ffd.name in ('CreatedDate')
        and c.title in ('Tracker101') 
        and  get_artifact_date_value(ff.flex_fields, ffd.flex_field_key)='2015-09-02 00:00:00'

group by  1,2,3,4,5,6
order by 1,2,3,4,5,6;
````

**Use Case 5: Multi-select Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

* Multi-select flex field name: 'Country'
* Value: 'Russia,India'
* Tracker name: 'TrackerN'
* Conditional parameter: 'ALL'

  {% capture multiselectflexfieldsnote %}
  {% include inline_image.html file="status-success-small.png" %} You can change the field name, tracker title and values based on the data in your system. <br><br>
  {% include inline_image.html file="status-success-small.png" %} Flex field name, value and tracker title that are used in the SQL filter conditions are case sensitive. <br><br>
  {% include inline_image.html file="status-success-small.png" %} If you want to select all the values in User flex field, then pass 'ALL' as the conditional parameter. <br><br>
  {% include inline_image.html file="status-success-small.png" %} If you want to select any value, then pass 'ANY' as the conditional parameter.
  {% endcapture %}
  {% include callout.html type="primary" content=multiselectflexfieldsnote %}

**Sample Query**

```shell
select b.date_of_trans as Date, e.title as Project,c.title as Tracker, 
d.title as Planing_folder,'P'||a.priority as Priority,
 get_artifact_multiselect_value(ff.flex_fields,ffd.flex_field_key,'{Russia,India}','ALL') as MultiselectFlexField,
count(distinct a.artifact_key) Artifacts
--,a.artifact_key
from 
    artifact_transaction_fact a, 
    date_dimension b, 
    artifact_flex_fields ff, 
    tracker_dimension c, 
    pf_dimension d, 
    project_dimension e ,
    flex_field_dimension ffd
where 
    a.trans_date_key=b.date_key 
    and ff.artifact_flex_fields_key = a.flex_fields_key 
    and a.tracker_key=c.tracker_key 
    and a.pf_key=d.pf_key 
    and a.project_key=e.project_key 
    and a.tracker_key=ffd.tracker_key
    --and e.title='TestMultiFunction'
    and ffd.name = 'Country'
    and c.title in ('TrackerN') 
    and get_artifact_multiselect_value(ff.flex_fields,ffd.flex_field_key,'{Russia,India}','ALL')!='' 
    --and date(a.effective_from)<=date(now()) and date(a.effective_till)>'2012-04-01' 
group by 1,2,3,4,5,6 
order by 1,2,3,4,5,6;
````

**Use Case 6: Filter User Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * User flex field name: 'Select User'
 * Value: 'user1,user2'
 * Tracker name: 'TrackerN'
 * Conditional parameter: 'ALL'

   {% capture filteruserflexfields %}
   {% include inline_image.html file="status-success-small.png" %} You can change the field name, tracker title and values based on the data in your system. <br><br>
   {% include inline_image.html file="status-success-small.png " %} Flex field name, value and tracker title that are used in the SQL filter conditions are case sensitive. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select all the values in User flex field, then pass 'ALL' as the conditional parameter. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select any value, then pass 'ANY' as the conditional parameter.
   {% endcapture %}
   {% include callout.html type="primary" content=filteruserflexfields %}

**Sample Query**

```shell
select b.date_of_trans as Date, e.title as Project,c.title as Tracker, 
d.title as Planing_folder,'P'||a.priority as Priority,
 get_artifact_user_value(ff.flex_fields,ffd.flex_field_key,'{user1,user2}','ALL') as UserFlexField,
count(distinct a.artifact_key) Artifacts
--,a.artifact_key
from 
    artifact_transaction_fact a, 
    date_dimension b, 
    artifact_flex_fields ff, 
    tracker_dimension c, 
    pf_dimension d, 
    project_dimension e ,
    flex_field_dimension ffd
where 
    a.trans_date_key=b.date_key 
    and ff.artifact_flex_fields_key = a.flex_fields_key 
    and a.tracker_key=c.tracker_key 
    and a.pf_key=d.pf_key 
    and a.project_key=e.project_key 
    and a.tracker_key=ffd.tracker_key
    --and e.title='TestMultiFunction'
    and ffd.name = 'Select User'
    and c.title in ('TrackerN') 
    and get_artifact_user_value(ff.flex_fields,ffd.flex_field_key,'{user1,user2}','ALL')!='' 
    --and date(a.effective_from)<=date(now()) and date(a.effective_till)>'2012-04-01' 
group by 1,2,3,4,5,6 
order by 1,2,3,4,5,6;
````

**Use Case 7: Filter Text Flex fields: Case-insensitive Search**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'Text102'
 * Value contains: 'soft'
 * Tracker name: 'Tracker101'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system. The upper() function can be replaced with the lower() function appropriately for case-insensitive search. " %}

**Sample Query**

```shell
select
            b.date_of_trans as Date,
        e.title as Project,
        c.title as Tracker, 
        d.title as Planing_folder,
        'P'||a.priority as Priority,
        get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) as TextFlexField,
        count(distinct a.artifact_key) as TotalCounts
from 
        artifact_transaction_fact a, 
        date_dimension b, 
        artifact_flex_fields ff, 
        tracker_dimension c, 
        pf_dimension d, 
        project_dimension e ,
        flex_field_dimension ffd
where 
        a.trans_date_key=b.date_key 
        and ff.artifact_flex_fields_key = a.flex_fields_key 
        and a.tracker_key=c.tracker_key 
        and a.pf_key=d.pf_key 
        and a.project_key=e.project_key 
        and a.tracker_key=ffd.tracker_key
        and UPPER(e.title)=UPPER('Project SCD-2 Test')
        and UPPER(ffd.name)=UPPER('Text102')
        and UPPER(c.title) = UPPER('Tracker101')
        and UPPER(get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type)) like UPPER('soft%')

group by 1,2,3,4,5,6
order by 1,2,3,4,5,6;
````

### Query Oracle Datamart Based on Flex Fields

Create query scripts to query and extract the required information from the Oracle datamart. Make sure these scripts are available to any user (including users with read-only permission) who wants to execute these scripts. This topic lists the functions and sample queries for a few specific use cases.

 {% capture oracledatamartflexfields %}
 **Important:** <br><br>
 {% include inline_image.html file="status-success-small.png" %} Log into TeamForge as a Reporting user and run these queries. Note that this is a one-time process. <br><br>
 {% include inline_image.html file="status-success-small.png" %} Use the following flex field functions by joining the `flex_field_dimension`, `artifact_flex_field` and `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` tables as it depends on the XML data and flex field key generated by the platform.
 {% endcapture %}
 {% include callout.html type="primary" content=oracledatamartflexfields %}


#### Function for Date Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

<u>Date Flex Field Values</u>

```shell
create or replace FUNCTION get_artifact_date_value( artifact_xml IN XMLTYPE, field_key IN INTEGER )
   RETURN varchar2
   IS
 flex varchar2(4000);
   BEGIN
      SELECT x.val INTO flex FROM dual ,
      XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(4000) PATH '@val') x;
   RETURN(flex);
   END;
````

#### Function for Text Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

<u>Text Flex Field Values</u>

```shell
create or replace FUNCTION replacen( artifact_xml1 IN XMLTYPE)
   RETURN varchar2
   IS 
   replaceval  varchar2(3000);
   BEGIN
   SELECT REPLACE((REPLACE(cast(artifact_xml1 as varchar2(3000)),'','')),'','') into replaceval  from dual; 
   RETURN(replaceval);
   END;
create or replace FUNCTION get_artifact_text_value( artifact_xml IN XMLTYPE, field_key IN integer )
   RETURN varchar2
   IS flex varchar2(3200);
   fields_xml XMLTYPE;
   BEGIN
   SELECT XMLTYPE(replacen(artifact_xml)) INTO fields_xml FROM dual;
      SELECT x.val INTO flex FROM dual ,
      XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING fields_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(400) PATH '@val' ) x;
   RETURN(flex);
   END;
````

#### Function for Single-select Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

**Output Arguments**

<u>Values selected or stored in single-select flex field</u>

```shell
create or replace FUNCTION get_artifact_select_value( artifact_xml IN XMLTYPE, field_key IN INTEGER)
   RETURN VARCHAR2
   IS
    singleSelectValue VARCHAR2(100);
    flex INTEGER;
   BEGIN
      SELECT x.val INTO flex FROM dual ,
      XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(30) PATH '@val') x;
   SELECT  z.value INTO singleSelectValue from  FLEX_FIELD_VALUE_DIMENSION z  where z.FLEX_FIELD_VALUE_KEY=flex;
   RETURN(singleSelectValue);
   END;
````

#### Function for Multi-select Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

 * Specific value(s) stored in the field or the keyword 'ALL' for retrieving all values stored in multi-select flex field.

 * Logical conditional operator. Possible values are 'ALL' or 'ANY'. The argument value of 'ALL' performs a search equivalent to the 'AND' condition and the value of 'ANY' performs a search equivalent to the 'OR' condition.

**Output Arguments**

<u>Values selected or stored in multi-select flex field</u>

```shell
-----Inner Function----
    create or replace FUNCTION get_artifact_multiselect_any(artifact_xml IN XMLTYPE, field_key IN INTEGER,selectedfields IN varchar2)
   RETURN varchar2
   IS 
   flexs varchar2(300);
   arraylength integer default 1;
   loop1 integer default 1;
   loop2 integer default 1;
    i integer default 1;
    j integer default 1;
     v_array1 apex_application_global.vc_arr2; 
     v_array2 apex_application_global.vc_arr2; 
     v_array3 apex_application_global.vc_arr2; 
     results varchar2(200) ; 
      
   BEGIN
       SELECT x.val  INTO flexs FROM dual ,
        XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(4000) PATH '@val') x;
   v_array1 := apex_util.string_to_table(flexs,',');
   
   FOR  loop1 in 1..v_array1.count LOOP
     select value into v_array2(loop1) from  flex_field_value_dimension where flex_field_value_key=v_array1(loop1);
   END LOOP;
 
 v_array3 := apex_util.string_to_table(selectedfields,',');
 
 
 FOR   loop2 in 1..1 LOOP
                IF (v_array3(loop2)='ALL') THEN
                                 FOR i in 1..v_array2.count LOOP
                                       IF LENGTH(results)!=0 THEN 
                                                     results:=results ||','||v_array2(i);
                                                 ELSE
                                                      results:=v_array2(i);
                                                  END IF;
                                                 
                             END LOOP;
                     EXIT;
     
            ELSE
     
     
                                     FOR  i in 1..v_array2.count LOOP
                                          FOR  j in 1..v_array3.count LOOP
                                               IF (v_array3(j)=v_array2(i)) THEN
                                                    IF LENGTH(results)!=0 THEN 
                                                        results:=results ||','||v_array3(j);
                                                        ELSE
                                                        results:=v_array3(j);
                                                    END IF;
                                                    EXIT;
                                                END IF;
     
                                          END LOOP;
                                     END LOOP;
                END IF;
  END LOOP;

 RETURN(results);
           END;
/
    
-----End Inner function-----
   
   create or replace FUNCTION get_artifact_multiselect_value(artifact_xml IN XMLTYPE, field_key IN INTEGER,selectedfields IN varchar2,condition IN varchar2)
   RETURN varchar2
   IS 
   flexs varchar2(300);
   loop1 integer default 1;
   loop2 integer default 1;
    i integer default 1;
    j integer default 1;
     v_array1 apex_application_global.vc_arr2; 
     v_array2 apex_application_global.vc_arr2; 
     v_array3 apex_application_global.vc_arr2; 
     results varchar2(200) ; 
     filteredField varchar2(200) ; 
   valcount integer default 0;
      
   BEGIN
       SELECT x.val  INTO flexs FROM dual ,
        XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(4000) PATH '@val') x;
   v_array1 := apex_util.string_to_table(flexs,',');
   
   FOR  loop1 in 1..v_array1.count LOOP
     select value into v_array2(loop1) from  flex_field_value_dimension where flex_field_value_key=v_array1(loop1);
   END LOOP;
 
 v_array3 := apex_util.string_to_table(selectedfields,',');
 
 IF (UPPER(condition)=UPPER('ALL')) THEN
                      FOR   loop2 in 1..1 LOOP
                          IF (v_array3(loop2)='ALL') THEN
                                   FOR i in 1..v_array2.count LOOP
                                         IF LENGTH(results)!=0 THEN 
                                           results:=results ||','||v_array2(i);
                                         ELSE
                                            results:=v_array2(i);
                                         END IF;
                                         
                                     END LOOP;
                                     filteredField:=results;
                                     EXIT;
                     
                          ELSE
                     
                     
                                   FOR  i in 1..v_array3.count LOOP
                                      FOR  j in 1..v_array2.count LOOP
                                         IF (v_array3(i)=v_array2(j)) THEN
                                          IF LENGTH(results)!=0 THEN 
                                            results:=results ||','||v_array3(j);
                                            valcount:=valcount+1;
                                            ELSE
                                            results:=v_array3(j);
                                            valcount:=valcount+1;
                                          END IF;
                                          EXIT;
                                        END IF;
                   
                                      END LOOP;
                                   END LOOP;
                                   IF (valcount=v_array3.count) THEN
                                   filteredField:=results;
                                   ELSE 
                                   filteredField:='';
                                   END IF;
                          END IF;
                    END LOOP;
  
     
   
   
   ELSE
      select get_artifact_multiselect_any(artifact_xml,field_key,selectedfields) into results from dual;
        IF results IS NOT NULL THEN
          filteredField:=results;
        ELSE 
          filteredField:='';
        END IF;
   END IF;
filteredField:=TRIM(TRAILING ',' FROM filteredField);
         
RETURN(filteredField);
           END;

````

#### Function for Multi-user Flex Fields

**Input Arguments**

 * Flex field XML (derived automatically by joining the `artifact_transaction_fact` (or) `artifact_daily_snapshot_fact` and `artifact_flex_field` tables).

 * Flex field key (derived automatically from `flex_field_dimension` table and other tables).

 * Specific value(s) stored in the field or the keyword 'ALL' for retrieving all values stored in multi-select flex field.

 * Logical conditional operator. Possible values are 'ALL' or 'ANY'. The argument value of 'ALL' performs a search equivalent to the 'AND' condition and the value of 'ANY' performs a search equivalent to the 'OR' condition.


**Output Arguments**

<u>Values selected or stored in multi-user flex field</u>

```shell
------Inner Function-----
    create or replace FUNCTION get_artifact_user_any(artifact_xml IN XMLTYPE, field_key IN integer,selectedfields IN varchar2)
   RETURN varchar2
   IS 
   flexs varchar2(300);
   arraylength integer default 1;
   loop1 integer default 1;
   loop2 integer default 1;
    i integer default 1;
    j integer default 1;
     v_array1 apex_application_global.vc_arr2; 
     v_array2 apex_application_global.vc_arr2; 
     v_array3 apex_application_global.vc_arr2; 
     results varchar2(200) ; 
      
   BEGIN
       SELECT x.val  INTO flexs FROM dual ,
        XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(4000) PATH '@val') x;
   v_array1 := apex_util.string_to_table(flexs,',');
   
   FOR  loop1 in 1..v_array1.count LOOP
     select full_name into v_array2(loop1) from  user_dimension where user_key=v_array1(loop1);
   END LOOP;
 
 v_array3 := apex_util.string_to_table(selectedfields,',');
 
 
 FOR   loop2 in 1..v_array3.count LOOP
                IF (v_array3(loop2)='ALL') THEN
                                 FOR i in 1..v_array2.count LOOP
                                       IF LENGTH(results)!=0 THEN 
                                                     results:=results ||','||v_array2(i);
                                                 ELSE
                                                      results:=v_array2(i);
                                                  END IF;
                                                 
                             END LOOP;
                     EXIT;
     
            ELSE
     
     
                                     FOR  i in 1..v_array2.count LOOP
                                          FOR  j in 1..v_array3.count LOOP
                                               IF (v_array3(j)=v_array2(i)) THEN
                                                    IF LENGTH(results)!=0 THEN 
                                                        results:=results ||','||v_array3(j);
                                                        ELSE
                                                        results:=v_array3(j);
                                                    END IF;
                                                    EXIT;
                                                END IF;
     
                                          END LOOP;
                                     END LOOP;
                END IF;
  END LOOP;

 RETURN(results);
           END;

------End Inner Function----

create or replace FUNCTION get_artifact_user_value(artifact_xml IN XMLTYPE, field_key IN INTEGER,selectedfields IN varchar2,condition IN varchar2)
   RETURN varchar2
   IS 
   flexs varchar2(300);
   loop1 integer default 1;
   loop2 integer default 1;
    i integer default 1;
    j integer default 1;
     v_array1 apex_application_global.vc_arr2; 
     v_array2 apex_application_global.vc_arr2; 
     v_array3 apex_application_global.vc_arr2; 
     results varchar2(200) ; 
     filteredField varchar2(200) ; 
   valcount integer default 0;
      
   BEGIN
       SELECT x.val  INTO flexs FROM dual ,
        XMLTABLE ('/fields/field[@key=$keyalias]'
          PASSING artifact_xml,field_key as "keyalias"
          COLUMNS val VARCHAR2(4000) PATH '@val') x;
   v_array1 := apex_util.string_to_table(flexs,',');
   
   FOR  loop1 in 1..v_array1.count LOOP
     select full_name into v_array2(loop1) from  user_dimension where user_key=v_array1(loop1);
   END LOOP;
 
 v_array3 := apex_util.string_to_table(selectedfields,',');
 
 IF (UPPER(condition)=UPPER('ALL')) THEN
                      FOR   loop2 in 1..1 LOOP
                          IF (v_array3(loop2)='ALL') THEN
                                   FOR i in 1..v_array2.count LOOP
                                         IF LENGTH(results)!=0 THEN 
                                           results:=results ||','||v_array2(i);
                                         ELSE
                                            results:=v_array2(i);
                                         END IF;
                                         
                                     END LOOP;
                                     filteredField:=results;
                                     EXIT;
                     
                          ELSE
                     
                     
                                   FOR  i in 1..v_array3.count LOOP
                                      FOR  j in 1..v_array2.count LOOP
                                         IF (v_array3(i)=v_array2(j)) THEN
                                          IF LENGTH(results)!=0 THEN 
                                            results:=results ||','||v_array3(j);
                                            valcount:=valcount+1;
                                            ELSE
                                            results:=v_array3(j);
                                            valcount:=valcount+1;
                                          END IF;
                                          EXIT;
                                        END IF;
                   
                                      END LOOP;
                                   END LOOP;
                                   IF (valcount=v_array3.count) THEN
                                   filteredField:=results;
                                   ELSE 
                                   filteredField:='';
                                   END IF;
                          END IF;
                    END LOOP;
  
     
   
   
   ELSE
      select get_artifact_user_any(artifact_xml,field_key,selectedfields) into results from dual;
        IF results IS NOT NULL THEN
          filteredField:=results;
        ELSE 
          filteredField:='';
        END IF;
   END IF;
filteredField:=TRIM(TRAILING ',' FROM filteredField);
         
RETURN(filteredField);
           END;
````

#### Sample Use Cases and Queries

 {% include note.html content="Flex field Name, Value, Tracker title and so on that are used in the filtering conditions are case-sensitive. See Case 7 below for building a case-insensitive search using upper() or lower() functions." %}

**Use Case 1: Filter Date and Text Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Date flex field named 'CreatedDate' that has a value of '2015-07-07 00:00:00'
 * Text flex field named 'TEXT' with part of its value containing the pattern 'cre'
 * Tracker title is 'TestDateTracker'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system. The date passed as input should be of the format `YYYY-MM-DD HH24:MI:SS`." %}

**Sample Query**

```shell
SELECT t.date_of_trans  "Date",
       t.Project  ,
       t.Tracker  ,
       t.PlaningFolder  ,
       t.Priority,
       count(distinct t.artifact_key) "TotalArtifacts"  FROM (SELECT          b.date_of_trans,
                        e.title  AS Project,
     c.title AS Tracker,
                        d.title AS PlaningFolder,
                        'P'||a.priority AS Priority,
                        a.artifact_key
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
                      inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
                      inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
            inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
            inner join  project_dimension e on  (a.project_key=e.project_key) 
                  inner join flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
                  and ffd.name='Date'
                  and c.title='TestDateTracker'
            and get_artifact_date_value(ff.flex_fields,ffd.flex_field_key)='2015-08-12 00:00:00'

UNION


 SELECT            b.date_of_trans,
                           e.title  AS Project,
        c.title AS Tracker,
                           d.title AS PlaningFolder,
                           'P'||a.priority,
                            a.artifact_key
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
                       inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
                       inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
             inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
                   inner join  project_dimension e on  (a.project_key=e.project_key)
                   inner join  flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
                   and ffd.name='TEXT' 
 and c.title='TrackerTest'
            and get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) LIKE 'cre%'
            and d.id='plan1004' ) t

GROUP BY  t.date_of_trans,t.Project,t.Tracker,t.PlaningFolder,t.Priority
ORDER BY  t.date_of_trans,t.Project,t.Tracker,t.PlaningFolder,t.Priority
````

**Use Case 2: Filter Single-select Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'FSS1'
 * Value selected or stored: 'S1'
 * Tracker title: 'FTracker'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
SELECT    b.date_of_trans  "Date",
                   e.title "Project",
                   c.title  "Tracker",
                   d.title  "Planingfolder",
                   'P'||a.priority  "Priority",
                  count( distinct a.artifact_key) "TotalArtifacts"
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
                             inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
                             inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
         inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
        inner join  project_dimension e on  (a.project_key=e.project_key)  
                    inner join flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
                    and ffd.name='FSS1' 
                    and c.title='FTracker' and get_artifact_select_value(ff.flex_fields,ffd.flex_field_key)='S1'
--where a.effective_from <= sysdate and a.effective_till > to_date('2012-04-01', 'YYYY-MM-DD')
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

**Use Case 3: Filter Text Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'TEXT'
 * Value contains: 'cre
 * Tracker name: 'TrackerTest'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
SELECT            b.date_of_trans  "Date",
                           e.title "Project",
        c.title  "Tracker",
                           d.title  "Planingfolder",
                           'P'||a.priority  "Priority",
                           count( distinct a.artifact_key) "TotalArtifacts"
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
                       inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
                       inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
             inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
                   inner join  project_dimension e on  (a.project_key=e.project_key)
                   inner join  flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
                   and ffd.name='TEXT' 
 and c.title='TrackerTest'
            and get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type) LIKE 'cre%'
            and d.id='plan1004'  
--where a.effective_from <= sysdate and a.effective_till > to_date('2012-04-01', 'YYYY-MM-DD')
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

**Use Case 4: Filter Date Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'Date'
 * Value: '2015-08-12 00:00:00'
 * Tracker name: 'TestDateTracker'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system." %}

**Sample Query**

```shell
SELECT          b.date_of_trans  "Date",
                        e.title "Project",
     c.title  "Tracker",
                        d.title  "Planingfolder",
                        'P'||a.priority  "Priority",
                        count( distinct a.artifact_key) "TotalArtifacts"
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
                      inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
                      inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
            inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
            inner join  project_dimension e on  (a.project_key=e.project_key) 
                  inner join flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
                  and ffd.name='Date'
                  and c.title='TestDateTracker'
            and get_artifact_date_value(ff.flex_fields,ffd.flex_field_key)='2015-08-12 00:00:00'
--where a.effective_from <= sysdate and a.effective_till > to_date('2012-04-01', 'YYYY-MM-DD')
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

**Use Case 5: Multi-select Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * Multi-select flex field name: 'Multiselect'
 * Value: 'M12,M11'
 * Tracker name: 'TrackerTest'
 * Conditional parameter: 'ALL'

   {% capture multiselectflexfieldsnote2 %}
   {% include inline_image.html file="status-success-small.png" %} You can change the field name, tracker title and values based on the data in your system. <br><br>
   {% include inline_image.html file="status-success-small.png" %} Flex field name, value and tracker title that are used in the SQL filter conditions are case sensitive. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select all the values in User flex field, then pass 'ALL' as the conditional parameter. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select any value, then pass 'ANY' as the conditional parameter.
   {% endcapture %}
   {% include callout.html type="primary" content=multiselectflexfieldsnote2 %}

**Sample Query**

```shell
SELECT          b.date_of_trans  "Date",
                              e.title "Project",
                          c.title  "Tracker",
                              d.title  "Planingfolder",
                         'P'||a.priority  "Priority",
               count(distinct a.artifact_key)
 FROM       artifact_transaction_fact a   inner join date_dimension b on (a.trans_date_key=b.date_key) 
               inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
               inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
           inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
           inner join  project_dimension e on  (a.project_key=e.project_key) 
               inner join flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
               and ffd.name='Multiselect'
               and c.title='TrackerTest'
               and
get_artifact_multiselect_value(ff.flex_fields,ffd.flex_field_key,'M11,M12','ALL') IS NOT NULL  
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

**Use Case 6: Filter User Flex Fields**

Suppose you want to retrieve data based on the following assumptions:

 * User flex field name: 'Select User'
 * Value: 'user1,user2'
 * Tracker name: 'TrackerTestUser'
 * Conditional parameter: 'ALL'

   {% capture filteruserflexfieldsnote2 %}
   {% include inline_image.html file="status-success-small.png" %} You can change the field name, tracker title and values based on the data in your system.   <br><br>
   {% include inline_image.html file="status-success-small.png" %} Flex field name, value and tracker title that are used in the SQL filter conditions are case sensitive. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select all the values in User flex field, then pass 'ALL' as the conditional parameter. <br><br>
   {% include inline_image.html file="status-success-small.png" %} If you want to select any value, then pass 'ANY' as the conditional parameter.
   {% endcapture %}
   {% include callout.html type="primary" content=filteruserflexfieldsnote2 %}


**Sample Query**

```shell
  SELECT
          b.date_of_trans  "Date",
          e.title "Project",
      c.title  "Tracker",
          d.title  "Planingfolder",
         'P'||a.priority  "Priority",
         count( distinct a.artifact_key) "TotalArtifacts"
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
        inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
        inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
    inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
    inner join  project_dimension e on  (a.project_key=e.project_key) 
        inner join flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
        and ffd.name='Select User'
        and c.title='TrackerTestUser'
        and get_artifact_user_value(ff.flex_fields,ffd.flex_field_key,'user1,user2','ALL') IS NOT NULL  
--where a.effective_from <= sysdate and a.effective_till > to_date('2012-04-01', 'YYYY-MM-DD')
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

**Use Case 7: Filter Text flex fields: Case-insensitive Search**

Suppose you want to retrieve data based on the following assumptions:

 * Flex field name: 'TEXT'
 * Value contains: 'cre'
 * Tracker name: 'TestDateTracker'

   {% include note.html content="You can change the field name, tracker title and values based on the data in your system. The upper() function can be replaced with the lower() function appropriately for case-insensitive search. " %}

**Sample Query**

```shell
 SELECT
            b.date_of_trans  "Date",
            e.title "Project",
       c.title  "Tracker",
            d.title  "Planingfolder",
           'P'||a.priority  "Priority",
            count( distinct a.artifact_key) "TotalArtifacts"
 FROM  artifact_transaction_fact a inner join date_dimension b on (a.trans_date_key=b.date_key) 
            inner join  artifact_flex_fields ff  on (ff.artifact_flex_fields_key = a.flex_fields_key)
            inner join  tracker_dimension c on (a.tracker_key=c.tracker_key) 
        inner join  pf_dimension d on  (a.pf_key=d.pf_key) 
        inner join  project_dimension e on  (a.project_key=e.project_key)  
            inner join  flex_field_dimension ffd on (a.tracker_key=ffd.tracker_key)
            and UPPER(ffd.name)=UPPER('TEXT')
            and upper(c.title)=upper('TestDateTracker')
        and upper(get_artifact_text_value(ff.flex_fields,ffd.flex_field_key,ff.encoding_type)) like upper('cre%')   
--where a.effective_from <= sysdate and a.effective_till > to_date('2012-04-01', 'YYYY-MM-DD')
GROUP BY  b.date_of_trans,e.title,c.title,d.title,a.priority
ORDER BY  b.date_of_trans,e.title,c.title,d.title,a.priority
````

## TrackerInitialJob---Parallel Processing

A parallel processing feature has been introduced in TeamForge 8.1 Patch 1 to improve the performance of the tracker initial load job.

A performance observation was conducted on the tracker initial load job when fetching data from TeamForge and loading them to datamart. For more information on the performance observation, see [TrackerInitialJob Performance Observation][reporting_datamart_overview.html#TIJobperformobserv].

Based on the result, a parallel processing feature has been introduced to reduce the data processing time. For the observation results on parallel processing, see [here][reporting_datamart_overview.html#TIJobperformobservparallel].

To enable parallel processing:

 1. Change the JVM heap size by setting the Xmx value to -Xmx2048m in the `ETL_JAVA_OPTS` site options token (`/opt/collabnet/teamforge/etc/site-options.conf`).

    {% include important.html content="To make this a permanent change, you must modify the above setting before installing the product. If you do not want to make this a permanent change due to hardware resource constraint or for any other reason, then change the value in the set-env.sh file located in `runtime/conf` directory as below." %}

    1. Open `set-env.sh` from `<teamforge-installer-base-dir>/runtime/conf` directory.

    2. In `ETL_JVM_OPTS` site options token, change the Xmx setting to `-Xmx2048m`.

 2. Restart the CollabNet ETL service.

    ```shell
    teamforge restart
    ````
    {% include warning.html content="If the heap size (Xmx) is not set to 2048 MB for the ETL service, the tracker initial load job is more likely to throw an exception due to insufficient memory." %}


#### TrackerInitialJob Performance Observation {#TIJobperformobserv}

A performance observation was conducted on the tracker initial load job when fetching data from TeamForge and loading them to datamart.

For this observation, the tracker initial load job was run on the following key configuration parameters of the environment (configuration/resource allocation/capacity of the test server):

 * 64-bit CentOS 6.6
 * 8 CPU machine type with 8 GB RAM and 8 GB swap space
 * TeamForge application, ETL service and database server are all installed on the same box
 * The ETL service is configured to use a maximum heap size of 1524 MB
 * Postgres database
 * Maximum connections of database configuration server - 400
 * Database client connection pool configuration set to 30

It took, approximately, 15 hours and 30 minutes for the tracker initial load job to process the following number of records:

 {% include note.html content="All the relevant processes (for example, building dimensions, populating details around facts and hierarchies (team, artifacts and planning folder) were run in a sequence and not in parallel." %}

 * Projects: 570
 * Trackers:1692
 * Planning folders: 4731
 * Artifacts: 184992
 * Customers: 1692
 * Statuses: 1692
 * Releases: 4409
 * Categories: 1692
 * Teams: 45
 * Users: 1556
 * Flex fields: 3772
 * Flex field values: 15427
 * Audit change rows: 3516016
 * Audit entry rows: 3110684
 * Total number of fields: 27950
 * Total number of field values: 62580
 * Number of artifact transaction fact rows generated: 769212
 * Number of artifact daily snapshot fact rows generated: 536672

<table>
<tr>
<th>﻿Dimension/Fact name</th>
<th>ETL Start Date</th>
<th>ETL End Date</th>
<th>Record Count</th>
<th>Duration</th>
</tr>
<tr>
<td markdown="1">
  **flex_field_dimension**
</td>
<td rowspan="4">
  08-11-2015 05:16:03
</td>
<td rowspan="4">
  08-11-2015 14:15:11
</td>
<td>
  4511
</td>
<td rowspan="4">
  9 hrs (approx)
</td>
</tr>
<tr>
<td markdown="1">
  **flex_field_value_ dimension**
</td>
<td>
  17881
</td>
</tr>
<tr>
<td markdown="1">
  **pf_bridge**
</td>
<td>
  15621</td>
</tr>
<tr>
<td markdown="1">
  **artifact_dependency_bridge**
</td>
<td>
  32515
</td>
</tr>
<tr>
<td colspan="5" markdown="1">
  **artifact_transaction_fact**
</td>
</tr>
<tr>
<td>
  Batch 1
</td>
<td>
  08-11-2015 14:15:11
</td>
<td>
  08-11-2015 15:02:04
</td>
<td>
  122350
</td>
<td>
  47 minutes
</td>
</tr>
<tr>
<td>
  Batch 2
</td>
<td>
  08-11-2015 15:02:04
</td>
<td>
  08-11-2015 16:40:42
</td>
<td>
  130570
</td>
<td>
  1 hr 38 minutes
</td>
</tr>
<tr>
<td>
  Batch 3
</td>
<td>
  08-11-2015 16:40:43
</td>
<td>
  08-11-2015 17:42:59
</td>
<td>
  107961
</td>
<td>
  1 hr 02 minutes
</td>
</tr>
<tr>
<td>
  Batch 4
</td>
<td>
  08-11-2015 17:42:59
</td>
<td>
  08-11-2015 18:21:24
</td> 
<td>
  104260
</td>
<td>
  39 minutes
</td>
</tr>
<tr>
<td>
  Batch 5
</td>
<td>
  08-11-2015 18:21:24
</td>
<td>
  08-11-2015 19:03:47
</td>
<td>
  107449
</td>
<td>
  42 minutes
</td>
</tr>
<tr>
<td>
  Batch 6
</td>
<td>
  08-11-2015 19:03:47
</td>
<td>
  08-11-2015 20:07:46
</td>
<td>
  104023
</td>
<td>
  1 hr 3 minutes
</td>
</tr>
<tr>
<td>
  Batch 7
</td>
<td>
  08-11-2015 20:07:46
</td>
<td>
  08-11-2015 20:41:37
</td>
<td>
  92599
</td>
<td>
  34 minutes
</td>
</tr>
<tr>
<td></td>
<td></td>
<td markdown="1" >
  Total number of `artifact_transaction_fact` rows
</td>    
<td>
  769212
</td>
<td></td>
</tr>
<tr>
<td colspan="5" markdown="1">
  **artifact_daily_snapshot_fact**
</td>
</tr>
<tr>
<td>
  Batch 1
</td>
<td>
  08-11-2015 20:41:38
</td>
<td>
  08-11-2015 20:42:33
</td>
<td>
  70275
</td>
<td rowspan="7">
  11 minutes
</td>
</tr>
<tr>
<td>
  Batch 2
</td>
<td>
  08-11-2015 20:42:33
</td>
<td>
  08-11-2015 20:44:02
</td>
<td>
  87406
</td>
</tr>
<tr>
<td>
  Batch 3
</td>
<td>
  08-11-2015 20:44:03
</td>
<td>
  08-11-2015 20:45:32
</td>
<td>
  78238
</td>
</tr>
<tr>
<td>
  Batch 4
</td>
<td>
  08-11-2015 20:45:37
</td>
<td>
  08-11-2015 20:47:09
</td>
<td>
  72840
</td>
</tr>
<tr>
<td>
  Batch 5
</td>
<td>
  08-11-2015 20:47:19
</td>
<td>
  08-11-2015 20:48:36
</td>
<td>
  72919
</td>
</tr>
<tr>
<td>
  Batch 6
</td>
<td>
  08-11-2015 20:48:36
</td>
<td>
  08-11-2015 20:50:33
</td>
<td>
  79406
</td>
</tr>
<tr>
<td>
  Batch 7
</td>
<td>
  08-11-2015 20:50:34
</td>
<td>
  08-11-2015 20:52:24
</td>
<td>
  75588
</td>
</tr>
<tr>
<td></td>
<td></td>
<td markdown="1">
  Total number of `artifact_daily_snapshot_fact` rows
</td>
<td>
  536672
</td>
<td></td>
</tr>
<tr>
<td></td>
<td></td>
<td></td>
<td markdown="1">
  **Overall time**
</td>
<td markdown="1">
  **15 hrs 30 minutes (approx)**
</td>
</tr>
</table>

    
#### TrackerInitialJob Performance Observation - Parallel Process {#TIJobperformobservparallel}

Using parallel processing, it was established that the time taken to process the data was considerably less when compared to the sequential flow.

For this observation, the tracker initial load job was run on the following key configuration parameters of the environment (configuration/resource allocation/capacity of the test server):

* 64-bit CentOS 6.6
* 8 CPU machine
* Overall 8 GB RAM and 8 GB swap space
* TeamForge application, ETL service and database server are all installed on the same box
* The ETL service is configured to use a maximum heap size of 2048 MB
* Postgres database
* Maximum connections of database configuration server - 150
* Database client connection pool configuration set to 40

It took, approximately, 8 hours 40 minutes for the tracker initial load job to process the following number of records:

 * Projects: 570
 * Trackers:1692
 * Planning folders: 4731
 * Artifacts: 184992
 * Customers: 1692
 * Statuses: 1692
 * Releases: 4409
 * Categories: 1692
 * Teams: 45
 * Users: 1556
 * Flex fields: 3772
 * Flex field values: 15427
 * Audit change rows: 3516016
 * Audit entry rows: 3110684
 * Total number of fields: 27950
 * Total number of field values: 62580
 * Number of artifact transaction fact rows generated: 769212
 * Number of artifact daily snapshot fact rows generated: 536672

<table>
<tr>
<th>﻿Dimension/Fact Name</th>
<th>ETL Start Date</th>
<th>ETL End Date</th>
<th>Record Count</th>
<th>Duration</th>
<th>Remarks</th>
</tr>
<tr>
<td markdown="1">
  **flex_field_dimension**
</td>
<td rowspan="2">
  27-08-2015 05:59
</td>
<td rowspan="2">
  27-08-2015 06:23
</td>
<td>
  4511
</td>
<td rowspan="2">
  24 minutes
</td>
<td rowspan="2">
  This includes all the dimensions.
</td>
</tr>
<tr>
<td markdown="1">
  **flex_field_value_ dimension**
</td>
<td>
  17881
</td>
</tr>
<tr>
<td markdown="1">
  **pf_bridge**
</td>
<td>
  27-08-2015 06:23
</td>
<td>
  27-08-2015 09:00
</td>
<td>
  15621
</td>
<td></td>
<td rowspan="21">
  Running as three threads in parallel.
</td>
</tr>
<tr>
<td markdown="1">
  **artifact_dependency_bridge**
</td>
<td>
  27-08-2015 06:23
</td>
<td>
  27-08-2015 14:43
</td>
<td>
  32515
</td>
<td></td>
</tr>
<tr>
<td colspan="5" markdown="1">
  **artifact_transaction_fact**
</td>
</tr>
<tr>
<td>
  Batch 1
</td>
<td>
  27-08-2015 06:23
</td>
<td>
  27-08-2015 07:15
</td>
<td>
  122350
</td>
<td>
  52 minutes
</td>
</tr>
<tr>
<td>
  Batch 2
</td>
<td>
  27-08-2015 07:15
</td>
<td>
  27-08-2015 09:10
</td>
<td>
  130570
</td>
<td>
  1 hr 55 minutes
</td>
</tr>
<tr>
<td>
  Batch 3
</td>
<td>
  27-08-2015 09:10
</td>
<td>
  27-08-2015 10:16
</td>
<td>
  107961
</td>
<td>
  1 hr 7 minutes
</td>
</tr>
<tr>
<td>
  Batch 4
</td>
<td>
  27-08-2015 10:16
</td>
<td>
  27-08-2015 10:56
</td>
<td>
  104260
</td>
<td>
  40 minutes
</td>
</tr>
<tr>
<td>
  Batch 5
</td>
<td>
  27-08-2015 10:56
</td>
<td>
  27-08-2015 11:42
</td>
<td>
  107449
</td>
<td>
  46 minutes
</td>
</tr>
<tr>
<td>
  Batch 6
</td>
<td>
  27-08-2015 11:42
</td>
<td>
  27-08-2015 12:51
</td>
<td>
  104023
</td>
<td>
  1 hr 9 minutes
</td>
</tr>
<tr>
<td>
  Batch 7
</td>
<td>
  27-08-2015 12:51
</td>
<td>
  27-08-2015 13:28
</td>
<td>
  92599
</td>
<td>
  37 minutes
</td>
</tr>
<tr>
<td colspan="3" markdown="1">
  Total number of `artifact_transaction_fact` rows
</td>
<td>
  769212
</td>
<td></td>
</tr>
<tr>
<td colspan="5" markdown="1">
  **artifact_daily_snapshot**
</td>
</tr>
<tr>
<td>
  Batch 1
</td>
<td>
  27-08-2015 13:28
</td>
<td>
  27-08-2015 13:29
</td>
<td>
  70275
</td>
<td rowspan="7">
  12 minutes
</td>
</tr>
<tr>
<td>
  Batch 2
</td>
<td>
  27-08-2015 13:29
</td>
<td>
  27-08-2015 13:31
</td>
<td>
  87406
</td>
</tr>
<tr>
<td>
  Batch 3
</td>
<td>
  27-08-2015 13:31
</td>
<td>
  27-08-2015 13:32
</td>
<td>
  78238
</td>
</tr>
<tr>
<td>
  Batch 4
</td>
<td>
  27-08-2015 13:32
</td>
<td>
  27-08-2015 13:34
</td>
<td>
  72840
</td>
</tr>
<tr>
<td>
  Batch 5
</td>
<td>
  27-08-2015 13:34
</td>
<td>
  27-08-2015 13:36
</td>
<td>
  72919
</td>
</tr>
<tr>
<td>
  Batch 6
</td>
<td>
  27-08-2015 13:36
</td>
<td>
  27-08-2015 13:38
</td>
<td>
  79406
</td>
</tr>
<tr>
<td>
  Batch 7
</td>
<td>
  27-08-2015 13:38
</td>
<td>
  27-08-2015 13:40
</td>
<td>
  75588
</td>
</tr>
<tr>
<td colspan="3" markdown="1">
  Total number of `artifact_daily_snapshot_fact` rows
</td>
<td>
  536672
</td>
<td></td>
</tr>
<tr>
<td colspan="4" markdown="1">
  **Overall time**
</td>
<td markdown="1">
  **8 hrs 40 minutes (approx)**
</td>
</tr>
</table>


## Extract Base64-Encoded Text Flex Field Contents {#base64conversion}
<!-- Artifact artf395216 : Documentation for Base64 and conversion in datamart -->
  
The `artifact_flex_fields` table binds the flex field updates on artifacts into a well formed XML, which stores the ‘field key’, ‘value’ and ‘type’ of the flex field. There were ETL failures in datamart when complex or special character data set appears in the generated XML.

To prevent such complex XML creation in datamart, which in turn averts such ETL failures, text flex field contents stored in the `artifact_flex_fields` table are converted to Base64 encoding and stored inside the XML tags.

If you want to extract data from the `artifact_flex_fields` table for analysis, you must convert the Base64 encoded content into human readable format.

Here's a few example code base and queries used for conversion from Base64 to human readable format. 

### Function for Text Flex Fields (Oracle)
<!-- Input Arguments
: Flex field XML (derived automatically by joining the artifact_transaction_fact (or) artifact_daily_snapshot_fact and artifact_flex_field tables).
: Flex field key (derived automatically from flex_field_dimension table and other tables).

Output Arguments
: Text flex field values -->

```sql
CREATE OR REPLACE FUNCTION get_artifact_text_value( AFF IN number,ffkey IN number,EncodeFlag char )
RETURN varchar2
IS
 flex varchar2(3200)            ;
 vflex varchar2(3200)            ;
 flexkey integer                ;
 fields_xml XMLTYPE             ;
 Decoded_Fromhex raw(6000)      ;
 BEGIN
 select  x2.val INTO flex  from (select '<root>'||cdata||'</root>' as cdata from ( select object as cdata from  artifact_flex_fields A  , XMLTABLE('//fields'  passing FLEX_FIELDS  columns  object PATH 'text()') X where artifact_flex_fields_key =AFF ) ) inner , xmltable('root/field[@key=$keyalias]' passing xmltype(cdata) ,ffkey  as "keyalias" columns val varchar2(30) path '/field/@val') as x2;
IF   EncodeFlag = 'b' then  
      IF flex IS NOT NULL THEN                                      
                Decoded_Fromhex := UTL_ENCODE.BASE64_DECODE(UTL_RAW.CAST_TO_RAW(flex));
                flex            := UTL_RAW.CAST_TO_VARCHAR2(Decoded_Fromhex);
                RETURN flex;
    ELSE
        flex:='';
          RETURN flex;
      END IF;
ELSE
    RETURN flex;        
END IF;   
EXCEPTION
   when others then
   null;
   RETURN NULL;
END;
/ 
````

### Function for Text Flex Fields (PostgreSQL)

```sql
CREATE OR REPLACE FUNCTION replacen(artifact_xml1 xml)
 RETURNS text AS
$BODY$
 select replace ((select
 replace(artifact_xml1::varchar(3000),'<!','&lt;!')),']>',']&gt;')
$BODY$
 LANGUAGE sql STABLE
 COST 100;
                        
 CREATE OR REPLACE FUNCTION public.get_artifact_text_value(artifact_xml xml, field_key integer,EncodeFlag char) RETURNS character varying
 LANGUAGE plpgsql
AS $function$
 DECLARE
  field_value_keyEn Text ;
  field_value_key varchar(9055) default '';
 BEGIN
 SELECT cast((xpath('/fields/field/@val',replacen(artifact_xml)::xml)) [(array_search(field_key::text,(xpath('/fields/field/@key',replacen(artifact_xml)::xml))::text[]))]
  as varchar) into field_value_keyEn;
IF   EncodeFlag = 'b' then
    IF field_value_keyEn IS NOT NULL THEN

      select  convert_from(decode(field_value_keyEn,'base64'), 'UTF8') into field_value_key;
      RETURN field_value_key;
    ELSE
      RETURN field_value_key;
    END IF;
ELSE
field_value_key:=field_value_keyEn;
    RETURN field_value_key;
END IF;
EXCEPTION
    when others then
field_value_key:=null;
RETURN field_value_key;
END;
$function$;


      
CREATE OR REPLACE FUNCTION array_search(needle anyelement, haystack
 anyarray)
 RETURNS integer AS
$BODY$
 SELECT i
 FROM generate_subscripts($2, 1) AS i
 WHERE $2[i] = $1
 ORDER BY i
$BODY$
 LANGUAGE sql STABLE
 COST 100;
````


{% include links.html %}
