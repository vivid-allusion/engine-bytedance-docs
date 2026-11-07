---
title: "Restarting compute"
product: "AI Native BaaS for Supabase"
product_code: "aidap"
source: "https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Restarting_compute"
---

This topic introduces the procedure for restarting compute.

<span id="Z3M7uLch"></span>
## Prerequisites


* A workspace is created and its status is **Running**.

* The status of the compute to be restarted is **Running**.


<span id="0fWB2wuI"></span>
## Precautions


* Restarting the specified compute will interrupt all connections and queries on the compute. Proceed with caution.

* When restarting all computes, all computes under the branch that are in the **Running** status will be restarted, interrupting all running tasks. Proceed with caution.


<span id="0fWB2wuI"></span>
## Procedure


<Tabs>
<Tab zoneid="xrETlGYnCm" title="Restart specified compute">
<TabTitle>Restart specified compute</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, under the **Compute** tab, click  **… ** \> **Restart** in the target compute row to enter the **Restart compute** page.

6. On the **Restart compute** page, confirm the compute information to be restarted, then click **OK**.


</Tab>
<Tab zoneid="pXQgMSKrPe" title="Restart all computes">
<TabTitle>Restart all computes</TabTitle>

1. Log in to the [AI Native Database Platform](https://console.byteplus.com/aidap).

2. Select the target project and target region in the top navigation bar.

3. Enter the target workspace's **Branch management** page. You can enter the **Branch management** page of the target workspace by either of the following two ways.

   * Click <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d6a6bd14e29a4147670589c8181cc1a.png)<sub> </sub></span>**Branch management** in the center navigation bar of the page, then click the icon<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a1b21e2628b99b7cc66d1f2a7f9b1fcb.png)<sub> </sub></span> to the right of the workspace name at the top left of the page to select the target workspace from the dropdown list and enter the **Branch management** page of the target workspace.

   * Click the middle navigation bar on the page<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_91cbf438e775b519ccb60e548fbb0a79.png)<sub> </sub></span>**Workspaces** in the center navigation bar to enter the **Workspaces** page **.**  Click the target workspace name on the **Workspaces** page to enter the target workspace **Overview** page. On the **Overview** page, click **All branches** at the top right of the branches list to enter the target workspace **Branch management** page.

4. On the **Branch management** page, click the name of the target branch to access the **Branch overview** page.

5. On the **Branch overview** page, under the **Compute** tab, click **Restart all computes** to enter the **Restart all computes** page.

6. On the **Restart all computes** page, confirm the compute information to be restarted, then click **OK**.


</Tab>
</Tabs>


<span id="PlobnT4k"></span>
## Related APIs


|**API** |**Decscription** |
|---|---|
|[RestartBranch](https://docs.byteplus.com/en/docs/330/RestartBranch) |call the RestartBranch API to restart a branch. |
