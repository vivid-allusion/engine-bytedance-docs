---
title: "Resetting an account password"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Resetting_an_account_password"
---

This topic introduces how to reset an account password.

<span id="PuRRJGqR"></span>
## Prerequisites

A workspace is created and its status is **Running**.

<span id="bGvjJaaQ"></span>
## Precautions

After resetting the account password, the previous account password becomes invalid and can no longer be used to access the workspace.

<span id="R79ElXzX"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page's **Account** tab, click … \> **Reset password** on the target account row to access the **Reset password** page.

6. On the **Reset password** page, enter the new password in the **New password** textbox, then click **OK**.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Account password must meet the following rules:</div>


   * <div data-tips="true" data-tips-type="default">Can only contain letters (a~z and A~Z), numbers (0~9), and the following special characters  <code>!#$%&()*+,-.=?@^_|/</code>.</div>


   * <div data-tips="true" data-tips-type="default">The length must be between 8 and 32 characters.</div>


   * <div data-tips="true" data-tips-type="default">Must contain at least three of the following character types: uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters.</div>


   * <div data-tips="true" data-tips-type="default">Using easily cracked weak passwords (such as Admin@123) is not allowed.</div>


* <div data-tips="true" data-tips-type="default">After resetting the account password successfully, the <strong>Reset password</strong> page will switch to the <strong>Reset successfully</strong> page. On this page, you can view and copy the account's password or download a file containing the account and password information to your local device.</div>



<span id="DJfrFENL"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[ResetDBAccountPassword](https://docs.byteplus.com/en/docs/330/ResetDBAccountPassword) |Call the ResetAccountPassword API to reset the account password. |
