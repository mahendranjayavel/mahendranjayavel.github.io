---
title: FAQs on Documents 
keywords: FAQ, frequently asked questions
tags: [faq, documents]
sidebar: teamforge_sidebar
permalink: documents-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on Documents.
---

## How does TeamForge support Documents?

A key element in a successful product development project is ensuring that stakeholders from all functional groups are involved in an alterative document review and approval process, particularly for critical documents, such as Product Requirements Documents.

It is also critical that any changes to key documents are recorded and the new information quickly communicated to everyone concerned.

The TeamForge Document Manager helps you manage your documents throughout their lifecycle and ensure the appropriate level of involvement of other project members. In addition to storing documents for reference purposes, the Document Manager provides a document review workflow process to allow you to actively engage other users in the review and approval of a document.

### Simple Notification Process

If you would like to keep other TeamForge users informed when the status of a document, such as when a document is posted or updated, or there is a change in the conents or status of an existing document, but do not require a formal review and approval process, the following steps provide a best practice for this level of document management.

  * Post the document to the Document Manager in the desired location. If you would like to prevent other users from editing, moving, or deleting the document, use the 'Lock Document' feature. (If you choose not to lock the document), any user with the document edit permission can edit and update the document.)
  * Notify other users that the document is available and request that they begin monitoring it. All users monitoring an item receive email notification whenever the item is updated.

### Document Workflow Review and Approval

In cases where more formal document review is desired, the TeamForge Document Manager provides an easy-to-use workflow process for managing a document's review and approval.

After submitting a document, you can start a document review. You are prompted to provide the following information:

  * The names of all required and optional reviewers (All reviewers must have permission to access the document.)
  * The date by which the review must be completed.
  * Email message text.

You will be notified each time a reviewer submits review comments.

When selected to review a document, users receive an email notification with the relevant details and a link to the document.

You can also choose to attach the document to the email notification. An item also appears in the **Documents Awaiting Review** section of each reviewer's **My Page**, including the due date.

A **Submit a Response** section is provided within the Document Manager where reviewers can enter their review comments. Reviewers should be instructed to include "I approve this document" or similar text in the **Submit a Response" section to indicate that they have approved the document. 

All reviewers and the document submitter will be able to read the reviews of all other reviewers once they have been submitted.
{{site.data.alerts.hr_shaded}}

## Why can't I edit a document when it opens in my browser?

There are chances that your browser swallowed the running application.

If you click on a document in TeamForge (for example, a Word doc), and it opens in your browser instead of launching a separate MS Word window, chances are you will not be able to edit this document. This is because your browser has either called one of the MS document viewers that do not have native edit capabilities, or the browser has 'swallowed' the running MS Word process and the document has written to your %TEMP% directory as a read-only file.

You can either choose to download the file to your desktop and then click on it to edit, or configure your browser to not swallow the application (this is described in various MS KB articles).
{{site.data.alerts.hr_shaded}}

## How can a user who deleted a document get it back?

It is possible to recover the latest version of a document if someone has accidentally deleted it from TeamForge.

However, note that you can recover the raw document but not undelete it from the app. The user will have to add the document back into TeamForge, and the history of the document will not be recovered. If you need a true undelete so that the history is available, please contact Technical Support and ask for us to schedule our Professional Services group for you.

Let's assume you have a project in TeamForge called Test, and the URL in your browser when you load this project is: http://your_sfee_server/sf/projects/Test. Please note the word after projects, this is your project name.

Now, let's assume the file to be retrieved was in a folder called 'foo' in the document manager. Further, let's assume the document was called 'example'. On the database, run the following command:

```shell
select stored_file.raw_file_id, document.id, item date_last_modified, item.title,
    stored_file.file_name, sfuser.full_name from item, folder, document, document_version,
    stored_file, sfuser where item.title like '%example%' and item.folder_id = folder.id and
    folder.path = 'docman.root.b' and document.id = document_version.document_id and
    document_version.stored_file_id = stored_file.id and item.is_deleted = 't' and
    item.last_modified_by_id = sfuser.id ;  
````

This will return something like:

```shell
raw_file_id | id | date_last_modified | title | file_name | full_name
````

