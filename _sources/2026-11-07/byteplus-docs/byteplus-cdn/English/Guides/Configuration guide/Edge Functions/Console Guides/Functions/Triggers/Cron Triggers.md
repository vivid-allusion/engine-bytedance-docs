---
title: "Cron Triggers"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cron-triggers"
---

This document describes how to configure a Cron trigger for a function.

You can create a Cron trigger to set up periodic tasks. The Cron trigger will automatically trigger the cron event in the function code at specified times. You need to listen for and handle the cron event in your code.

<span id="create-a-cron-trigger"></span>
## Create a Cron trigger

Follow these steps to create a Cron trigger.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page.

2. Find the function for which you want to create a Cron trigger and click on the function name.

3. Select the **Triggers** tab, then select the **Cron** tab.

4. Click **Create Cron trigger**.

5. In the **Create Cron trigger** dialog box, fill in the relevant configurations referring to the table below, then click **Save** to complete.



|Parameter |Description |
|---|---|
|Name |Enter the name of the Cron trigger. The naming rules are as follows:<br><br><br>* Can only contain English letters, numbers, and hyphens (\-).<br><br>* Cannot exceed 128 characters. |
|Scheduling type |Select the edge node where the cron event will be triggered.<br><br><br>* **Global**: The cron event is triggered on all edge nodes.<br><br>* **Single Point**: The cron event is triggered on a random edge node. |
|Execution time |The time when the cron event is triggered. After configuration, you can check if it meets your expectations in the **Estimated execution time (UTC)**  on the right.<br><br><br>* **Cron expression**: Enter a Cron expression, see [Supported Cron Expressions](https://docs.byteplus.com/en/docs/18/17378#supportedcron).<br><br>* **Custom**: Select **Execution frequency** and **Execution time**, and Edge Functions will automatically generate the corresponding Cron expression. |
|Parameter |Enter custom parameters. During function execution, Edge Functions passes this parameter to [CronEvent](https://docs.byteplus.com/docs/byteplus-cdn/docs-CronEvent). |


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_56e1aa502ebe9824dad3d378500bdd81.jpeg) </span>


6. After creating the Cron trigger, to ensure it takes effect, you also need to:

   * Ensure that the status of the Cron trigger is **Enabled**.

      <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_59e152a187fe6479609f5a84d73be657.jpeg) </span>

   * Listen for the cron event in the function code. The example code below shows how to register an event listener to listen for cron events and call a callback function to implement scheduled tasks when the cron event is triggered.

      ```JavaScript
      // Register an event listener to listen for cron event
      addEventListener('cron', onCron);
      
      // Function to be called when cron event fires
      async function onCron(event) {
        // Code logic of the scheduled task
          return 'this is log';
      }
      ```
      


&nbsp;

<span id="supported-cron-expressions"></span>
### Supported cron expressions

A Cron expression is a string composed of 5 fields. These fields are separated by spaces. Cron expressions run in the UTC+8:00 time zone by default.

**Cron expression field description**


|First field |Second field |Third field |Fourth field |Fifth field |
|---|---|---|---|---|
|Minute |Hour |Day |Month |Week |


Each field has its corresponding value range:


|Field |Value range |Allowed special characters |
|---|---|---|
|Minute |Integers 0\-59 |,\-\*/ |
|Hour |Integers 0\-23 |,\-\*/ |
|Day |Integers 1\-31 (consider the number of days in the month) |,\-\*?/L |
|Month |Integers 1\-12 or case\-insensitive three\-letter abbreviations of months ("JAN", "aug", etc.) |,\-\*/ |
|Week |Integers 0\-6 or case\-insensitive three\-letter abbreviations of weekdays ("MON", "fri", etc.). 0 represents Sunday, 1 represents Monday, and so on. |,\-\*?/L |


**Special characters**


|Character |Meaning |Description |
|---|---|---|
|\* (Asterisk) |Represents all values in the field |For example, in the "Minute" field, it means execute every minute. |
|, (Comma) |Specifies multiple values |For example, in the "Week" field, "MON,WED,FRI" means "Monday, Wednesday, and Friday". |
|\- (Hyphen) |Specifies a range |For example, in the "Hour" field, "10\-12" means "from 10 o'clock to 12 o'clock". |
|? (Question mark) |Represents an uncertain value |Used in combination with other specified values. For example, if you specify a particular date of each month but don't need to care about which day of the week it is, then you can use ? in the "Week" field. |
|/ (Forward slash) |Represents an increment, n/m means start from n and increment by m each time |For example, in the "Minute" field, 1/3 means start from 1 minute and execute every 3 minutes. |
|# (Hash) |Represents the nth weekday of each month, can only appear in the "Week" field |Used in combination with other specified values. For example, in "Week", 5#2 means the second Friday of the month, where 5 represents Friday and 2 represents the second. |
|L (Uppercase L) |Represents the last, can only appear in the "Day" and "Week" fields |For example, in the "Day" field, it means the last day of each month. Using 5L in the "Week" field means trigger on the last Friday. |


**Examples**


|Cron Expression |Description |
|---|---|
|\* \* \* \* \* |Execute once every minute |
|\* /30 \* \* \* \* |Execute once every 30 minutes |
|\* 23 \* \* \* |Execute every minute at 23:00 daily |
|10,20,30 \* \* \* \* |Execute at 10 minutes, 20 minutes, and 30 minutes of every hour |
|30 7 \* \* MON\-FRI |Execute at 7:30 every day from Monday to Friday |
|0 8 1 \* \* |Execute at 8:00 on the first day of each month |
|0 8 \* JAN\-JUN \* |Execute at 8:00 every day from January to June |


<span id="view-schedule-records"></span>
## View schedule records

Follow these steps to view the schedule records of a Cron trigger. Currently, you can only view the schedule records for the last 6 months.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page. Find the function you want to view and click on the function name.

2. Select the **Triggers** tab, then select the **Cron** tab.

3. In the **Cron triggers** list, find the Cron trigger you want to view, click on the trigger name to enter the **Schedule records** page.

4. On the **Schedule records** page, view the schedule record information, including execution expression, parameters, status, creation time, etc. You can also search for specific records using the **Cron expression** and **Parameter** fields.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_14e74f990bf2f356c20262c0d0e0578e.jpeg) </span>

5. Click **View log** to see the detailed logs of function execution on various nodes.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dd9fefc26e001b539c69c37003eade1f.jpeg) </span>


<span id="enable-or-disable-a-cron-trigger"></span>
## Enable or disable a Cron trigger

You can enable or disable a Cron trigger. The change in the Cron trigger's status takes effect immediately, and you don't need to republish the function.


1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page. Find the function you want to view and click on the function name.

2. Select the **Triggers** tab, then select the **Cron** tab.

3. Find the Cron trigger you want to enable or disable, click the switch in the **Status** column to toggle the enable status of the Cron trigger.


<span id="delete-a-cron-trigger"></span>
## Delete a Cron trigger

If you no longer need a Cron trigger, you can delete it.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once a Cron trigger is deleted, it cannot be recovered. Please operate with caution.</div>



1. Open the [Functions](https://console.byteplus.com/cdn/edge-function/list) page. Find the function you want to delete and click on the function name.

2. Select the **Triggers** tab, then select the **Cron** tab.

3. Find the Cron trigger you want to enable or disable, click **Delete** in the **Actions** column.

4. In the pop\-up window, confirm the Cron trigger to be deleted, and click the **OK** button to complete the operation.
