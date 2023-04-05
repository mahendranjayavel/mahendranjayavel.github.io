---
title: pebble-app.xml 
keywords: authentication, pebble application configuration file
tags: [installation, upgrade, site-options.conf, config_files]
sidebar: teamforge_sidebar
permalink: pebble-app-xml.html
last_updated: Feb 27, 2018
toc: false
summary: The pebble-app.xml file, also known as the Pebble application configuration file, contains the text that the Pebble application displays in the TeamForge user interface.
---

This is an example of a default (unedited) `pebble-app.xml` file. To create your own integrated application config file, copy this one into a new file and replace the values with the values appropriate for the application you are integrating.

```shell
<?xml version="1.0" encoding="utf-8"?>
<!DOCTYPE integrated-application 
  PUBLIC "-//CollabNet, Inc.//DTD Integrated Application Descriptor 1.0//EN"
  "http://schema.open.collab.net/sfee50/dtd/sf-pluggable-application-descriptor_1_0.dtd">
<integrated-application>
    <name>Pebble Blog</name>
    <description>l10n.application.description</description>
    <permissions>
        <permission dapMappedTo="View">Blog Reader</permission>
        <permission>Blog Contributer</permission>
        <permission>Blog Publisher</permission>
        <permission>Blog Owner</permission>
    </permissions>
    <prefix>PB</prefix>
    <id-pattern></id-pattern>
    <require-per-project-prefix>true</require-per-project-prefix>
    <require-scm-integration>true</require-scm-integration>
    <is-search-supported>false</is-search-supported>
    <!-- Page components for Integrated apps is not implemented for Alpha -->
    <page-component>
      <require-page-component>true</require-page-component>
      <page-component-details>
        <inputtype>text</inputtype>
        <resultformat>html</resultformat>
        <description>l10n.pce.description</description>
        <title>l10n.pce.title</title>
      </page-component-details>
    </page-component>
    <config-parameters>
        <!-- Pebble Configuration Parameters -->
        <param>
            <title>l10n.blogname.title</title>
            <name>blogName</name>
            <description>l10n.blogname.description</description>
            <defaultvalue>My Blog</defaultvalue>
            <displaytype valuetype="String" maxlength="25">TEXT</displaytype>
            <editable>false</editable>
        </param>
        <param>
            <title>l10n.blogdescription.title</title>
            <name>blogDescription</name>
            <description>l10n.blogdescription.description</description>
            <defaultvalue>My Awesome Blog</defaultvalue>
            <displaytype valuetype="String" maxlength="40">TEXT</displaytype>
            <editable>true</editable>
        </param>
        <param>
            <title>l10n.richtexteditor.title</title>
            <name>richTextEditorEnabled</name>
            <description>l10n.richtexteditor.description</description>
            <defaultvalue>checked</defaultvalue>
            <displaytype valuetype="String">CHECKBOX</displaytype>
            <editable>true</editable>
        </param>
        <param>
            <title>l10n.noofrecentblogentries.title</title>
            <name>recentBlogEntries</name>
            <description>l10n.noofrecentblogentries.description</description>
            <defaultvalue>3</defaultvalue>
            <displaytype valuetype="String">SELECT</displaytype>
            <option name="3">l10n.three.value</option>
            <option name="5">l10n.five.value</option>
            <option name="7">l10n.seven.value</option>
            <option name="9">l10n.nine.value</option>
            <editable>true</editable>
        </param>
    </config-parameters>
    <bundles> 
      <bundle locale="en">
        <key name="l10n.application.description">Pebble Blog App</key>
        <key name="l10n.pce.description">Display Blog Title for Given Date.</key>
        <key name="l10n.pce.title">Enter Blog Date (in yyyy-mm-dd)</key>
        <key name="l10n.blogname.title">Blog Name</key>
        <key name="l10n.blogname.description">Please provide a name for the Blog. This appears on all blog pages</key>
        <key name="l10n.blogdescription.title">Blog Description</key>
        <key name="l10n.blogdescription.description">Please provide a description for the Blog. This appears below blog name on all pages</key>
        <key name="l10n.richtexteditor.title">Rich Text Editor</key>
        <key name="l10n.richtexteditor.description">Enable Rich Text Editor for comments and Blog entries?</key>
        <key name="l10n.noofrecentblogentries.title">Recent Blog Entries</key>
        <key name="l10n.noofrecentblogentries.description">How many recent blog entries do you want to see in the home page?</key>
        <key name="l10n.three.value">3</key>
        <key name="l10n.five.value">5</key>
        <key name="l10n.seven.value">7</key>
        <key name="l10n.nine.value">9</key>
      </bundle>
    </bundles>
</integrated-application>
````

{% include links.html %}