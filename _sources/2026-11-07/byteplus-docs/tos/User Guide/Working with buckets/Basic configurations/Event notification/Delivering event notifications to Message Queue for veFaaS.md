---
title: "Delivering event notifications to Message Queue for veFaaS"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configuring-event-notifications"
---

This text outlines the specific steps for setting event notification rules in TOS.

<span id="9ac8c418"></span>
## Background Information

[Event Notification Overview](https://docs.byteplus.com/docs/tos/Event-notification-overview)

<span id="6ac17ec0"></span>
## Prerequisites

A function service has been created and published based on the **vefaas\-golang\-tos\-trigger** template. For details, see [Create Function](https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection) and [Release function](https://docs.byteplus.com/en/docs/faas/Release_function).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Asynchronous functions do not support receiving TOS events. When creating a function for the event notification feature, do not enable asynchronous tasks.</div>


<span id="94f57ff5"></span>
## Precautions


* A bucket can create a maximum of 30 event notification rules.

* An object cannot match multiple rules containing the same event type. That is, in the same bucket, different rules cannot have overlapping combinations of **type + prefix or suffix** scope.


<span id="5cba4525"></span>
## Action Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation bar, select **Basic configurations \> Event notification**. On the **Event notification** page, click **Create rule**.

4. On the **Create event notification** page, configure the following parameters.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |Basic Settings |Event Name |Set the name of the event notification with the following naming conventions:<br><br><br>* Event names created under the same bucket must not be duplicated.<br><br>* Length must not exceed 255 characters. |
   ||Prefix |Set the prefix information to match the desired object.<br><br>For example, setting the prefix to **test/**  filters objects under the `test` directory. |
   ||Suffix |Set the suffix information for the object to be matched.<br><br>For example, if the suffix is set to  **.png**, it will filter all objects with the format `png`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If neither prefix nor suffix is set, all objects within the storage bucket will be matched.</div><br> |
   |Event type |Events |Select the events you want to be notified about. TOS supports the following event list, see [Supported event types](https://docs.byteplus.com/docs/tos/Event-notification-overview#a4b7f029).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you choose the same event type in different rules, the range of objects that match this event type must not overlap; that is, an object cannot match multiple rules that contain the same event type.</div><br><br><br><div data-tips="true" data-tips-type="warning">For example, if you create Rule A to set PutObject event notifications for objects with the suffix png, then objects with the suffix png cannot be included in the matching objects for the PutObject event in Rule B. Including them will cause rule creation to fail.<code>png, then objects with the suffix png cannot</code> be included in the matching objects for the PutObject event in Rule B. Including them will cause rule creation to fail.<code>png cannot be included in the matching objects for the PutObject event in Rule B. Including them will cause rule creation to fail.</code></div><br> |
   |&nbsp;<br><br>Data target |Target type |Select **Function service**. |
   ||Function service |Select the function service you need to deploy. Click **Add a row** to select multiple function services, up to a maximum of 5 function services.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not have an available function service, you can log in to the Function Service Console to create one. For detailed steps, please see <a href="https://docs.byteplus.com/en/docs/faas/Function_Creation_Option_Selection">Create Function</a>.</div><br> |
   

5. Click **Confirm**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once the event notification rules are created, the target function service will automatically create a trigger with the same name as the event. You can log in to function service console and click the target function service to view it.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the event notification rules are created, they will take effect in 5 minutes.   </div>
   


<span id="3d109db4"></span>
## Other Operations


* Edit event notification rule: click **Edit** in the **Action** column of the target rule to modify the event notification rule.

* Delete event notification rule: click **Delete** in the Action column of the target rule. In the pop\-up dialog, click **Delete** to remove the event notification rule.
