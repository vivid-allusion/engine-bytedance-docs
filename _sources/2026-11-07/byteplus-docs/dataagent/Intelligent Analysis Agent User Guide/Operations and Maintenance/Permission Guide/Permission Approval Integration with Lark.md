---
title: "Permission Approval Integration with Lark"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Permission_Approval_Integration_with_Lark"
---

<span id="554b7a4e"></span>
# 1. Overview

In [Detailed Explanation of User Permissions](https://docs.byteplus.com/docs/dataagent/Detailed_Explanation_of_User_Permissions), it was introduced that different permissions can only be obtained through authorization by the permission owner. The DataAgent product supports permission application through the Lark approval workflow, allowing users to independently request permissions from resource owners. Once the owner approves, the applicant will obtain the corresponding permissions for the requested resource. This lowers the threshold for data usage and shortens the time required for data or IT personnel to authorize data access.

<span id="0b9ce39c"></span>
# 2. Administrator configuration process

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>1. Prerequisites</strong>: Complete <a href="https://docs.byteplus.com/docs/dataagent/Lark_Integration_">Lark Integration</a> basic configuration, account binding, and message notification setup.</div>


<div data-tips="true" data-tips-type="tip"><strong>2. Caution:</strong> Only private deployment supports the Lark approval flow; SaaS environments are not supported.</div>


<div data-tips="true" data-tips-type="tip">3. Administrator configuration operations, <strong>only DataAgent system administrators can perform</strong>, and can only be performed if the configured users in <a href="https://docs.byteplus.com/docs/dataagent/Lark_Integration_">Lark Integration</a> are consistent.</div>


(1) Go to the [Lark Open Platform](https://open.feishu.cn/), enter the bot backend where configuration messages need to be pushed, and click **Event Subscription**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a47f39f4f714e209f8ccf419a237fed~tplv-goo7wpa0wc-image.image) </span>

(2) Click **Configure Request Address**, and fill in the configuration information: http://environment address (ip:port or domain name)/aeolus/api/v3/dispatcher/action

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/673b20e89f0e45ec9339ae1b6ba3739e~tplv-goo7wpa0wc-image.image) </span>

(3) Select **Add "Approval Instance Status Change" event,**  then enable the [Access Approval Application] permission.

(4) According to [Permission approval integration with Lark](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#20c9b20e)the steps, add the following four permissions: [View, Create, Update, Delete approval application related information], [Query approval list], [Access approval application], [Obtain user ID]

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03d1aef6618b4eeda898e5722bf908af~tplv-goo7wpa0wc-image.image) </span>

(5) After completion, click Application Release \-\- Version Management and Release, then click Create Version, and follow [Publish the Lark application](https://docs.byteplus.com/docs/dataagent/Lark_Integration_#39ea040a)the steps to publish.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db96883320704cb3a9fcb34b4a0d0871~tplv-goo7wpa0wc-image.image) </span>

(6) After completing all the above operations, return to the DataAgent platform, log in as an administrator, go to **System Management Configuration**, and click **Approval Settings** on the left to start the following configuration.

(7) Select process administrators


* Multiple process administrators can be selected, but only users who have completed Lark account binding on the platform can be chosen.

* The process administrator acts as a fallback. The configured Lark workflow will first send approval requests to the resource administrator of the resource, but if none of the resource administrators have bound their Lark accounts, the approval will be routed to the process administrator.


(8) After completing the above operations, select the enabled status to enable the Lark approval workflow setup.

<span id="55b9550d"></span>
# 3. Lark permission approval application scenarios

<span id="6f5fe170"></span>
## 3.1 Initiate permission approval

When data permissions, project permissions, or similar permissions are unavailable, or when you do not have permission, click **Apply for permission** to initiate an approval process.

> Caution: Currently, visual modeling and data connection do not support access to the Lark approval flow.


* No permission for datasets, dataset folders, or similar resources.

* No permission for project space.


<span id="a80c6cba"></span>
## 3.2 Fill out the approval application


* The approval process will proceed as illustrated below.

* When a user without permission clicks to apply for permission, they will be redirected to the following interface, where they can request permission for the resource and also add other resource permissions to combine into a single application.

* After clicking Submit, the illustrated effect will appear. Click the [Approval] link in the upper right corner to quickly jump to the workspace and view the approval flow.


<span id="312720e8"></span>
## 3.3 Approval process notifications


* **After submitting the application, both the applicant and the approver will receive a message notification.** 

   * Applicant

   * Approver

* **After receiving the notification, the approver can choose to approve or reject the application.** 

   * Approve application

   * Reject application

* **After the approver takes action, the applicant will also receive a notification indicating whether the application was approved or rejected.** 

   * If the application is approved, the applicant can view the resource in DataAgent and use it within the scope of the granted permissions.

   * If the application is not approved, the applicant will remain without permission for the resource as before.
