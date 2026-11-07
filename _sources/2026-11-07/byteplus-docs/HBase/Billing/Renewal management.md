---
title: "Renewal management"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Renewal_management"
---

You can enable automatic renewal for your subscription instance or renew it manually before it expires to avoid business impacts caused by expiration.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Pay\-as\-you\-go instances have no expiration date and do not require renewal. You only need to ensure that your account has sufficient available credit.

* Subscriptions have expiration dates. Failure to renew subscriptions before the expiration date can result in business interruption or even data loss. For more details, see the [Arrears and expiration](https://docs.byteplus.com/en/docs/HBase/Arrears_and_expiration).


<span id=".57ut6LS55pa55byP"></span>
## Renewal method

Table Storage for HBase supports the following two renewal methods:


* **Manual renewal**: You can manually renew your instance at any time before it expires.

* **Automatic renewal**: You can enable automatic renewal when creating a subscription instance. You can also enable automatic renewal at any time when using the instance to avoid affecting business due to instance expiration if you forget to renew it manually. Once it is enabled, the system will automatically renew the instance before expiration each time, so please make sure that your account has a sufficient balance.


<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. You can go to the **Renew** page via any of the methods below.

   * **Method 1**

      1. In the upper\-right corner of the console, choose **Billing \> Renewal management**.

      2. On the **Renewal management** page, use the search and filtering functions to find the target instance in the **Manual renewal** tab.

      3. In the **Actions** column to the right of the target instance, click **Renewal**.

   * **Method 2**

      On the **Instances** page, click **Renew** in the **Actions** column to the right of the target instance.

   * **Method 3**

      1. On the **Instances** page, click the name of the target instance.

      2. On the **Summary** tab, in the **Billing information** area, click **Renewal** after **Billing method.** 

4. On the **Renewal** page, confirm the instance information to be renewed and configure the following parameters in the **Renewal cycle** area according to business needs.

   
   |Renewal cycle |Description |
   |---|---|
   |Specifying purchase period |Supports renewing instances by the whole month or the whole year. The available durations are as follows:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Yearly renewal: 1 to 3 years.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also check the option of <strong>Unified expiration date</strong> and set the renewal expiration date. After the setting is completed, it will take effect for all monthly subscribed (non\-natural month) instances involved in this renewal operation. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day">Unified expiration day</a>.</div><br> |
   |Specifying an expiration time |Supports specifying the specific year, month, and day when the instance expires. After renewal, the expiration times of the instances involved in this operation will be exactly the same.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After specifying the expiration time, the expiration times of all the instances involved in this renewal operation will be exactly the same. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time">Specifying an expiration time</a>.</div><br> |
   

5. Click **Pay** in the bottom right corner of the page.

6. Confirm the order details on the **Confirm order** page and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After successful renewal, you can return to the <strong>Instances</strong> page to check the new expiration time of the target subscription instance. There may be a certain delay in updating the expiration time. It is recommended that you wait for a while before refreshing to confirm.   </div>
   

<span id=".6Ieq5Yqo57ut6LS5"></span>
## Activating automatic renewal


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. You can go to the **Renew** page via any of the methods below.

   * **Method 1**

      1. On the **Instances** page, click the name of the target instance.

      2. On the **Summary** tab, in the **Billing information** area, click **Enable** after **Automatic renewal**.

   * **Method 2**

      1. In the upper\-right corner of the console, choose **Billing \> Renewal management**.

      2. On the **Renewal management** page, use the search and filtering functions to find the target Redis instance in the **Manual renewal** 、**Auto\-renewal** or **Non\-renewal upon expiration instances** tab.

      3. In the **Actions** column to the right of the target instance, click **Enable auto\-renewal**. Alternatively, select multiple target instances and click **Enable auto\-renewal** at the bottom of the page.

4. On the **Enable auto\-renewal** page, first confirm the instance information to be renewed (such as instance ID, current expiration date, etc.) in the **Auto\-renewal confirmation** area, and configure the following parameters according to your business needs.

   
   |Parameter |Description |
   |---|---|
   |Set interval for auto\-renewal |The length of each renewal. The available lengths are listed below:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Yearly renewal: 1 to 3 years. |
   |Set auto\-renewal times |You can choose the number of auto\-renewals according to your business needs with the following range of values:<br><br><br>* **Unlimited**.<br><br>* **Custom**. If Custom is checked, you will also need to set a specific number of times, up to a maximum of 100 auto\-renewals at a time.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once the customized number of times is used up, it will be changed to manual renewal, be careful with it.   </div><br>    |
   

5. Click **Enable**.
