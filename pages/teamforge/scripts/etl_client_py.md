---
title: etl-client.py
keywords: ETL initial load jobs
tags: [installation, upgrade, etl, scripts, datamart, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: etl_client_py.html
last_updated: Mar 14, 2018
summary: The etl-client.py script allows you to access the Extract, Transform and Load (ETL) scheduler and check the status of the jobs configured. The script also supports triggering jobs manually.
---

## Parameters
The following parameters are available for the `etl-client.py` script:

<dl>
<dt>-s | --status</dt>
<dd>Prints the status of all the jobs configured in the ETL service. </dd>
<dt>-a | --status-all</dt>
<dd>Prints the status of incremental and historical jobs configured in the ETL service.</dd>
<dt>-v| --verbose</dt>
<dd>Chronicles the process of requested operation a bit more.</dd>
<dt>-r| --run=</dt>
<dd>Triggers a job manually for a given job.</dd>
</dl>

## Data Collection (ETL) Jobs Supported by the ETL Service

While some ETL jobs are scheduled to run automatically, some must be triggered manually. The following table lists the available ETL jobs in TeamForge.

<table>
<tr>
<th>Job Category</th>
<th>Job Name</th>
<th>Description</th>
</tr>
<tr>
<td rowspan="3"><b>History Data Collection</b>
Historical data collection jobs must be triggered manually. As a best practice, these jobs are run as part of post migration activities. Refer to the "Related Links" for more information.
</td>
<td>SCMCommitInitialJob</td>
<td>Collects the historical commit data from TeamForge.</td>
</tr>
<tr>
<td>TrackerInitialJob</td>
<td>Collects the historical data of artifacts from TeamForge.</td>
</tr>
<tr>
<td>LoadFlexFields <br><br>
<b>Note: </b> This job must be executed if and only if you are upgrading from TeamForge 8.0 and earlier versions.</td>
<td>Collects the historical data of custom-defined artifacts from TeamForge.</td>
</tr>
<tr>
<td rowspan="3"><b>Incremental Data Collection</b>
Incremental data collection jobs collect data that are added or modified incrementally on an ETL run-to-run basis. These jobs are scheduled to run automatically on a regular basis.
</td>
<td>SCMCommitActivityJob</td>
<td>Collects the SCM commit data incrementally on an ETL run-to-run basis.</td>
</tr>
<tr>
<td>TrackerIncrementalJob</td>
<td>Collects the tracker artifacts data incrementally on an ETL run-to-run basis.</td>
</tr>
<tr>
<td>UserLoginActivityJob</td>
<td>Collects the user logon activity data incrementally on an ETL run-to-run basis.</td>
</tr>
<tr>
<td><b>Imported Data Collection (Simbel)</b>
TeamForge supports bulk data import through Simbel. This job collects Simbel-imported data. This job must be triggered manually post data import into TeamForge.
</td>
<td>SimbelImportJob</td>
<td>Collects all Simbel-imported data such as the user logon activity, SCM commit and tracker artifacts data.</td>
</tr>
</table>





{% include links.html %}