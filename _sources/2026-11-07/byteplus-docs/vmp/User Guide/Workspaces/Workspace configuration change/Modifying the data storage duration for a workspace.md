---
title: "Modifying the data storage duration for a workspace"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Modifying_the_data_storage_duration_for_workspace"
---

After a Vital Managed Service for Prometheus (VMP) workspace is created, you can modify its metric storage duration. This topic describes how to modify the data storage duration of a workspace.

<span id="mrXTkIxl"></span>
## Limits


* A package has its corresponding storage duration. Therefore, if you modify the data storage duration of a Standard Edition workspace, the existing packages in the modified workspace will become invalid. Proceed with caution.

* Data that is written before the modification will still expire according to the storage duration during writing.

* You can modify the parameters of a workspace within the following limits:

   * You can modify the parameters once in 10 minutes.

   * You can modify the parameters up to 10 times in 30 days.


<span id="JlPc8Ty5"></span>
## Prerequisites

A Standard Edition workspace is created. For details, see [Create common workspaces](https://docs.byteplus.com/en/docs/vmp/Creating-workspaces).

<span id="B3ksifWS"></span>
## Procedure


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target region.

3. Click **Workspace** in the left navigation bar to go to the workspace list page.

4. In the workspace list, find the target workspace and click the Edit icon in the **data storage duration** column.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_36d209284a6f0d5928fe67cd3f0ed382.png) </span>

5. In the Modify storage duration panel, modify the data storage duration of the workspace.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The modification of the data storage duration for the workspace does not affect normal data writing and reading in the workspace.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The modification of the data retention period in the workspace will only apply to data written after this change. Data already written before the modification will still follow the original retention policy and expire based on the retention period set at the time of writing, which will not be extended due to this change.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can purchase resource packages to offset fees for standard workspaces billed by reported metric volume. The resource package to apply to a workspace must have the same duration as the storage retention period of the workspace. If you have purchased a package and modified the data storage duration of the corresponding Standard Edition workspace, the existing package will become invalid in the modified workspace. Proceed with caution.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_607883c2217d047a3398ac17969da82a.png) </span>

6. After confirming the duration, click **Confirm**.


<span id="3XKsTxuw"></span>
## Verifying results

After the configuration is complete, the workspace will be in the **Updating** state. After the update is complete, you can view the latest data storage duration of the workspace.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0544300c97b04f6c3ee3d337d9edd88c.png) </span>

&nbsp;

&nbsp;
