---
title: FAQs on Associations 
keywords: FAQ, frequently asked questions, association, associations
tags: [faq, associations]
sidebar: teamforge_sidebar
permalink: associations-faqs.html
last_updated: Apr 5, 2018
summary: These are some of the frequently asked questions on Associations in TeamForge.
---

## My Associations do not appear. What should I do?

You may not be seeing your assocations for several reasons. If you are not able to see your associations, verify the following:

* Only repositories scoped to the configured TeamForge project will result in associations. That is, make sure the version control repository you’re using is a part of the TeamForge project that has been mapped to the JIRA project in question.
* When a TeamForge project is first mapped to a JIRA project, the JIRA issues need to be synced into the TeamForge data store. Association will fail if you attempt to create an association between a commit and JIRA issue that has not yet been synced. Please refer to the Sync Issues functionality.
* Make sure the association syntax is correctly using square brackets. Association syntax is case sensitive.
{{site.data.alerts.hr_shaded}}

## Can I associate objects of different projects?

Yes, you can associate an object (for example from document to subversion commit) in one project to an object in another project if you have access or are a Site Admin.

You must have permission to view the object that you're associating with before you can associate with that object, unless you are a Site Admin.
{{site.data.alerts.hr_shaded}}

{% include links.html %}