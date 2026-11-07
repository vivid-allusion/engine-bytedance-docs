---
title: "Billing of Viking Memory"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Billing_of_VikingMem"
---

<span id="fc830c70"></span>
# Billing Overview

This document provides a detailed overview of the billing for Viking Memory, including the billing method, cycle, and items.

<span id="4d191fe8"></span>
## Billing Method

Viking Memory uses a pay\-as\-you\-go billing method. You are billed for the resources you consume, and you can settle the payment after the bill is generated.

<span id="3f5385e0"></span>
## Billing Cycle

Viking Memory calculates usage and generates bills on an hourly basis. After you create a memory instance, uploading a session will trigger the allocation of computing resources, and hourly billing will commence. Deleting a session does not affect resource allocation. If you no longer need the service, please delete the memory instance to avoid further charges.

<span id="433de46f"></span>
## Billable Items

The pay\-as\-you\-go billing for Viking Memory consists of the following:

**Hourly Resource Billing**: After memory extraction, the memory is vectorized and streamed into an index, which continuously consumes computing resources. You will be billed hourly based on your actual usage.

⚠️ Note: The size of computing and storage resources is proportional to the amount of memory. The system will automatically scale resources based on actual usage.

⚠️ Note: Charges are incurred every hour. If you are not using the service, please delete the memory instance in a timely manner.

**Model Usage Billing**: The inference of vectorization and memory extraction models is billed based on the actual token consumption.

The detailed billable items are as follows:


|**Billing Items** |**Definition** |**Measurement Metric** |**Billing Type** |**Price** |
|---|---|---|---|---|
|Memory Extraction Large Language Model Input 128k |When invoking the large language model for memory extraction, billing is based on input token consumption in the range (0, 128k]. |Measured by input tokens |Pay\-As\-You\-Go |0.00025 USD / K tokens |
|Memory Extraction Large Language Model Input 256k |When invoking the large language model for memory extraction, billing is based on input token consumption in the range (128k, 256k]. |Measured by input tokens |Pay\-As\-You\-Go |0.0005 USD / K tokens |
|Memory Extraction Large Language Model Output 128k |When invoking the large language model for memory extraction, billing is based on output token consumption when the input size is in the range (0, 128k]. |Measured by output tokens |Pay\-As\-You\-Go |0.002 USD / K tokens |
|Memory Extraction Large Language Model Output 256k |When invoking the large language model for memory extraction, billing is based on output token consumption when the input size is in the range (128k, 256k]. |Measured by output tokens |Pay\-As\-You\-Go |0.004 USD / K tokens |
|Standard Memory Storage and Computing Resources |Storage resources cover vectorized memory data and related metadata. Compute resources include index building, auto\-optimization, and retrieval. Standard Edition uses shared resources. |Measured by memory count \* time |Pay\-As\-You\-Go |0.01 USD / 10K items / Hour |
|Memory Embedding Model (Text) |Viking Memory provides text embedding services, enabling developers to rapidly convert text data into vector data for memory retrieval. |Measured by input tokens |Pay\-As\-You\-Go |0.00015 USD / K tokens |
|Ultimate Memory Storage and Computing Resources |Viking Memory leverages the computing resources of the Ultimate Edition, including index construction, automated optimization and analysis, and the computing resources required for online retrieval. |Measured in CU (Compute Unit: 8GB RAM + 1 CPU Core) |Pay\-As\-You\-Go |0.325 USD / CU / Hour |


<span id="1bee4326"></span>
# Overdue Payments

If the available credit in your account (including account balance and vouchers) is less than the outstanding bill, your account will be considered overdue. You will receive an SMS or email notification about the insufficient balance. This section describes the status of your resources and the actions you can take if your account is overdue.

Please top up your account and settle the overdue bill within **72** hours. Otherwise, you will not be able to use the vector database and Viking Memory services normally.

The service status changes for vector database and Viking Memory after an overdue payment are as follows:


* Within **72** hours of the payment becoming overdue, the system will continue to operate normally, and billing will continue.

* If the payment is overdue for more than **72** hours but less than **720** hours, BytePlus will suspend the service, but your data and related resources will be retained. No charges will be incurred during the suspension period.

* If the payment is overdue for more than **720** hours, you will be deemed to have voluntarily given up the pay\-as\-you\-go service for the vector database and Viking Memory. The relevant resources and data will be released and cannot be recovered.

* If you pay all overdue bills within **720** hours, the service will be restored to normal.


<span id="5675d66e"></span>
# Invoices

You can request invoices for your completed orders and/or issued bills in your BytePlus account. You can apply for an invoice through the BytePlus Console → Cost Center → Invoice Management. We will issue the invoice to you in a timely manner after receiving your application.

If the service rules for the services you use are inconsistent with this document, or if both parties have agreed otherwise, the specific service rules or the otherwise agreed\-upon terms and conditions shall apply. For services with periodic settlement and specific usage, BytePlus also reserves the right to require users to provide credit certificates, prepayments, deposits, or other subscription conditions that BytePlus deems necessary.

We will issue invoices to you with the following content according to the specific product or service type you purchase.
