---
title: "Non-admin user management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/non-admin-user-management"
---

System admin can define permission strategies for all non\-admin users in the system, manage the usage permissions of console functions for non\-admin users, including the ability to use the data download in SQL Editor, the maximum number of rows viewable, whether individual account passwords are allowed, and whether creating new clusters is permitted.

<span id="95c3b7a5"></span>
# Background

Non\-admin users are those who have not been granted the system admin role. You can view [View Non-admin users](https://docs.byteplus.com/docs/bytehouse/non-admin-user-management#aa7718f9) in the user list. Aside from admins, ByteHouse has also defined multiple user types. For more details, refer to [User types](https://docs.byteplus.com/docs/bytehouse/privilege-model#b7c2623a).

<span id="c8164300"></span>
# Configuration entry

Log into the ByteHouse Console, click the **Personal center icon \> System Settings** to view the non\-admin permission management module.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f7b45dc7fd44e6da2051a9b14deb30f~tplv-goo7wpa0wc-image.image) </span>

<span id="aa7718f9"></span>
# View non\-admin users

Click **View non\-admin users** and the system will automatically jump to the user list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44e5c8ffe14d458ab36d1e17c66dc0c4~tplv-goo7wpa0wc-image.image) </span>

Users marked as “No” in the Admin user column are non\-admin users.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc0ebd602d974ce8abd7d439a4427988~tplv-goo7wpa0wc-image.image) </span>

<span id="b49a264d"></span>
# Permission control: SQL Editor

<span id="038fc008"></span>
## Download data

Configure whether to show the 'Download Data' button on the SQL Editor page for non\-admin users.

When download data permission is activated, non\-admin users can download data from the SQL Editor page.

After terminating this permission, non\-admin users will be unable to view the 'Download Data' button on the SQL Editor page of their console and will not be able to download data.

<span id="4d768bb4"></span>
## Maximum number of returned rows

Click **Edit** button to modify the maximum number of returned rows.

After setting the maximum return value, non\-admin users on their console can only view the content of the set number of rows and cannot display content beyond the set number.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf3354968c25478f9090728e7c03fe54~tplv-goo7wpa0wc-image.image) </span>

<span id="e051b712"></span>
# Permission control: Customize password

Configure whether to allow non\-admin users to change their own account password.

When permission to change one's account password is activated, non\-admin users can customize their own account passwords.

After this permission is deactivated, the console page for managing accounts for non\-admin users will no longer display the password modification option, making it impossible to customize passwords.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c69e79ac057d4f57a0b6c38820b9daa3~tplv-goo7wpa0wc-image.image) </span>

<span id="b7b82205"></span>
# Permission control: Create new cluster

Configure whether to allow non\-admin users to create new clusters.

When permission to create new clusters is activated, the overview and manage clusters page on the console for non\-admin users will show the entry to create new clusters and support the creation of new clusters.

After this permission is disabled, the overview and manage clusters page on the console for non\-admin users will no longer display the option to create new clusters, making it impossible to create new clusters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a342a4a747a43ada39b476a26926cc5~tplv-goo7wpa0wc-image.image) </span>
