---
title: FAQs on Wiki 
keywords: FAQ, frequently asked questions
tags: [faq, wiki]
sidebar: teamforge_sidebar
permalink: wiki-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on Wiki.
---

## Why are statistics charts broken on a wiki page?

Statistics charts such as artifact statistics, task statistics, FRS statistics and document statistics, when added to a wiki page, do not get displayed because the relevant markup formats `[sf:artifactStatistics]`, `[sf:taskStatistics]`, `[sf:frsStatistics]` and `[sf:documentStatistics]` have been deprecated from TeamForge 8.1 and later.

So, if you try to create a wiki page with these values, instead of displaying the charts, the following error messages are displayed:

 * For task charts, "The Task Statistics are discarded." is displayed.
 * For all the other statistics charts, "The Statistics charts are deprecated viewing from Wiki. It can be accessible from Project Home Page." is displayed.
{{site.data.alerts.hr_shaded}}

## How do I generate a wiki table of contents?

You can create a table of contents from any heading text that you have in your wiki page.

For versions 5.2 and earlier, generating a wiki table of contents requires the Wiki TOC plugin, available through CollabNet Professional Services.

To enable TOC for a Wiki page, place the following in your Wiki page at the spot where you want the Table of Contents to appear.

```shell
%%insert-toc
%%
````

The Table of Contents is generated automatically based on the heading markers in the wiki page. Example: `!!!Heading`.
{{site.data.alerts.hr_shaded}}

## How do I delete an attachment from a wiki page?

You can delete an attachment from the wiki page.

Use the following steps to delete an attachment:

 1. Browse to the wiki page that contains the attachment and click **Edit**.

 2. Update the wiki page, even though you have not made any changes to it.

 3. Click **Show Details**.

 4. Click the _Attachments_ tab.

 5. Select the attachment you want removed and click **Remove**.
{{site.data.alerts.hr_shaded}}

## How can I detect orphan wiki pages?

No. You cannot detect orphan wiki pages.

Unfortunately at this time, TeamForge does not have the ability to locate or display orphaned wiki pages within the UI. This functionality is slated to be included in a future release. If you have an immediate need, please contact Technical Support and a suitable SQL query will be devised.
{{site.data.alerts.hr_shaded}}

## How do I edit the wiki home page?

Navigate to the project home page and click the **Edit** button to edit the wiki home page.

Once you have enabled the wiki as the project home page option in Project Admin, you must return to the project home page by clicking the **Project Home** button. There will be an **Edit** button on the bottom right corner of the page under graphs. You may need to scroll your browser window to the right to see this button.
{{site.data.alerts.hr_shaded}}

## How do I make the version comment required for wiki updates?
You can use Velocity to customize the pages of TeamForge and make the version comment required.

Create `/opt/collabnet/teamforge/sourceforge_home/templates/body_footer.vm` with the following contents:

```shell
<script>
var updateButton = document.getElementById('edit_wiki_page.update');
if ( updateButton ) {
updateButton.href = 'javascript:submitWikiPageUpdate();';
}
function submitWikiPageUpdate () {
if ( document.editPage.versionComment.value ) {
submitForm(document.editPage, 'submit');
return;
}
alert("Please include a detailed Version Comment for this change.");
}
</script>
````

Ensure that the file is owned by the sf-admin user:

```shell
chown -R sf-admin.sf-admin /opt/collabnet/teamforge/sourceforge_home/templates 
````

Ensure proper permissions:

```shell
chmod 0644 /opt/collabnet/teamforge/sourceforge_home/templates/body_footer.vm
````

TeamForge picks up the change immediately.
{{site.data.alerts.hr_shaded}}

## I have set my project to 'use wiki homepage'. Why isn't my wiki showing up?

TeamForge currently uses two distinctly different wikis.

 * If there is the wiki you have already edited, which is available by clicking on the **Wiki** button at the top of any project page, and there is the 'project home' wiki, which is what you enabled in the **Project Admin** screen.

 * If you visit the project home page after setting this option, and if you have the proper RBAC permissions, there should be an **Edit** button in the bottom-right corner of the home page under the graphs. Use this button to edit the project home page wiki.
{{site.data.alerts.hr_shaded}}

## Why would I attach things to a wiki?

There are specific scenarios that would require attachments to a wiki.

The most common example of when you would attach something to a wiki would be when you need an image in the wiki page and you are concerned that if the image is hosted remotely (a corporate web server, for example), it might be moved or removed. Additionally, you might wish to attach a file to a wiki page if the attachment is only truly important in the context of the wiki page and therefore is not important enough to be uploaded to the Document Manager of TeamForge.

{% include links.html %}