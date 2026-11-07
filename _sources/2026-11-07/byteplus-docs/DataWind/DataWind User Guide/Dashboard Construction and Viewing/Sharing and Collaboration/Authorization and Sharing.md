---
title: "Authorization and Sharing"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Authorization_and_Sharing"
---

<span id="_1-概述"></span>
# 1. Overview

Dashboard/folder administrators can use the authorization feature to conveniently complete sharing operations and permission management.

<span id="_2-快速入门"></span>
# 2. Quick start

**Common usage scenarios**


* One\-click sharing: When viewing a dashboard, share it with relevant users with one click.

* Convenient management: When organizing dashboards/folders, conveniently manage dashboard/folder authorizations.


**Example usage process**

(1) Click the authorization button in the upper right corner of the dashboard (dashboard management or project management permissions are required).

(2) Enter the name of the user or user group, and click to select the user or user group to be authorized. To authorize multiple users at once, repeat steps 1–2 as needed.

(3) Set the authorization level for the selected user or user group, set whether to send a Lark notification to the authorized user (only effective for individual users, not for user groups), and click "Confirm".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a764f324a13475fbaf34a2d08e59528~tplv-goo7wpa0wc-image.image) </span>

(4) The system will grant permissions to all sharing recipients and send Lark notifications to users according to the settings.

Authorization information can be pushed to Lark. This requires the enterprise domain administrator to complete the office platform integration configuration.

<span id="_3-功能说明"></span>
# 3. Feature details

<span id="_3-1-操作入口"></span>
## 3.1 Operation entry points

The system provides the following two authorization entry points:


* "Authorize" button in the upper right corner of the dashboard

* "Authorize" option in the pop\-up menu of the dashboard or folder in the left dashboard directory


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d0021f6115143a88571344d58545dd5~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-2-一键授权"></span>
## 3.2 One\-click authorization

Click the authorization button, select the authorization recipient and permission level in the pop\-up window. The system will send the dashboard link to the sharing recipient and grant the corresponding permissions.


* Types of sharing recipients: individual users, user groups

* If the sharing recipient is a user group, the system will not send the dashboard link to all users in the user group.

* Available permission levels for authorization

* If the resource belongs to a personal dashboard space, the dropdown option only includes [View].

* If the resource belongs to a public dashboard space, the dropdown options include [View], [Edit], and [Manage].

* Send Feishu notification to sharing recipients: This option is selected by default and can be deselected.

* If the sharing recipient is a user group, the system will not send the dashboard link to all users within the group.


<span id="_3-3-便捷管理"></span>
## 3.3 Efficient management

Click the authorize button to adjust permissions or remove authorization for items in the authorized list in the pop\-up window.


* Available permission levels (including removal)

* If the resource belongs to a personal dashboard space, the dropdown options are only [View] and [Remove].

* If the resource belongs to a public dashboard space, the dropdown options are [View], [Edit], [Manage], and [Remove].


<span id="_3-4-权限控制"></span>
## 3.4 Permission control

Dashboard management or project management permissions are required.
