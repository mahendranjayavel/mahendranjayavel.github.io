---
title: SearchReindex.py
keywords: index, reindex
tags: [upgrade, scripts, site_admin_tasks, search_filter_sort]
sidebar: teamforge_sidebar
permalink: searchreindex-py.html
last_updated: Mar 14, 2018
summary: The SearchReindex.py script allows you to reindex the entire TeamForge data.
---

## Overview

You can use this script to reindex the entire TeamForge data or you can choose to reindex the subset of data types.
Usage

Run this script as follows:

```shell
./SearchReindex.py --<component name>
````

## Example

* To perform a search reindex for the tracker, run this command:
  ```shell
  ./SearchReindex.py --trackers-only
  ````
* To perform a search reindex for the wiki, run this command:
  ```shell
  ./SearchReindex.py --wiki-only
  ````
* To perform a search reindex for documents run this command:
  ```shell
  ./SearchReindex.py --documents-only
  ````


## Options

<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath"> --single-item itemId, | -i</span></dt>
<dd class="dd"> Schedules a re-index for just the given item. If the item id is for a project the scheduling results in the server re-indexing all of the project data. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath"> ---force-index | -f</span></dt>
<dd class="dd"> Force indexing (doesn't check if item is searchable already). </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath"> --artifacts only | -a</span></dt>
<dd class="dd"> Reindex all artifacts on the site that are currently not searchable or all artifacts if option f is selected. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath"> --documents only | -d </span></dt>
<dd class="dd"> Reindex all documents on the site that are currently not searchable or all artifacts if option f is selected. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---posts only </span></dt>
<dd class="dd"> Reindex all posts on the site that are currently not searchable or all artifacts if option f is selected. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---trackers only  </span></dt>
<dd class="dd"> Reindex all trackers on the site. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---document_folders-only  </span></dt>
<dd class="dd"> Reindex all document folders on the site. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---topics-only  </span></dt>
<dd class="dd"> Reindex all topics. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---forums-only  </span></dt>
<dd class="dd"> Reindex all forums on the site. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---news-only  </span></dt>
<dd class="dd"> Reindex all news. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---project_pages-only  </span></dt>
<dd class="dd"> Reindex all project pages. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---packages  </span></dt>
<dd class="dd"> Reindex all packages. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---commits-only  </span></dt>
<dd class="dd"> Reindex all commits. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---frs_files-only  </span></dt>
<dd class="dd"> Reindex all frs files. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---releases-only </span></dt>
<dd class="dd"> Reindex all releases. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">---wikis-only  </span></dt>
<dd class="dd"> Reindex all wikis. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">--project-id projectID | -p </span></dt>
<dd class="dd"> Limit the re-indexing to data for single project when re-indexing only artifacts and or documents. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">--verify | -x </span></dt>
<dd class="dd"> Searches for each item that is scheduled for re-indexing. There is a one minute wait limit for each item to be re-indexed by the server. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">--dryrun | -r </span></dt>
<dd class="dd"> Executes all the steps for scheduling a re-index without actually sending any re-index requests to the server. This provides a list of items that need re-indexing. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">output-file filePath, | -o </span></dt>
<dd class="dd">Prints the output for the given file. </dd>
</dl>
<dl class="dl">
<dt class="dt dlterm"><span class="ph filepath">--verbose | -v </span></dt>
<dd class="dd">Chronicles the process of scheduling the re-index a bit more. </dd>
</dl>

{% include links.html %}