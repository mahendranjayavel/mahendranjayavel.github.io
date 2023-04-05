---
title: Jump to ID / Advanced Search
keywords: jump to ID, search
tags: [project_member_tasks, search_filter_sort]
sidebar: teamforge_sidebar
permalink: search-keyword.html
last_updated: Mar 19, 2019
summary: When you want to search for TeamForge objects such as tracker artifacts or documents, you can quickly search using a unique identifier or a keyword or you can perform an advanced search.
---
{% include tip.html content="While searching with an ID, you can select an object category from the drop-down list and search only within the selected object category. You can also select **Advanced Search** from the drop-down list to perform an advanced search." %}

## Full-text Search in TeamForge

Here is some detailed information to help you make the most of TeamForge's full-text search capabilities powered by the Apache Lucene full-text search engine.

### An Overview of Full-text Search

Here is some detailed information about the TeamForge's full-text search.

#### Searchable Items in TeamForge

The following items are searchable in TeamForge.

* Discussion forums, posts and topics
* Documents and document folders
* File releases, packages, and FRS files
* News posts
* Visible project pages
* Projects
* Source code files and commits
* Tasks and task folders
* Trackers and tracker artifacts
* Users
* Wiki pages
* Integrated applications

**Integrated applications**

Integrated applications may or may not have search capabilities. Refer to the integrated application's documentation to know more about its search features and to appreciate how the search features of the integrated application and TeamForge differ.

**Attached files**

