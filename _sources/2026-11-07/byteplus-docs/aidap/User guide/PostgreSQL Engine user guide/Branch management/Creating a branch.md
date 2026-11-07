---
title: "Creating a branch"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_branch"
---

This topic introduces the procedure for creating a branch for the workspace.

<span id="Sc88BFbb"></span>
## Prerequisites

A workspace is created and its status is **Running**.

<span id="6U6HhSVH"></span>
## Precautions


* A maximum of 100 branches can be created for each workspace.

* Creating a branch automatically creates a primary compute. You can create more compute as needed. For details, refer to [Creating a compute](https://docs.byteplus.com/en/docs/330/PostgreSQL-Creating_a_compute).


<span id="vOOFOJ6X"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click **Create branch** in the upper\-right corner to access the **Create branch** page.

5. On the **Create branch** page, complete the following configurations and click **Create** to finish creation.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Name |Configure the branch name. The name must meet the following rules:<br><br><br>* The length must be between 1 and 128 characters.<br><br>* It can only contain letters (a~z and A~Z), numbers (0~9), hyphens (\-), and underscores (_).<br><br>* It must start with a letter (a~z and A~Z) and end with a letter (a~z and A~Z) or a number (0~9).<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, <code>branch-8-digit random code</code> is used as the branch name.</div><br> |
   |Parent branch |Specify the parent branch for the new branch. Any existing branch in the workspace can serve as the parent branch. By default, the current "default branch" of the workspace is selected as the parent branch. |
   |Initialization source |Set the initialization source for the new branch by choosing **Schema and data** or **Schema only**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When choosing <strong>Schema only</strong>, only the Schema structure will be copied from the specified parent branch to the new branch. There is no actual "parent\-child" branch relationship.</div><br> |
   |Target time for data synchronization |Select the time point to copy from the parent branch to the new branch. You can choose **Present time** or **Specific time**. If the specific time is selected, specify the time point in the time selection window.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">No configuration is needed when selecting <strong>Initialization source</strong> as <strong>Schema only</strong>.</div><br> |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">After clicking <strong>Create</strong>, you enter the details page of the new branch. The branch status will show as <strong>Initializing</strong>. Refresh the page later to update the status to <strong>Running</strong>. When creating a branch, a compute resource is automatically configured for it based on the workspace’s compute expansion range. This compute resource serves as the main compute for the branch. You can create more compute resources for the branch as needed once its status switches to <strong>Running</strong>. For detailed information about creating compute resources, refer to <a href="https://docs.byteplus.com/en/docs/330/PostgreSQL-Creating_a_compute">Creating compute</a>.   </div>
   

<span id="WAI2p3rj"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateBranch](https://docs.byteplus.com/en/docs/330/CreateBranch) |Call the CreateBranch API to create a branch for the workspace. |
