---
title: "Batch instance renewal"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/batch_instance_renewal"
---

RDS for MySQL supports batch renewal. You can renew multiple yearly/monthly subscription instances at a time. This topic describes how to batch renew instances.

<span id="prerequisites"></span>
## Prerequisites

The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id="precautions"></span>
## Precautions


* Only yearly/monthly subscription instances can be batch renewed.

* When you batch renew instances, the renewal duration of each instance must be the same.

* The instances cannot have unpaid orders for conversion to yearly/monthly subscription.

* A maximum of 100 instances can be renewed at the same time.


<span id="procedure"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If no project is set, you should select the option <strong>Account's all resource</strong> at this step.</div>



3. On the **Instances** page, select multiple instances with a **Billing method** of **Subscription**.

4. In the lower\-left corner of the **Instances** page, choose  **...**  \> **Renewal**.

5. Confirm the information about the instances to be renewed on the renewal management page.

6. Select the **Renewal duration**, and then click the **Pay** button.

7. On the **Confirm order information** page, confirm the order information and click **Next step**.

8. On the **Submit payment information** page, confirm the payment details and select the payment method, click **Pay**, and complete payment according to the prompts to complete renewal.
