---
title: "Creating a workspace"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace"
---

This topic introduces the preparations required before using the AI Native Database Platform for the first time and the procedure to create a workspace.

<span id="cIi7UKPD"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign Up and Verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).


<span id="8rZwgSa1"></span>
## Precautions

Each BytePlus primary account can create up to 1,000 workspaces using the Supabase engine by default. If you need to adjust the quota, [submit a ticket](https://console.byteplus.com/workorder/create) to contact us.

<span id="JQOtgkVB"></span>
## Procedure


1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. In the top navigation bar, select the target project and target region.

3. Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e37bb3bc4acc38cf3cc3d4cbd15b26ec.png)<sub> </sub></span>**Workspaces** to enter the **Workspace list** page.

4. On the **Workspace list** page, click **Create workspace** in the upper right corner to enter the **Create workspace** page.

5. On the **Create workspace ** page, complete the following configurations, read and check the [Customer agreement](https://docs.byteplus.com/en/docs/aidap/Customer_agreement), and then click **Create** to complete the workspace creation.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Engine |Select the workspace engine as **Supabase 1.24**. |
   |Workspace name |Configure the workspace name. The workspace name must meet the following rules:<br><br><br>* Can only contain Chinese characters, letters (a\-z and A\-Z), digits, hyphens (\-), and underscores (_).<br><br>* Must start with a Chinese character or letter (a\-z and A\-Z).<br><br>* Must be 2 to 128 characters in length. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking <strong>Create</strong>, you will enter the workspace <strong>Overview</strong> page.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">In the dialog box that appears when selecting the protocol, you can enable <strong>Automatic selection</strong> as needed. Enabling automatic selection indicates your acceptance of this product's service terms and service level agreement (latest version applies). The system will automatically select the service terms and service level agreement for you when creating a workspace next time, eliminating repeated operations. Click <strong>Decide later</strong> to disable automatic selection. Click <strong>OK</strong> to enable automatic selection.   </div>
   


<span id="P1Oy1afq"></span>
## Next steps


* [Modifying the workspace name](https://docs.byteplus.com/en/docs/330/Supabase-Modifying_workspace_name)

* [Configuring workspace deletion protection](https://docs.byteplus.com/en/docs/330/Supabase-Configuring_workspace_deletion_protection)


<span id="bxbt0l6I"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateWorkspace](https://docs.byteplus.com/en/docs/330/CreateWorkspace) |Call the CreateWorkspace API to create a workspace. |
