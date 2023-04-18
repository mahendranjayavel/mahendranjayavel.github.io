---
title: task-data-export.py
keywords: back up, restore, tasks
tags: [upgrade, backup_restore, scripts]
sidebar: teamforge_sidebar
permalink: task-data-export-py.html
last_updated: Apr 17, 2020
summary: Tasks, as a component, is no longer supported and was completely removed from TeamForge 20.1 and later. The task-data-export.py script is used to back up the Tasks data.
---
<!-- Artifact artf397074 : Documentation for task decommission in CTF -->
Tasks, as a component, is no longer supported and was completely removed from TeamForge 20.1 and later. However, if you have been using Tasks, you can use the `task-data-export.py` script to export the Tasks data to Excel files, which you can later import into one of the TeamForge trackers.

## Usage

```shell
[RUNTIME_DIR]/scripts/task-data-export.py [--rows|-r] | [--path|-p] | [--help|-h]
````

## Parameters

The following parameters are available for the `tasks-data-export.py` script.

<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>-r | --rows</td>
		<td>The maximum number of rows to export to an Excel file. Ignoring this option allows a maximum of 4500 rows exported to an Excel file.</td>
	</tr>
	<tr>
		<td>-p | --path</td>
		<td>The path to the location where the Excel files (with Tasks data) are stored.</td>
	</tr>
	<tr>
		<td>-h | --help</td>
		<td>Provides a list of all available options for this script.</td>
	</tr>
</table>

Usage Example 1
: The following command exports the Tasks data to as many Excel files as required with no more than 400 rows in each Excel file. For example, if you have 900 records, the following command exports 400 records to the first two Excel files and the remaining 100 records to a third Excel file.

   ```shell
   ./task-data-export.py -r 400 -p /tmp/TaskExport/
   ````

Usage Example 2
: The following command exports the Tasks data to as many Excel files as required with a maximum of 4500 rows per Excel file. For example, if you have 9000 records, the following command exports the data to two excel files with 4500 records per file. 

   ```shell
   /task-data-export.py -p /tmp/TaskExport/
   ````

## Importing Tasks Data to a TeamForge Tracker

You can create a new Tasks tracker and [mass import][trackers-importingtrackerartifacts] the data that you exported as discussed earlier using the `tasks-data-export.py` script. 

However, the new tracker you create must comply with the following field structure. The following table lists the fields (both fixed and flex fields) and their values, if any, as expected in the new Tasks tracker that you create. 

| Artifact ID 	| Field Values 	| Type 	|
|-------------------	|--------------------------------------------------------------------------	|------------------	|
| Title 	|  	| Fixed Field 	|
| Description 	|  	| Fixed Field 	|
| Assigned To 	|  	| Fixed Field 	|
| Team 	|  	| Fixed Field 	|
| Status 	| Pre-configured values of Task<br>Alert, OK, Warning, NotStarted, Complete 	| Fixed Field 	|
| Priority 	| None<br>1 - Highest<br>2 - High<br>3 - Medium<br>4 - Low<br>5 - Lowest 	| Fixed Field 	|
| Category 	|  	| Fixed Field 	|
| Start Date 	|  	| Text-Flex Fields 	|
| End Date 	|  	| Text-Flex Fields 	|
| Percent Complete 	|  	| Text-Flex Fields 	|
| Estimated Hours 	|  	| Text-Flex Fields 	|
| Created Date 	|  	| Text-Flex Fields 	|
| Task Created By 	|  	| Text-Flex Fields 	|
| Planned 	|  	| Text-Flex Fields 	|
| Accomplishments 	|  	| Text-Flex Fields 	|
| Issues 	|  	| Text-Flex Fields 	|
| Actual Hours 	|  	| Text-Flex Fields 	|
| Task Calendar 	|  	| Text-Flex Fields 	|
| Task Associations 	|  	| Text-Flex Fields 	|
| Task Successor 	|  	| Text-Flex Fields 	|
| Task Id 	|  	| Text-Flex Fields 	|
| Folder Hierarchy 	|  	| Text-Flex Fields 	|
| Task Predecessor 	|  	| Text-Flex Fields 	| 

{% include links.html %}