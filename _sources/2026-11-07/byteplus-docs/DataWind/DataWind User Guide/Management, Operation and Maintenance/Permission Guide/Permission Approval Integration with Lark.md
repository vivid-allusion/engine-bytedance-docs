---
title: "Permission Approval Integration with Lark"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Permission_Approval_Integration_with_Lark"
---

<span id="_1-概述"></span>
# 1. Overview

In [Detailed Explanation of Permission Features](https://docs.byteplus.com/docs/DataWind/Detailed_Explanation_of_Permission_Features), it was introduced that different permissions can only be obtained through authorization by the permission owner. Starting from `V2.48` of the DataWind product, approval workflows through Lark are supported, allowing users to independently apply for permissions from resource owners. Once the owner approves, the applicant will obtain the corresponding permissions for the requested resources. This lowers the barrier to data usage and shortens the time required for data or IT personnel to grant data permissions.

<span id="_2-管理员配置过程"></span>
# 2. Administrator configuration process

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>1. Prerequisites</strong>: Complete the following operations of <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9">Basic Configuration for Lark Integration</a>: <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9#_2-%E5%9F%BA%E7%A1%80%E9%85%8D%E7%BD%AE">Basic configuration</a> and <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9#_3-%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF%E6%89%80%E9%9C%80%E9%85%8D%E7%BD%AE">Configuration required for usage scenarios</a>.</div>


<div data-tips="true" data-tips-type="tip"><strong>2. Caution:</strong> Only private deployments support the Lark approval flow; SaaS environments are not supported.</div>


<div data-tips="true" data-tips-type="tip">3. Administrator configuration operations, <strong>only DataWind system administrators can perform these operations</strong>, and the configured user must be consistent with the user configured in <a href="https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9">Basic Configuration for Lark Integration</a> to proceed.</div>


(1) Go to the [Lark Open Platform](https://open.larkoffice.com/?lang=en-US), enter the backend of the bot that needs to push configuration messages, and click **Event Subscription.** 

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d1dfda9848646b4825a7cdb0d7795a0~tplv-goo7wpa0wc-image.image) </span>

(2) Click **Request Address Configuration** and fill in the configuration information: http://environment address (ip:port or domain name)/aeolus/api/v3/dispatcher/action.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d7453c78a654f98aebde53870a3fcf8~tplv-goo7wpa0wc-image.image) </span>

(3) Select **Add "Approval Instance Status Change" event,**  then enable the [Access Approval Application] permission

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16f5a76d1dfd4133959ee81872e799a2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/240d213946214000908e4334d52da54e~tplv-goo7wpa0wc-image.image) </span>

(4) According to [Permission management configuration](https://docs.byteplus.com/docs/undefined/69c349c050cba904c1f628d9#_2-2-%E6%9D%83%E9%99%90%E7%AE%A1%E7%90%86%E9%85%8D%E7%BD%AE) the steps, add the following four permissions: [View, Create, Update, and Delete Approval Application Information], [Query Approval List], [Access Approval Application], and [Obtain User user ID]

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b871ee5bce7d4bde810518dfef7a012c~tplv-goo7wpa0wc-image.image) </span>

(5) After completion, click Application Release \-\- Version Management and Release, then click Create Version, and publish.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2e229a7e24f940c1ac136eff8888fb87~tplv-goo7wpa0wc-image.image) </span>

(6) After completing all the above operations, return to the DataWind platform, log in as an administrator, go to **System Management Configuration**, and click **Approval Settings on the left to start the following configuration**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4e8fde476a34cccb16dc88e6929571e~tplv-goo7wpa0wc-image.image) </span>

(7) Select process administrators


* Multiple process administrators can be selected, but only users who have completed Lark account binding on the platform can be selected.

* The process administrator serves as a fallback. The configured Lark process will first send approval requests to the resource administrator of the resource. If none of the resource administrators have bound their Lark accounts, the approval request will be routed to the process administrator.


(8) After completing the above operations, set the status to enable to complete the configuration of the Lark approval workflow.

<span id="_3-飞书权限审批应用场景"></span>
# 3. Lark permission approval application scenarios

<span id="_3-1-发起权限审批"></span>
## 3.1 Initiate permission approval

When dashboard permissions, chart permissions, data permissions, project permissions, and similar permissions are not visible, click **Apply for Permission** to initiate an approval process.

> Caution: Currently, visual modeling, large screens, and data connections do not support integration with the Lark approval flow.


* **Dashboard**: If you do not have resource\-level permissions such as view or edit.

* **You have dashboard permissions, but do not have permissions for data rows or columns.** 

* No permissions for datasets, dataset folders, and so on.

* No permissions for project spaces.


<span id="_3-2-填写审批申请"></span>
## 3.2 Fill in the approval application


* The configured Lark process will first send approval to the resource administrator of the resource. However, if none of the resource administrators have bound their Lark accounts, the approval will be routed to the process administrator.

* When a user without permission clicks to apply for permission, the interface below will appear, allowing the user to apply for permission to the resource. You can also add other resource permissions to combine into one application; explanation of resource permissions [Permission Operation Manual](https://docs.byteplus.com/docs/DataWind/Permission_Operation_Manual)

* After clicking Submit, the following screen will appear. Click the [Approval] link in the upper right corner to quickly jump to the workspace to view the approval flow.


<span id="_3-3-审批过程通知"></span>
## 3.3 Approval process notifications


* **After submitting the application, both the applicant and the approver will receive a message notification.** 

   * Applicant

   * Approver

* **After receiving the notification, the approver can choose to approve or reject the application.** 

   * Approve application

   * Reject application

* **After the approver takes action, the applicant will also receive a notification indicating whether the application was approved or rejected.** 

   * If the application is approved, the applicant can view the resource in DataWind and use it within the scope of the approved permissions.

   * If the application is not approved, the applicant will remain without permission to the resource as before.
