---
title: FAQs on Review Board
keywords: FAQ, frequently asked questions
tags: [ctf_20.0, faq, review_board]
sidebar: teamforge_sidebar
permalink: reviewboard-faqs.html
last_updated: Apr 7, 2020
summary: These are some of the frequently asked questions on Review Board.
---

## Review Board deployment fails on sites that use a self-signed certificate. What should I do? {#cert-verification-cfg}

Review Board deployment fails on sites that use a self-signed certificate. Remove the `verify=platform_default` parameter from the `[https]` section of the `cert-verification.cfg` file and then try deploying Review Board again.

```shell
vim /etc/python/cert-verification.cfg
````

Delete or comment out the `verify=platform_default` parameter.
```shell
[https]
# verify=platform_default
````
{{site.data.alerts.hr_shaded}}

## Could not initialize Review Board due to 502 or 503 Bad Gateway Error. What should I do?
<!-- Artifact artf394776 : [Doc] Troubleshoot if reviewboard initialization fails with 502 or 503 -->

Reinitialize Review Board in case Review Board initialization fails the first time due to 502 or 503 Bad Gateway error.

Reinitialize TeamForge on the Review Board Server.
```shell
teamforge reinitialize
````
{{site.data.alerts.hr_shaded}}

<!-- https://forge.collab.net/sf/go/artf304542#3 -->
## Users are not getting email notifications for review requests and reviews. What should I do? {#rbemailsettings}
You must update the Review Board application's E-mail Server Settings with the user name and password used for the `JAMES_RELAY_USER` and `JAMES_RELAY_PASSWORD` tokens. Do this post install or upgrade of TeamForge and Review Board. 

{% capture emailsettings %}
{% include inline_image.html file="status-success-small.png" %} Keep the values of the `JAMES_RELAY_USER` and `JAMES_RELAY_PASSWORD` tokens handy before you begin.
{% endcapture %}
{% include callout.html type="primary" content=emailsettings %}

1. Log on to TeamForge as a Site Administrator.
2. Select **My Workspace > Admin**. 
3. Select **Integrated Apps** from the **Projects** menu. 
4. Select **Review Board** and click **Administer**.
5. Click **E-Mail** from the **System Settings** pane. 
6. Under **E-MAIL SERVER SETTINGS**, type the `JAMES_RELAY_USER` and `JAMES_RELAY_PASSWORD` values in the **Username** and **Password** fields respectively.
7. Click **Save**.
{{site.data.alerts.hr_shaded}}

## What are the software requirements for installing Review Board as an integrated application in TeamForge {{site.data.identifiers.teamforge}}?

* Review Board can run on {{site.data.identifiers.rhel_centos_now}} and {{site.data.identifiers.rhel_centos_past}}.
* In addition, Review Board needs PostgreSQL {{site.data.identifiers.postgres_long}}. See [TeamForge Installation Requirements][requirements] for more information.
{{site.data.alerts.hr_shaded}}

## Which version of Review Board does TeamForge {{site.data.identifiers.teamforge}} support?

TeamForge {{site.data.identifiers.teamforge}} supports Review Board {{site.data.identifiers.review_board}}.
{{site.data.alerts.hr_shaded}}

## Which repositories does Review Board support?

Review Board supports only Subversion repositories in TeamForge.
{{site.data.alerts.hr_shaded}}

## How do I manage users in Review Board?
You can manage Review Board users from TeamForge. Whenever you create or edit users in TeamForge, they are synchronized automatically in Review Board.
{{site.data.alerts.hr_shaded}}

## Can I specify 'RB' as a prefix in my project?
No. You cannot specify 'RB' as a prefix in your project. The prefix for Review Board must be unique for every project.
{{site.data.alerts.hr_shaded}}

## Is it possible to grant TeamForge specific-permissions as part of the system generated Review Board administrator?
No. It is not possible to grant TeamForge specific-permissions as part of the system generated Review Board administrator (integrated application specific role).
{{site.data.alerts.hr_shaded}}

## Can I use the Review Board 'Search' feature after integrating Review Board with TeamForge?
No. TeamForge does not support the 'Search' feature of Review Board.
{{site.data.alerts.hr_shaded}}

## What are the additional features available in Review Board after you integrate it with TeamForge?
Review Board uses some of the TeamForge features like object IDs, links, GO URLs, and SVN integration and associations. For more information, see [How does an integrated application interact with other TeamForge tools?][externalapplicationsforprojects.html#integratedappinteractionwithTF].
{{site.data.alerts.hr_shaded}}

## What are the other TeamForge features which Review Board does not support after you integrate Review Board with TeamForge?
Global search, page component, recent history and project template features of TeamForge are not supported in Review Board.
{{site.data.alerts.hr_shaded}}

## Where can I find the documentation for Review Board?
You can find the documentation for Review Board [here](http://www.reviewboard.org/docs).
{{site.data.alerts.hr_shaded}}

## How do I rectify incorrect pending review count in Review Board ?
You can reset the counters using the following command and restart the Apache server.
```shell
/opt/collabnet/reviewboard/bin/rb-site manage /opt/collabnet/reviewboard/ReviewBoard-2.5.6.1 fixreviewcounts
````

{% include links.html %}
