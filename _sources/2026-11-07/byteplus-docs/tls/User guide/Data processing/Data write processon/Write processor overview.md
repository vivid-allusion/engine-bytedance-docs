---
title: "Write processor overview"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Overview_of_the_data_processor"
---

This document introduces the features, usage restrictions, and other information about the write processor in TLS.

## Billing information

The charging schedule will be announced later.

## Feature overview

The write processor of TLS is a powerful tool for real\-time, lightweight data cleansing, transformation, and enrichment before data is written to TLS. It is suitable for business scenarios that require unified formatting, filtering of invalid data, and protection of sensitive information before data is persisted.

You can directly create a write processor in the TLS console, associate it with a log topic, and use SQL\-like DSL (data processing language) to define processing rules. This enables string masking, encryption, renaming of fields, conditional logic, flow control, and structured processing of JSON fields.

* For details on processing rules using DSL, see [Data transformation overview](https://docs.byteplus.com/docs/tls/data_transformation_overview).

* For supported data processing functions, see [Functions overview](https://docs.byteplus.com/docs/tls/overview_of_functions).

   > **Note**

   > The following functions in the function list are currently not supported:

   * > Event processing functions: e_output function, e_auto_output function.

   * > Resource functions: res_rds_mysql function.

## Feature highlights

* Zero client overhead: All processing is performed on the server side, without consuming any client computing resources.

* Centralized rule management: Unified DSL rules allow centralized management of preprocessing logic for all data sources, ensuring consistency.

* Improved data quality: Effectively intercepts "dirty data" and ensures that ingested data is standardized and high\-value from the source.

* Reduced cost and risk: Filtering and masking reduce storage costs for invalid data and lower the risk of sensitive information leakage.

|Feature comparison |Write processor |Consumer processor |Data transformation task |
|---|---|---|---|
|Processing stage |Data before being written to TLS |Data has been collected by TLS |Data has been collected by TLS |
|Scope of application |* Exists within a project and applies to log topics in that project.<br><br>* Does not support cross\-region, cross\-account, or cross\-project operations. |* Exists within a project and applies to log topics in that project.<br><br>* Does not support cross\-region, cross\-account, or cross\-project operations. |* An independent data transformation task that applies to selected source and target log topics.<br><br>* Supports cross\-region, cross\-account, and cross\-project operations. |
|Billing information |No charges currently apply. The billing start date will be announced separately. |No charges currently apply. The billing start date will be announced separately. |Data transformation fees, cross\-region data transfer fees, and more. |
|Data transformation rules |Supports writing data transformation rules using built\-in functions provided by TLS DSL.<br><br>The e_output function, e_auto_output function, and res_rds_mysql function are not supported. |Supports writing data transformation rules using built\-in functions provided by TLS DSL. |Supports writing data transformation rules using built\-in functions provided by TLS DSL. |

## Usage restrictions

|**Limitations** |**Specifications** |
|---|---|
|Number of write processors<br><br> |* A maximum of 100 write processors can be created in each project.<br><br>* To adjust the quota, see [Apply for resource quota](https://docs.byteplus.com/docs/tls/Apply_for_resource_quota). |
|Associations |* Each log topic can be associated with only one write processor.<br><br>* One write processor can be associated with multiple log topics.<br><br>* Associating log topics across projects is not supported. |
|Effective time |Newly created or edited write processors take effect within 1 minute. |
|Protocol compatibility |Compatible with all log data ingestion methods provided by TLS, including Logtail, SDKs/APIs in various languages, Web Tracking, and more. |
|DSL rules and performance impact |For details, see [Data transformation overview](https://docs.byteplus.com/docs/tls/data_transformation_overview). |
