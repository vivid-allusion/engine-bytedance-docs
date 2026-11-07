---
title: "Automatic and manual renewal"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/automatic-manual-renewal"
---

A subscription instance has an expiring date. Renew the instance promptly before it is closed and deleted to avoid affecting your business due to instance expiration. This topic introduces how to enable automatic renewal and manual renewal.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Target subscription instances must meet at least one of the following conditions:


* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

* The instance status is **Closed**, but it has not been forcibly deleted.

   After a subscription instance expires, it will be retained for a period of time but not deleted immediately, and you will need to renew it before it is forcibly deleted. For more information about instance expiration, refer to [Expiration](https://docs.byteplus.com/en/docs/mongodb/arrears-and-expiration#.5Yiw5pyf6K-05piO).


<span id=".6Ieq5Yqo57ut6LS5"></span>
## Enable automatic renewal

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on auto\-renewal rules for billing center, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-auto-renewal-rules">Auto\-renewal rules</a>.</div>



1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. You can go to the **Enable auto\-renewal** page via any of the methods below.

   
   |Method description |Procedure |
   |---|---|
   |Enter through the MongoDB instance list page |1. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.<br><br>2. On the target instance type list page, click the name of the target instance.<br><br>3. On the **Summary** tab, in the **Billing information** area, click **Enable** next to **Automatic renewal**. |
   |Enter through the upper right corner navigation |1. In the upper right corner of the console, click the user's image and select **Billing.** <br><br>2. In the left navigation bar of the **Billing center** page, select **Renewal management.** <br><br>3. On the **Renewal management** page, use the search and filtering functions to find the target MongoDB instance in **Manual renewal ** or **Non\-renewal upon expiration instances** tab.<br><br>4. Select the target instances, then click **Enable auto\-renewal** below the instances list.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also select multiple instances to enable the automatic renewal feature in batches.</div><br> |
   

4. on the **Enable auto\-renewal** page, in the **Confirm renewal information** area, confirm the information about the instance to be renewed (such as the instance ID and the current expiration time), and then configure the following parameters according to your business needs.

   
   |Parameter |Description |
   |---|---|
   |Set interval for auto\-renewal |The length of each renewal. The available lengths are listed below:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years. |
   |Set auto\-renewal times |You can choose the number of auto\-renewals according to your business needs with the following range of values:<br><br><br>* **Unlimited**.<br><br>* **Custom**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If <strong>Custom</strong> is selected, you must also set the specific number of times. You can set a maximum of 100 automatic renewals each time.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the custom count is used up, it will revert to manual renewal. Proceed with caution.   </div><br>    |
   

5. Click **Enable**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the <strong>Auto\-renewal</strong> tab, you can check the details about the instances for which the auto renewal function has been successfully enabled, such as expiration time, renewal cycle, and so on.   </div>
   

<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For details on manual renewal rules for billing center, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-manual_renewal_rules">Manual renewal rules</a>.</div>



1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. You can go to the **Renew** page via any of the methods below.

   
   |Method description |Procedure |
   |---|---|
   |Enter through the MongoDB instance list page |1. In the upper\-left corner of the top menu bar, select the project and region for instance.<br><br>2. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.<br><br>3. On the target instances page, according to the actual business situation, choose to renew a single instance or renew instances in batchs.<br><br>   * Renew single instance<br><br>      On the target instances page, locate the target instance, and select  **... \> Renew** in the right\-side **Actions** column.<br><br>   * Renew instances in batchs<br><br>      On the target instances page, select the target instances for renewal, and at the bottom of the list, select  **... \> Renewal**.<br><br>      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Only subscription instances with <strong>Running</strong> status can be selected for batch renewal. For more details, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/instance-status">Instance status</a>.      </div><br>      <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">A maximum of 100 instances can be renewed at the same time.      </div><br>       |
   |Enter through the upper right corner navigation |1. In the upper right corner of the console, click the user's image and select **Billing**.<br><br>2. In the left navigation bar of the **Billing center ** page, select **Renewal management.** <br><br>3. On the **Renewal management** page, use the search and filtering functions to find the target MongoDB instance in the **Auto\-renewal**, **Manual renewal** or **Non\-renewal upon expiration instances** tab.<br><br>4. In the **Actions** column to the right of the target instance, click **Renew**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also select multiple instances, then click <strong>Batch renew</strong> below the instance list to renew multiple instances simultaneously.   </div><br>    |
   

3. On the **Renew** page, first confirm the instance information to be renewed (such as instance ID and current expiration time) in the **Renewal confirmation** area. Then, in the **Renewal cycle** area, configure the following parameters according to your business needs.

   
   |Renewal cycle |Description |
   |---|---|
   |Specifying purchase period |Supports renewing instances by the whole month or the whole year. The available durations are as follows:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also check <strong>Set all expiration dates to</strong> and set the renewal expiration date. After the setting is completed, it will take effect on all monthly subscribed (non\-natural month) instances involved in this renewal operation. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day">Unified expiration day</a>.</div><br> |
   |Specifying an expiration time |Supports specifying the specific year, month, and day when the instance expires. After renewal, the expiration times of the instances involved in this operation will be exactly the same.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After specifying the expiration time, the expiration times of all the instances involved in this renewal operation will be exactly the same. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time">Specifying expiration time</a>.</div><br> |
   

4. In the lower\-right corner of the page, click **Pay**.

5. On the **Confirm order information** page, confirm the order details, and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After successful renewal, you can return to the Instances page to check the new expiration time of the target subscription instance.   </div>
