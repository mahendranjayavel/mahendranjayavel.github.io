---
title: Reset the Admin Account Password
keywords: user management, roles, rbac
tags: [site_admin_tasks, users, role_based_access_control, license]
sidebar: teamforge_sidebar
permalink: resettheadminaccountpassword.html
last_updated: Mar 5, 2018
summary: If your TeamForge installation authenticates against an LDAP directory, follow these instructions to reset your admin account password.
---
If your installation does not validate against LDAP, click Forgot Your Password on the TeamForge home page to reset the password for the admin account.

1. With a web browser, go to the URL `http://<host>sf/sfmain/do/forgotAdminPassword`.
2. On the **Admin Account Password Retrieval** page, Click **Send Email**. TeamForge sends an email to the address specified for the admin user.
3. Check your email and click the link provided to reset your password.
4. On the **Reset Password** page, enter and confirm a new password.
5. Click **Reset Password**.
   
   You can now log into Digital.ai TeamForge with your new password.

{% include links.html %}