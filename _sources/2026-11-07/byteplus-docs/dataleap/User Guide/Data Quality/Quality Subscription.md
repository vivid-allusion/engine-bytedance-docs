---
title: "Quality Subscription"
product: "DataLeap"
product_code: "dataleap"
source: "https://docs.byteplus.com/en/docs/dataleap/Quality_Subscription"
---

Quality subscription receives quality daily report messages. This feature lets you create subscriptions, view the list of existing quality subscriptions, and edit or delete the quality subscriptions you manage.

<span id="_1-操作步骤"></span>
## Constraints

Only the quality subscription owner can edit or delete subscriptions they manage.

<span id="9ddc603d"></span>
## Operation Steps


1. Log in to the DataLeap Console.

2. Choose **Overview \> Quality \> Quality Subscription** to enter the quality subscription page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d55d924159d4d919c05a993f9d826cf~tplv-goo7wpa0wc-image.image) </span>

3. You can view all subscription information and perform the following actions:

   * New Subscription

      Click the **New Subscription** button. On the New Quality Subscription page, set the subscription information and then click the **Confirm** button to complete creation.

      The related parameters are described in the table below.

      
      |Parameters |Description |
      |---|---|
      |* Subscription name |The name of the quality subscription, supporting Chinese characters, English letters, and underscores, with a length no more than 128 characters. |
      |\*Owner |The owner of this subscription data, automatically filled with the current user. You can enter account keywords to select other users from the dropdown. |
      |Description |Description information for the created quality subscription, no longer than 200 characters. |
      |\*Project scope |Choose a project you have joined. |
      |\*Engine |The database storage engine to create rules for, supporting three engines: EMR, LAS, and EMR_SERVERLESS_SPARK, selectable from the dropdown.<br><br><br>* LAS: the instance defaults to **default**.<br><br>* EMR: you need to select the instance to use.<br><br>* EMR_SERVERLESS_SPARK: The instance defaults to **default**. |
      |\*Database scope |Select one or more databases you have read permission for. |
      |\*Recipients |People who receive the quality report.<br><br>The recipients default to the current user. Enter account keywords to select other users from the dropdown; multiple recipients are supported. |
      |\*Push frequency |Every day. |
      |\*Sending time |The time to send quality report messages.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Choosing a sending time between 00:00 and 01:00 may cause delays because the messages are received only after the batch data calculation completes.</div><br> |
      

   * Search Subscription

      Set search criteria to find quality subscription information that matches the conditions.

   * View Subscription Details

      Click the subscription name of an item to view its subscription details.

   * Edit Subscription

      Click the edit icon in the **Action** column of an item. On the Edit Quality Subscription page, modify the subscription information and click the **Confirm** button to complete the update.

   * Delete Subscription

      * Click the delete icon in the **Action** column of an item. In the confirmation dialog that appears, click the **Confirm** button to complete the deletion.

      * After selecting one or more items, click the **Batch Delete** button and then click the **Confirm** button in the popup confirmation dialog to complete the batch deletion.


<span id="_2-操作结果"></span>
## Operation Result

After creating a quality subscription, recipients receive daily quality report messages from the alarm bot at the specified time, displaying the following information:


* The total monitoring amount, operating monitor count, alarm monitor count, and alarm monitor count by type for the specified project **yesterday**.

* Top 5 monitored items with the most alarms in the specified project **this week**.

* The number of profiling tables in the specified database **yesterday** and the discovered risk items.
