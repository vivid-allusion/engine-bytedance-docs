---
title: "Creating a TOS trigger"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/Creating_a_TOS_trigger"
---

Function service supports connecting to [Torch Object Storage](https://docs.byteplus.com/en/docs/tos/docs-what-is-tos). By creating a TOS trigger, the function service can monitor various types of events in a specified bucket, relaying the events to the user function and triggering function logic. You do not need to concern yourself with the details of how the function service obtains events, just focus on writing the function to handle them. This article introduces how to create a TOS trigger.

<span id="background-information"></span>
## Background information


* **TOS trigger mechanism and precautions**

   When a TOS event meeting the criteria occurs, TOS will send the event to FaaS; FaaS will write the event into a queue and quickly respond back to TOS, indicating the event has been received. Subsequently, an independent process reads the event from the queue, triggering the function to execute user\-defined business logic.

   * **Maximum retry count for errors**: 10 attempts, after which it will be discarded. If an error occurs during the function execution (e.g., the handler directly returns an error or a status code \>= 400), FaaS will retry the error, and you do not need to write retry logic in the code.

   * **Maximum retention time of events**: 6 hours, exceeding this will result in the events being discarded. Configure the multiple concurrent requests per instance and the maximum number of instances reasonably, to ensure that the function has sufficient performance and resources to handle event notifications.

   * **Message redelivery**: Due to the eventual consistency of the event queue, the same event may be delivered multiple times to the function. Ensure that the function code can correctly handle duplicate events.

* **TOS trigger is a bi\-directional integration trigger.** 

   For each TOS trigger created on the FaaS side, a corresponding event notification rule with the same name will be synchronized to the Torch Object Storage side. Correspondingly, for each event notification rule created on the Torch Object Storage side, a same\-named TOS trigger will be synchronized under the target function on the FaaS side.

* **A TOS event supports delivery to multiple functions.** 

   If you have such requirements, please go to the Torch Object Storage console to create event notification rules.


<span id="prerequisites"></span>
## Prerequisites


* Functions have been created based on either `vefaas-python38-default` template or `vefaas-golang-tos-trigger` template, and at least one full release has been completed. For details, refer to [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

* TOS Bucket has been created. For details, refer to [Creating a Bucket](https://docs.byteplus.com/en/docs/tos/docs-create-a-bucket).


<span id="usage-limit"></span>
## Usage limit


* Each function can support up to 20 triggers; canary releases do not support trigger creation.

* Before deleting a function, the TOS trigger must be deleted first.

* Once the TOS trigger is created, you cannot change the Bucket.

* If you need to deliver a TOS event to multiple functions, you must operate from the Torch Object Storage console.

* If a TOS event notification is bound to multiple delivery targets, only viewing and deleting are supported on the function service side; editing is not supported. If editing is needed, please proceed to the Torch Object Storage console.


<span id="procedures"></span>
## Procedures


1. Log in to the [Function Service console](https://console.byteplus.com/vefaas).

2. On the top navigation bar, select the target region.

3. On the **Function** page, select the function for which you need to create a trigger, and click the function name.

4. In the function details page, under the **Triggers** tab, click **Create trigger**.

5. In the **Create trigger** panel, set the parameters as required.

   
   |Parameter |Description |
   |---|---|
   |Trigger type |In this scenario, select TOS <trigger\></trigger\>. |
   |TOS Bucket |Torch Object Storage (TOS) Bucket is a storage space for objects. Select the TOS Bucket that the FaaS needs to monitor, with support for fuzzy search. |
   |Trigger event |Select the events that the FaaS needs to monitor; multiple selections are supported.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For scenarios monitoring file upload events, if large files are uploaded in fragments, select both <strong>tos:ObjectCreated:Put</strong> and <strong>tos:ObjectCreated:CompleteUpload</strong>. If there are no fragment uploads, simply choose <strong>tos:ObjectCreated:Put</strong> to trigger after a straightforward object upload.</div><br> |
   |Filter condition |By setting filter conditions, it is possible to precisely match the range of objects included in the events to be monitored, effectively reducing the trigger frequency and cost.<br><br><br>* **Prefix**: Set the prefix information for the object to be matched as needed.<br><br>* **Suffix**: Set the suffix information for the object to be matched as needed.<br><br>   For example: If the trigger event is `tos:Object:Created:*`, the prefix is `test/`, and the suffix is `.png`, then the function will be executed when objects in the format of png are detected being uploaded in the test direct`png are detected being uploaded in the test` directory.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Prefix and suffix are logical "AND" relationships, with matching rules being exact matches.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If neither prefix nor suffix is set, all objects within the bucket will be matched.</div><br> |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A trigger created under one Bucket must ensure semantic uniqueness, meaning the <strong>Trigger event</strong>, <strong>Prefix</strong>, and <strong>Suffix</strong> must not overlap in their matched range.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For instance: A trigger has been created, Trigger 1, to monitor events in Bucket\-A involving objects with a suffix of <code>png</code> for <code>tos:Object:Created:Put</code> event. For Trigger 2, if the event monitored includes the <code>tos:Object:Created:Put</code> event from Trigger 1, then the match object must not overlap with Trigger 1, meaning it cannot include objects with a suffix of <code>png</code>. If it does include, Trigger 2 will fail to create.   </div>
   

6. Click **Confirm** to complete the creation of the TOS trigger.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">After the TOS trigger has been successfully created, a same\-named event push rule will be synchronized under the specified Bucket in Torch Object Storage, and you can visit the <a href="https://console.byteplus.com/tos">Torch Object Storage console</a> to view it.</div>


* <div data-tips="true" data-tips-type="tip">After the TOS trigger is successfully created, it will take about 2 minutes to take effect.</div>



<span id="what-to-do-next"></span>
## What to do next


* If you need to modify the TOS trigger, refer to [Managing triggers](https://docs.byteplus.com/en/docs/faas/Managing_triggers).

* If you need to monitor the operational status of the function, refer to [Monitoring and logs](https://docs.byteplus.com/en/docs/faas/Monitoring_and_logs).
