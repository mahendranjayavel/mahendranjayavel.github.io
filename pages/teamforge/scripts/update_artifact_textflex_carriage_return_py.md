---
title: update_artifact_textflex_carriage_return.py
keywords: CRLF, dummy, updates
tags: [upgrade, scripts, site_admin_tasks, ctf_20.0]
sidebar: teamforge_sidebar
permalink: update_artifact_textflex_carriage_return_py.html
last_updated: Jan 29, 2020
summary:  If you have been updating your tracker artifacts both via the UI and CLI/SOAP, you may optionally run the `update_artifact_textflex_carriage_return.py` script to fix the inconsistent CRLF characters that were found to exist in the text flex field data.
---
<!-- Artifact artf395054 : [Doc Task] for artf394617 : Provide update script to fix artf302209 -->

Artifact updates done via the UI and CLI/SOAP were found to be saving the text flex field data (that span multiple lines) inconsistently with the `\r\n` and `\n` CRLF characters respectively. This caused dummy updates to the text flex fields on subsequent artifact updates even if the fields were not updated. 

This issue was fixed in TeamForge 20.0. However, you can optionally run the `update_artifact_textflex_carriage_return.py` script in case you want to fix the existing text flex field data to avert any such dummy updates from happening to existing artifacts in the future.

## Usage
Use the following command to run this script.
```shell
[RUNTIME_DIR]/scripts/update_artifact_textflex_carriage_return.py [[--run|-r] | [--projectId|-p] | [--trackerId|-t] | [--help|-h]
````

## Parameters

| Paramater | Description |
|-----------|-------------|
| -r \| --run | Run the script to fix all the artifacts. Note that the script might run for quite a long time depending on the number of artifacts you have. |
| -p \| --projectId | Run the script to fix the artifacts in a specific project. |
| -t \| --trackerId | Run the script to fix the artifacts in a specific tracker. |
| -h \| --help | To view help information for the script. |

This script was added in TeamForge 20.0. 


{% include links.html %}