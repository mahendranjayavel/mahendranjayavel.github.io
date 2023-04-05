---
title: backup-rb-data.py
keywords: back up, restore
tags: [upgrade, backup_restore, review_board, scripts]
sidebar: teamforge_sidebar
permalink: backup-rb-data-py.html
last_updated: May 14, 2019
summary: The backup-rb-data.py script is used to back up the Review Board application data.
---
The Review Board application data includes Review Board database and files. If there are any files in the backup directory, the script overwrites these files.

## Usage

```shell
python ./backup-rb-data.py --backupdir={dir}
````

## Parameters

The following parameters are available for the `backup-rb-data.py` script.

<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>-b | --both</td>
		<td>Back up both the database and the filesystem. This is the default option.</td>
	</tr>
	<tr>
		<td>-d | --database</td>
		<td>Back up the database.</td>
	</tr>
	<tr>
		<td>-f | --files</td>
		<td>Back up the filesystem.</td>
	</tr>
	<tr>
		<td>-h | --help</td>
		<td>Provides a list of all available options for this script.</td>
	</tr>
</table>

{% include links.html %}