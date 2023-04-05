---
title: Upload Build to Project Build Library (PBL)
keywords: upload files
tags: [project_admin_tasks]
sidebar: teamforge_sidebar
folder: teamforge
permalink: uploadbuild.html
last_updated: Feb 7, 2018
summary: To get your software into users' hands, upload your build to the Project Build Library.
---

## Get the PBL Upload Client

You must download the `pbl.py` script to transfer files into the **Project Build Library**.

The PBL upload client is free, open-source, and freely modifiable and distributable.

Download the PBL upload client from http://cubit.open.collab.net/pbl/.

 {% include note.html content="The API operations are fully documented, for users who might want to develop their own PBL upload client." %}


## Upload a File

To upload a file, run the `pbl.py` upload command.

In this example, we upload a file named `Release.zip` from our local machine into the public area of the project **myproject**, in the directory `/foo/bar/baz/`.

 {% include note.html content="If any part of the requested path does not already exist, `pbl.py` creates the intermediate directories." %}

Run the `pbl.py` upload command like this, substituting the correct values for your situation.

```shell
pbl.py upload --api-user=username --api-key=713cdf90-2549-1350-80c3-2d0bcf9a1697 --api-url http://$external_host/cubit_api/1 --project=myproject -t pub -r /foo/bar/baz -d "This is the description." /home/Release.zip
````

 {% include tip.html content="Wildcards are accepted in the filename argument. If the file argument is a directory, or a wildcard which includes one or more directories, `pbl.py` recursively uploads all the subdirectories underneath the parent. All the files in the recursive upload get the same description." %}

Once this operation has completed, you can download this file from https://$external_host/myproject/pub/foo/bar/baz/Release.zip.

For other options of `pbl.py` scrip, run 

```shell
pbl.py help upload
````

## Change the Description of a File

You can change the description associated with a file or directory without changing the file itself or the md5 checksum of the file.

In this example, you have already authenticated and saved your user name and key credentials in your home directory.

Run the `pbl.py changedesc` command like this:

```shell
pbl.py changedesc -l http://$external_host/cubit_api/1 --project=myproject -t pub -r /foo/bar/baz/Release.zip -d "This is the new description"
````

## Move a File

With the `pbl.py move` command, you can move files or directories within a project, or even between projects.

The syntax for this command is a bit different than the rest of the commands, because the other commands only operate on one project or file or directory at a time, and that is not the case the the move operation.

To move a file, run the `pbl.py move` command with these options. In the simplest case, we move a file, or a directory and all its contents, from one name to another.

<table>
<tr>
<th>Commands</th>
<th>Description</th>
</tr>
<tr>
<td>
<b>--srcproj projname</b>
</td>
<td>
The name of the project the source file is located in.
</td>
</tr>
<tr>
<td>
<b>--destproj projname</b>
</td>
<td>
The name of the project to move the file to. If left blank, defaults to value of --srcproj.
</td>
</tr>
<tr>
<td>
<b>--srcpath path</b>
</td>
<td>
The path to the file or directory to move.
</td>
</tr>
<tr>
<td>
<b>destpath path</b>
</td>
<td>
The destination path for the file or directory specified in --srcpath. Two important things to note about this option:
<ul>
<li>If you specify a path which does not exist, that path will be automatically created for you as part of the move.</li>
<li>If the --destpath parameter ends with a slash ("/"), the destination will be assumed to be a directory. If it does not end with a slash, the destination will be assumed to be a file. An example of this behavior is below. This is approximately how the UNIX "mv" command behaves.</li>
</ul>
</td>
</tr>
<tr>
<td>
<b>--srctype {pub|priv}</b>
</td>
<td>
The visibility type of the source file, either "pub" or "priv".
</td>
</tr>
<tr>
<td>
<b>--desttype {pub|priv}</b>
</td>
<td>
The visibility type of the destination file, either "pub" or "priv".
</td>
</tr>
<tr>
<td>
<b>--force</b>
</td>
<td>
If the destination file exists, the --force option must be used to replace it.
</td>
</tr>
</table>

 {% include note.html content="Because destpath does not end with a slash -- `/foo/bar/baz/Release_old.zip` -- the last component of the path is interpreted as `a file named 'Release_old.zip'`." %}

```shell
pbl.py move -l http://$external_host/TeamForge Lab Management_api/1 --srcprj=myproject --srctype=pub --srcpath=/foo/bar/baz/Release.zip --destpath=/foo/bar/baz/Release_old.zip
````

To move a file from one project to another, and also change it from public to private, run the command like this.
 
 {% include note.html content="Because destpath ends with a slash -- `/foo/bar/baz/archive/` -- the last component of the path is interpreted as `a directory named 'archive'`." %}

```shell
pbl.py move -l http://$external_host/TeamForge Lab Management_api/1 --srcprj=myproject --destproj=myproject_archive --srctype=pub --desttype=priv --srcpath=/foo/bar/baz/Release.zip --destpath=/foo/bar/baz/archive/
````


{% include links.html %}