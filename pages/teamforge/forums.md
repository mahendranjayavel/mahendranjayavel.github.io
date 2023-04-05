---
title: Discussion Forums
keywords: forum, forums, discussion, discussions, discussion forums, discussion forum
tags: [discussion_forums, associations]
sidebar: teamforge_sidebar
last_updated: Feb 8, 2018
folder: teamforge
permalink: forums.html
summary: You can communicate with project members via discussion forums. Discussions provide workspaces where project members can discuss project-related topics online or by email. Forum administrators create forums and do what is needed to keep them on track, such as editing or moderating forum posts.
---

## What is a Discussion Forum?

TeamForge discussions provide workspaces where project members can work together online or by email.

Discussion forums and mailing lists are closely integrated. Forum administrators can choose to enable a mailing list for each project forum. A mailing list extends the discussion forum functionality to allow project members to post messages to the forum using email.

Discussion forums can be public or private, depending on the forum's objective and desired level of access into the forum. Private discussion forums restrict anyone without specific access permissions from viewing or posting into the forum.

In a moderated discussion, messages from anyone except "trusted" users are screened by a moderator before they are posted. Messages posted by trusted users do not require the moderator's approval.

It's a good idea to use a discussion forum instead of direct personal email whenever privacy or security concerns don't prevent it, even when the communication only involves two project members.

 * Members not directly involved often can make unexpected contributions if they are aware of the discussion.

 * TeamForge archives all news items, forum posts, and mailing list communications, so you can go back and find valuable information later.

{% capture forumnotes %}
{% include inline_image.html file="status-success-small.png" %} Encourage project members to work together by creating discussion forums to which project members with the appropriate permissions can post messages.<br><br> 
{% include inline_image.html file="status-success-small.png" %} Discussion forums can also function as mailing lists.<br><br>
{% include inline_image.html file="status-success-small.png" %} You can choose to make a discussion forum either public or private.<br><br>
{% include inline_image.html file="status-success-small.png" %} You can be a forum or mailing list administrator without being a project administrator. Ask your project administrator or site administrator to grant you forum administration permissions.<br><br>
{% include inline_image.html file="status-success-small.png" %} Forum administrators can enable or disable forum moderation and add or remove moderators and trusted users. Any project member with forum post permissions can be a moderator.<br><br>
{% include inline_image.html file="status-success-small.png" %} Forum administrators can also make forums work like mailing lists.<br><br>
{% include inline_image.html file="status-success-small.png" %} Guest users can monitor a forum if email monitoring is set to **Allow all site users and guests**.<br><br>
{% include inline_image.html file="status-success-small.png" %} Additionally, guest users can email-post or subscribe to a forum if the mailing list is enabled and **Email Posting** is set to **Allow all site users and guests** from the discussion settings.

{% endcapture %}
{% include callout.html type="primary" content=forumnotes %}

   {% include tip.html content="Who can post by email to a discussion forum is controlled by the **Email Posting** options set for the forum. It does not depend on the permissions set for users of the Web forum." %}

## Create/Rename/Edit a Discussion Forum

### Create a Discussion Forum

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, click **Create**.
3. On the **Create Discussion Forum** page, enter a title and description for the forum.
4. To make it a private discussion forum, set the **TYPE** to **Private**. 
   {% include callout.html type="primary" content="Private discussion forums restrict anyone without specific access permissions from posting to the forum. For example, you may want to restrict a preliminary planning discussion to your project's core team before sharing it more widely." %}
   
