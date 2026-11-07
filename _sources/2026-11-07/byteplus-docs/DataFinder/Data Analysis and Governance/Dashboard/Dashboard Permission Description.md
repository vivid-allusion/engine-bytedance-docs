---
title: "Dashboard Permission Description"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Dashboard_Permission_Description"
---

This document describes the permissions of different roles in Dashboard.

<span id="_1-文件夹与看板授权逻辑说明"></span>
# 1. Folder and Dashboard authorization logic description

<span id="_1-1-文件夹授权"></span>
## 1.1 Folder authorization

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All member (role) configuration items in this application are only open to administrators, and cannot be configured by non\-administrators.</div>


If you authorize through folder configuration, the user who is given the folder view/edit permissions has the view/edit permissions for all subfolders and Dashboard within the current folder.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3fcccc70e2d34cb99cd87275111f75e5~tplv-goo7wpa0wc-image.image) </span>

It should be noted that all member (role) configuration items in this application are only open to administrators, and cannot be configured by non\-administrators.

When the option is set to "invisible", it means that the current folder is not visible to other members by default. **At this time, the current folder, subfolders, and folder internal Dashboard can all grant additional viewing or editing permissions to other members (roles).** 

The following figure is an example:


* The first\-level folder authorization is invisible to all employees by default, and Xiao Zhang can view it, then Xiao Zhang can view all the content in the folder, including the content of the second\-level subfolder, and other members are not visible.

* The secondary subfolder is set to be editable by Xiao Wang and viewable by Xiao Li, then Xiao Wang can edit all the content in the secondary subfolder, and Xiao Li can view all the content in the secondary subfolder, and other members are not visible.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df6f1a1dafff43d2a45bf6e38e929a7a~tplv-goo7wpa0wc-image.image) </span>

<span id="_1-2-看板授权"></span>
## 1.2 Dashboard authorization

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">All member (role) configuration items in this application are only open to administrators, and cannot be configured by non\-administrators.</div>


If you configure authorization through Dashboard, the authorization scope is only valid for the current Dashboard. If the board is in a folder, users with Dashboard privileges can see the entry of the folder where the board is located, but not other boards in the folder.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5d276d159e04ab0a66ba869c12e5823~tplv-goo7wpa0wc-image.image" width="600px" /></div>


When set to "invisible", it means that the current Dashboard is not visible to other members by default. At this time, other members (roles) can still be authorized to view or edit permissions individually, and users who are not specially authorized are not visible.

Take the following picture as an example. The current Dashboard is invisible to all staff by default. Xiao Wang can edit and Xiao Li can view it.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa93b3d47f66477c940ff29b8dfe202a~tplv-goo7wpa0wc-image.image" width="584px" /></div>


<span id="_1-3-图表授权"></span>
## 1.3 Graph authorization

Dashboard and chart permissions are juxtaposed, not subordinated.

To facilitate chart editing under Dashboard, users with "Dashboard and Chart Editing Rights" can authorize chart editing permissions under Dashboard to others.


* Go to the Chart tab and select Authorized User

* Then select the single or multiple charts that need to be authorized (you can only authorize your own permissions charts)

* After the selection is complete, click "Confirm Invitation".


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91355a6a92de4d97bf65dae4b60b4f83~tplv-goo7wpa0wc-image.image" width="600px" /></div>


<span id="_2-各角色权限说明"></span>
# 2. Description of permissions for each role

<span id="_2-1-saas权限说明"></span>
## 2.1 SaaS permission description


| |**Operation** |**Group administrator** |**App administrator** |**Owner** |**Editor** |**Viewer** |**Unauthorized** |
|---|---|---|---|---|---|---|---|
|Public space dashboard |Create |**Administrators only, Dashboard public space management permissions can be created, accessible to all by default, configurable authorization scope** ||||||
||View |✅ |✅ |✅ |✅ |✅ |❌ |
||Edit |✅ |✅ |✅ |✅ |❌ |❌ |
||Delete |✅ |✅ |✅ |❌ |❌ |❌ |
||Copy |✅ |✅ |✅ |✅ |❌ |❌ |
||Share (Authorize) |✅ |✅ |✅ |❌ |❌ |❌ |
||Collection |✅ |✅ |✅ |✅ |✅ |❌ |
||Chart sorting |✅ |✅ |✅ |✅ |❌ |❌ |
||Mobile Storage Path |✅ |✅ |✅ |❌ |❌ |❌ |
||Transfer of ownership |✅ |✅ |✅ |❌ |❌ |❌ |
|Private space dashboard |Create |**All users can create, only visible to themselves by default, and the authorization scope can be configured** ||||||
||View |✅ |✅ |✅ |✅ |✅ |❌ |
||Edit |✅ |✅ |✅ |✅ |❌ |❌ |
||Delete |✅ |✅ |✅ |❌ |❌ |❌ |
||Copy |✅ |✅ |✅ |✅ |❌ |❌ |
||Share (Authorize) |✅ |✅ |✅ |configurable |configurable |❌ |
||Collection |✅ |✅ |✅ |✅ |✅ |❌ |
||Chart sorting |✅ |✅ |✅ |✅ |❌ |❌ |
||Mobile Storage Path |✅ |✅ |✅ |❌ |❌ |❌ |
||Transfer of ownership |✅ |✅ |✅ |❌ |❌ |❌ |
