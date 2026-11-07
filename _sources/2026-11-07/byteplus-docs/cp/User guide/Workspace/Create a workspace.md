---
title: "Create a workspace"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Create_a_workspace"
---

Creating a workspace means creating an independent research and development project space. This article explains how to create a workspace.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The account has been configured with Code Pipeline permission. For specific operations, refer to [Configure permission](https://docs.byteplus.com/en/docs/cp/Configure_IAM_user_permissions).

* When specific accounts are visible in the workspace, please create IAM users or user groups in the IAM console in advance. For specific operations, refer to [User management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-management) and [User group management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-user-group-management).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **workspace**.

3. On the workspace page, click **Create workspace**.

4. On the create workspace page, fill in the parameter information as required.

   
   |Configuration Item |Descriptions |
   |---|---|
   |Name |Customize the workspace name. To facilitate resource identification, it is recommended that different workspaces under the same account avoid using duplicate names. |
   |Avatar |Set an avatar picture for your workspace to make it easier to distinguish between different workspaces. If you select not to upload an avatar, the system will provide a default avatar. |
   |Description |Enter workspace\-related description or remarks. The length must not exceed 100 characters. |
   |Visible to members |Settings for workspace visibility make it easier for the team to control permissions.<br><br><br>* **All**: All accounts under the current BytePlus main account (root account) can view this workspace.<br><br>* **Specific accounts**: Only specific accounts can view this workspace. Supports specified users or user groups.<br><br>   * **User**: Specify visible users. The selected users include the BytePlus root user and the creator by default. Among them, the BytePlus root user cannot be deleted.<br><br>   * **User groups**: Specify visible user groups. This is optional. A user group is a collection of users. Users who require the same permission configuration can be placed in a user group, making it easier to assign permissions collectively. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If your workspace visibility settings do not include yourself, you can see the workspace under the <strong>Workspace \> My</strong> tab, but you cannot access the workspace.   </div>
   

5. Click **confirm** to complete the creation of the workspace.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After the workspace is created successfully, you can [Integrate code source](https://docs.byteplus.com/en/docs/cp/Integrate_code_source) and [create a pipeline](https://docs.byteplus.com/en/docs/cp/Create_pipelines) within the workspace.
