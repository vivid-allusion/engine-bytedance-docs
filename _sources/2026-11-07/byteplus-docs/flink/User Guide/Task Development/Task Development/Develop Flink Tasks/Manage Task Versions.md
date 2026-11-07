---
title: "Manage Task Versions"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Manage_Task_Versions"
---

When you perform task deployment operations, the system will record a version of the task, documenting each operation serially. In the task version page, you can compare the current version with historical versions, rollback to a previous version, or delete previous versions.

<span id="530f8cdb"></span>
## Important Notes

Apart from generating task versions when deploying from the development side, if task resource configurations are changed when starting tasks on the operational side, an additional version will be created and pushed back to the development side.

<span id="03b65fef"></span>
## View Task Versions


1. Log in to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. In the left sidebar, select **Project Management**, search for the project name in the search box, then click on the project block to enter the project.

4. In the project sidebar, select **Task Development**, then click on the target task within the destination folder.

5. In the task editing area on the right, click **Version Information**.

6. View task versions.

   In the **Version Information** panel, you can view the release times of all versions, who deployed them, and the current latest version.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1481b2c6793a4d18b416ff320e39742a~tplv-goo7wpa0wc-image.image) </span>


<span id="3cc7cefb"></span>
## Compare versions

In the **Version** panel, click **Compare** behind a historical version to view the differences between the current editing version and the historical version.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/580bae77533f47feb62c98ab54b4a70f~tplv-goo7wpa0wc-image.image) </span>

<span id="25d01e6e"></span>
## Revert versions

Support the restoration of historical task versions to achieve version rollback.


1. In the **Version Information** panel, click **Revert to this version** behind the target version.

2. In the confirm version restoration dialog, review the differences between the target version and the current version, and click **revert** when you decide to restore the historical version.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae93658d831c4f74ac90f093a46c5f2d~tplv-goo7wpa0wc-image.image) </span>


3. After reverting to a previous version, you can resubmit the task for deployment.

   For guidelines on how to deploy a task, please see [Launch Flink Task](https://docs.byteplus.com/docs/flink/Launch_Flink_Task).


<span id="df023f78"></span>
## Delete Version

You can opt to delete past versions of tasks to avoid having too many versions and reduce operational pressure. Deleting a version is irreversible, please proceed with caution.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The current version (already deployed) cannot be deleted, but all other versions can be.</div>



1. On the **Version Information** panel page, click **Delete** next to the target version.

2. In the confirm delete version dialog, click **Confirm**.
