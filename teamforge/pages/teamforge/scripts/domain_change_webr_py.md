---
title: domain_change_webr.py
keywords: webr domain change
tags: [ctf_19.1, upgrade, scripts, site_admin_tasks]
sidebar: teamforge_sidebar
permalink: domain_change_webr_py.html
last_updated: June 14, 2019
summary: The domain_change_webr.py script is used to change the domain name or host name of the subscriber in the TeamForge Webhooks-based Event Broker database. 
---

## Usage
Execute this script with a command like this:

```shell
[RUNTIME_DIR]/scripts/domain_change_webr.py [old_domain] [new_domain]
````

{% include note.html content="The new domain name must match the value defined for the [PUBLIC_FQDN][siteconfigtokens.html#hostpublic_fqdn] token in the `site-options.conf` file." %}

## Parameters

<table>
	<tr>
		<th>Parameter</th>
		<th>Description</th>
	</tr>
	<tr>
		<td>old_domain</td>
		<td>Old domain name</td>
	</tr>
	<tr>
		<td>new_domain</td>
		<td>New domain name</td>
	</tr>	
	<tr>
		<td>--help</td>
		<td>To view help information for the script.</td>
	</tr>	
</table>


{% include links.html %}