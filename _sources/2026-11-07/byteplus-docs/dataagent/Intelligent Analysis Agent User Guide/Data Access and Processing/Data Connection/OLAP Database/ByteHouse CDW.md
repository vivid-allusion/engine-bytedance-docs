---
title: "ByteHouse CDW"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouse_CDW"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with ByteHouse cloud data warehouse edition for BI analysis and report display.

**Prerequisites**: You must have [ByteHouse CDW cloud data warehouse edition](https://www.byteplus.com/en/product/bytehouse).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1b1c560a9dd34d1a96e8e9d462ba1c2f~tplv-goo7wpa0wc-image.image) </span>

**Preparatory steps:** 

(1) Apply for a [BytePlus account](https://console.byteplus.com/auth/signup). Enterprise users must visit the BytePlus official website to apply for a primary BytePlus account and complete account verification. For steps, refer to ["BytePlus account registration and verification operation guide"](https://www.volcengine.com/docs/6261/64925).

(2) Complete real\-name authentication. For steps, refer to Real\-name authentication.

(3) Enter the BytePlus ByteHouse console ([ByteHouse product page](https://www.byteplus.com/en/product/bytehouse)) and activate the product.

(4) Create a database, create a table, and import data. Using **Cell tower public data table** as an example, follow the steps shown in the figure below to complete the creation of the data table.

> Note: The Cell tower data table collects information about base stations worldwide (GSM, LTE, UMTS, and more), as well as geographic coordinates, country codes, and other information.


You can use the following SQL statement to create a table for trial purposes.

```sql
CREATE TABLE `sampledb`.`cell_towers`
(
    radio String,
    mcc UInt16,
    net UInt16,
    area UInt16,
    cell UInt64,
    unit Int16,
    lon Float64,
    lat Float64,
    range UInt32,
    samples UInt32,
    changeable UInt8,
    created DateTime,
    updated DateTime,
    averageSignal UInt8
)
ENGINE = CnchMergeTree ORDER BY (radio, mcc, net, created);
sql
```


(5) After creating the table, go to the data loading module, click "Create import task", fill in the relevant information, and then click "Create" in the lower right corner.

(6) Select a folder to start the import task and complete the process.

The process for obtaining access keys, compute groups, and roles will be described in detail below. For more information about ByteHouse CDW, see the document [ByteHouse cloud data warehouse edition overview](https://www.volcengine.com/docs/6517/75861).

<span id="_2-快速入门"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

**Enter the following parameters according to the information items below.** 


* **Data connection name**: Use the default value.

* **Region**: Use the default value.

* **Access key**: In [ByteHouse account details](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/account/details), create an Access Token and obtain the API Token ID shown in the figure below to fill in.

* **Compute group**: Obtain from the [ByteHouse compute group page](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/virtual-warehouse), fill in the name shown in the figure below (example: default_vw). For more information about compute groups, you can refer to ["Compute group"](https://www.volcengine.com/docs/6517/76332).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Compute group notes</strong> You need to confirm that the current status is "Enabled", or that auto\-start is "Enabled".</div>



* **Role**: View and obtain the role from the settings button in the upper right corner of ByteHouse. For more information about roles, you can refer to ["Role management"](https://www.volcengine.com/docs/6517/1250178).


**Caution**


* Role precautions: You must ensure that the role has SELECT and SHOW CREATE permissions for the table in order to use the table in DataWind.

* If the [Role] parameter is not required among the data connection parameters, the current user must have AccountAdmin role permissions in ByteHouse. For details, see ["Data permission management"](https://www.volcengine.com/docs/6517/1288723).


<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, select a specific project, go to Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) In the pop\-up data source list, select "ByteHouse CDW".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d952cba9214b432380d5dc71c7ad8d79~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and after a successful connection, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43c8cca2a5c9406cb9be026145c5bb68~tplv-goo7wpa0wc-image.image) </span>

(4) On the ByteHouse CDW page, perform the add allowlist operation. Enter the "public IP used by DataWind to access" in the allowlist settings area to grant this IP address permission to access the CDW service.

Public IP list: 101.126.44.93, 101.126.44.36, 180.184.39.171, 101.126.46.117, 101.126.86.154, 101.126.47.167, 180.184.47.241, 180.184.49.32, 180.184.38.134, 180.184.92.195, 180.184.77.6.

(5) After confirming that the basic information of the data connection is correct, the data connection is completed.

(6) This connection can be used as a data source to create a dataset: Click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(7) Search or browse existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and click the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click "Create configuration".

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After uploading is completed, you will remain in the pop\-up window to select a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="_3-常见问题"></span>
# 3. Frequently asked questions

(1) If real\-name authentication has not been completed, you cannot access the BytePlus ByteHouse (Cloud Data Warehouse Edition) console normally. You need to complete real\-name authentication.

(2) To use the LAS service, cross\-service authorization is required. If not used, this can be ignored.
