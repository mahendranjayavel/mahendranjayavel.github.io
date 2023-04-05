---
title: restore-data.py
keywords: back up, restore
tags: [ctf_20.2, installation, upgrade, backup_restore]
sidebar: teamforge_sidebar
permalink: restore-data-py.html
last_updated: Jul 13, 2020
summary: The restore-data.py script restores the compressed data from the named source directory and deletes any existing data. By default, the TeamForge and the reporting database are backed up to the destination directory. If reporting is disabled, only the TeamForge database is backed up.
---

## Overview

`restore-data.py` finds and unpacks these data resources:

* Subversion repositories
<!-- * CVS repositories (if any) -->
* The data directory ( /var)
* The SourceForge database

## Usage

Run this script as follows:

```shell
./restore-data.py --source=<directory name>
````

where \<directory-name\> is the directory to which you backed up the data with the `backup-data.py` script.

## Location

```shell
/opt/collabnet/teamforge/runtime/scripts/
````

## Options

<dl>
<dt>--source</dt>
<dd>Directory where the compressed copy of the site's data is available.</dd>
<dt>--help | -h</dt>
<dd>Print this usage message and exit. </dd>
</dl>


{% include links.html %}

