---
title: "Switch from Pay-As-You-Go to Subscription"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Switch_from_Pay-As-You-Go_to_Subscription"
---

E\-MapReduce (EMR) clusters provide the ability to switch from **pay\-as\-you\-go** to **Subscription** billing, making it easy for you to convert temporary pay\-as\-you\-go clusters into long\-term, stable Subscription clusters. This allows you to reserve resources in advance and maximize cost savings.

This document provides instructions on converting a pay\-as\-you\-go cluster to a Subscription cluster in the EMR console.

<span id="41ee6a44"></span>
## **Prerequisites**

Pay\-as\-you\-go clusters to be converted must meet the following conditions:


* The ECS instances in the node are not of any instance types that have already been discontinued.

* The cluster status is **Running**.

* Clusters are purchased using the **pay\-as\-you\-go** model.

* There is no outstanding balance on the account. If the account is in arrears, you must first pay the outstanding amount and initiate the conversion when the cluster is in the **Running** state.


<span id="4a871d96"></span>
## **Limitations**


* Once a pay\-as\-you\-go cluster is converted to subscription, it cannot be converted back to pay\-as\-you\-go. Please operate with caution to avoid cost wastage.


<span id="13b34500"></span>
## **Procedures**


1. Log in to the **EMR Console**.

2. In the left navigation bar, click **Resources \> on ECS** to go to the cluster list page.

3. Confirm the target Pay\-As\-You\-Go cluster. In **Action**, click the  **...**  button, and select **Switch to subscription** from the dropdown list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e5df69d21e7e48b69a016b4c45e720a8~tplv-goo7wpa0wc-image.image) </span>

4. On the Pay\-As\-You\-Go to Subscription conversion page, perform the appropriate conversion as needed.

   * Task node groups can be converted accordingly based on actual requirements.

   * Select the conversion duration, and agree to the "[EMR Service Terms](https://docs.byteplus.com/en/docs/E-MapReduce/on_ECS_Terms_BytePlus_EMR_on_ECS_Service_Level_Agreement)".

5. Click the **OK** button to complete the switching of payment and billing methods.
