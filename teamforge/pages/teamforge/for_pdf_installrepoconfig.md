---
title: Configure your TeamForge Installation Repository
output: pdf
keywords: 
sidebar: teamforge_sidebar
permalink: for_pdf_installrepoconfig.html
last_updated: Mar 09, 2017
search: exclude
summary: Configure your TeamForge installation repository.
---
<div markdown="1">
<h3>TeamForge installation repository configuration for sites with internet access</h3>

1. Contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) and download the TeamForge {{site.data.identifiers.teamforge}} installation repository package to `/tmp`.
2. Install the repository package.
   ```shell
   yum install -y /tmp/{{site.data.identifiers.teamforge_noarch_repo_name}}
   ````
3. Refresh your repository cache.
   ```shell
   yum clean all
   ````
<h3>TeamForge installation repository configuration for sites without internet access</h3>

1. Contact the [CollabNet Support](http://www.collab.net/support/secure-customer-login) to get the auxiliary installer package for TeamForge {{site.data.identifiers.teamforge}} disconnected installation and save it in `/tmp`.
   * {{site.data.identifiers.rhel_centos_now}} 64 bit: `{{site.data.identifiers.teamforge_rhel_centos_now_64_bit_dm_repo_name}}`
   * In addition to the above CentOS {{site.data.identifiers.rhel_centos_now}} 64 bit RPM package, you must get the following CentOS {{site.data.identifiers.rhel_centos_now}} compatibility RPM, which is required for TeamForge {{site.data.identifiers.teamforge}} disconnected media installation on CentOS {{site.data.identifiers.rhel_centos_now}} profile: `{{site.data.identifiers.centos_compat_rpm}}`.
2. Unpack the disconnected installation package.
   ```shell
   rpm -ivh <package-name>
   ````
3. Unpack the `{{site.data.identifiers.centos_compat_rpm}}` package if you are installing TeamForge {{site.data.identifiers.teamforge}} on CentOS {{site.data.identifiers.rhel_centos_now}}.
   ```shell
   rpm -ivh {{site.data.identifiers.centos_compat_rpm}}
   ````
4. If not mounted already, mount the RHEL/CentOS installation DVD.
   
   The DVD contains the necessary software and utilities required for installing TeamForge without internet access. In the following commands, replace "cdrom" with the identifier for your server's CD/DVD drive, if necessary.
   ```shell
   cd /media/
   mkdir cdrom
   mount /dev/cdrom ./cdrom/
   ````

   If there are any spaces in the automount, unmount it first and mount it as a filepath, with no spaces.
5. Create a yum configuration file that points to the RHEL/CentOS installation DVD.
   ```shell
   vi /etc/yum.repos.d/cdrom.repo
   ````

   Here's a sample yum configuration file.
   ```shell
   [RHEL-CDROM]
   name=RHEL CDRom
   baseurl=file:///media/cdrom/Server/
   gpgfile=file:///media/cdrom/RPM-GPG-KEY-redhat-release 
   enabled=1
   gpgcheck=0
   ````
6. Verify your yum configuration files.
   ```shell
   yum list httpd
   yum list apr
   ````
</div>

{% include links.html %}