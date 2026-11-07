---
title: "Renewal management"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/renewal_management"
---

The Database Transmission Service (DTS) supports the renewal of yearly/monthly subscription tasks. If you need to use the service for a long time after purchasing the yearly/monthly subscription resources, you can renew the task before it expires. This document introduces how to renew yearly/monthly subscription tasks.

<span id="prerequisites"></span>
## Prerequisites

You have created a data subscription task or a data synchronization task that is subject to yearly/monthly subscription. For more information on operations, refer to [Overview of subscription scheme](https://docs.byteplus.com/en/docs/DTS/overview_of_subscription_solutions) and [Overview of synchronization scheme](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

<span id="precautions"></span>
## Precautions


* Only data synchronization tasks and data subscription tasks in DTS support the yearly/monthly subscription.

* For bidirectional synchronization tasks, renewal needs to be performed in the forward synchronization task.

* Regardless of whether a task is suspended due to account arrears or expiration, the task will automatically restart after the account is recharged or the task is renewed.


<span id="renewal-methods"></span>
## Renewal methods

BytePlus currently provides two renewal methods: manual renewal and automatic renewal.


* Manual renewal: Before the task expires, you need to manually renew the task; otherwise, the task will affect the normal operation of the business after the resource expires.

* Automatic renewal: After enabling the automatic renewal feature, the system will automatically renew the resources before they expire, without the need for manual renewal. Once enabled, ensure that the account balance is sufficient; otherwise, it will affect the normal operation of the business.


<span id="the-procedure-is-as-follows"></span>
## **The procedure is as follows:** 

**The following introduces two renewal methods. Please choose the one that suits your needs.** 

<span id="manual-renewal"></span>
### Manual renewal


1. Log in to the [DTS Console](https://console.volcengine.com/dts/region:dts+cn-beijing/).

2. Choose one of the following methods to access the renewal page:

   * **Method 1**

      1. Select **project** and **region** in the upper left corner of the top menu bar.

      2. In the navigation pane on the left, click **Data subscription** or **Data synchronization**.

      3. On the **Data subscription** or **Data synchronization** task list page, select the target task and click **Manual renewal**.

   * **Method 2**

      1. Select **project** and **region** in the upper left corner of the top menu bar.

      2. In the navigation pane on the left, click **Data subscription** or **Data synchronization**.

      3. On the **Data subscription** or **Data synchronization** task list page, click the target task ID.

      4. In the **Billing information** pane on the **Task information** tab page, click **Renewal**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Batch renewal for multiple tasks is supported.         </div>
         

3. On the **Renewal** page, confirm the task information to be renewed (for example, task ID and current expiration date) and select the **Renewal cycle** in the lower\-left corner of the page.

   Currently, **Renewal cycle** supports **1 month**, **2 months**, **3 months**, **4 months**, **5 months**, **6 months**, **7 months**, **8 months**, **9 months**, **10 months**, **11 months**, **1 year**, **2 years**, and **3 years**. The default value is **1 months**.

4. Click **Pay**.

5. On the **Payment details** configuration wizard page, confirm the billing information for the task.

6. (Optional) Click **Coupon redemption**. In the **Coupon redemption** dialog box, enter the cash coupon redeem code and click **Redeem** for fees reduction.

7. Click **Next step**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">On the <strong>Payment completed</strong> configuration wizard page, if <strong>Payment successfully</strong> is displayed, the task is renewed successfully.   </div>
   

Execution result: After successful renewal, you can click **Manual renewal** from the **Renewal management** page of the Billing Center console to view the updated expiration date of the target task on the **Manual renewal** tab.

<span id="enabling-automatic-renewal"></span>
### Enabling automatic renewal


1. Log in to the [DTS Console](https://console.volcengine.com/dts/region:dts+cn-beijing/).

2. Choose a method to access the Automatic Renewal page as needed:

   * **Method 1**

      1. Select **Project** and **Region** in the upper left corner of the top menu bar.

      2. In the navigation pane on the left, click **Data subscription** or **Data synchronization**.

      3. On the **Data subscription** or **Data synchronization** task list page, select the target task and click **Renewal**.

   * **Method 2**

      1. Select **Project** and **Region** in the upper left corner of the top menu bar.

      2. In the navigation pane on the left, click **Data subscription** or **Data synchronization**.

      3. On the **Data subscription** or **Data synchronization** task list page, click the target task ID.

      4. In the **Payment details** pane on the **Task information** tab page, click **Renewal**.

3. Check the target task on the **Manual renewal** or **Non\-renewal upon expiration instances** tab of the **Renewal management** page, and then click **Open Auto\-renewal**.

4. Configure the following parameters on the **Auto\-renewal** page.

   
   |**Parameter** |**Description** |
   |---|---|
   |**Single automatic renewal length** |Indicates the duration of each renewal operation. Please set the automatic renewal length as needed.<br><br>Currently supports the following durations: **1 months**, **2 months**, **3 months**, **4 months**, **5 months**, **6 months**, **7 months**, **8 months**, **9 months**, **10 months**, **11 months**, **1 year**, **2 year**, and **3 year**.The default value is **1 months**. |
   |**Preset number of automatic renewals** |Check whether to automatically renew as needed. It indicates the number of times the system will perform automatic renewal operations. If not selected, automatic renewal will be permanently effective, and the system will automatically renew the resources based on the single automatic renewal length before each resource expires. The maximum is **100** times, and The default value is **1** time. |
   

5. Click **Open**.


Execution result: After successfully enabling automatic renewal, you can view the task information for automatic renewal by clicking the **Auto\-renewal** tab on the **Renewal management** page in the Billing Center console.

<span id="related-documents"></span>
## Related Documents

The principle for non\-renewal upon expiration is as follows:


* Resource tasks that are no longer in use upon expiration can be set to "Expire Without Renewal" and moved to the **Non\-renewal upon expiration instances** tab.

* Tasks that have been set to **Non\-renewal upon expiration instances** can be batch renewed, manually renewed, restored to manual renewal, or have automatic renewal enabled.

* Tasks under the **Expired** status only support batch renewal, manual renewal, and restoration to manual renewal.
