---
title: "Creating an account"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_an_account"
---

This topic introduces how to create an account.

<span id="ENelCrPA"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="VAq48U4h"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page's **Account** tab, click **Create account** to access the **Create account** page.

6. On the **Create account** page, complete the following configurations and then click **Create**.

   
   |Configuration item |Decscription |
   |---|---|
   |Account name |Set the new account's name. The name must meet the following rules:<br><br><br>* Unique within the branch.<br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 63 characters in length.<br><br>* Cannot use certain reserved words. For forbidden reserved words, refer to List of reserved words. |
   |Account password |Configure the new account's password. Password must comply with the following rules:<br><br><br>* Can only contain letters (a~z and A~Z), numbers (0~9), and the following special characters `!#$%&()*+,-.=?@^_\|/`.<br><br>* The length must be between 8 and 32 characters.<br><br>* Must contain at least three of the following character types: uppercase letters (A~Z), lowercase letters (a~z), digits (0~9), and special characters.<br><br>* Using easily cracked weak passwords (such as Admin@123) is not allowed.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When creating an account, you do not need to specify the account's password. The system will create a 16\-character random password for the account. After the account is created successfully, the <strong>Create account</strong> page will switch to the <strong>Created successfully</strong> page. On this page, you can view and copy the account's password or download a file containing the account and password information to your local device.</div><br> |
   


<span id="mUOGcN0T"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/330/CreateDBAccount) |Call the CreateDBAccount API to create a database account for the branch. |
