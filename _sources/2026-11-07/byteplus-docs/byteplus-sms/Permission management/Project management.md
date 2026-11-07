---
title: "Project management"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/project-management"
---

BytePlus provides customers with project management capabilities, which are commonly used in financial accounting and group operations scenarios. In the context of SMS, you can manage different message groups by moving them into different projects. This document discusses how to manage projects in SMS services. For details on project management, refer to [IAM documentation](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).

<span id="41cdfbec"></span>
## Scenarios


* **Manage projects for resource isolation and cost calculation**

   If your company has multiple product lines, you can set different projects for each product line, and associate message groups with them to achieve resource isolation and cost calculation.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d177c7676b7741fe9e6de6d3ccff8d9f~tplv-goo7wpa0wc-image.image) </span>

* **Manage projects by departments**

   You can manage permissions by departments for control resources.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9886e07fd6e441f68014aa1f2379821b~tplv-goo7wpa0wc-image.image) </span>


<span id="7a4ed776"></span>
## Managing projects and resources

In the [BytePlus SMS console](https://console.byteplus.com/sms), you can switch different projects or go to the project management page by clicking **All resources**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52071a2feb494c6ea4f1d415f5804c9b~tplv-goo7wpa0wc-image.image) </span>


* For how to create a project, see [Creating a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-a-project).

* For how to manage a project, see [Editing a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-editing-a-project).

* For how to delete a project, see [Deleting a project](https://docs.byteplus.com/en/docs/byteplus-platform/docs-deleting-a-project).


<span id="4be07dfc"></span>
## Manage user's project permissions

This section describes how to grant user permissions. For more information, see [Permission management](https://docs.byteplus.com/docs/byteplus-sms/permissions-management).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Compared to standard policy authorization, project\-based authorization requires specifying the scope of action. If not specified, the scope defaults to "global," which includes all current and future resources within the account.</div>


* <div data-tips="true" data-tips-type="tip">Users with only project\-specific permissions cannot access other projects or global data, such as the total sending volume of the account.</div>


1. Go to IAM's [User page](https://console.byteplus.com/iam/identitymanage/user), select and click the target user name.

   You will enter the **User detail** page.

2. On the user detail page, click **Policy** \> **Project policy** \> **Add Permission**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/27509510e1e145b3b34f18b8236a87a0~tplv-goo7wpa0wc-image.image) </span>

   The **Add Permission** window will slide out.

3. Add policies and scope of action as you need.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/58359a68b6d447388d06cf2e40f9dabc~tplv-goo7wpa0wc-image.image) </span>

   After the submission is complete, this IAM identity (user, user group, role) will have the permissions described within the policy for the resources within the project.


<span id="a27b9ba8"></span>
## Delete a project


1. Log in to the [Project Console](https://console.byteplus.com/iam/resourcemanage/project/).

2. Click **Delete** on the right side of the target project.

   A confirmation dialog box will pop up.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4623a4ae659c47b89d1d016680a75877~tplv-goo7wpa0wc-image.image) </span>

3. In the confirmation delete dialog box, click **Delete**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b33889faa64043319dffd5f2af6cb278~tplv-goo7wpa0wc-image.image) </span>


<span id="889a0e2b"></span>
## Switch to a project


1. Log in to the [BytePlus console](https://console.byteplus.com/sms).

2. On the Overview page, you can switch projects in the top navigation bar and manage the message groups under the corresponding project.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da12e7f1255f4b6dbedf14c3ed564fe8~tplv-goo7wpa0wc-image.image) </span>
