---
title: Set up Git—Slack Integration 
keywords: integrations, slack, git, gerrit
tags: [ctf_21.1, git_gerrit]
sidebar: teamforge_sidebar
permalink: scm-gerrit-slack-integration.html
last_updated: Jun 29, 2021
summary: You can now integrate TeamForge-Git with Slack and have notifications about certain Gerrit events posted to a Slack channel.
---

Gerrit has a plugin that lets you publish certain Gerrit events to a Slack channel. For more information, see [Gerrit's Slack Integration Plugin documentation](https://gerrit.googlesource.com/plugins/slack-integration/). 

[Install the Gerrit's Slack Integration Plugin](https://gerrit.googlesource.com/plugins/slack-integration/#installation) and do the following to publish Gerrit events to a Slack channel:

1. Create a Slack App and Webhook URL
2. Configure the Slack Integration Gerrit Plugin with the Webhook URL

Let us go through these procedures step-by-step. 

## Create a Slack App and Webhook URL

1. Log on to your [Slack account](http://my.slack.com/). Skip this step if you are logged on already.

   {% include image.html file="sign-in-1.png" %}

   {% include image.html file="sign-in-2.png" %}

   {% include image.html file="sign-in-3.png" %}

   {% include image.html file="sign-in-4.png" %}

2. [Create a Slack App](https://api.slack.com/apps/new). Skip this step if you already have an app and want to use that to integrate with Gerrit.

   {% include image.html file="app-create-1.png" %}

   {% include image.html file="app-create-2.png" %}

   {% include image.html file="app-create-3.png" %}

3. [Go to the Slack Apps List page](https://api.slack.com/apps) and click the Gerrit app.

   {% include image.html file="enable-wh-1.png" %}

4. Select **Basic Information** from the **Settings** pane on the left. Click **Add Features and Functionality** to expand the pane. 

   {% include image.html file="enable-wh-2.png" %}

5. Click **Incoming Webhooks**.

   {% include image.html file="enable-wh-3.png" %}

6. Click the **Activate Incoming Webhooks** toggle button to turn it on.

   {% include image.html file="enable-wh-4.png" %}

   {% include image.html file="enable-wh-5.png" %}

7. Click **Add New Webhook to Workspace**. 

   {% include image.html file="channel-add-1.png" %}

8. Select the Slack channel where you want your Gerrit notifications posted and click **Allow**.

   {% include image.html file="channel-add-2.png" %}

   A success message appears in your Slack channel.

   {% include image.html file="channel-add-3.png" %}

You have now configured the Webhook URL and this URL is bound to your Slack channel. Gerrit event data posted to this Webhook URL posts a message to the Slack channel.

The Webhook URL for this Slack channel and a sample CURL request to post data to the Webhook URL can be found at the bottom of the page. Keep this Webhook URL handy for later use when you in Gerrit. You can use the CURL command on your CLI to verify that the Webhook URL is indeed emptying itself on the configured Slack channel.

{% include image.html file="channel-add-4.png" %}

{% include image.html file="curl-verify-1.png" %}

{% include image.html file="curl-verify-2.png" %}


## Configure the Slack Integration Gerrit Plugin 

The Gerrit's Slack Integration Plugin is configured via a Gerrit project-specific configuration file. In other words, you must add the Slack channel's name, Webhook URL, and so on to this configuration file, which is the Gerrit project’s `project.config` file on the `refs/meta/config` branch of the project. 

Here's a sample `project.config` file.

```yaml
[plugin "slack-integration"]
  channel = gerrit-post-hackathon-test
  enabled = true
  publish-on-patch-set-created = true
  webhookurl = https://hooks.slack.com/services/T02GN6UQX/B020ZN6/vMrGO
```
This sample configuration sends notifications for Gerrit events such as `patch-set-creation`, `Removing WIP`, `Review comment add` (including `Verify` and `Code-Review votes`), `Reviewer add`, and `Review merge`.

{% include note.html content="This sample configuration sends no notification when you make a private review public." %}

{% include image.html file="gerrit-config-1.png" %}

{% include image.html file="gerrit-config-2.png" %}

Now, if you create a review in this repository, we should see a message from Gerrit in the Slack channel.

{% include image.html file="gerrit-config-3.png" %}

## Points to Consider

* `ignore`: A dotall enabled regular expression pattern—when matches against a commit message—prevents the publishing of `patchset created` event's messages.
* `ignore-wip-patch-set`: Can be set to `true` to prevent Slack notifications regarding a `work-in-progress` change.
* `ignore-comment-author`: Regular expression pattern—when matches against the comment author username—prevents the publishing of `comment added` event's messages.
* `publish-on-reviewer-added`: Set to `false` to prevent a notification when a reviewer is added to a review.
* Sometimes, it may take time for the Gerrit configuration changes to be applied to the repository. In such a case, force-refresh the repository. For example, here's a CURL request to force-refresh a repository with `reps1022` as its repository ID in TeamForge:

```
curl -k -X GET https://gerrit.collab.net/api/refresh/repositories/reps1022
```

The CURL option `-k` is added to avoid SSL error. If not CURL, just opening the above repository URL in a browser's address bar can refresh the repository. Opening the repository URL in a browser is the easiest way and if you are using Gerrit over the browser,  you can avoid the SSL error too.

{% include links.html %}