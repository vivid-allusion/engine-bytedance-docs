---
title: "Instance renewal"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/renewal"
---

To avoid any impact on your business due to instance expiration, you can enable automatic renewal or manually renew your subscription instances before they expire.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Before you begin**


* Verify that your instance is running or stopped.

* Verify that the billing method of your instance is subscription.


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**

You can renew only subscription instances. For pay\-as\-you\-go instances, you do not need to renew them but make sure that the available balance in your BytePlus account is sufficient. For more information, refer to [Overdue payments](https://docs.byteplus.com/en/docs/cloudsearch/overdue).

<span id=".6IOM5pmv5L-h5oGv"></span>
## **Background information**

Cloud Search supports the following two renewal methods:


* **Automatic renewal**: You can enable automatic renewal when you create a subscription instance. This prevents your instance from being automatically released upon expiration and ensures business continuity. Once automatic renewal is enabled, your instance can be renewed automatically before expiration. Make sure that the available balance in your BytePlus account is sufficient.

* **Manual renewal**: You can manually renew your instance at any time before it expires.


<span id=".6Ieq5Yqo57ut6LS5"></span>
## **Automatic renewal**


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. On the upper\-left corner of the top menu bar, select the Region to which your instance belongs.

3. On the upper\-right corner of the console, select **Billing \> Renewal management**.

4. On the **Renewal management** page, use the search filter feature to find the Cloud Search instance that you want to renew on the **Manual renewal** or **Non\-renewal upon expiration instances** tab.

5. Check the instance, and click **Enable auto\-renewal** below the instance list.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also check multiple instances to enable automatic renewal for them at a time.   </div>
   

6. On the **Enable auto\-renewal** page, configure the following parameters.



|**Parameter** |**Description** |
|---|---|
|Set single auto\-renewal duration |Specify the duration of the renewal period for each renewal. Valid values:<br><br><br>* Renewal by month: 1 month–11 months<br><br>* Renewal by year: 1 year–3 years |
|Set auto\-renewal times |Select this parameter and set the number of automatic renewals.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">说明</div><br><br><br><div data-tips="true" data-tips-type="tip">If you do not set the number of automatic renewals, automatic renewal is permanently effective. The system performs an automatic renewal each time before the resource expires based on the setting of single auto\-renewal duration.</div><br> |



6. Click **Enable**.

   You can view details, such as expiration time and renewal period, of the instance for which you have enabled automatic renewal on the **Automatic renewal** tab.


<span id=".5omL5Yqo57ut6LS5"></span>
## **Manual renewal**


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. On the upper\-left corner of the top menu bar, select the Region to which your instance belongs.

3. Go to the **Renew** page by using one of the following methods:

   * **Method 1**

      * On the upper\-right corner of the console, select **Billing \> Renewal management**.

      * On the **Renewal management** page, use the search filter feature to find the Cloud Search instance that you want to renew on the **Manual renewal** or **Non\-renewal upon expiration instances** tab.

      * In the **Operations** column on the right side of the instance, click **Renew**.

         You can also check multiple instances and click **Batch renew** below the instance list to renew them at the same time.

   * **Method 2**

      * On the **List of Instances** page, click the name of the target instance.

      * Click the **Instance information** tab, go to **Payment information \> Billing type**, then click **Renewal fee**.

4. On the **Renew** page, confirm the information of the instance that you want to renew, such as the instance ID and the current expiration time. On the lower\-left corner of the page, select a renewal period.

5. On the lower\-right corner of the page, click **Pay**.

6. On the **Confirm order information** page, confirm the order details and click **Next step**.

   After finishing the renewal steps, you can return to the **List of Instances** page and view the expiration time of the renewed subscription instance.
