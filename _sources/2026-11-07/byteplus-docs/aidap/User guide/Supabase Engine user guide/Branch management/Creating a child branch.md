---
title: "Creating a child branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_child_branch"
---

This topic describes how to create a child branch.

<span id="TFBHqd7w"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="pAbBMh3Y"></span>
## Precautions


* A maximum of 100 branches can be created for each workspace.

* When creating a branch, compute resources are automatically allocated for the Supabase service and the database management service. The Supabase service compute is automatic scaling compute with a default compute expansion range of 0.5 to 2 CU, and it can be adjusted within 0.5 to 32 CU. The database management service compute is automatic scaling compute with a default compute expansion range of 0.25 to 2 CU, and it can be adjusted within 0.25 to 32 CU. The ratio between the upper and lower limits of the compute expansion range for both the Supabase service compute and the database management service compute must be less than or equal to 8.

* When creating a child branch, the new branch will have the same Database, Authentication, and Edge Function as the parent branch at the data synchronization target time. Storage metadata will be restored to the parent branch’s data at the specified restoration time point, but the object files corresponding to the metadata can only remain current temporarily.


<span id="1nIRgj1a"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click  **...**  \> **Create child branch** in the target branch row to enter the **creating a branch** page.

5. On the **Create branch** page, complete the following configurations and click **Create** to finish creation.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Name |Configure the branch name. The name must meet the following rules:<br><br><br>* The length must be between 1 and 128 characters.<br><br>* Only letters (a~z and A~Z), numbers (0~9), hyphens (\-), and underscores (_) are allowed.<br><br>* It must start with a letter (a~z and A~Z) and end with a letter (a~z and A~Z) or a number (0~9).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the branch will be named branch\- followed by an 8\-digit random code.</div><br> |
   |Parent branch |Automatically select the target branch selected in step 4 as the parent branch of the new branch. Adjustment is not supported. |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking <strong>Create</strong>, it returns to the <strong>Branch management</strong> page. The new branch will show <strong>Initializing</strong> status, and after creation, the status switches to <strong>Running</strong>.   </div>
   

<span id="Sb9e9UbI"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateBranch](https://docs.byteplus.com/en/docs/aidap/CreateBranch) |Call the CreateBranch API to create a child branch for the branch. |
