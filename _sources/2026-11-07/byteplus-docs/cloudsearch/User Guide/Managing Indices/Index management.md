---
title: "Index management"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/index_management"
---

Index management enables quick actions such as create index, index configuration, field management, alias management, as well as operations on index templates and lifecycle policies. This article explains how to manage indexes.

## Prerequisites

* Before using Cloud Search service, register a Volcengine account and complete enterprise verification.

* When using Cloud Search for the first time, you must first obtain cross\-service authorization to access other cloud product resources. For authorization details, see [Cross-service authorization](https://docs.byteplus.com/en/docs/cloudsearch/cross-service-authorization).

* You need to create an ES or OpenSearch instance before managing indexes. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/cloudsearch/creating-an-instance-2).

## Create index

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the project and region for which you want to create an index.

3. In the left navigation bar, select **PaaS model \> Index management**.

4. From the dropdown list, select the instance whose index you want to manage, enter the instance's username and password, choose the authentication validity period as needed, then click Authorize **view index**.

5. On the **Index management** tab, click **Create index**.

6. In the **Create index** panel, configure the following parameters, then click **Next step**.

   |**Parameter** |**Description** |
   |---|---|
   |Index name |Name of the index. Limits are as follows:<br><br><br>* Cannot start with a number or underscore (_).<br><br>* Length must be between 1 and 128 characters.<br><br>* Can only contain lowercase letters, numbers, underscores (_), and hyphens (\-). |
   |Number of active shards |The number of active primary shards in the index. |
   |Replicas |Number of Replicas for the index, value range 1 to 10. |
   |Translog (optional) |Select **Asynchronous flush** or **Synchronous flush**. |
   |Compression method (optional) |Select **Speed priority**, **Compression ratio priority**, or **ZSTD**.<br><br>> **warning**<br><br><br>> OpenSearch 3.3.0 does not support enabling ZSTD compression and ANN Search simultaneously.<br> |
   |ANN Search |Select whether to enable approximate nearest neighbor (ANN) search.<br><br>> **warning**<br><br><br>> OpenSearch 3.3.0 does not support enabling ZSTD compression and ANN Search simultaneously.<br> |
   |Index encryption |Select whether to enable index encryption. For indexes storing sensitive data such as PII (personally identifiable information), static encryption is provided based on KMS to meet security compliance requirements.<br><br>> **warning**<br><br><br><br>* > The index encryption feature only supports OpenSearch 3.3.0 instances.<br><br><br>* > The index encryption feature requires KMS service activation to use.<br><br><br>* > The index encryption setting cannot be modified after the index is created.<br> |
   |Index settings (optional) |Set index details. |

7. In the index field area, choose **Visual editing** or **JSON editing** tab.

   * Visual editing

      * Select **Scalar field**, specify the **scalar type**, check **searchable** and **aggregatable** options as needed, enter **analyzer**, then click **add a row** as required.

      * Select **Vector field**, specify **vector type**, **dimension**, and **metric type**, then click **add a row** as needed.

   * JSON editor

      Enter field content in JSON format within the code box.

8. Configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Dynamically add columns |select **True**, **False**, or **Strict**. |
   |Routing |routing switch; enable as needed.<br><br>> **warning**<br><br><br>> this setting cannot be changed once the index is created. Confirm before submitting.<br> |

## edit index

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the project and region where you want to edit the index.

3. In the left navigation bar, select **PaaS model \> Index management**.

4. From the dropdown list, select the instance whose index you want to manage, enter the instance's username and password, choose the authentication validity period as needed, then click Authorize **view index**.

5. On the **Index management** tab, under the **actions** column of the target index, click **edit**.

6. In the **edit index** panel, modify the parameters as needed, then click **OK**.

## Turn off index

> **warning**

> After turning off the index, data will not be queryable; operate with caution.

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. Select the project and Region for which you want to disable the index in the top navigation bar.

3. Select **PaaS model \> Index Management** in the left navigation bar.

4. From the dropdown list, select the instance whose index you want to manage, enter the instance's username and password, choose the authentication validity period as needed, then click Authorize **view index**.

5. On the **index management** tab, in the **actions** column of the target index, click **turn off**.

6. In the popup dialog, click **OK**.

## Turn on index

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. Select the project and Region for which you want to disable the index in the top navigation bar.

3. Select **PaaS model \> Index Management** in the left navigation bar.

4. From the dropdown list, select the instance whose index you want to manage, enter the instance's username and password, choose the authentication validity period as needed, then click Authorize **view index**.

5. On the **Index Management** tab, in the **actions** column of the target index, click **turn on**.

6. In the popup dialog, click **OK**.

## Delete an index

1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. Select the project and Region for which you want to delete the index in the top navigation bar.

3. In the left navigation bar, select **PaaS model \> Index management**.

4. From the dropdown list, select the instance whose index you want to manage, enter the instance's username and password, choose the authentication validity period as needed, then click Authorize **view index**.

5. On the **index management** tab, click **delete** in the **actions** column of the target index.

6. In the popup dialog, confirm the index information, enter the index name, and then click **delete**.
