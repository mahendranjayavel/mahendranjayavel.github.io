---
title: Monitoring Activities in TeamForge 
keywords: monitoring an item, monitoring an application, monitoring discussion forums
tags: [project_member_tasks, monitoring]
sidebar: teamforge_sidebar
folder: teamforge
last_updated: Aug 29, 2017
permalink: monitoring.html
summary: When you monitor an item, such as a task or a document, you are notified by email when that item is updated. You can also monitor a discussion forum or project news by subscribing to its Really Simple Syndication (RSS) feed.  
---

## Monitor an Item
To get notified by email whenever an item changes, monitor the item. In TeamForge, an item is something you produce with the site's tools. These are some examples of items:

  * Documents
  * Tasks
  * Tracker artifacts
  * Discussion forum topics
  * Files in a release
   
  1. Go to the folder containing the item or items that you want to begin monitoring.
  2. Select the item or items that you want to begin monitoring.
  3. Click the **Monitor** down arrow, then choose **Monitor Selected**.

You are now monitoring all selected items. The monitoring icon {% include inline_image.html file="bellicon.png" %} is displayed in the item list view and the monitored items appear in the monitored items list on your personal **Monitoring** page.

  {% include note.html content="When you update two or more artifacts at a time, each user who is monitoring any of the changed artifacts gets a single email describing all the updates." %}

To stop monitoring an item, select it, then roll your mouse over the **Monitor** down arrow and choose **Stop Monitoring Selected**.

  {% include note.html content="You can also stop monitoring any item from the monitored items list on your personal **Monitoring** page." %}

## Monitor an Item for someone else
To alert another user to an item, add that user to the list of people monitoring that item.

After a user is added to a monitored item, the user can configure their own monitoring preferences for the item, or stop monitoring the item. 

  1. Go to the item to which you want to add a user.
  2. Click the item to view the artifact.
  3. On the item's **View Artifact** page, click **Users Monitoring**.
  4. In the **Users Monitoring This Item** window, click **Add**.
  5. From the list of available project members, select the user or users that you want to add to the monitored item.
     {% include tip.html content="Press and hold the **Ctrl** key to select more than one user." %}
  6. Click **Add**.
     {% include tip.html content="You can also click **Add All** to select all users." %}
  7. Click **OK**.

The users are now added to the monitored item.

## Monitor Many Items {#monitormanyitems}
To get notified about a whole class of items whenever one is created or changed, monitor the foler that contains the items.

In TeamForge, a folder is a container for multiple items. Any container can be considered as a folder, even if it is not explicitly called a folder. 

  * A document folder contains documents.
  * A task folder contains tasks.
  * A tracker is a folder that contains tracker artifacts.
  * A forum is a folder that contains discussion topics.
  * A repository is a folder that contains code commits.
  * A package is a folder that contains files.

  1. Select the folder that you want to begin monitoring. For example, in a project where you are a member, click **SOURCE CODE** from your **Projects Home** menu and select one of the code repositories in the project.
  2. Click the **Monitor** down arrow, then choose **Monitor Current Folder**.

You are now monitoring the folder. The monitoring icon {% include inline_image.html file="bellicon.png" %} is displayed in the item list view and the monitored items appear in the monitored items list under the _MONITORING_ menu available in the **My Workspace** page.

  {% include note.html content="You do not receive monitoring notifications for changes that you yourself make to an item in a monitored folder." %}

To stop monitoring a folder, click the **Monitor** down arrow, then choose **Stop Monitoring Folder**.

  {% include note.html content="You can also stop monitoring any item from the monitored items list under the _Monitoring_ menu available in the **My Workspace** page." %}

## Monitor an Application {#monitor-an-application}
To monitor the entire application, such as all trackers or all documents in a project, select it from the **Monitoring** tag available in the **My Workspace** page.

Monitoring an application keeps you updated on all items and folder within the application. Unlike individual items, list of items, and folders, you don't monitor entire applications from within a project.

  1. Click **Monitoring** from the **My Page** menu.
  2. From the **Edit Monitoring Subscriptions and Preferences** pane, on the **My Workspace** page, choose the project in which you want to monitor an application.
  3. Click the _MONITORED APPLICATIONS_ tab and select the applications that you want to begin monitoring.
  4. Click **Save**.

You are now monitoring the selected applications.

## Monitor Discussion Forums as RSS Feed
To get an update in your RSS feed reader each time there is an exchange of ideas in a discussion forum, subscribe to the forum's RSS feed.

In TeamForge, you can subscribe to discussion forums via RSS feeds.

  1. Click **DISCUSSIONS** from the **Project Home** menu.
  2. On the **Forum Summary** page, click the name of the forum that you want to subscribe through RSS feed.
  3. On the **Topic Summary** page, click the RSS feed icon {% include inline_image.html file="RSSicon.png" %}.

You can now monitor all topics in the selected discussio forum using your RSS feed reader.

  {% include note.html content="You can access the project message via the RSS reader without logging in to TeamForge, so long as you have the discussion view permissions." %}

