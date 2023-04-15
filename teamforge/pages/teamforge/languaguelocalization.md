---
title: Internationalize Your Integrated Application
keywords: teamforge, extend, api
tags: [extend_teamforge]
sidebar: teamforge_sidebar
folder: teamforge
permalink: languagelocalization.html
last_updated: March 1, 2018
search: exclude
summary: You can configure your integrated application to display languages based on the TeamForge site user's browser locale.
---

These parameters can be internationalized:

 * The description of the integrated application.

 * The title and description of the integrated application when it appears as a component on a project page.

 * The name and description of any configuration parameter.

 1. In the [XML application configuration file][externalapplicationsforprojects.html#describeintegratedapp], select the values for which you want to provide localized content.

 2. Inside the `bundles` tag, create a `bundle` tag identical to the default English bundle tag. (Keep the `en` bundle.)

 3. Change the value of the `locale` attribute of the new `bundle` tag to the language you are going to provide. The value for each of the internationalized tags must start with `l10n`.

    For example:

    ```shell
    <bundles>
          <bundle locale="en">
            <key name="l10n.application.description">My Test App</key>
            <key name="l10n.blogname.title">Blog Name</key>
            <key name="l10n.blogname.description">Please provide a name for the Blog. This appears on all blog pages</key>
                ........
          </bundle>
          <bundle locale="ja">    <!-- Japanese Language Translations -->
            <key name="l10n.application.description">My Test App</key>
            <key name="l10n.blogname.title">Blog Name</key>
            <key name="l10n.blogname.description">Please provide a name for the Blog. This appears on all blog pages</key>
                ........
          </bundle>
    </bundles>
   ````  

 4. Save the application configuration file.


{% include links.html %}