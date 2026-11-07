---
title: "Creating a compute"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_compute"
---

This topic introduces the procedure for creating a compute for a branch.

<span id="6RfDmljt"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The target branch status is **Running**.


<span id="se4afX5Z"></span>
## Precautions


* Each branch can have up to 20 computes. A branch can have up to 1 primary compute and at least 0; up to 20 read\-only computes and DuckDB read\-only computes with a minimum of 0 each.

* If the branch currently has no primary compute, only primary compute or read\-only compute can be created.

* If the AP acceleration function of the primary compute is enabled, DuckDB read\-only compute cannot be created.


<span id="4AvomE2N"></span>
## Procedure


1. Login to [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the **Branch management** page of the target workspace. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, under the **Compute** tab, click **Create compute** to enter the **Create compute** page.

6. On the **Creating compute** page, complete the following configuration, then click **Create** to complete the compute creation.

   
   |**Configuration item** |**Decscription** |
   |---|---|
   |Name |Set the name of the compute. The compute name must meet the following rules:<br><br><br>* Must start with a letter and end with a letter or number.<br><br>* Can only contain letters, numbers, underscores (_), and hyphens (\-).<br><br>* Must be 2 to 64 characters in length.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Name is optional. If not set, it will be automatically named based on the compute type with the following rules:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the compute type is <strong>Primary compute</strong>, the compute will be named <code>Primary</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the compute type is <strong>Read\-only compute</strong>, the compute will be named <code>ReadReplica-{number}-{4-digit random code}</code>.</div><br> |
   |Workspace/Branch |No need to set, only to confirm the compute belongs to the correct Workspace and Branch. |
   |Compute type |Configure the type of compute by selecting **Primary compute, Read\-only compute**, or **DuckDB read\-only compute**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch has a primary compute and its AP acceleration function is not enabled, read\-only compute or DuckDB read\-only compute can be created, but primary compute creation is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If the branch has a primary compute and its AP acceleration function is enabled, only read\-only compute can be created; primary compute or DuckDB read\-only compute creation is not supported.</div><br> |
   |Compute expansion range |Configure the compute expansion range. The default is the Workspace's compute expansion range, and adjustments are supported within this range.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The ratio of the maximum compute to the minimum compute must be less than or equal to 8.</div><br> |
   


<span id="kNUFowLo"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[CreateCompute](https://docs.byteplus.com/en/docs/330/CreateCompute) |Call the CreateCompute API to create a compute. |
