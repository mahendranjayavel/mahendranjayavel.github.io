---
title: Create Tracker Artifacts
keywords: create tracker artifacts
tags: [ctf_19.3, ctf_19.2, project_member_tasks, trackers, tracker_artifact]
sidebar: teamforge_sidebar
toc: yes
permalink: trackers-creatingatrackerartifact.html
last_updated: Jan 24, 2020
summary: You can create a tracker artifact whenever you need to report and track a bug, feature request, support request, or other type of issue. You can also create a tracker artifact without logging into TeamForge just by sending an email to the tracker.
---

{% include note.html content="For more information on Trackers, see [Set up Trackers][trackers-creatingatracker]." %}

## Create a Tracker Artifact
Individual tracker entries are referred to as tracker artifacts, or just artifacts.

1. In any tracker, planning folder or teams view, click **Create Artifact** and select the tracker in which you want to create your artifact. By default, your new artifact is created in the tracker, planning folder or team you are currently looking at.
2. Answer the questions posed by the required fields.
   {% include note.html content="Different trackers will have different combinations of fields to fill out, depending on what the tracker administrator has set up." %}
   1. Provide a **Title** and **Description** that summarize the issue or work item in a few words.
      {% include tip.html content="Descriptions help users learn how best to provide the informaiton you want from them. To maximize your chances of getting useful data, make your description as information as you can." %}  
      {% include note.html content="A new Markdown editor has been introduced for the description field. Now, you can change the format of the content of the description and make its look and feel better than ever. With this editor, you can preview your content, undo and redo the changes, set the bold and italics font styles, add a codeblock, include headers, add bulleted and numbered lists, choose to indent or outdent a paragraph, add horizontal rule and images." %}

       {% include image.html file="richtexteditor.png" %}

       TeamForge uses Showdown—a bidirectional Markdown to HTML to Markdown converter written in Javascript. For more information, see the official [Showdown Documentation](https://github.com/showdownjs/showdown/wiki). Here's an abridged version of the [Markdown syntax documentation](https://sourceforge.net/p/teamforge/wiki/markdown_syntax/).

      **Artifacts support @mentions:** Artifact description and comments now support @mentions and users called out via @mentions are added to the monitoring list. Include usernames with "@" as prefix (for example, @mphippard) to add users to the monitoring list.
        {% include note.html content="Users called out via @mentions must have _Artifact View_ permission to be added to the monitoring list." %}

   2. Now project members with CREATE/EDIT permissions can also create new tags or add existing tags, if required from **Create Artifact** page. Tags creation from **Create Artifact** page enables you to create tags on the go and overrides the limitation of creating tags only from the **Tags** page. However, you cannot rename or delete a tag from **Create Artifact** page. Click the **Add tag** button next to get the list of tags mapped to your project. You can add up to a maximum of 10 tags to any artifact and a message is displayed if your try to add more than 10 tags. If the entered tag name is not available already. a context menu **Create a new tag** shows up for you to create a new tag with the desired tag name.  
       {% include image.html file="17-4-maptags.png" %}
       {% include note.html content="Wherever the tag widget is not applicable, the associated tags are displayed as read only tags. For example in **View Artifact** page." %}
   3. For **Priority**, select a value that expresses the important or urgency of the work you are describing.
   4. Assign the artifact to a team by selecting a name from the **Team** list.
   5. If you want to assign it to a specific project member, choose a name from the **Assigned To** list. This list displays the names of all the project members, irrespective of the team you may have selected in the previous step.
      
      {% include note.html content="If you project administrator has configured the tracker to automatically assign artifacts to project members, you can skip this step." %} 

       Reassigning artifacts can now be done in no time. Use the links under the **Assigned To** field to quickly unassign the artifact to "None", and reassign the artifact to yourself or to the previous assignee. You can also click the "Re-assign" icon to search and reassign the artifact to any other user.
       {% include image.html file="assignedto1.png" %}
       {% include image.html file="assignedto2.png" %}

   6. Select the planning folder that the work belongs to from the **Planning Folder** list.

   7. For defect trackers, the **Reported in Release** field shows up. Select a file release from this drop-down list.

      A new check box, **Show Pending/Obsolete releases** added in TeamForge 19.2, if selected, lets you select one of the pending and obsolete file releases for the **Reported in Release** and **Fixed in Release** fields. 
         
      {% include image.html file="show-pending-obsolete-file-release-2.png" caption="\"Show Pending/Obsolete releases\" checkbox" %}

      Selecting this check box, lists the pending and obsolete file releases in the **Reported in Release** and **Fixed in Release** fields. The pending and obsolete file releases are greyed out to distinguish them from active file releases.

      {% include image.html file="pending-obsolete-file-releases.png" caption="Pending and Obsolete File Releases" %}

      The **Show Pending/Obsolete releases** check box becomes disabled, once you’ve selected a pending or an obsolete file release. To enable it, select an active file release or “None”.    

3. Record any other information that may be appropriate. For example, if your project is using a Scrum-based methodology, your project manager may have provided a **Points** field to track estimates of relative effort.
4. Add a file attachment, if appropriate.

   {% include note.html content="When creating or editing an artifact, you can drag and drop any number of files with their overall size not exceeding 25 MB in the Attachments field. You can also select multiple files using the Browse button. Make sure that you add only files of restricted file types. For more information on attaching restricted files types, see [New Features in TeamForge 17.8](http://help.collab.net/topic/teamforge178/releasenotes/teamforge-new.html). " %}

5. Save your changes.

{% include note.html content="From 17.8 release, TeamForge is configured to send HTML emails to users assigned to and users monitoring the artifact you create or update. For more details, see [HTML EMails][html-emails]." %}

### View Progress of File Uploads

When file attachments are uploaded while creating an artifact, a file upload progress indicator shows up on the **Create Artifact** page.

{% include image.html file="file-upload-progress-bar.png" %}

<!--artf390604 - TeamForge 19.3-->
### Attachment Reminder for Tracker Artifacts {#attachmentreminderartfs}

Have you ever forgotten to attach files when creating or updating Tracker Artifacts? If yes, the **Attach Reminder** feature comes in handy to alert you in case you've missed attaching the files while submitting an artifact. 

#### How it works?

If you've included one of the following keywords exactly in the **Description** field on the **Create Artifact** page or in the **Comment Text** field on the **View Artifact** page, the **Attachment Reminder** dialog shows up, when you try to save the changes without attaching the files.

<table>
  <tr>
    <td>attach</td>
    <td>attached are</td>
    <td>attached to this artifact</td>
    <td>attached is</td>
  </tr>
  <tr>
    <td>attached file</td>
    <td>attached files</td>
    <td>attached document</td>
    <td>attached documents</td>
  </tr>
  <tr>
    <td>are attached</td>
    <td>find attached</td>
    <td>find the attached</td>
    <td>find included</td>    
  </tr> 
  <tr>
    <td>find the included</td>
      <td>'ve attached</td>
    <td>have attached</td>
    <td>is attached</td>
  </tr>
  <tr>
    <td>I attached</td>
    <td>I'm attaching</td>
    <td>I am attaching</td>
      <td>PFA</td>
  </tr>
  <tr>
    <td>see attached</td>
    <td>see attachment</td>
    <td>see attachments</td>
    <td>see the attachment</td>
  </tr>
  <tr>
    <td>see the attached</td>
        <td>see included</td>
        <td></td>
        <td></td>        
    </tr>
</table>

Attachment Reminder, if keyword is included in the **Description** field on the **Create Artifact** page.

{% include image.html file="attachment-reminder-for-description.png" caption="Attachment Reminder alert, if keyword is included in the Description field" %}

Attachment Reminder, if keyword is included in the **Comment Text** field of the **View Artifact** page.

{% include image.html file="attachment-reminder-for-comments.png" caption="Artifact Reminder alert, if keyword is included in the Comment Text field" %}

Click **Cancel** to get back to the artifact for attaching the files. Click **OK** to submit the artifact without attaching the files.
<!--artf390604 - TeamForge 19.3-->

## Create a Tracker Artifact by Email
You do not have to be logged into TeamForge to submit a tracker artifact using email, but you must have the tracker submit permission for the tracker to which you are submitting.

Send an email message to `<tracker id>@<TeamForge server>`. 
{% include tip.html content="You can find the tracker ID on the **List Artifacts** page." %} 
{% include image.html file="17-4-trackerid.png" %}  
TeamForge maps your email to the tracker record like this:

| Email field | Tracker field |
|-------------|---------------|
| **To** | Tracker email address | 
| **Subject** | Artifact title |
| **Body** | Artifact description |
| **Attachments** | Attachments |

**Artifacts support @mentions**: Artifact description and comments now support `@mentions` and users called out via `@mentions` are added to the monitoring list. Include usernames with "@" as prefix (for example, `@mphippard`) to add users to the monitoring list.
{% include note.html content="Users called out via @mentions must have _Artifact View_ permission to be added to the monitoring list." %}

{% include links.html %}