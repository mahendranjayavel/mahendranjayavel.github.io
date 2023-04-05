---
title: Contribute to Project Wiki
keywords: creating wiki page, add wiki content, search wiki, viewing wiki page as html, viewing wiki page as pdf
tags: [project_member_tasks, wiki]
sidebar: teamforge_sidebar
last_updated: Aug 18, 2017
folder: teamforge
permalink: wiki.html
summary: The TeamForge Wiki allows you to create an unlimited number of Wiki pages in each TeamForge project. A Wiki page is a tool for managing project information as unstructured, linkable content.
---

## What is a Wiki Component?

A wiki component lets you link to an existing wiki page from a project page.


## Start a Wiki

To start communicating with other project members via Wiki, create a new page in your project's Wiki.

Every TeamForge project starts with a blank Wiki. You do not need to create a Wiki before you can begin adding content. After a Wiki is started, any user with the appropriate permissions can add or edit content. However, you cannot delete all of the content to start over with a new, blank Wiki.

1. Click **Wiki** from the **Project Home** page.
2. On the Wiki home page, click **Edit**.
3. On the **Edit Wiki** page, write your Wiki text. Wiki content is a combination of plain text, markup for font elements such as bold or italics, headers, bulleted and numbered lists, and links.
4. Customize your Wiki entry with any of these optional steps:
   1. Use the buttons at the top of the text area to add Wiki markup to your text in the **WYSIWYG Editor** mode. You can also enter Wiki syntax directly into the text area in the **Plain Editor** mode. For an explanation of Wiki syntax, click [Syntax Reference](wiki-wikisyntax.html).
   2. To insert a link to another TeamForge item, just type the item id. You do not need additional Wiki syntax to create the link.
   3. To change the size of the display window, drag the arrow available at the bottom right of the window.
   4. To attach an external file to a wiki page, click **CHOOSE FILE**, then browse for the desired file.
   5. To add a version comments, write it in the **Version Comment** field.
5. Click **Preview Changes** to see how your Wiki content will look. You can make further edit from the Previewing Home page before saving your changes.
6. Click **Update** to save your changes.

## Add Wiki Content

When the information you want to share with other project members does not file neatly into a tracker comment or a document review, use a Wiki page for a more free-form communication flow.

After a Wiki is created, any user with the Wiki create, edit, or view permission can add or edit Wiki content. You can also add associations or multiple attachments, or create additional Wiki pages.

   {% include note.html content="You can now add multiple attachments in a Wiki page without updating the Wiki each time to include another attachment. If attachments are not required, they can be deleted before updating the Wiki page." %}

1. Click **Wiki** from the **Project Home** menu. Any existing Wiki content appears.
2. For more information about this Wiki, click **View Details**.
3. On the Wiki home page, click **Edit**.
4. On the **Edit Wiki** page, make your changes or additions to the Wiki content.
   * If you prefer to use buttons to do your text formatting, the way you would with a word processor, click [NAME OF BUTTON].
   * If your tastes run more to typing in your wiki formatting, see [Wiki Syntax](wiki-wikisyntax.html) for the choices available.
     {% include tip.html content="You can use a variety of preconfigured queries to generate up-to-date content for your Wiki page. For more preconfigured Wiki content, see [Wiki Syntax](wiki-wikisyntax.html)." %}
5. In the **Version Comment** box, note the reason for your change. It is options, but advisable, to get in the habit of recording a version comment. If your project manager has made it mandatory, then you must record a version  comment before you can save your changes.
6. Click **Preview Changes** to see how your Wiki content will look. YOu can make further edits on the **Previewing** page before saving your changes.
7. Click **Update** to save your changes.

## Create a New Wiki page
A TeamForge site can have any number of Wiki pages. All Wiki pages are linked, and their relationships are traced on the Back Links tab of each Wiki page.

1. Click **Wiki** from the **Project Home** page.
2. In the large text field, insert the title of your new page between square brackets, like this: <br><br>
   `Please post comments about [test results] here`. <br><br>
   Then click **Update**. The text between the square brackers becomes a link on your Wiki page.
      {% include note.html content="You can also type the new link in CamelCase (each word starts with an uppercase letter, no spaces) and skip the square brackets." %}

3. Click the link to open the new Wiki page. The new page is created. The title of the new page is the same text as the link, rendered in CamelCase.
4. On the **Create Wiki** page, write the content you need, then click **Save**.
   {% include tip.html content="You can use a variety of preconfigured queries to generate up-to-date content for your Wiki page. For more preconfigured Wiki content, see [Wiki Syntax](wiki-wikisyntax.html)." %}
The new Wiki page is created. The back link to the page from which it was created appears on the _Back Links_ tab of the **Show/Hide Details** section.

## Search a Wiki

Use the wiki search page to find content in a project wiki.

1. Click **Wiki** from the **Project Home** page.
2. On the **Wiki home** page, click **Search Wiki Pages**.
3. Try one of the predefined searches. These can save you time by running some of the most widely used content searches with a single click: 
   * List the wiki pages that have changed in the last 15 days.
   * List the wiki pages that no other wiki page links to.
   * List all the pages in this project's wiki.
4. If you need to narrow your search beyond the predefined searches, enter some search terms under _Wiki Pages Search Criteria_. Wildcards are allowed.
   * To search active wiki content, enter the search keywords in the **SEARCH TEXT** field.
   * To search active and inactive wiki page versions, select **Search All Versions**. (By default, searches are performed on active wiki page versions only.)
   * To search wiki attachments, select **Include Attachments**.
   * If you know approximately when the wiki content was created or last edited, enter the start and end dates for the search and click **Search**. Click the calendar icon to select dates from a calendar.
   * To search by author, click the Search icon in the **CREATED OR EDITED BY** field that displays a list of project members.
5. Click **Search**.

A list of wiki pages matching your search criteria appears.

## View a Wiki page as HTML

One way to resolve messy or incorrect formatting on a wiki page is by converting the page to HTML. 

1. Click **Wiki** from the **Project Home** page.
2. Find your wiki page by navigating or searching.
3. Click the **View HTML** button.

The wiki uses **HTML Tidy** to display the cleanest HTML it can manage. View the page source to see the results.

## View a Wiki page as a PDF

When you want to send a wiki page to someone outside the project, it can be handy to convert it to a PDF document.

1. Click **Wiki** from the **Project Home** page.
2. Find your wiki page by navigating or searching.
3. Click the **View PDF** button.

Depending on how your browser is set up, the resulting PDF document appears or the browser offers to download it for you.


{% include links.html %}
