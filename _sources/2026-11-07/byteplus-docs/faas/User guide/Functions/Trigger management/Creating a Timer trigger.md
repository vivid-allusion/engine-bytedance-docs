---
title: "Creating a Timer trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_a_Timer_trigger"
---

Timer triggers are used to schedule function logic execution. This article will guide you on how to create a Timer trigger.

<span id="prerequisites"></span>
## Prerequisites

The function must have been fully released at least once. For detailed operations, refer to [Release Function](https://docs.byteplus.com/en/docs/faas/Release_function).

<span id="usage-limit"></span>
## Usage Limit

A maximum of 20 triggers can be created for each function.

<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Functiont** page, find the function for which you need to create a trigger and click its name.

4. In the function details page, under the **Triggers** tab, click **Create Trigger**.

5. In the **Create Trigger** panel, set the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |Select Timer trigger here. |
   |Trigger name |Custom trigger name. Under the same function, trigger names cannot be duplicated. Trigger names cannot be modified after being successfully created. |
   |Push time |There are two settings available; after setting is complete, you can **click to preview the trigger time** to see the actual trigger time\-points.<br><br><br>* **Set time**: Set specific **recurrence cycles** and **trigger times**.<br><br>* **Cron expression**: Set the time using a Crontab expression. Crontab expressions consist of five parts: minute, hour, day, month, and weekday, where:<br><br>   * Minute: The value range is 0\-59. When the value is`*`it means matching any value.<br><br>   * Hour: The value range is 0 to 23. When the value is`*`it means matching any value.<br><br>   * Day: The value range is 1 to 31. When the value is`*`it means matching any value.<br><br>   * Month: The value range is 1 to 12. When the value is`*`means to match any value.<br><br>   * A certain day within a week: values range from 0 to 7. When the value is 0 or 7, it represents Sunday; when the value is`*`means to match any value.<br><br>      For example: `0 12 * * *`, triggers every day at noon. |
   |Enable immediately |Whether to enable the trigger at the same time it is created. |
   |Request concurrency |Whether to enable request concurrency for the trigger:<br><br><br>* **Enable**: If the previous request of the trigger has not completed but the time for the next request has arrived, it will handle the next request concurrently without waiting for the previous request to complete.<br><br>* **Disable**: If the previous request of the trigger was not completed, it will skip the scheduling of this request. |
   |Trigger message |The message that triggers the execution of the function can be empty. |
   |Description |Enter the remark information for the trigger; it can be empty. |
   

6. Click **Confirm** to complete the creation of the Timer trigger.


<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the Timer trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).
