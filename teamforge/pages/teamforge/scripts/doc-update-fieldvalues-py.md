---
title: doc_update_fieldvalues.py
keywords: back up, restore, tasks
tags: [documents, scripts]
sidebar: teamforge_sidebar
permalink: doc-update-fieldvalues-py.html
last_updated: Apr 21, 2020
summary: Run this script to fix data discrepancies that might arise as a result of deleting one of the Single-select, Multi-select or Status field values of documents. 
---
<!-- Artifact artf397133 : [Doc Task] for artf395460-Script to fix data discrepancy in documents -->
If you have been using Single-select, Multi-select or Status flex fields in TeamForge Documents—and if you have inadvertently deleted one of the flex field values that was being used widely by existing documents—you will end up being unable to access the documents/document folders due to data discrepancy issues.

While TeamForge 20.1 has been fixed to prevent such deletions, you can run this script to fix such data discrepancy issues, if any, found with documents created in TeamForge 20.0 (or earlier). 

## Usage

```shell
[RUNTIME_DIR]/scripts/doc_update_fieldvalues.py [--run|-r] | [--projectId|-p] | [--help|-h]
````

## Parameters

The following parameters are available for the `doc_update_fieldvalues.py` script.

<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>-r | --run</td>
		<td>Updates all the documents across all the projects. The more the number of documents you have, the longer it takes to complete.</td>
	</tr>
	<tr>
		<td>-p | --projectId</td>
		<td>Updates all the documents in a given project.</td>
	</tr>
	<tr>
		<td>-h | --help</td>
		<td>Provides a list of all available options for this script.</td>
	</tr>
</table>

{% include links.html %}