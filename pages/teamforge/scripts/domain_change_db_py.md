---
title: domain_change_db.py
keywords: domain change
tags: [upgrade, scripts, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: domain_change_db_py.html
last_updated: June 14, 2019
summary: The domain_change_db.py script handles all the steps required to change the domain name in the site database. It does not change anything in the file system.
---
Changing the domain through any other mechanism may cause problems.

## Usage
Execute this script with a command like this:

```shell
[RUNTIME_DIR]/domain_change_db.py [--debug] [--dir] --old={domain_name} --new={domain_name}
````

{% include note.html content="The new domain name must match the value defined for the [PUBLIC_FQDN][siteconfigtokens.html#hostpublic_fqdn] token in the `site-options.conf` file." %}

## Parameters

<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>--help</td>
		<td>Show command help information</td>
	</tr>
	<tr>
		<td>--debug</td>
		<td>Include debugging information</td>
	</tr>
	<tr>
		<td>--old</td>
		<td>Old domain</td>
	</tr>
	<tr>
		<td>--new</td>
		<td>New domain</td>
	</tr>
	<tr>
		<td>--dir</td>
		<td>Run domain change in this directory only. <br>You must specify the full path. Use this feature to do a subset of the data directory. This instructs the script to do a recurse in the specified directory looking for the old <code class="highlighter-rouge">domain_name</code> and replacing it with the new <code class="highlighter-rouge">domain_name</code>. <br> 
		{% include note.html content="Without this option, only HTML, text, and VM files are modified." %} </td>
	</tr>
	<tr>
		<td>--threadlimit</td>
		<td>Defines the maximum number of simultaneous threads that can invoked by this program. The default value is 50.</td>
	</tr>
</table>


{% include links.html %}