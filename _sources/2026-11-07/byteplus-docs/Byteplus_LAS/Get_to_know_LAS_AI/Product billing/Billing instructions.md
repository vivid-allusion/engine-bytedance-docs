---
title: "Billing instructions"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Billing"
---

This document introduces the current billing items for the AI Data Lake Service (LAS), as well as the billing methods and logic for each item.

<span id="overview-of-billing-items"></span>
# Overview of billing items

After enabling the LAS product, charges will be incurred when using the following LAS functional modules.


|Feature modules |Billing items |Billing overview |
|---|---|---|
|Operator marketplace & operator services |**ModelArk models**<br><br>When processing data with LAS, some operator capabilities are based on ModelArk models. When using such operators, model fees will be charged according to the type of ModelArk model used. |Billing method: "Pay\-as\-you\-go", fees are calculated based on the type of model used.<br><br>For details, see [Large model invocation billing- BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
||**Self\-developed models, model enhancement**:<br><br>Some operators use LAS self\-developed models, or have enhanced capabilities based on certain models. When using such operators, model fees will be charged according to the type of model associated with the operator. |Billing method: "Pay\-as\-you\-go", fees are calculated based on the type of model used.<br><br>For details, see [Large model invocation billing- BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Metadata management |**Metadata objects**:<br><br>To perform unified metadata management of various data using LAS metadata management features, fees for metadata objects will be charged based on the number of metadata objects you create. |* Billing method: Pay\-as\-you\-go, fees are calculated based on the number of metadata objects.<br><br>* LAS provides a certain free quota. Any usage exceeding the free quota will be charged on a pay\-as\-you\-go basis.<br><br><br>For details, see [Metadata objects](https://docs.byteplus.com/docs/Byteplus_LAS/Billing#d5b148bd) below. |
||**Metadata requests**:<br><br>When you create, read, modify, or delete metadata objects for storage management in LAS, corresponding request fees will be charged. |* Billing method: Pay\-as\-you\-go, charged by number of requests<br><br>* LAS provides a certain free quota. Usage exceeding the free quota is billed on a pay\-as\-you\-go basis.<br><br><br>For details, see [Metadata requests](https://docs.byteplus.com/docs/Byteplus_LAS/Billing#9f650601) below. |
|Data development |**Cloud disk**:<br><br>To develop data tasks using the LAS development machine, you need to mount a cloud disk. The cloud disk is mounted as persistent storage at the root directory (/), and data in this directory will be retained after shutdown or restart. |* Billing method: "Pay\-as\-you\-go"<br><br>* Billed based on cloud disk capacity (GiB/hour). The billing details vary depending on the resource specifications of the cloud disk.<br><br><br>For details, see [Billing details: Cloud disk](https://docs.byteplus.com/docs/Byteplus_LAS/Billing#dfb690b8) below. |


<span id="billing-details-operators-models"></span>
# Billing details: Operators/models

For details, see [Large model invocation billing- BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing).

<span id="billing-details-metadata-management"></span>
# Billing details: Metadata management

The metadata management feature of LAS only supports pay\-as\-you\-go billing, that is, postpaid billing.

<span id="metadata-objects"></span>
## Metadata objects

<span id="definition-of-billing-items"></span>
### Definition of billing items


* Metadata objects refer to all levels of metadata stored and managed in LAS, including all databases, tables, volumes, functions, partitions, and indexes.

* Relationship between datasets and metadata

   * General datasets: When metadata storage is specified for a general dataset (for example, when creating or editing a general dataset, a metadata table is associated), the corresponding general dataset is considered a metadata object.

   * Inference datasets: Each inference result set is backed by a metadata table. Depending on the dataset type, text data uses an iceberg table, and multimodal data uses a lance table. Each iceberg table or lance table is a metadata object.


<span id="billing-details"></span>
### Billing details

After billing begins, both existing and newly added metadata will be charged.


|Billing unit |Billing mode |Billing method |
|---|---|---|
|Number of metadata objects |Pay\-as\-you\-go |* Free quota: First 1,000,000 per month are free<br><br>* Billed portion: For usage exceeding 1,000,000, each additional 10,000 is charged 0.1 USD/month |


<span id="billing-settlement-cycle"></span>
### Billing/settlement cycle

The number of objects is counted monthly. On the 1st of each month, billing and settlement are performed.

<span id="metadata-requests"></span>
## Metadata requests

<span id="definition-of-billing-items"></span>
### Definition of billing items


* Metadata access refers to the actions of creating, reading, modifying, and deleting metadata objects stored and managed in LAS.

* Metadata object access can be performed by executing DDL statements in one or more compute engines integrated with LAS (such as EMR Serverless Spark, Hive on EMR, SparkSQL on EMR, Serverless Presto, LAS, and so on), or directly operating metadata objects via the LAS product console or API.


<span id="billing-details"></span>
### Billing details


|Billing unit |Billing mode |Billing method |
|---|---|---|
|Number of metadata requests |Pay\-as\-you\-go billing |* Free quota: The first 1,000,000 requests per month are free<br><br>* Billed portion: For requests exceeding 1,000,000, each additional 10,000 requests is charged at $0.01 per month |


<span id="billing-settlement-cycle"></span>
### Billing/settlement cycle

The number of objects is counted monthly. On the 1st of each month, billing and settlement are performed.

<span id="billing-details-cloud-disk"></span>
# Billing details: Cloud disk

<span id="billing-details"></span>
### Billing details


|Billing unit |Billing mode |Unit price |Cost calculation |
|---|---|---|---|
|Cloud storage disk |Pay\-as\-you\-go |* **Extreme SSD PL0 unit price**: $0.0025/GiB/hour<br><br>* **Extreme SSD FlexPL unit price**: $0.0005/GiB/hour |Cost = cloud storage disk unit price × capacity × billing duration |


<span id="billing-settlement-cycle"></span>
### Billing/settlement cycle

The billing cycle is accurate to the second.
