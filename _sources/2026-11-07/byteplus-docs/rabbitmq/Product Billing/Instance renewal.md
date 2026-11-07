---
title: "Instance renewal"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Instance_renewal"
---

You can enable automatic renewal or manually renew your subscription\-based instance before it expires to avoid service interruptions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance must be running or stopped.

* The instance payment mode is subscription\-based.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Note

Only subscription\-based instances support renewal. Pay\-as\-you\-go instances require no renewal but a sufficient available account balance. For more information, please see [Description of arrears or expiration](https://docs.byteplus.com/en/docs/rabbitmq/Description_of_arrears_or_expiration).

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background information

The message queue for RabbitMQ supports the following two renewal methods:


* **Automatic renewal**: You can enable the automatic renewal feature when creating new annual or monthly instances to avoid any potential disruption to your business due to forgetting to manually renew the instance before its expiration. Once enabled, the system will automatically renew the instance before each expiration. Please ensure your account has sufficient available balance.

* **Manual renewal**: You can manually renew your instance at any time before it expires.


<span id=".5byA6YCa6Ieq5Yqo57ut6LS5"></span>
## Enable automatic renewal


1. Log in to [BytePlus console](https://console.byteplus.com/home).

2. In the upper right corner of the console, select **Billing\> Renewal management**.

3. On the **Renewal management** page, use the search and filter function to find the target instances in the **Manual renewal** or **Non\-renewal upon expiration** tabs.

4. In the **Actions** column corresponding to the target instance, click **Enable auto\-renewal**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select multiple instances and click <strong>Enable auto\-renewal</strong> at the bottom of the page to enable the automatic renewal feature in bulk.   </div>
   

5. On the **Auto\-renewal** page, confirm the instance information that needs renewal (such as instance ID, current expiration time, etc.) and configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Interval for auto\-renewal. |Interval of the renewal action for each action. Optional durations are as follows:<br><br><br>* **Monthly renewal**: 1 to 11 months.<br><br>* **Annual renewal**: 1 to 3 years. |
   |Preset the frequency of automatic renewals |You can select this configuration and set the frequency of automatic renewal operations.<br><br><br>* **Unlimited**: Default setting The system will perform automatic renewal operations based on the duration of each automatic renewal before each resource expires.<br><br>* **Custom frequency**: Set the auto\-renewal times to a custom value, with a maximum limit of 100. After the custom times are used up, it will switch to manual renewal. |
   

6. Click **Confirm** to proceed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After enabling, you can view the details of instances with automatic renewal enabled, such as expiration time and renewal cycle, under the <strong>Renewal management</strong> tab on the <strong>Auto\-renewal</strong> page.   </div>
   

<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal


1. Log in to [BytePlus console](https://console.byteplus.com/home).

2. In the upper right corner of the console, select **Billing\> Renewal management**.

3. On the **Renewal management** page, use the search and filter function to find the target instances in the **Manual renewal** or **Non\-renewal upon expiration** tabs.

4. In the **Actions** column on the right side of the target instance, click **Renew**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select multiple instances and click <strong>Batch renewal</strong> below the instance list to renew several instances at once.   </div>
   

5. On the **Renewal confirmation** page, confirm the information of the instance you need to renew (such as instance ID, current expiry date, etc.), and select the renewal duration at the bottom left corner of the page.

6. Click **To Pay** at the bottom right corner of the page.

7. On the **Confirm order information** page, confirm the order details and click **Next step** to proceed.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After successful renewal, you can view the new expiration date of the target subscription instance under the <strong>Manual renewal</strong> tab on the <strong>Renewal management</strong> page.   </div>
