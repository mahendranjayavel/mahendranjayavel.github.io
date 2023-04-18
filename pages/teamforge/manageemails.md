---
title: Manage Email Settings
keywords: emails
tags: [site_admin_tasks, monitoring, authentication, users]
sidebar: teamforge_sidebar
permalink: manageemails.html
last_updated: Jul 24, 2018
summary: These are additional details you can follow while configuring your email settings.
---
## Remove Users from Monitoring Objects

As a site or project administrator, if one or more users are no longer project members, you can remove them from monitoring selected TeamForge objects they once subscribed for monitoring.

However, you cannot remove a user from the monitoring list if the user is monitoring applications such as trackers, documents, tasks, and so on instead of individual TeamForge objects.

By default, this feature is disabled. To enable this feature, set the [USER_MONITORING_REMOVE_ENABLED][siteoptiontokens.html#USER_MONITORING_REMOVE_ENABLED] token to `true` in the `site-options.conf` file.

{% include note.html content="Every user removal operation is being logged in the database for audit purposes." %}

1. Go to the item, from which you want to remove users from monitoring.
2. Select users to remove from monitoring list.
3. If you want to remove one or more users from monitoring one of the items, select the item, then click **Monitor > Users Monitoring Selected**. 

   The Users Monitoring This Item window appears.
4. If you want to remove one or more users from monitoring more than one item, select all the items, then click **Monitor > Users Monitoring This Folder**.
   
5. In the case of team monitoring, click **Monitor > Users Monitoring This Team**.
6. In the following window, select one or more check boxes corresponding to the users you want to remove from monitoring.
7. Click **Remove**. The `Are you sure you want to remove the selected user(s) from monitoring?` message appears.
8. Click **OK**.
   
   The selected users are removed from monitoring the selected object. An e-mail notification is sent to all active users that are removed from monitoring selected objects.

## Limit the Size of Message Attachments
To avoid overtaxing your mail server or your storage volume, you may want to set a ceiling on the size of the attachments that users can send to a forum via email.

When a user sends an attachment that is larger than the limit, the message is rejected and the user gets an email from the Site Administrator explaining that the attachment exceeded the limit.

{% include tip.html content="Before imposing a file attachment size limit, it's a good idea to point your users to better ways of collaborating around large files. Consider suggesting source code repositories, backup systems, or other appropriate solutions." %}

1. Open the `site-options.conf` file, the master configuration file that controls your TeamForge site.
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````
2. Set the value of the [DISCUSSION_MAX_ATTACHMENT_SIZE][siteoptiontokens.html#DISCUSSION_MAX_ATTACHMENT_SIZE] token.
   
   For example, if your users are given to using Microsoft Word documents on the site, you might set `DISCUSSION_MAX_ATTACHMENT_SIZE` to 10 MB, and increase the value by two or three MB at a time if users need more headroom.
3. Review the changes, then save the `site-options.conf` file.

## Limit the Size of Document Attachments
When many users store very large documents on your site, you may sometimes notice a slowdown in your site's performance. You can reduce the impact of such a use pattern by telling TeamForge not to attach documents larger than a certain size.

{% include tip.html content="It's also a good idea to let your users know that the Documents tool in TeamForge is not designed primarily as a storage device. As a best practice, upload documents to make them available for collaboration, not for backup or long-term storage." %}

1. Open the `site-options.conf` file, the master configuration file that controls your TeamForge site.
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````
2. Add the [DOCUMENT_MAX_FILE_UPLOAD_SIZE][siteoptiontokens.html#DOCUMENT_MAX_FILE_UPLOAD_SIZE] parameter and give it a value equal to the maximum size (in megabytes) of documents to be uploaded.
3. Review the changes, then save the `site-options.conf` file.


## Relay Emails Through SMTP Gateway with Authentication {#relayemailssmtp}
You can set up TeamForge to relay emails through an SMTP gateway (such as Amazon AES) that uses authentication. By default, James sends emails directly. However, you may prefer relaying emails through an enterprise relay server. Configuring the [JAMES_GATEWAY_*][siteoptiontokens.html#JAMES_GATEWAY] tokens let you do that.

{% include note.html content="By default, TeamForge uses the user's email address (as registred in TeamForge user profile) as the sender address (`From`). Therefore, it is important that the mail relay does not impose any restrictions on the email sender address and accepts all emails to be relayed." %}

To relay emails through an SMTP gateway:

1. Set the following site-options.conf tokens.
   ```shell
   vi /opt/collabnet/teamforge/etc/site-options.conf
   ````
   ```conf
   JAMES_GATEWAY_HOST=
   JAMES_GATEWAY_PORT=
   JAMES_GATEWAY_USERNAME=
   JAMES_GATEWAY_PASSWORD=
   ````
2. Save the `site-options.conf` file.
3. {% include installupgrade/deploy_services_without_note.html %}

## DomainKeys Identified Mail (DKIM) {#dkim}

A <a href="teamforge-new.html#dkim" data-toggle="tooltip" title="DKIM (DomainKeys Identified Mail) is an email authentication mechanism, which by means of public key cryptography, attaches the sender's domain name in the headers of the outgoing emails, thus ensuring the authenticity of the email.">DKIM</a> signature is being added to the headers of all outgoing TeamForge emails to authenticate all outbound emails against email spoofing.

DKIM is enabled by default. Once enabled, the DKIM signature is included in all the outgoing TeamForge emails. However, you can disable DKIM using the **JAMES_DKIM_VERIFICATION** token. In general, you must set up the following four newly added tokens on your TeamForge site (`site-options.conf`).

* **JAMES_DKIM_VERIFICATION**
* **JAMES_DKIM_SELECTOR**
* **JAMES_DKIM_SIGNINGDOMAIN**
* **JAMES_DKIM_KEY_TYPE**

For more information, see [TeamForge site-options.conf Tokens][siteoptiontokens].

{% include image.html file="dkim-signature.png" caption="A TeamForge notification email with DKIM signature in its header" %}

{% include links.html %}