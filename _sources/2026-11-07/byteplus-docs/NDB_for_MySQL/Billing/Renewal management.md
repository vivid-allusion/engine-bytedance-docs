---
title: "Renewal management"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Renewal_management"
---

You can enable automatic renewal or manually renew a yearly/monthly subscription instance before it expires to prevent your business from being affected by its expiration.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Pay\-as\-you\-go instances do not have an expiration date and do not require renewal. Ensure your account has a sufficient balance.

* Yearly/monthly subscription instances have an expiration date. Failure to renew upon expiration will lead to business interruption and even data loss. For more details, see [Arrears and expiratio](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Arrears_and_expiration)n.

* You can select a maximum of 100 instances with the Calculate billing type as yearly/monthly subscription for batch renewal at one time.


<span id=".57ut6LS55pa55byP"></span>
## Renewal methods

 NDB for MySQL support the following two renewal methods.


* **Manual renewal**: You can manually renew your instance at any time before it expires.

* **Automatic renewal**: You can enable automatic renewal when creating a new yearly/monthly subscription instance or enable it for the instance at any time after creation. Once it is enabled, the system will automatically renew the instance before expiration each time, so please make sure that your account has a sufficient balance. This prevents your business from being affected by an expired instance if you forget to renew it manually.


<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. You can access the **Renewal** page in any of the following ways.

   * **Method 1**

      1. In the upper\-right corner of the console, select **Billing \> Renewal management**.

      2. On the **Renewal management** page, use the search and filter function to find the target instance on the **Manual renewal**, **Auto\-renewal**, or **Non\-renewal upon expiration instances** tab.

      3. In the **Actions** column for the target instance, click **Renew**. Or select multiple target instances and click **Batch renew** at the bottom of the page.

   * **Method 2**

      On the **Instance list** page, click **Renewal** in the **Actions** column for the target subscription instance.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can select multiple instances simultaneously on the <strong>Instance list</strong> page by choosing <strong>...</strong> <strong>\> Renewal</strong> at the bottom of the page.      </div>
      

   * **Method 3**

      1. On the **Instance list** page, click the name of the target instance.

      2. On the **Instance information** tab, in the **Billing information** section, click **Renewal** next to **Calculate billing type**.

4. On the **Renewal** page, confirm the information of the instance to be renewed, and configure the following parameters in the **Renewal period** section based on business needs.

   
   |Renewal period |Description |
   |---|---|
   |Specifying purchase period |You can renew instances by the full month or year, with the following options:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also check <strong>Set all expiration dates to</strong> and set the renewal expiration date. After the setting is completed, it will take effect on all monthly subscribed (non\-natural month) instances involved in this renewal operation. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day">Unified expiration day</a>.</div><br> |
   |Specifying an expiration time |Supports specifying the specific year, month, and day when the instance expires. After renewal, the expiration times of the instances involved in this operation will be exactly the same.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After specifying the expiration time, the expiration times of all the instances involved in this renewal operation will be exactly the same. For more details, refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time">Specifying an expiration time</a>.</div><br> |
   

5. In the lower\-right corner of the page, click **Pay**.

6. On the **Confirm order information** page, confirm the order details, and click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the payment is completed, you can return to the <strong>Instance list</strong> page to check if the expiration time of the target instance has been successfully changed. The expiration time update may be delayed. Wait for a moment and refresh to confirm.   </div>
   

<span id=".6Ieq5Yqo57ut6LS5"></span>
## Automatic renewal


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-right corner of the console, select **Billing \> Renewal management**.

3. On the **Renewal management** page, use the search and filter function to find the target instance on the **Manual renewal**, **Auto\-renewal**, or **Non\-renewal upon expiration instances** tab.

4. In the **Actions** column for the target instance, click **Enable auto\-renewal**. Or, select multiple target instances and click **Enable auto\-renewal** at the bottom of the page.

5. on the **Enable auto\-renewal** page, in the **Confirm renewal information** area, confirm the information about the instance to be renewed (such as the instance ID and the current expiration time), and then configure the following parameters according to your business needs.

   
   |Parameter |Description |
   |---|---|
   |Set interval for auto\-renewal |The duration for each renewal operation. The optional durations are as follows:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Annual renewal: 1 to 3 years. |
   |Set auto\-renewal times |You can choose the number of auto\-renewals according to your business needs with the following range of values:<br><br><br>* **Unlimited**.<br><br>* **Custom**. You can set a maximum of 100 automatic renewals each time.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After the custom count is used up, it will revert to manual renewal. Proceed with caution.   </div><br>    |
   

6. Click **Enable**.
