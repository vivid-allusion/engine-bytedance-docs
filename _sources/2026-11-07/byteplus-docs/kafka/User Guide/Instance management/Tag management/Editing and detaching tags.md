---
title: "Editing and detaching tags"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/editing-and-detaching-tags"
---

After tags are associated with a specified instance, you can modify the tag keys or tag values anytime as needed. To adjust the category of the instance, you can also disassociate tags from the instance. This topic describes how to edit and disassociate tags.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can batch disassociate a maximum of 20 tags from an instance at a time.</div>


<span id="为单个实例修改或解绑标签"></span>
## Modifying or disassociating tags from an instance


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. Locate the Kafka instance and click the Edit icon in the **Tag** column.

   Alternatively, click the name of the instance. In the **Instance Details** pane, click the Edit icon in the **Tag** row.

4. Edit or disassociate tags as needed.

   * To edit tags, reset **Tag Key** or **Tag Value**.

      Follow tag setting rules to set tags. For more information, refer to [Tag setting rules](https://docs.byteplus.com/en/docs/kafka/associating-with-tags).

   * To delete tags, locate the tag key and click Delete.

5. Click **OK**.


<span id="批量解绑标签"></span>
## Batch disassociating tags


1. Log on to the [Message Queue for Kafka console](https://console.byteplus.com/kafka).

2. In the top menu bar, select the Region of your instance.

3. Select all target instances and click **Unbind Tag** on the upper\-left corner of the page.

4. Select the tag key you want to delete from the drop\-down list or enter the tag key for filtering.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The page displays the number of the selected instances associated with the specified tag key. All tags corresponding to the specified tag key are disassociated from the selected instances. Tags of unselected instances remain unchanged.   </div>
   

5. Click **OK**.