## Monitor Project News as RSS Feed
To get an update in your RSS feed reader each time something important is announced in your project, subscribe to the project news as RSS feeds.

In TeamForge, you can subscribe to project news for all the projects via RSS feeds but not to the news of any specific project.

On the _NEWS_ tab of **My Page**, click the RSS feed icon {% include inline_image.html file="RSSicon.png" %}.
  {% include note.html content="You must be a member of a project to view its news." %}
You can now monitor all project news announcements regarding your projects using your RSS feed reader.
  {% include note.html content="You can access the project news via the RSS reader without logging into TeamForge, so long as you have project membership in any project." %}

## View what is being monitored?
All of your monitored items appear under the _MONITORING_ tab available in the **My Workspace** page.

From this list, you can view or stop monitoring any item you are currently monitoring. You can also monitor entire applications from this page.

  1. Select **MONITORING** from the **My Page** menu. Your personal monitoring page lists all items you are currently monitoring.
  2. Specify the filter criteria in one or more filter fields (at the top of each column) and click **FILTER**.
     * You can find a filter field at the top of each column in most of the tables in the TeamForge application.
     * The filter field could be a text box or a drop-down list with multi-select checkboxes.
       {% include image.html file="17-4-filtertables02.png" %}
     * You can type your filter criteria in the text boxes. The search text is case-insensitive.
     * You can also select the filter values from one or more drop-down lists. By default, you can only select up to 10 filter values in a drop-down list. However, you can set a value that suits your requirement for the _FILTER_DROPDOWN_MAX_SELECTION_ token in the `site-options.conf` file to increase or decrease the count.
     * **Filter-as-you-type**: You can find the **Enter keywords** text box in all filter drop-down lists. As you type your filter keyword, instant search results are shown in the drop-down list. For example, in the following illustration, typing "R" instantly shows all statuses having the alphabet "R". The search text is case-insensitive.
       {% include image.html file="filtertables01.png" %}
     * Some search filters may not appear if your site administrator has not enabled them.
  3. After filtering, if you wnat to clear the filters, click **FILTER** and select **Clear** from the drop-down list.
  4. Use the up-down arrow at the top of any column to sort your list by that column.
     * Your primary sort column is identified by a superscript **1** next to the up-down arrow, and your secondary and third-level sort columns, if any, are likewise marked.
     * Click the up-down arrow again to reverse the sort order. 

To stop monitoring an item from your personal monitoring page, select the item you want to stop monitoring, then click **Stop Monitoring**.

## Check who monitors an item?
To see who is monitoring an item or folder, check the **Users Monitoring This Item** list.

 1. Go to the page where the item appears.
 2. Click the item to view the artifact.
 3. On the item's **View Artifact** page, click **Users Monitoring**.

The **Users Monitoring This Item** window displays a list of all users who are monitoring the item.

## Set Frequency for Monitoring Emails {#emailfrequency}
You can set the frequency to check how often you receive monitoring email notifications for all the applications, folders and items you are monitoring.

 1. Select **MY SETTINGS** from your **My Page** menu.
 2. On your _User Details_ section, in the _USER PREFERENCES_ tab, choose an email notification preference.
    * **Email Per Change** - Get a separate email notifiaction for each change to a monitored item.
    * **Daily Digest Email** - Get one email notification each day containing a digest of all changes made to monitored items in the preceding twenty-four hours.
    * **Don't Send Email** - Get no email notifications for changes to monitored items. This can be handy when you are on vacation.
 3. Click **Save**.

After you have set your global email frequency, you can further customize the frequency of application monitoring emails.
 {% include note.html content="When you update two or more artifacts at a time, each user who is monitoring any of the changed artifacts gets a single email describing all the updates." %}

## Set Frequency for Email Notifications on Monitored Applications 
You can specify how often you want to receive email notifications about the applications you are monitoring.

To further personalize your monitoring preferences, you can set the frequency of email notifications for each monitored application on a project level. If you don't set your application monitoring email frequency settings, your global settings will get applied.

For example, suppose you are contributing code to the "Widgets" project, but your role in the "Gizmos" project is of a more advisory nature. When you monitor an item in the "Widgets" project, you'll want more details updates than you will want from items you've monitored in the "Gizmos" project.

 1. Set the global default email frequency from your **MY SETTINGS** page. See [Set Frequency for Monitoring Emails](#emailfrequency).
 2. Click **MONITORING** from the **My Page** menu.
 3. From the **Edit Monitoring Subscriptions and Preferences** page, choose the project in which you want to configure monitoring email frequency.
 4. On the _EMAIL NOTIFICATION PREFERENCES_ tab, specify how often you want to be notified and click **Save**.

Any email notification preferences you set here will override the default preferences that you set on your **MY SETTINGS**page.
 {% include note.html content="When you update two or more artifacts at a time, each user who is monitoring any of the changed artifacts gets a single email describing all the updates." %}




{% include links.html %}



