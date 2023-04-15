---
title: FAQs on Customization
keywords: FAQ, frequently asked questions
tags: [faq, customize]
sidebar: teamforge_sidebar
permalink: customization-faqs.html
last_updated: Apr 3, 2018
summary: These are some of the frequently asked questions on customizing the TeamForge site.
---

## What elements of a site can I customize?

You can customize the site home page and the default home page of every project on the site. You can also customize the menu bars, headers and footers of any page.

For more information about branding, see: [Customize anything on your site][customize.html#customizeanything].
{{site.data.alerts.hr_shaded}}

## How does TeamForge use stylesheets?

The look and feel of much of TeamForge is controlled by cascading style sheets (CSS).

All default CSS styles can be customized to alter the look of the application. You can customize fonts (color, size, font face, etc.), links, backgrounds, headings, tables, tabs, and anything else that CSS can control.

The default TeamForge CSS file is `css/styles_new.css`.

New CSS files can be added to the css/ directory and reference them via `templates/body_header.vm`.

 {% include tip.html content="If you override an existing CSS file, it will be used instead of the default CSS file. So you must be sure to include all the default styles in your customized file. A best practice is to add any new or overridden styles to the bottom of the CSS file so that they can be easily identified." %}
{{site.data.alerts.hr_shaded}}

## Can I substitute my own images for the default TeamForge images?

Every image in TeamForge can be edited or replaced by a new image file.

Images are stored in an `images` directory in the branding repository.

 {% include note.html content="The default TeamForge image files are included in both the Quick Start and Advanced branding zip file." %}

**Examples**

 * To replace the masthead graphic, replace the image file `images/masthead/logo.gif`.
 * To replace the folder graphic, replace the image file `images/my/all_projects.gif`.
{{site.data.alerts.hr_shaded}}

## Can I use my own custom JavaScript on my site?

The JavaScript scripts used in TeamForge can be customized.

Existing JavaScript scripts are located in the js/ directory in the branding repository.

New scripts can be checked into the `js/` directory and then referenced from Velocity templates.
{{site.data.alerts.hr_shaded}}

## Can I customize the web interface?

You can customize the way the web interface looks and functions through the use of Velocity templates.

 {% include note.html content=" Even though Velocity as a technology is supported by CollabNet, Inc., the customizations themselves are not supported. Any future upgrade of TeamForge may, in fact, break your customization. Furthermore, making these types of changes to your installation is considered a customization and will impede our ability to support you. Should you experience issues and open a ticket with Technical Support, you may be asked to remove these customization to debug your issue." %}

{% include links.html %}