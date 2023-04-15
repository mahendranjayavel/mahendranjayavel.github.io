---
title: FAQs on Discussions
keywords: FAQ, frequently asked questions
tags: [faq, discussion_forums]
sidebar: teamforge_sidebar
permalink: discussions-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on Discussions and Discussion Forums in TeamForge.
---

## Is the discussion forum creator subscribed by default?

Yes. The user creating the discussion forum is subscribed by default.
{{site.data.alerts.hr_shaded}}


## How can I monitor a forum or mailing list?

There are two methods for monitoring a forum or mailing list in TeamForge: at the Discussion Forum level and at the My Workspace level.

At the Discussion Forum level:

* Check the box beside the forum in question.
* Select the **Monitor** button.
* Select **Monitor Selected**.

At the My Workspace level:

* Select **Monitoring**.
* Select the project name.
* Select the _Monitored Applications_ tab.
* Select **Discussions**.
* Click **Save**.
  
  {% include note.html content="You must monitor a forum to receive email from the mailing list associated with that forum." %}
{{site.data.alerts.hr_shaded}}

## How do I find the email address for a forum?

The email address for the forum is displayed on the Topic Summary page. If a mailing list is not enable, you will not see an email address on the Topic Summary page.

To find the email address for a forum:

  1. Click **DISCUSSIONS** from the **Project Home** menu.
  2. On the **Forum Summary**  page, click the title of the forum in which you want to create a forum topic. The **Topic Summary** page is displayed. The email address is listed in the **Mailing List** field.
{{site.data.alerts.hr_shaded}}

## How do I remove a user from Discussion?

Unfortunately, currently there is not a way for a TeamForge admin to remove a user from monitoring.

Instead, you can remove the user from monitoring the discussion by clicking the **Stop Monitoring Selected** option from the **Monitor** drop-down button on the **Forum Summary** page.
{{site.data.alerts.hr_shaded}}

## I can see the message I posted to a discussion in the web UI, but I didn't receive any of the responses through email.Why?

To receive forum posts through email, you must monitor the forum.

You can do this by selecting the forum you wish to monitor and choosing the **Monitor Selected** option from the **Monitor** drop-down button at the bottom of the **Forum Summary** page. For more information, see [Monitor Many Items][monitoring.html#monitormanyitems].
{{site.data.alerts.hr_shaded}}

## Why are some of the discussions threaded?

Posts that are sent the mailing list address of the discussion will create new topics, and hence will not be threaded.

Posts that are made in response to another post will be threaded beneath the original post.
{{site.data.alerts.hr_shaded}}

## What happens when I post to a moderated discussion forum?

A message to a moderated discussion forum is held until a moderator acts on it. (Except if you are a trusted user. These messages do not require moderation.)

* The moderators of the discussion receive an email notification that you have posted a message. The email notification contains the URL path to moderate the post.
* A moderator can either approve or reject your message.
* If the moderator accepts the message, the message status changes to "Accepted" and the message is posted to all the users monitoring the forum.
* If the moderator accepts the message and trusts the sender, the message status changes to "Approved and Trusted" and the message is posted to all the users monitoring the forum. All subsequest posts from you are automatically approved.
* If the moderator rejects the message, he/she can include his/her comments or reasons in the moderation rejection email, and the message is removed from the archive.
* In the _All Topics_ tab, an hourglass icon indicates which topic contains posts that await approval.
{{site.data.alerts.hr_shaded}}

## Who can be a moderator?

A discussion forum moderator is selected by the forum administrator.

* You can be a moderator by being a project member with forum post permissions.
* A moderator can moderate a discussion forum using emails or the web UI or one of the CollabNet desktops.

  If the mailing list isn't enabled for a moderated discussion forum, moderation can be done only through the Web UI.

* A moderator can trust the sender and approve a message or reject the message.

  {% include note.html content="To enable or disable moderation or add or remove moderators, you must be either the forum administrator or project administrator." %}
{{site.data.alerts.hr_shaded}}

## Do project owners get automatically subscribed to the discussion forum started by another member?

A project owner does not get subscribed to the discussion forum started by another user.

To make sure the project owner is included, add the user as a member when creating the forum.
{{site.data.alerts.hr_shaded}}

## Can I subscribe to a TeamForge discussion forum's mailing list through an email? {#subscribetoforumbyemail}

Sure, you can subscribe to a discussion forum's mailing list to keep up with changes, through an email. When you subscribe or monitor a discussion forum, you are notified by an automatic email whenever there is any update to the discussion.

**To subscribe to a mailing list** - You can subscribe to the discussion forum's mailing list by sending an email to `<mailing list name>-project name-subscribe@domain>`.

You must have the _Discussion: view_ permission to be made a subscriber. Check with the forum administrator, if you do not have the permission.

As with other items that you may be monitoring, the discussion forum to which you subscribe through an email is also added to the **My Workspace > Monitoring > Monitored Objects** list. Your user name is added to the 'Users Monitoring' list of the discussion forum. Both these entries are removed when you unsubscribe from the mailing list.

To subscribe in digest type, send an email to `<mailing list name>-project name-digest-subscribe@<domain>`.

**To unsubscribe from a mailing list** - You can unsubscribe from the discussion forum's mailing list by sending an email to `<mailing list name>-project name-unsubscribe@<domain>`.
{{site.data.alerts.hr_shaded}}

## Why would I want to make a discussion forum moderated?

Automated processes can only do so much to protect forum quality. Moderated posting can be thought of as a temperory transfer of control from automated processes to a human decision maker.

Software can instantly analyze an email to determine whether the sender is allowed to post messages directly to the list or if the message should be sent for moderation. However, the software doesn't recognize the sender as a person who participates in the organization, nor does it have the sophistication needed to determine whether the message contents are on-topic for the mailing list.

Advantages of moderated posting:

  * Moderators help keep content on-topic by rejecting off-topic messages and providing helpful suggestions to users whose posts are rejected.
  * Moderators help maintain a positive environment for list users by rejecting messages containing harsh or abusive language. 
  * Moderators can allow deserving non-members to post to lists that are ordinarily closed to non-members.
  * Moderators prevent spam.

### Example

Ashish makes the development forum in his project a moderated one as he wants to make sure that all the messages posted to the discussion come to him for approval before they're included in the forum. When a message arrives, he reads the message, and if it's appropriate for the discussion, he accepts it; if not, he rejects it.

Over time, Ashish finds that the traffic in his discussion has increased and he is no longer able to moderate all the posts by himself. So he adds a couple of other senior developers in his project as moderators, who can share the responsibility of moderating the forum.

After a while, Ashish realises that he doesn't have to reject any messages posted to the forum as everyone seems to understand the purpose of the forum and users appropriate language in emails. so he removes the restriction and make the forum an unmoderated one. Now Ashish and the other moderators no longer receive emails for approval when a user posts a message to the discussion. Messages are directly included in the forum and delivered to the forum subscribers.

{% include links.html %}