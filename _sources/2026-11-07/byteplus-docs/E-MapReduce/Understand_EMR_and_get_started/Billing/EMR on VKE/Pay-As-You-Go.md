---
title: "Pay-As-You-Go"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_pay_as_you_go"
---

By reading this article, you can quickly learn about the billing resources for EMR on VKE and information about related product billing.

<span id="c99a949d"></span>
## **Restrictions**


* You must first complete before you begin for your Byteplus account before purchasing EMR on VKE.

* Before purchasing, ensure that your account balance (that is, cash balance) is greater than or equal to 0 yuan, and the total amount of the balance plus vouchers is not less than RMB 100.00.


<span id="6e1e4280"></span>
## **Billing rules**

Byteplus EMR on VKE calculates the hourly service fee based on the specifications and quantity of POD resources actually used by the virtual cluster. The billing standards are shown in the table below.


|Region |Billing item |Unit price |
|---|---|---|
|Johor |vCPU |$ 0.01 /core/hour |
||Memory |$ 0.001 /GiB/hour |


<span id="f764c4cf"></span>
## Billing

The cost of EMR on VKE only includes the EMR service fee. Other cloud product fees are also involved during use. For details, see the table below.


|Related products |Billing |
|---|---|
|Object Storage (TOS) |TOS is used to store information such as jobs, logs, and JAR packages. For billing details, see [Billing overview](https://docs.byteplus.com/zh-CN/docs/tos/docs-billing-overview). |
|Container Service (VKE) |Big data service components are installed and deployed on VKE resources and run inside containers. For billing details, see [billing](https://docs.byteplus.com/zh-CN/docs/vke/Billing). |
