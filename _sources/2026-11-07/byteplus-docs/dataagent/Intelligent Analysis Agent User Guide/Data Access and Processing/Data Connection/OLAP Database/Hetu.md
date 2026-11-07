---
title: "Hetu"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hetu"
---

<span id="18f97447"></span>
# 1. Overview

The data connection module supports integrating with Hetu to create datasets. Data connections support direct connection or extraction from Hetu 3.3 data sources.

Note:

Before connecting to the data, please collect the following information:


* The IP address and port number of the server where the database is located

* The username and password for the database

* The database connection method (IP/Port, JDBC connection string)

* The database authentication method (username and password, Kerberos)


<span id="5fd863df"></span>
# 2. Quick start

The following describes two methods for creating a data connection.

<span id="abcf883f"></span>
## 2.1 Create a data connection

(1) Enter BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) Select Hetu on the page.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a97cdef35d2747d7a4e628114b790c45~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/225da33c033347faba8f501bc602d66b~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Enter keywords to search and select the previously created data connection.

<span id="13729c8b"></span>
## 2.2 Create a dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner, and create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click the Other button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are the same as steps (2) and (3) in section 2.1. After completing the configuration, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.

<span id="716bd899"></span>
# 3. Function overview

The basic information to pay attention to during the data connection process is described as follows.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Hetu.<br><br>The name can be modified. Please enter a standardized name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Two types: IP/Port and JDBC connection string |
|Server |The public network address of Hetu<br><br>For information, refer to the official Hetu documentation |
|Port |Hetu instance port<br><br>For more information, refer to the official Hetu documentation. |
|Authentication methods |Two authentication methods are supported: username and password, and Kerberos. |
|Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the operations personnel for the corresponding engine. |
|Keytab file |Files or information related to Kerberos authentication (keytab, krb5, principal, jks) are usually located in the Hetu engine installation directory. It is recommended to contact the relevant operations personnel or Hetu after\-sales support to obtain them. |
|Krb5 file ||
|Principal ||
|jks ||
|Database |Name of the database created in Hetu. |
