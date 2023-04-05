---
title: FAQs on Search
keywords: FAQ, frequently asked questions
tags: [faq, search]
sidebar: teamforge_sidebar
permalink: search-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on search operations in TeamForge.
---

## What resources can be searched on a TeamForge site?

The resources that show up in search results depend on the context in which you are working.

Here is a summary:

<table>
<tr>
<th>Tool</th>
<th>Searchable resources</th>
</tr>
<tr>
<td>Projects</td>
<td>Project id, title/description, created by, project status</td>
</tr>
<tr>
<td>Project categories</td>
<td>Title, description</td>
</tr>
<tr>
<td>Discussions</td>
<td>
<ul>
<li>Web UI: author, subject, content, attachment.</li>
<li>Email: we index the original email after we process it.</li>
<li>Topics: author, title and description.</li>
<li>Forums: title, description, author.</li>
</ul>
</td>
</tr>
<tr>
<td>Documents</td>
<td>
<ul>
<li>Document folders: title, description</li>
<li>Documents; version comment, title, status, description, the attachment itself (all versions), authors</li>
</ul>
</td>
</tr>
<tr>
<td>SCM</td>
<td>Commit message, title, author</td>
</tr>
<tr>
<td>Tracker</td>
<td>
<ul>
<li>Tracker title, description, author</li>
<li>Artifacts: title, group, category, customer, status, description, authors, tracker, all text flex fields, single-select fields, multi-select fields</li>
<li>Artifact attachments: the attachment itself and comments</li>
</ul>
</td>
</tr>
<tr>
<td>News</td>
<td>Body, title, author</td>
</tr>
<tr>
<td>File Releases</td>
<td>
<ul>
<li>Packages; title, description, author</li>
<li>Releases: title, description, author, maturity, status</li>
<li>Files: description, filename</li>
</ul>
</td>
</tr>
<tr>
<td>Tasks</td>
<td>Title, description, authors, planned</td>
</tr>
<tr>
<td>Users</td>
<td>Username, full name, email, status, details</td>
</tr>
<tr>
<td>Pages</td>
<td>
<ul>
<li>HTML components: title, content</li>
<li>Subpages: page title, component title</li>
</ul>
</td>
</tr>
<tr>
<td>Wiki</td>
<td>Content of wiki page, using wiki syntax</td>
</tr>
</table>
{{site.data.alerts.hr_shaded}}

## Why do I get a server status error when I perform a search?

Occasionally, an exceedingly large or complex document causes the search indexing service to abort.

This is typically when all searches in TeamForge return an exid to the user.

Check the server status page and see if the search server is listed as anything other than OK. If it is not OK, then you should restart the search service by logging into the TeamForge application server as root and issuing the following command:

```shell
/opt/collabnet/teamforge/james/james-/bin/phoenix.sh restart
````

Check the server status page again in TeamForge and ensure that it shows a status of OK. If it shows OK, then searches should now work, and the site will slowly catch up on any indexing requests that were logged while the service was down. If you continue to get exids returned for all searches even with an OK status, then you probably have corrupt search index files.

{% include links.html %}