You can search the contents of attached files. For more information about supported document formats, click [here](http://tika.apache.org/1.0/formats.html).


#### Notes

You may witness some delay for the TeamForge objects to appear in the search results and the extent of delay depends on the load on the server.

When you search, the contents of all the search-able fields (of an object) are collectively searched for matches. For instance, when you search for an artifact, the contents of the title, description and comment fields, put together, are searched. As an example, the search entry CollabNet AND TeamForge returns an artifact if the content of its title, description and comment, put together, has both the words "CollabNet" and "TeamForge". In other words, the word "CollabNet" could be in the artifact title and the word "TeamForge" could be in the artifact description (and not necessarily present on the same field).

If you search with multiple words, items containing any of the words in the search string are returned. For more information, see [Multiple Terms Search][search-keyword.html#multipletermssearch]. On the other hand, if you want to find items where the words, say CollabNet and TeamForge, both appear, type CollabNet AND TeamForge. For more information, see [Boolean Operators][search-keyword.html#booleanoperators].

The TeamForge searches for full words. Use [Wildcard Searches][search-keyword.html#wildcards] for partial word searches.

Search terms are case-insensitive. For example, if you search using the keyword `collabnet`, pages that contain COLLABNET, CollabNet and collabnet are all returned.

### TeamForge Full-text Search Guidelines

Here is some guidelines to help you create effective searches.

#### Single Term Search

Single-term search looks for all search results that match the search text. For example, a search entry of `doc` only returns search results of "doc".

#### Multiple Terms Search {#multipletermssearch}

Multiple-terms search looks for all search results that match any of the words in the search text. For example, a search entry of `document plan` returns search results of "document", "plan", and "document plan".


#### Search by Phrase

A group of words surrounded by double quotes, such as `"product requirements"`, return only search results containing the entire phrase.

#### Boolean Operators {#booleanoperators}

Terms and phrases can be combined with Boolean operators for more complex searches. Boolean operators must be in upper case. Use:

* `OR` between two terms returns search results containing either of the terms. This is the default operator used if no other operator is specified.
* `AND` between two terms returns only search results containing both of the terms.
* The `+` operator before a term makes the term required. Only search results containing the terms are returned.
* The `-` or `NOT` operator before a term returns only search results that do not contain the term. The character "-" represents the Boolean operator AND NOT.

 {% include tip.html content="You can group Boolean searches using parentheses. For example, (`doc` OR `test`) AND `plan` returns search results containing \"doc plan\" and \"test plan\"." %}

#### Wildcard Searches {#wildcards}

To look for search results with a single character replaced, use the ? symbol. For example, to look for search results with "text" or "test", enter `te?t`.

To look for search results with more than one character replaced, use the * symbol. For example, to look for search results such as "content" or "contest" or "continuous" or "control", enter `cont*`.

{% include note.html content="You can use wildcard symbols in the middle or at the end of a search, but not as the first character of a search keyword." %}

#### Fuzzy Searches

To look for search results with spelling similar to the search term entered, use the ~ symbol as the last character of the search keyword. For example, to look for search results with spelling similar to "roam", enter `roam~`. This returns search results such as "roam" and "roams".

#### Special Characters

If you have any of the following special characters in your search text, you must escape them by enclosing the entire phrase in double quotes. `+ - & || ! ( ) { } [ ] ^ " ~ * ? : \`

For example, to look for search results containing the hyphenated term "product-development", enter `product-development`.

The special character "+" represents the Boolean operator AND. The special character "-" represents the Boolean operator AND NOT.

#### Regular Expression Search with Forward Slashes

Lucene 4 supports regular expression searches matching a pattern between forward slashes "/". For example, to look for search results containing the words "moat" or "boat", use the search string `/[mb]oat/.`

If you are specifically looking for search results containing a forward slash "/" character, you must backslash-escape or quote-escape the forward slash character. For example, to look for search results containing `<opt/collabnet>`, use the search string `<opt\/collabnet>`.

#### Excluded Words

The following words are considered stop words and are not search-able on their own: `a, an, and, are, as, at, be, but, by, for, if, in, into, is, it, no, not, of, on, or, s, such, that, the, their, then, there, these, they, this, to, was, will, with`.

#### Range Searches

You can do a range-bound search using the TO operator. For example, the search entry, `[artf1100 TO artf1200]`, returns items containing values between artf1100 and artf1200, including artf1100 and artf1200. To exclude the upper and lower bounds from the search results, use curly brackets {} instead of square brackets [].

## Jump to ID Search {#jumptoidsearch}

1. Log on to TeamForge. If you are not logged on, you can search only projects and items that have been designated public.
2. If you know the unique identifier of an object and want to quickly go to the object, type the unique identifier in the **Jump to ID** text box and click the search icon.
   {% include callout.html type="primary" content="The default quick search option is **Jump to ID**." %}
   {% include note.html content="In addition to other objects, the **Jump to ID** search supports Baseline and Baseline Definition IDs." %}
3. If you want to do a keyword search of a specific object type (such as documents or discussions), type the keyword in the text box, select an object type from the drop-down list and click the search icon. The following table lists the search-able object types you can select from the drop-down list.

   | Searchable object types | Description |
   |-------------------------|-------------|
   | Discussions | Select this option to search in discussion forums. |
   | Documents | Select this option to search for documents. |
   | File Releases | Select this option to search in file releases. |
   | News | Select this option to search project news. |
   | Project Pages (Visible) | Select this option to search project pages. |
   | Projects |	Select this option to search projects. |
   | Source Code | Select this option to search the source code. For more information, see [How to search for Source Code?][searchcode]. |
   | Tasks | Select this option to search for tasks. |
   | Trackers | Select this option to search for tracker artifacts. |
   | Users | Select this option to search for users.|
   | Wiki | Select this option to search in Wiki pages. |

## Advanced Search {#advancedsearch}

The Advanced Search function lets you search globally on all the projects or on specific projects of interest. You can also scope your search to one or more components such as Documents, Discussions and so on using the Advanced Search. 

1. Click **Advanced Search** from the **Jump to ID** menu (drop-down list).
2. On the **Search Criteria** page, enter the keywords to search for.
3. Select one or more components such as **Discussions**, **Documents** and so on from the **IN** list.
4. Select one or more projects listed in the **IN PROJECTS** list. You can also select **All Projects**.
5. Select the **Search Attachments** check box and the **Search Comments** check box if you want to search attachments and comments respectively.
   {% include callout.html type="primary" content="Attachments refer to tracker artifact attachments. Comments refer to tracker artifact comments and task comments." %} 
6. Select one of the two options, **Search Active Versions Only** or **Search All Versions**, to specify whether you want to search active document versions only or all document versions respectively.
   {% include callout.html type="primary" content="Searching only active document versions allows you to eliminate search results for outdated documents." %}
7. Click **Search**.

   {% include callout.html type="primary" content="Your search results are organized by TeamForge application. The search score indicates the relevance of each result to your search criteria. You can see only those items that your project membership and permissions allow you to see." %}

{% include links.html %}