5. If you want the forum to work as a mailing list, select **Enable Mailing List**.
   1. Provide a name for the mailing list in the **EMAIL ADDRESS** field.
      {% include callout.html type="primary" content="The mailing list name must be unique within a project." %}
   2. Set who can [post to the forum via emails][forums.html#posttoforumbyemail].
      {% include callout.html type="primary" content="Choose either **User with Roles and Permissions** (default) or **Allow only forum admins** from the **Email Posting** drop-down list." %} 
   3. Set who can [subscribe to monitoring via emails][discussions-faqs.html#subscribetoforumbyemail].
      {% include callout.html type="primary" content="Choose either **User with Roles and Permissions** (default) or **Allow only forum admins** from the **Email Monitoring** drop-down list. Selecting **Allow only forum admins** for **Email Monitoring** will not restrict users with `Discussion-View` permission from getting monitoring emails in case they choose to monitor the forum via the web UI." %} 
   4. Choose how replies to posts are handled by setting the **REPLY BEHAVIOR**.
      {% include tip.html content="Many users are accustomed to having their replies go automatically to the whole list. Others are used to having replies go just to the original sender. You should check with your users to see what makes more sense for a particular mailing list.<br><br>When **REPLY BEHAVIOR** is set to `To the list`, email replies are sent to the list as a whole, not to the individual post. This may be a change from what some users are used to." %}
   5. Specify a prefix for the subject lines of messages from this list. This can help users sort their incoming messages, if they are subscribed to multiple lists.
   6. You may limit the size of emails (including attachments, if any). Enter the size (in MB) in the **MESSAGESIZE** field.
   7. Under **FOOTER TEXT**, provide any information you want to show up at the bottom of each email that subscribers receive. For example, you may want to offer useful web locations or email addresses.
6. To make this a moderated forum, select **ENABLE MODERATION**.
7. Click the **Search** icon to add moderators. 
   {% include callout.html type="primary" content="A moderated discussion must have at least one moderator. If your project includes members of a parent project, you can select those members too." %}
8. Click the **Search** icon to add trusted users. Posts by trusted users do not need moderator approval.
9. Click **Save**.

If you set your forum to work as a mailing list, all project members monitoring the forum will receive notifications whenever a new topic or message is posted.

### Rename or Edit a Discussion Forum

To help keep a forum or mailing list focused, try updating its title.

As a forum administrator, you can enable/disable mailing list or moderation features or just update their settings for the discussion forum.

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, select the forum you want to change, and click **Edit**.
3. On the **Edit Discussion Forum** page, make your changes.
4. Click **Save**.
   {% include note.html content="All project members monitoring the forum receive notifications of the update." %}

## Subscribe to a Discussion Forum or Mailing List

When you monitor a discussion forum, you are notified of contributions to the forum by email. Monitoring a forum is the same thing as subscribing to a mailing list.

A bell icon {% include inline_image.html file=bellicon.png %} in the **Monitoring** column indicates that you are subscribed to a forum.

* If you prefer to do it by email:
  1. To subscribe in message by message type subscription, send an email to `<Email address name in Mailing list>-<project name>-subscribe@<domain name>`
  2. To subscribe in digest type, send an email to `<Email address name in Mailing list>-<project name>-digest-subscribe@<domain name>`
  3. You can also change the subscription type from message by message to digest and vice versa.

* If you prefer to do it through the web interface:
  1. Click **Discussions** from the **Project Home** menu.
  2. Click **Monitor**. Set the notification frequency using **Monitoring Preference** as it suits you.

## Subscribe Others to a Discussion Forum or Mailing List

You can add other users to a discussion.

If you are a forum administrator, you can also add users to the discussion as a group.
1. Click **DISCUSSIONS** from the **Project Home** menu.
2. Select the forums that you want to add users to.
3. In the **Monitor** list, click **Users Monitoring Selected**.
4. On the **USERS** tab, Click **Add**.
5. On the **Find a User** window, move the users you want into the **USERS TO ADD** column.

   {% include tip.html content="To add users as a group (assuming you are a forum administrator), do the same operation on the **USER GROUPS** tab." %}

## Create a Discussion Forum Topic

Create a new forum topic to begin discussion of a new subject.

A topic starts a message thread to which other users can reply. A forum can have any number of topics.

A forum topic is similar to an email, in that you can use it communicate with other people subscribed to the forum, as if it were an email list. If the forum owner has enabled the forum to work as a mailing list, then you can [post to the forum by email][forums.html#posttoforumbyemail] as well.

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, click the title of the forum in which you want to create a topic.
3. On the **Topic Summary** page, click **Create**.
4. On the **Create a Topic** page, describe the topic in the **Subject** field.
5. Type the message in the Message field. After the topic is created, other users can reply to this message.
6. If you want the message sent by email to people who are not members of the forum, add their email addresses to the **Other Recipients** field. If there is more than one, put commas, semicolons or spaces between them.
   {% include note.html content="In a moderated discussion forum, addresses in the **Other Recipients** field get your message only after the moderator approves the message." %}
7. To add an attachment to the topic, click **CHOOSE FILE** and select the file.
8. Click **Save**.
   {% include note.html content="If this discussion forum is moderated, the topic is held until a moderator approves or rejects it. (Except if it is from a trusted user, these messages don't require moderation.)" %}

## Reply to a Discussion Forum Message

You can post a message in any topic in any forum you have access to. You can also post a message in reply to another message.

If the forum is moderated, you must have posting permission. Contact the forum moderator.

Tip: If you are getting your forum messages delivered as email, you can reply to a post by email too.

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, find the topic in which you want to post a message.
3. In the section containing the message to which you want to respond, do one of the following:
   * Click **Quote** to quote the original message in your response message.
   * Click **Reply** to omit the original message from your response message.
4. Write the message.
5. To add an attachment to the message, click **CHOOSE FILE** and select the file.
6. Click **Save**.

The forum message is posted. Other project members can reply to it using the same process.

## Moderate Discussion Forum Posts

A message to a moderated discussion forum is held until a moderator acts on it. (Except if it is from a trusted user. These messages don't require moderation.)

As a moderator, you get an email when a message is awaiting moderation. The email contains the URL where you can approve or reject the message.

### Add or Modify Moderators

As a forum administrator, you can add or remove forum moderators.

{% include callout.html type="primary" content="If a forum is moderated, it must have at least one moderator.<br><br>When you designate a forum moderator, you also become a moderator yourself." %}
1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, select the forum for which you want to add or modify the moderators.
3. On the **Topic Summary** page, click **Edit**.
4. On the **Edit Discussion Forum** page, add or modify the forum moderators.
   {% include note.html content="The existing moderators are listed." %}
5. Click the **Search** icon to add or remove forum moderators. You can select one or more moderators.
   {% include note.html content="You can select the inherited project members also from the list." %}
6. To add moderators, select the required users, click **Add** and click **OK**.
7. To remove moderators, select the required users, click **Remove** and click **OK**.
8. On the **Edit Discussion Forum** page, click **Save**.

### Moderate a Discussion Forum by Email

If your discussion forum is also a mailing list, you can approve or reject the post by email.

See the notification email for your options.


|--------|-------------|
| Option | Description |
|--------|-------------|
| To accept the message | Send an email to \<postId>-accept@\<domain>, or just click **Reply**. |
| To accept the message and add the sender to the "Trusted Users" list | Send an email to \<postId>-allow@\<domain>, or click **Reply-to-All**. |
| To reject the message | Send an email to \<postId>-reject@\<domain>. |
| To add your comments to the message | Include your comments in the **Start Comment** and **End Comment** blocks in your response email. Your comments will appear in the approved post. |


### Approve a Forum Post
If a post is appropriate, you can add it to the forum by approving it.

{% include callout.html type="primary" content="If your discussion forum is also a mailing list, you can approve or reject the post by email. See the options in the notification email.<br><br>If the sender consistently contributes useful and appropriate input, you can save the moderation time by designating that user as a `trusted` user. Posts from trusted users don't have to be moderated." %}

1. On **My Page**, click the **ITEMS AWAITING MY APPROVAL** tab. The number of posts awaiting approval are displayed against the project names.
2. To view forum details, click the hyperlinked **Number of Posts** for your project.
3. Click the **Number of posts awaiting approval** link on the **Forum Summary** page.
   {% include note.html content="The Forum Summary page displays all the forum names and the corresponding number of posts awaiting approval, if any." %}
4. Select either of the three approval techniques in the **Posts Awaiting Approval** tab. 

   As the moderator of the post, you will be able to view the topic title in the **All Topics** tab; and post title in the **Posts Awaiting Approval** tab on the **Topic Summary** page.
   {% include note.html content="In the **All Topics** tab, the hourglass icons differentiate the topics that contain posts awaiting approval. To view posts nested within a topic, you can use the hyperlinked topic title." %}

   |--------|-------------|
   | Option | Description |
   |--------|-------------|
   | To approve posts and senders individually | Select the post and click **Approve** or **Approve and Trust**. |
   | To approve multiple posts and senders at once | Select all the posts to be approved and click **Approve** or **Approve and Trust** below the post details. |
   | To view the post details and approve | Click the post title and click **Approve** or **Approve and Trust** on the **Review Post Awaiting Approval** page after reading the details. |


### Reject a Forum Post

If a proposed message is not appropriate or does not contribute to the goals of your discussion forum, you can reject it.

{% include callout.html type="primary" content="If your discussion forum is also a mailing list, you can approve or reject the post by email. See the options in the notification email.<br><br> You can reject posts with or without comments or reasons for rejection." %}

1. On **My Page**, go to **ITEMS AWAITING MY APPROVAL** tab.
2. On the **Forum Summary** page, click **Number of posts awaiting approval**. Topics that contain posts awaiting approval have an hourglass icon.
3. On the **Posts Awaiting Approval** tab, choose your method of rejection.

|-------|---------|
| Option | Description |
|-------|---------|
| To reject the posts individually | Select the each post, then click **Reject** at the end of the post. |
| To bulk-reject the posts | Select all the posts you want to reject, then click **Reject** below the post details table. |
| To view the post details and reject | Click the hyperlinked post title, then click **Reject** on the **Review Post Awaiting Approval** page. |
| To explain your rejection with a comment | Click **Reject With Comment** instead of **Reject**. |

{% include note.html content="The rejection comment is posted to the message sender." %}

Rejected messages are deleted from the posts awaiting approval list and the message senders are notified by email.

### Stop Moderating a Forum
If a moderated discussion forum does not require posts to be moderated anymore, moderation can be disabled.

To change a moderated discussion forum to unmoderated discussion forum in Digital.ai TeamForge, select the forum and turn off its moderation feature.

* Users with forum admin permissions only can enable/disable moderation.
* On disabling moderation on a moderated forum, the posts awaiting approval are automatically approved.

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, select the moderated forum that does not require moderation anymore.
3. On the **Topic Summary** page, click **Edit**.
4. On the **Edit Discussion Forum** page, to disable moderation, de-select the **ENABLE MODERATION** check box.
   The following message is displayed:
   
   ```html
   Any post awaiting moderation will be approved automatically.
   ````
5. Click **Save** to turn off the moderation. To keep moderation enabled, select **Cancel**.

   The moderated discussion forum changes to an unmoderated discussion forum and any posts sent to the forum will be displayed without any restrictions.


## Post to a Forum by Email {#posttoforumbyemail}

If the forum also works as a mailing list, you can create a forum topic by sending an email message to the forum. You can also reply to a post by replying to the email.

If the forum is moderated, you must have posting permission. Contact the forum moderator.

The forum's email address, if it has one, appears on the Topic Summary page.
{% include tip.html content="If a forum is not set up to work as a mailing list, you can still get posts by email when you monitor the forum. See Monitor many items." %}

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, click the forum in which you want to create a topic.
3. On the **Topic Summary** page, find the email address in the **Mailing List** field. Send your email message to that address. Digital.ai TeamForge maps your email to the forum topic like this:

   |-------------|-------------------|
   | Email Field | Forum Topic Field |
   |-------------|-------------------|
   | To | Forum email address |
   | Subject | Title of forum topic |
   | Body | Text of forum topic |
   | Attachments | Attachments |

Emails from the forum can be read in RTF (Rich Text Format) or HTML format. The format of the message is delivered as an attachment to the post. Embedded attachments, such as text or images, are also delivered.

In a moderated discussion forum, if you add other addresses in the `cc:` field of your email, those addresses get your email only after the moderator approves the message.

## Search for Posts

Search for a post by using keywords, specifying the forum it belongs to, selecting the sender of the post or entering relative date or date range.

You can search for posts either across all forums or within specific forums.
1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, click **Search Posts**.
3. On the **Post Search Criteria** page, enter the desired search criteria.
   {% include tip.html content="You can use wildcards." %}
   * To search by subject, body or attachments, enter the text in the **Search Text** field and select **Subject**, **Body** and/or **Attachments** options.
   * To search by forum name, select the forum in the **Forum** field.
     {% include note.html content="When none of the forum options are selected, the system searches for matching posts across all forums." %}
   * To search by post-sender, select the user name in the **Posted By** field.
     {% include note.html content="You can select **User running search** option to display your posts." %} 
   * To search by time span, specify relative dates such as "Within the last 7 days".
   * To search by date range, enter the start and end dates for the search. Click the Calender icon to select dates from a calendar.
4. Click **Search**.

All posts matching your search criteria are displayed in the _Search Results_ page.

## Associate Forum Messages with Other Items

When a forum message concerns some other Digital.ai TeamForge items, such as a document, a tracker artifact, a file release, a code commit, or a task, link the message to the item under discussion by creating an association.

Creating association between items enables you to define relationships, track dependencies, and enforce workflow rules.

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, find the forum message with which you want to create an association. Any existing associations are displayed in the **Associations** section.
3. Click **Associate**.
4. In the **Add Association Wizard** window, select the items with which you want to associate the artifact:
   * **ENTER ITEM ID** - If you know the item's ID, you can enter it directly.

     {% capture associateitem %}
     {% include inline_image.html file="status-success-small.png" %} To associate an object in an integrated application from within TeamForge, use the `[<prefix_objectid>]` format. Successful associations appear hyperlinked. <br><br>
     {% include inline_image.html file="status-success-small.png" %} Each integrated application displays its prefix on moving the mouse over the application name in the tool bar.
     {% endcapture %}
     {% include callout.html type="primary" content=associateitem %}
   * **ADD FROM RECENTLY VIEWED** - Select one of the last ten items you looked at during this session.
   * **ADD FROM RECENTLY EDITED** - Select one of the last ten items you changed.
5. Click **Next**.
6. You may add a comment in the **ASSOCIATION COMMENT** text box.  
7. Save your work.
   * Click **Finish and Add Another** to add additional associations.
   * Click **Finish** to return to the **Details** page.
   {%capture associationnotes%}
   {%include inline_image.html file="status-success-small.png" %} When an association is added to or removed from TeamForge objects such as tracker artifacts, tasks, documents, discussions, and file releases, a notification mail is sent to users monitoring these objects. <br><br>
   {% include inline_image.html file="status-success-small.png" %} An option is provided at site level and user level to make sure whether the notification mail has to be sent or not. For more information on this, see [Configure your Site's Settings][siteadmin-configuresiteviaui].
   {% endcapture %}
   {% include callout.html type="primary" content=associationnotes %}

## Delete Forum Messages and Topics

### Delete a Forum Message 
When a message in a forum is off topic or potentially harmful, you may want to delete it.

Before deleting a forum message, consider leaving it in place so that future users can consult it if they need to. Consider this even if the message does not seem very useful right now.

   {include important.html content="You cannot delete the topic starter's original message without deleting the entire topic." %}

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, find the forum message that you want to delete.
3. Click **Delete** and confirm that you want to delete the forum message.

The forum message is deleted.

### Delete a Forum Topic

If you no longer want a forum topic in your project, you can delete it.

  {% include warning.html content="Deleting a forum topic deletes all of the forum messages in the topic. Delete a forum topic only if you are sure that you no longer need any of the forum messages in it." %}

1. Click **DISCUSSIONS** from the **Project Home** menu.
2. On the **Forum Summary** page, click the title of the forum containing the topic that you want to delete.
3. On the **Topic Summary** page, select the topic you want to delete.
4. Click **Delete** and confirm that you want to delete the topic.

The forum topic is deleted.

{% include links.html %}

