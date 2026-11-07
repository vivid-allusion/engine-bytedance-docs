---
title: "Restart instance or node"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/restarting"
---

This topic explains how to manually restart instances or nodes through the console.

<span id="a9c96ec3"></span>
## Precautions


* During instance restart, some services will be unavailable. It is recommended to perform the restart during off\-peak hours.

* Cloud Search offers two types of restart operations: normal restart (including restarting instances, data nodes, dedicated master nodes, Kibana/Dashboards nodes, coordinating nodes, warm data nodes, and cold data nodes) and forced restart (forced restart of instances). The differences between the two restart types are shown in the table below.

   
   |Restart type |Normal restart |Force restart |
   |---|---|---|
   |Explanation of instance status before restart |The instance running state is **Running** or **Exception**, and the instance health status is green. |The instance running state is **Running** or **Exception**. |
   |Restart process description |The restart process is a rolling restart. The next node will only restart after the previous node completes restarting and the instance health status turns green. |The restart process is a rolling restart, where the next node restarts immediately after the previous one finishes restarting, without waiting for the instance monitoring status to turn green. |
   


<span id="6193347d"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click **Restart** in the actions column of the target instance, then select the restart type from the dropdown menu.

   
   |**Restart type** |**Description** |
   |---|---|
   |Instance |Restart all nodes within the instance. |
   |Data node |Select one or more data nodes to restart.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If multiple nodes exist, you can select several to restart for easier operation. Restart still uses rolling restart. If there are 0 replicas, the instance will turn red. Operate with caution.</div><br> |
   |Dedicated master node |Select one or more dedicated master nodes to restart. |
   |Kibana/Dashboards node |Restart only the data visualization tool node. |
   |Coordinating node |Select one or more coordinating nodes to restart. |
   |Warm data node |Select one or more warm data nodes to restart. |
   |Cold data node |Select one or more cold data nodes to restart. |
   |Forced restart instance |If the instance status is exception and cannot restart, you can choose **Forced restart instance**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Forced restart may cause data loss or instance unavailability. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">During forced restart, the instance health check is skipped and the next node restarts immediately.</div><br> |
   

4. Click **OK**.

5. View restart status.

   After restarting the instance or node, refresh the page to check the instance status. During the restart, the instance running state is **Restarting**. If the status changes to **Running**, the instance has restarted successfully.

   If the instance status changes to **exception**, [submit a ticket](https://console.byteplus.com/workorder/create/?step=1) or contact customer support to troubleshoot.
