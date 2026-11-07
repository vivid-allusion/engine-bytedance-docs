---
title: "Managing subscription task tags"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/managing_subscription_task_tags"
---

A tag is a key\-value pair that identifies a cloud resource. Tags help categorize cloud resources, control access to cloud resources, and support billing and cost allocation. They also enable filtering and aggregation for easier cloud resource management. This topic describes how to manage migration task tags on the Database Transmission Service (DTS) console. This topic describes how to manage subscription task tags on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

[A subscription task has been created](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.

* For a single resource, tag keys must be unique, and each tag key can have only one Value.


<span id=".57uR5a6a5qCH562-"></span>
## Associate a tag


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

   * Associate tags for a single subscription task

      1. On the **Data subscription list** page, click the pen icon after the **Tag ** of the target task.

   * Batch associate tags for multiple subscription tasks

      1. On the **Data subscription list** page, check the target tasks to be terminated, then select  **...**  \> **Associate tag ** in the bottom menu bar.

4. On the **Task details** tab, locate the **Basic information** pane, click the pen icon next to the **Tag**.

5. In the **Edit tag** dialog box, set the tag key\-value pair information based on the following rules.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Tag key** |Set the key in the **Enter tag key** input box based on the following rules:<br><br><br>* Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>* Case\-sensitive, and the length is 1 to 128 characters.<br><br>* In UTF\-8 encoded Unicode format.<br><br>* Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`. |
   |**Tag value** |Set values in the enter tag value input box based on the following rules:<br><br><br>* Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>* Case\-sensitive, and the length is 0 to 256 characters.<br><br>* In UTF\-8 encoded Unicode format. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To set multiple key\-value pairs, click <strong>Associate tag</strong>.   </div>
   

7. Click **OK**.


<span id=".6Kej57uR5qCH562-"></span>
## Disassociate a tag


1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. In the upper\-left corner of the top menu bar, select the project and region.

3. In the left navigation bar, click **Data subscription**.

   * Disassociate tags for a single subscription task

      1. On the **Synchronization subscription list** page, click the pen icon after the **Tag** of the target task.

   * Batch disassociate tags for multiple subscription tasks

      1. On the **Data subscription list** page, check the target tasks to be terminated, then select  **...**  \> **Disassociate tag** in the bottom menu bar.

4. On the **Task details** tab, locate the **Basic information** pane, click the pen icon next to the **Tag**.

5. In the **Edit tag** dialog box, click **Delete** after the target key\-value pair.

6. Click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[AddTagsToResource](https://docs.byteplus.com/en/docs/DTS/addtagstoresource) |Call AddTagsToResource to add tags to a task. |
|[DescribeTagsByResource](https://docs.byteplus.com/en/docs/DTS/describesubscriptiongroup) |Call DescribeTagsByResource to query task tags. |
|[RemoveTagsFromResource](https://docs.byteplus.com/en/docs/DTS/removetagsfromresource) |Call the RemoveTagsFromResource API to disassociate the task tag. |
