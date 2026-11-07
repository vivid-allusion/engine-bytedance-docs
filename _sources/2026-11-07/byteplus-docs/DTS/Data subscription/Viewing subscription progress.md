---
title: "Viewing subscription progress"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/viewing_subscription_progress"
---

After successfully creating a data subscription task, you can view its details on the console, including the progress of database and table schema subscription, full subscription, and incremental subscription tasks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

To create an on\-demand data subscription task, refer to [Subscription solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you can not find a certain subscription type, it may be because the type was not selected during the configuration of the subscription task, or the subscribed database does not support this type.

* Database and table schema subscription and full subscription tasks will automatically complete. Do not manually terminate them during task execution.

* Incremental subscription tasks will not automatically complete. After verifying that data has been successfully pushed, you can manually terminate the subscription task.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

4. On the **Data subscription list** page, locate the target subscription task.

   You can view the overall progress of the subscription task or the progress of each subscription type based on your business needs.

   * View overall subscription progress

      You can view the overall progress of the target subscription task on the task list page.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">In the figure below, the progress percentage of the full subscription task is calculated as: Rows pushed ÷ Total rows to be pushed × 100%.      </div>
      

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a0bfba4aa2a848343afae439748a661f.png) </span>

   * View subscription progress by type

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When you can not find the tab for a specific subscription type, it may be because the type was not selected during the configuration of the subscription task, or the subscribed database does not support this type.      </div>
      

      * On the **Data subscription list** page, click the target task name.

      * On the target task page, click **Task progress**.

      * On the **Task progress** tab, click the target subscription type to view the corresponding task progress and execution details.

         
         |**Subscription type** |**Supported operations** |**Precautions** |
         |---|---|---|
         |**Database and table schema subscription** |* View the schema subscription objects, state, and their source databases.<br><br>* Enter the name of the subscription object in the search bar at the top\-right corner to search for its subscription details.<br><br>* If there is a large amount of data to subscribe to, you can quickly filter subscription objects by **Type** or **State** in the list to check whether the subscription is completed. |Database and table schema subscription tasks end automatically. Do not manually terminate tasks during their execution. |
         |**Full subscription** |* View the full subscription objects, state, pushed rows, elapsed time, average push rate, and other information.<br><br>* Enter the name of the subscription object in the search bar at the top\-right corner of the page to search for its subscription details.<br><br>* If a large amount of data needs to be subscribed to, you can quickly filter the list by **State** to identify objects currently **Being pushed** and sort them by the **Estimated total rows**. |Full subscription tasks end automatically. Do not manually end the task during the full subscription. |
         |**Incremental subscription** |* Enter the name of the subscription object in the search bar at the top\-right corner of the page to search for its subscription details.<br><br>* View information such as the object, state, pushed rows, data volume of pushed rows, and delay of the incremental subscription. |Incremental subscription tasks will not automatically complete. After verifying that data has been successfully pushed, you can manually terminate the subscription task. |
         


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[DescribeTransmissionTaskProgress](https://docs.byteplus.com/en/docs/DTS/describetransmissiontaskprogress) |Call the DescribeTransmissionTaskProgress API to query transmission task progress. |
