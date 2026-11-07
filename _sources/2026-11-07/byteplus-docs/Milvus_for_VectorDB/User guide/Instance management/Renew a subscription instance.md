---
title: "Renew a subscription instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Renew_a_subscription_instance"
---

You can renew a subscription instance anytime from the creation of the instance until 15 days after the instance expires. This topic describes how to renew a subscription instance.

## Prerequisites

A subscription Dedicated instance is created. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Precautions

Subscription instances will be forcibly deleted 15 days after expiration, and cannot be renewed or recovered. Renew promptly if needed.

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region of the instance in the top menu bar.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instances** list, select the **Dedicated** tab, then enter the **Renew** page by one of the following methods.

   * Select  **... \> Renew** on the right of the target subscription instance.

   * Click the name of the target subscription instance to enter the **Instance details** page, then click **Renew** to the right of **Billing type** in the **Billing information** section.

5. On the **Renew** page, confirm the instance information to be renewed (such as instance ID, current expiration time, etc.) in the **Renewal confirmation** area, then configure the following parameters in the **Renewal cycle** area according to business needs.

   |Renewal period |Description |
   |---|---|
   |Purchase duration |Supports renewing instances by full months or years. Available durations are as follows:<br><br><br>* Monthly renewal: 1 to 11 months.<br><br>* Yearly renewal: 1 to 3 years.<br><br><br>> **tip**<br><br><br>> You can also select **Set all expiration dates to** a unified enewal expiration date. Once set, this applies to all monthly (non\-calendar month) subscription instances affected by this renewal. For more details, see [Unified expiration date](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unified_expiration_day).<br> |
   |Specify expiration date |Supports specifying the exact year, month, and day for instance expiration. After renewal, the expiration time for all instances in this operation will be exactly the same.<br><br>> **tip**<br><br><br>> After setting the expiration time, all instances involved in this renewal will share the same expiration time. For more information, see [Specifying an expiration time](https://docs.byteplus.com/en/docs/byteplus-platform/docs-specifying-an-expiration-time).<br> |

6. Click **Pay** in the lower right corner of the page.

7. On the **Confirm order information** page, review the order details and click **Next step**.

   > **tip**

   > After successful renewal, you can return to the instance list page to check the new expiration time of the target subscription instance.