Examine the rows of output to determine which of the returned results is the document you need, from the title and the name of the file that was uploaded. Once you've determined this, look for the file in `/opt/collabnet/teamforge/var/deleted_files`.

 ```shell
 yujr0C98B989011083DBFF4F534F | doc1001 | 2007-04-11 08:49:19-07 | example |
   foo.txt | Joe User bxma0C98B98901115B9CE99E82C2 | doc1002 | 2007-04-11 08:49:19-07 |
   example | test.txt | Joe User rpyf0C98B98901116DD1E40F9F8B | doc1003 | 2007-04-11
   08:49:19-07 | example | findme.txt | Joe User ltrq0C98B9890111D76E74920A0E | doc1004
   | 2007-04-11 08:49:19-07 | example | project_logo.jpg | Joe User 
 ````

Let's say the fourth document above was the one you wanted. You can find it at: 
`/opt/collabnet/teamforge/var/deleted_files/l/lt/ltr/ltrq/ltrq0C98B9890111D76E74920A0E`. Simply copy that file off the system, rename it to `project_logo.jpg` and return it to the user.
{{site.data.alerts.hr_shaded}}

## Why can't I edit a document when it opens in my browser?

There are chances that your browser swallowed the running application.

If you click on a document in TeamForge (for example, a Word doc), and it opens in your browser instead of launching a separate MS Word window, chances are you will not be able to edit this document. This is because your browser has either called one of the MS document viewers that do not have native edit capabilities, or the browser has 'swallowed' the running MS Word process and the document has written to your %TEMP% directory as a read-only file.

You can either choose to download the file to your desktop and then click on it to edit, or configure your browser to not swallow the application (this is described in various MS KB articles).
{{site.data.alerts.hr_shaded}}

## Why are some uploaded documents missing icons when displayed in TeamForge?

TeamForge has a small internal mapping of which icon is associated with which mimetype(s). This mapping is necessarily small, as a complete mapping would be exceedingly large, and almost always out of date.

You can examine the mimetype that TeamForge is receiving by examining the document's attributes using our SOAP API. You can also override this mimetype info via the API by uploading a new version of the document (which can be the exact same document contents). There is sometimes a generic icon for documents from certain applications. TeamForge accepts and stores the mimetype that the user's browser sends on the HTTP upload of the original document. As an example, let's examine the MS Word document. Some browsers will send strings like `application/vnd.ms-word`; others will send `application/msword` and others will send something completely different.
{{site.data.alerts.hr_shaded}}

## Can I link to documents outside of TeamForge?

TeamForge has the concept of a 'url doc' to support this very usage.

When creating a document in TeamForge, simply choose this type from the Create screen and then enter the URL that references the document in the existing external system. This will create a 'placeholder' document in TeamForge that can be associated to, reviewed, and so on as if it were a normal document, while maintaining the document's actual contents in the external application.
{{site.data.alerts.hr_shaded}}

## Can I lock a document in TeamForge?

Absolutely, yes. You can specify a document as locked at any point in time (document create, document edit, etc).

You can do this through the UI or through the SOAP API. Simply check relevant boxes available in the **LOCK DOCUMENT** section on the **Document Details** page.

By default, edit and download locks are disabled for a document. To lock and unlock your document, you must have the Document Edit permission in addition to the Document Create permission. To prevent others from editing or downloading a document, you can choose the edit lock or the download lock as required. Selecting the edit lock automatically enables the Document Administrator to edit the document and allows you to select the download lock option.

To edit or download a locked document, the user must have the Document Edit permission. The user who has locked the document can edit or download it at any point in time. A Document Administrator that has the option, **Allow Document Admin to edit** enabled in the **LOCK DOCUMENT** section or a Site Admin can also edit or download a locked document.
{{site.data.alerts.hr_shaded}}

## Does TeamForge automatically resolve conflicts in documents made by multiple concurrent editors?

If you store your documents in Subversion or some other SCM tool, then that tool will handle conflict resolution per its normal means.

However, if you are using the Document Manager component of TeamForge, then there is no automated means within the product to prevent another user from uploading a newer version of a given document that does not contain the changes you just uploaded. To prevent this, we recommend you use the edit lock and download lock features of TeamForge to prevent others from editing and downloading a document you are currently editing.
{{site.data.alerts.hr_shaded}}

## What document types are supported in TeamForge?

TeamForge supports all known and unknown document types.

In fact, TeamForge makes absolutely no distinction on a file type when uploading a document. This means that you can even upload binary files (like a Zip archive) into the document manager. Note that while the TeamForge accepts any incoming data stream as a document, it does use the mimetype sent by the browser to determine if it has the proper icon to display for the document.
{{site.data.alerts.hr_shaded}}

## Why doesn't an open review automatically close when a new version of the document is uploaded?

TeamForge does not automatically close a document review under any circumstances (new document version, review due date passes, and so on).

This was a conscious decision on our part in which it was decided that TeamForge cannot always be aware of the business rules or personnel availability at a customer. For example, TeamForge cannot know that the one person whose document review input is most needed is on vacation for the four days the document was under review. If TeamForge were to close the review, then it would disappear from the user's **My Page**. Additionally, TeamForge cannot know that a new version of a document supersedes the prior versions (or that it does not supersede it). You may be uploading a 'draft' or 'work-in-progress' of the new version as document review feedback is received and if TeamForge were to close the review at this point, you might have received feedback from less than one percent of the reviewers.
{{site.data.alerts.hr_shaded}}

## Who can work with documents?

Any project member with the Document Edit permission can edit a document.
{{site.data.alerts.hr_shaded}}

## Can I set permissions so that users can move documents but not delete them?

You cannot configure document management permissions so that a user can move documents but not delete them.

It is not possible to separate move and delete permissions, because a move is actually a copy/delete action. The document is not really moved, it is copied to the new location and then deleted from the original location.
{{site.data.alerts.hr_shaded}}

## Why am I not able to access a folder in TeamForge documents?

You can access a folder in TeamForge documents only if you have permission for the folder or any of its parent folders.

For TeamForge documents, users having permissions to the parent folder can access all the subfolders. Users having permissions to a subfolder can only view the hierarchy of the parent folders; they cannot access the documents in those folders.
{{site.data.alerts.hr_shaded}}

## Are role-based permissions allowed for subfolders in the TeamForge Documents?

Yes. It is allowed in TeamForge Documents.

The Project Administrator can give permission to access sub folders in the TeamForge Documents based on the user roles, using the Roles option.
{{site.data.alerts.hr_shaded}}

## Can I set permissions for documents alone?

Yes, as a project administrator, you can set individual permissions only for documents.

The Document Admin permission allows a project member to create, edit and administer both documents and document folders. Though this does not include the delete permission, individual permissions to create, edit, and delete can be set separately for document folders and documents on the Documents Permissions page (**Project Admin > Permissions > Edit Role > Documents**). This is to restrict a project member from handling document folders or subfolders. For example, if you do not want a project member to create a document folder, but only create a document within a specific folder, you can set the 'Create/View' permission for documents alone. The available permissions are:

 * Create/View
 * Edit/View
 * Delete/View
 * View Only
{{site.data.alerts.hr_shaded}}

## Why can't I reply when someone comments on my review?

By default, TeamForge doesn't add the review initiator to a review, which would be needed to facilitate this.

To work around this, simply add yourself as an optional reviewer when creating the review. Alternatively, some customers have chosen to create a forum in TeamForge, and then include the forum's posting address in the review notes.
{{site.data.alerts.hr_shaded}}


{% include links.html %}