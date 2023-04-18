---
title: Wiki Syntax
keywords: wiki syntax, syntax of the wiki
tags: [project_member_tasks, wiki]
sidebar: teamforge_sidebar
last_updated: Mar 21, 2018
permalink: wiki-wikisyntax.html
summary: You can use special wiki text markup to do a wide variety of cool and useful things on TeamForge wiki pages.
---

For a quick introduction, see the [documentation for JSPwiki](http://www.ecyrd.com/JSPWiki/wiki/TextFormattingRules), which is the wiki engine that drives the TeamForge wiki tool.

## Text Effects on Wiki Pages

Wiki markup is great for making text look the way you need it to look.

 {% include note.html content="These tools are for use only when you are editing a wiki page in text mode. If you try to use them in WYSIWYG mode, they are displayed just the way you typed them in, which is not what you want." %}


| Syntax | Effect | Details |
|--------|--------|---------|
| - - - - | Creates a horizontal rule. | |
| `\\` | Creates a line break. | |
| !!!text | Creates a level 1 (large) header. | |
| !!text | Creates a level 2 (medium) header. | |
| !text | Creates a level 3 (small) header. | |
| ' 'text' ' | Creates italic text. (That's two single quotes on each side.) | |
| \_\_text\_\_ | Creates bold text. (That's two underscores on each side.) | |
| \{\{text\}\} | Creates monospaced text. | |
| *text | Creates a bulleted list item. | |
| #text | Creates a numbered list item. | |
| ;term:ex | Creates a definition for the word "term'"with the explanation "ex." | |
| \{\{\{text\}\}\} | Creates pre-formatted text. | |
| %%(\<css-style\>)\<your text\>%% | Defines a CSS style command. |%%(font-size: 150%; color: red;) Hello, world!%% |
| Blank line | Starts a new paragraph.| |

## Bring TeamForge Data into Wiki Pages

Use this markup format to bring in data from elsewhere on your TeamForge site.

 {% include note.html content="These are for use only when you are editing a wiki page in text mode. If you try to use them in WYSIWYG mode, they are displayed just the way you typed them in, which is not what you want." %}

<table>
<tr>
<th>Syntax</th>
<th>Effect</th>
<th>Details</th>
</tr>
<tr>
<td>[{INSERT ExcelToHTMLPlugin src='c:\somesheet.xls'}] or [{INSERT ExcelToHTMLPlugin border='1' src='\\the_server\somesheet.xls'}]</td>
<td>Reads a Microsoft Excel file and displays it as an HTML table.</td>
<td>Parameters:
<ul>
<li> src: URL / Attachment file name</li>
<li>srcsheet: Sheet name</li>
<li>height: height attribute for the html table</li>
<li> width: width attribute for the html table</li>
<li>border: border attribute for the html table</li>
</ul>
More at http://www.ecyrd.com/JSPWiki/wiki/ExcelToHTMLPlugin
</td>
</tr>
</table>


## Text Navigation Tools for Wiki Pages

You can use wiki syntax to help readers get around.

 {% include note.html content="To use these tools, copy and paste the sample syntax into your Wiki page in \"Plain Editor\" mode, then customize it appropriately." %}

<table>
<tr>
<th>Syntax</th>
<th>Effect</th>
<th>Details</th>
</tr>
<tr>
<td>%%insert-toc%%</td>
<td>Creates a table of contents consisting of the header text on the page.</td>
<td></td>
</tr>
<tr>
<td>[link]</td>
<td>Creates a link to a new Wiki page called "link."</td>
<td>If the link is a complete URL, a link to the URL is created. If the link points to a .gif, .jpg, or .png image, the image is rendered directly in the page.</td>
</tr>
<tr>
<td>[title|link]</td>
<td>Creates a link to a new Wiki page called "link" with the text "title" displayed for the URL.</td>
<td>If the link is a complete URL, a link to the URL is created. If the link points to a .gif, .jpg, or .png image, the image is rendered directly on the page with "title" as ALT text.</td>
</tr>
<tr>
<td>~TestText</td>
<td>Disables link creation for a CamelCase word.</td>
<td>CamelCase words are two or more uppercase words with no spaces. By default, a CamelCase word automatically creates a link to a new Wiki page.</td>
</tr>
<tr>
<td>[[link]</td>
<td>Creates the text "[link]."</td>
<td></td>
</tr>
<tr>
<td>[{IFramePlugin url='http://open.collab.net/' width='100%' height='500' border='1' scrolling='yes' align='center'}]</td>
<td>Embeds an iframe into a wiki page.</td>
<td>
<ul>
<li>attachment: Attachment path, e.g. 'IFramePlugin.jar(info)'</li>
<li>url: A URL, e.g 'http://www.google.com'</li>
<li>align: Align the iFrame to left/center/right</li>
<li>border: Whether there is a border or not</li>
<li>width: Width of the iFrame</li>
<li>height: Height of the iFrame</li>
<li>marginwidth: Margin width of the iFrame</li>
<li>marginheight: Margin height of the iFrame</li>
<li>scrolling: Whether the iFrame can be scrolled or not</li>
</ul>
See http://www.ecyrd.com/JSPWiki/wiki/iFramePlugin
</td>
</tr>
<tr>
<td>Tab Completion <Keyword+Tab></td>
<td>You can type a keyword and hit the Tab key (under the Tab Completion mode). The editor will fill in with a sample template for the specific markup represented by the keyword.</td>
<td>
<ul>
<li>link:Inserts a sample link.</li>
<li>h1:Inserts level 1 heading sample.</li>
<li>h2:Inserts level 2 heading sample.</li>
<li>h3:Inserts level 3 heading sample.</li>
<li>bold:Inserts a bold text sample.</li>
<li>italic:Inserts an italics text sample.</li>
<li>mono:Inserts a mono text sample.</li>
<li>mono:Inserts a mono text sample.</li>
<li>sup:Inserts a superscript sample.</li>
<li>sub:Inserts a subscript sample.</li>
<li>strike:Inserts a strike through text sample.</li>
<li>br:Inserts a line break.</li>
<li>hr:Inserts a horizontal line.</li>
<li>pre:Inserts a pre-formatted text sample.</li>
<li>code:Inserts a code block sample.</li>
<li>dl:Inserts a definition list block sample.</li>
<li>toc:Inserts the Table of Contents plugin syntax.</li>
<li>tab:Inserts a sample tabbed section block syntax.</li>
<li>table:Inserts a sample table syntax.</li>
<li>img:Inserts a sample image plugin syntax.</li>
<li>quote:Inserts a sample quoted text block.</li>
<li>sign:Inserts the user's signature.</li>
</ul>
</td>
</tr>
</table>

## Attachments for Wiki Pages

You can use wiki markup to bring in information from external sources.

 {% include note.html content="These tools are for use only when you are editing a wiki page in text mode. If you try to use them in WYSIWYG mode, they are displayed just the way you typed them in, which is not what you want." %}

<table>
<tr>
<th>Syntax</th>
<th>Effect</th>
<th>Details</th>
</tr>
<tr>
<td>[WikiPageName/attachmentName]</td>
<td>Embeds an attachment in the page.</td>
<td>If the attachment is a .gif, .jpg, or .png image file, the attachment will be embedded in the page; otherwise, the name of the attachment will display as a downloadable link. After adding attachments, the exact syntax for including the current page's attachments is shown next to each attachment's name in the Attachments section of the Edit Wiki page. You can use the same syntax to embed attachments from other wiki pages in the same project.</td>
</tr>
<tr>
<td>[{InsertAttachment page='WikiPage/attachment'}]</td>
<td>
Inserts the contents of an attachment (text file) into a page.	 </td>
<td markdown="1">
If the attachment is a text file, the content of the text file is inserted into the page. For more information, click [here](https://www.ecyrd.com/JSPWiki/wiki/InsertAttachment).
<ul>
<li>This markup is for inserting content of a text file.</li>
<li>Files with the following extensions are allowed as attachment: .txt, .html, .xml, .cpp and .java.</li>
<li>In addition to image files, inserting files with the following extensions is not supported by this markup: .doc, .xls, .pdf, .zip, .jar.</li>
</ul>
</td>
</tr>
<tr>
<td>[{Mediaplayer src='fileName.wmv'}]</td>
<td>Embeds a Windows Media Player or Quicktime Player on a wiki page.</td>
<td>
<ul>
<li>src: Media URL / Attachment file name</li>
<li>playertype: "mediaplayer" / "quicktime"</li>
<li>width, height: Dimension of the embedded media displayed</li>
<li>movieheight, moviewidth: Dimension of the display screen</li>
<li>caption: Caption to be displayed below the media player</li>
<li>control: Displays Control bar. mediaplayer: 1 (Show) / 0 (Hide); quicktime: true (Show) / false (Hide)</li>
<li>autostart: Play automatically. mediaplayer: 1 (Auto) / 0 (Manual, Click to play); quicktime: true (Auto) / false (Manual, Click to play)</li>
<li>autorewind: Automatically rewinds when play ends. mediaplayer: 1 (Auto Rewind) / 0 (Play once); quicktime: true (Auto Rewind) / false (Play once)</li>
<li>playcount: Number of times the movie will play. 0 represents always play.</li>
</ul>
See http://www.ecyrd.com/JSPWiki/wiki/MediaPlayerPlugin
</td>
</tr>
<tr>
<td>[{INSERT ExcelToHTMLPlugin src='WikiPage\somesheet.xls'}] or [{INSERT ExcelToHTMLPlugin border='1' 
src='\\the_server\somesheet.xls'}]</td>
<td>Reads a Microsoft Excel file and displays it as an HTML table.</td>
<td>Parameters:
<ul>
<li>src: URL / Attachment file name</li>
<li>srcsheet: Sheet name</li>
<li>height: height attribute for the html table</li>
<li>width: width attribute for the html table</li>
</ul>
More at http://www.ecyrd.com/JSPWiki/wiki/ExcelToHTMLPlugin
</td>
</tr>
<tr>
<td>[{arnaud.Flash src='yourAttachedFlash.swf'}]</td>
<td>Embeds a Flash Player on your wiki page.</td>
<td>
<ul>
<li>width='n'</li>
<li>height='n'</li>
<li>controls='true|false'</li>
<li>play='true|false'</li>
<li>loop='true|false'</li>
<li>parameters='param1=value1, &param2=value2'</li>
</ul>
See http://www.ecyrd.com/JSPWiki/wiki/AFlashPlugin
</td>
</tr>
<tr>
<td>[{IFramePlugin url='http://open.collab.net/' width='100%' height='500' border='1' scrolling='yes' 
align='center'}]</td>
<td>Embeds an iframe into a wiki page.</td>
<td>
<ul>
<li>attachment: Attachment path, e.g. 'IFramePlugin.jar(info)'</li>
<li>url: A URL, e.g 'http://www.google.com'</li>
<li>align: Align the iFrame to left/center/right</li>
<li>border: Whether there is a border or not</li>
<li>width: Width of the iFrame</li>
<li>height: Height of the iFrame</li>
<li>marginwidth: Margin width of the iFrame</li>
<li>marginheight: Margin height of the iFrame</li>
<li>scrolling: Whether the iFrame can be scrolled or not</li>
</ul>
See http://www.ecyrd.com/JSPWiki/wiki/iFramePlugin
</td>
</tr>
</table>

## Tables on Wiki Pages

You can use wiki markup to organize information in tables on a wiki page.

 {% include note.html content="These tools are for use only when you are editing a wiki page in text mode. If you try to use them in WYSIWYG mode, they are displayed just the way you typed them in, which is not what you want." %}

<table>
<tr>
<th>Syntax</th>
<th>Effect</th>
<th>Details</th>
</tr>
<tr>
<td markdown="1">
[{Table \<table-parameters\> || Table Header Example || More... | Table Data Example | More... }]
</td>
<td>Inserts a table on the wiki page. See this page for the markup for table elements.</td>
<td>
<ul>
<li markdown="1">
<b>rowNumber</b>: <i>\<integer\></i> - Row number starts counting at this value; default = 0 (used in conjunction with '#' syntax)
</li>
<li markdown="1">
<b>style</b>: <i>\<css-style\></i> Add formatting to the table, e.g. style:'border=2px solid black;'
</li>
<li markdown="1">
<b>dataStyle</b>: <i>\<css-style\></i> Format all data cells (prefixed by single pipe signs '|')
</li>
<li markdown="1">
<b>headerStyle</b>: <i>\<css-style\></i> Format all header cells (prefixed by double pipe signs '||')
</li>
<li markdown="1">
<b>evenRowStyle</b>: <i>\<css-style\></i> Format the even rows, e.g. evenRowStyle='background: #ffff00;'
</li>
<li markdown="1">
<b>oddRowStyle</b>: <i>\<css-style\></i> Format the odd rows, e.g. oddRowStyle='color: red;'
</li>
</ul>
</td>
</tr>
<tr>
<td>||head1||head2</td>
<td>Creates a table column with header text "head1" in the first cell and "head2" in the second cell.</td>
<td></td>
</tr>
<tr>
<td>|col1|col2</td>
<td>Creates a table row containing the text "col1" in the first cell and "col2" in the second cell.</td>
<td></td>
</tr>
<tr>
<td>|<</td>
<td>Collapses a cell with the previous cell so it spans multiple columns.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td>||<</td>
<td>Collapses a header cell with the previous header cell so it spans multiple columns.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td>|^</td>
<td>Collapses a cell with the cell above so that it spans multiple rows.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td>||^</td>
<td>Collapses a header cell with the header cell above so that it spans multiple rows.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td markdown="1">
( \<css-style\> )
</td>
<td>Inside a table cell, adds specific formatting to a cell.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td>#</td>
<td>Inside a table cell, displays the current row number with auto row numbering.</td>
<td>http://www.ecyrd.com/JSPWiki/wiki/TablePlugin</td>
</tr>
<tr>
<td>[{INSERT ExcelToHTMLPlugin src='WikiPage\somesheet.xls'}] or [{INSERT ExcelToHTMLPlugin border='1' 
src='\\the_server\somesheet.xls'}]</td>
<td>Reads a Microsoft Excel file that is attached to a wiki page, and displays it as an HTML table.</td>
<td>Parameters:
<ul>
<li>src: If the Excel file is attached to the current wiki page, this is the attachment file name. If it is attached to some other wiki page, this is the URL of the attachment.</li>
<li>srcsheet: Sheet name</li>
<li>height: height attribute for the html table</li>
<li>width: width attribute for the html table</li>
<li>border: border attribute for the html table</li>
<li>cellpadding: cellpadding attribute for the html table</li>
<li>cellspacing: cellspacing attribute for the html table</li>
<li>background: background attribute for the html table. Attachment file name is accepted as value</li>
<li>backgroundcolor: backgroundcolor attribute for the html table</li>
<li markdown="1">keepformat: Formating specified in the excel sheet is applied for the html table. 
{% include note.html content="The complete formating from excel sheet is not applied to the html table, for example, font, font size, etc are not applied and background color, foreground color, etc are applied. yes/no is accepted as value" %}</li>
<li>headercolor: Foreground color for the header (eg: #dcdcdc)</li>
<li>headerbackgroundcolor: Background color for the header (eg: #adadad)</li>
<li>evenrowcolor: Foreground color for the even rows (eg: #adadad)</li>
<li>evenrowbackgroundcolor: Background color for the even rows (eg: #adadad)</li>
<li>oddrowcolor: Foreground color for the odd rows (eg: #adadad)</li>
<li>oddrowbackgroundcolor: Background color for the odd rows (eg: #adadad)</li>
<li>tableclass: Style class name for the HTML table</li>
<li>headerclass: Style class name for header</li>
<li>evenrowclass: Style class name for the even rows</li>
<li>oddrowclass: Style class name for the even rows</li>
<li>stylesheet: Stylesheet for the table. Attachment file name is accepted as value</li>
</ul>
See href="http://www.ecyrd.com/JSPWiki/wiki/ExcelToHTMLPlugin"
</td>
</tr>
<tr>
<td>[{TableOfContents }]\\</td>
<td>Creates a table of contents consisting of the header text on the page.</td>
<td></td>
</tr>
</table>

## Wiki Plugins

You can use pre-defined wiki plugins to format your current page.

<table>
<tr>
<th>Plugin Name</th>
<th>Details</th>
</tr>
<tr>
<td>Section Headings Template</td>	
<td>Inserts a page template that includes a table of contents and several section headings. Typically, this can be used in a new or blank page.</td>
</tr>
<tr>
<td>Sortable Table</td>
<td>Inserts a new table that can be sorted when you click on the column headers.</td>
</tr>
<tr>
<td>Zebra Table</td>
<td>Inserts a new table that has alternating background colors for each row.</td>
</tr>
<tr>
<td>Table of Contents Plugin</td>
<td>This plugin automatically generates table of contents that provides links to all the headings on your page.</td>
</tr>
<tr>
<td>Insert Page Plugin</td>
<td>This plugin will insert a copy of another page into the current page. You must specify the name of the page to insert.</td>
</tr>
<tr>
<td>Current Time Plugin</td>
<td>This plugin displays the current date and local time of the server when the page is viewed.</td>
</tr>
<tr>
<td>Insert Attachment</td>
<td>The insert attachment plugin allows you to insert the contents of an attachment into a page.</td>
</tr>
<tr>
<td>Media Player</td>
<td>This is an embedded player in your wiki page, supporting Windows Media Player and Apple QuickTime.</td>
</tr>
<tr>
<td>Insert Table</td>
<td>Additional table support including multi-line table editing, cell merging, and automatic row numbering.</td>
</tr>
<tr>
<td>Flash Player</td>
<td>An embedded flash player for the wiki page.</td>
</tr>
<tr>
<td>Insert Excel</td>
<td>Allows you to insert a Microsoft Excel file as a table.</td>
</tr>
<tr>
<td>Insert iFrame</td>
<td>Allows embedding attachments, external urls, and files (relative to the docbase).</td>
</tr>
<tr>
<td>Code to HTML</td>
<td>Allows source code syntax to be rendered as a HTML output and supports syntax from 130 different programming languages.</td>
</tr>
<tr>
<td>Index Plugin</td>
<td>Displays all the pages in wiki in a alphabetical order.</td>
</tr>
<tr>
<td>Recent Changes Plugin</td>
<td>Inserts the latest changes in order.</td>
</tr>
<tr>
<td>Referred Pages Plugin</td>
<td>Finds and lists all the pages that are referred to by the current page. The depth parameter allows to display a recursive tree of referred pages.</td>
</tr>
<tr>
<td>Referring Pages Plugin</td>
<td>Finds and lists all the pages that refer to the current page.</td>
</tr>
<tr>
<td>Undefined Pages Plugin</td>
<td>Lists all the pages that are referred to, but not yet created.</td>
</tr>
<tr>
<td>Unused Pages Plugin</td>
<td>Lists all the pages that are not currently referred to by any other page.</td>
</tr>
<tr>
<td>ExcelToHTMLPlugin</td>
<td>Provides a HTML view for the Excel spread sheet files.</td>
</tr>
<tr>
<td>PDFPlugin</td>
<td>Provides the PDF output for the files.</td>
</tr>
<tr>
<td>WikiContentToHTML Plugin</td>
<td>Exports a specific page to HTML.</td>
</tr>
</table>


{% include links.html %}