---
title: "ByteHouse CDW"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouseCDW"
---

<span id="ddd7846e"></span>
# 1. Overview

Support docking with ByteHouse cloud data warehouse version for BI analysis and report display.

**Prerequisites** : Need to have [ByteHouse CDW cloud data warehouse version](https://www.byteplus.com/en/product/bytehouse);

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b8fb1ee692343048fe5f21d7ca2706f~tplv-goo7wpa0wc-image.image) </span>

**Preliminary preparations:** 

(1) Apply for a [BytePlus account ](https://console.byteplus.com/auth/signup); enterprise users need to go to the Volcano Engine official website to apply for a Volcano Engine main account and complete account authentication. For the steps, please refer to ["Volcano Engine Account Registration and Authentication Operation Guide" ](https://www.volcengine.com/docs/6261/64925);

(2) for real\-name authentication, the steps refer to [real-name authentication ](https://www.volcengine.com/docs/6261/64935);

(3) Enter the Volcano Engine ByteHouse console ( [ByteHouse product page ](https://www.byteplus.com/en/product/bytehouse)) to open the product.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9d82a62280c4a54a84ae70f291bc23b~tplv-goo7wpa0wc-image.image) </span>

(4) Create a database, create a table, import data, take the **Cell tower public data table** as an example, and complete the operation of creating the data table as shown in the figure below.

> Note: Cell tower data table statistics of base station information around the world (GSM, LTE, UMTS, etc.), as well as geographical coordinates, country codes and other information.


You can use the following SQL to build a table for trial use

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


(5) After the creation of the table is completed, enter the data loading module, click "New Import Task", fill in the relevant information and click "Create" in the lower right corner.

(6) Select the folder to start the import task and complete it.

The content of obtaining access keys, calculation groups, and roles will be described in detail below. For more information on ByteHouse CDW, see the document [Introduction to ByteHouse Cloud Data Warehouse Edition](https://www.volcengine.com/docs/6517/75861?lang=en).

<span id="834b0216"></span>
# 2. Quick start

Here are two ways to create a data connection.

**Fill in the following parameters according to the following information items**


* **Data connection name** : Use default

* **Region** : Use Default

* **Access key** : Create an Access Token [in ByteHouse account details ](https://console.byteplus.com/bytehouse/region:bytehouse+ap-southeast-1/database)and fill in the API Token ID in the figure below.

* **Calculation group** : Get it on the [ByteHouse Calculation Group page ](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/virtual-warehouse), fill in the name as shown in the figure below (for example default_vw), more information about the calculation group can be referred to, you can check [the "Calculation Group" ](https://www.volcengine.com/docs/6517/76332)to understand.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>Note for the calculation group</strong> You need to confirm that the current status is "On", or the automatic start is "On"</div>



* **Role** : View role acquisition in the settings button in the upper right corner of ByteHouse. For more information about roles, you can check ["Role Management" ](https://www.volcengine.com/docs/6517/1250178)to learn.


**Attention**


* Role Note: You need to ensure that this role has SELECT and SHOW CREATE permissions on the table before you can use the table in DataWind.

* If there is no [role] item to fill in in the parameters required for data connection, the current user needs to have AccountAdmin role permission in ByteHouse. For details, see ["Data Rights Management" ](https://www.volcengine.com/docs/6517/1288723).


<span id="9a3ae87c"></span>
## 2.1 Create a new data connection

(1) Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

(2) Select "ByteHouse CDW" in the pop\-up data source list

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c988778ddcf714795e69440787b94fe2.png) </span>

(3) Fill in the required basic information and test the connection. After the connection is successful, click Save.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f4149e0da35448ebb714fad048e53f90~tplv-goo7wpa0wc-image.image) </span>

(4) On the CDW page of ByteHouse, perform the add whitelist operation, fill in the "public network IP accessed by DataWind" into the whitelist setting area, and give the IP address permission to access the CDW service.

Public IP list: 101.126.44.93 , 101.126.44.36 , 180.184.39.171 , 101.126.46.117 , 101.126.86.154 , 101.126.47.167 , 180.184.47.241 , 180.184.49.32 , 180.184.38.134 , 180.184.92.195 , 180.184.77.6 .

(5) After confirming that the basic information of the data connection is correct, the data connection is completed.

(6) You can use this connection as a data source to create a dataset: click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(7) Search for or drop down an existing connection and select the newly created data source.

<span id="d383be68"></span>
## 2.2 Creating a new dataset

(1) Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting Data Connection, click New Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" /></div>


The following steps are consistent with steps (2) and (3) of 2.1 above. After the upload is completed, it will stop in the pop\-up box of Dataset Select Data Connection, and you can directly proceed to the next step of Dataset Creation.

<span id="62e41670"></span>
# 3. Frequently Asked Questions

(1) If the real\-name authentication is not performed, the Volcano Engine ByteHouse (Cloud Data Warehouse Edition) console cannot be accessed normally, and the [real-name authentication ](https://www.volcengine.com/docs/6261/64935)needs to be completed.

(2) To use LAS services, cross\-service authorization is required, which can be ignored if not used.
