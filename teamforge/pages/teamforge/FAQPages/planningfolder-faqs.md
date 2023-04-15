---
title: FAQs on Planning Folder 
keywords: FAQ, frequently asked questions
tags: [faq, planning_folder]
sidebar: teamforge_sidebar
permalink: planningfolder-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on planning folders.
---

## What is a planning folder? {#whatisaplanningfolder}

A planning folder is a virtual contain that helps you organize and planning the work that goes into delivering a product. 

You can create a hierarchy of planning folders to organize artifacts by product, release, iteration, etc. You can store artifacts from multiple trackers in a planning folder. This allows you to plan various stages of your project. (i.e. releases, iterations, etc.).

Selecting an individual planning folder provides a view of all artifacts from all trackers within the selected planning folder.

The **Planned For** field identifies which product, release, or iteration the artifact is planned for, based on the planning folder that is assigned to.

For example, in an agile development environment, a project manager breaks down the prospective product into its component parts and looks at what it would like to deliver each one. When all the parts planned for a given iteration are finished, the product is considered complete for that iteration.

Some parts of a product can be developed more or less in isolcation, but most depend on other parts. Tracking these relationships is one of the trickiest aspects of product development.

For example, you can only provide a graphical user interface for a shopping cart application if you also come up with a database for the customer's payment data to be stored and accessed. That in turn requires a data storage and backup solution of some kind and so on.

Use a planning folder to tracke the dependencies among the part of your project as each moves toward completion. As you work through the question of what depends on what, you'll move artifacts representing user stories into the appropriate release. As you proceed, you'll find a pattern like this emerging:

 * Product 1
   * Release 1
     * Iteration 1
     * Iteration 2
   * Release 2
 * Product 2
 
 {% include note.html content="`Move` is meant figuratively. When you move an artifact into a planning folder, it is still a member of the tracker where it livers, and you can still do all the things with it that you can do with an ordinary tracker artifact." %}

Your planning folder lets you see at a glance the pieces of the work that support other pieces, and the pieces that depend on other pieces. Think of this as "planning tree". If you are responsible for a development project, you can use this tree view to understand and predict the time and effort required to deliver a given set of features.
{{site.data.alerts.hr_shaded}}

## What does the status of a planning folder mean?

The status of a planning folder communicates where it currently stands in the development process. You can set the status of a planning folder to values you define yourself.

The status of a planning folder can help project members make sense of what can be a complex development process. For example, consider these scenarios:

### Drop everything!

Just when you have prepared a planning folder and are ready to kick off a sprint, the product owner gets word of a more pressing set of features and asks you to postpone this work and get right to the newly revealed priority. You are worried that your project's momentum lead project members to keep picking up tasks in this planning folder instead of switching to the new work.

Create a status called 'On hold', and specify it as an 'Inactive' status. When you give the planning folder your new 'On hold' status, project members whose view shows only active folders would not see this one in their planning folder list.

### It's a wrap

Your sprint has just concluded. You don't want any further development work to happen in this planning folder, but you do want team members and others to be able to peruse it for insight into what went right and what went wrong.

Create a status called 'Restrospective', and specify it as an 'Active' status. When you assign this status to your planning folder, participants will be able to confirm that the sprint in question is finished and their comments are invited.

### Status tips

* It is a good idea to choose a default status, such as 'Under construction', so that project members are not confused when new planning folders appear.
* You can organize your planning folder statuses in a way that makes sense for your team, such as alphabetically or chronologically.
* Delete statuses that are no longer being used, so you do not clutter up the section.
* When you delete a status that is in use by one or more planning folders, the status of those planning folders is changed to 'None'. Planning folders that were created in an earlier TeamForge version also get a 'None' status at first.


{% include links.html %}