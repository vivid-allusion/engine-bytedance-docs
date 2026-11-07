---
title: "Hetu"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Hetu"
---

<span id="18f97447"></span>
# 1. Overview

The data connection module supports connecting to Hetu to create datasets. The data connection supports direct connection or extraction from Hetu 3.3 data sources.

Note:

Please collect the following information before connecting to the data:


* The IP address and port number of the server where the database is located

* The username and password of the database

* The database connection method (IP/Port, JDBC connection string)

* The database authentication method (username and password, Kerberos)


<span id="5fd863df"></span>
# 2. Quick start

There are two methods for creating a data connection:

<span id="abcf883f"></span>
## 2.1 Create a data connection directly

(1) Enter BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and create a new data connection.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) Select Hetu on the page.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b0d034ba8764f02a06ecd78b011fa08~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e2567afc9b24b7bab27be065a40384c~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is completed.

(5) You can use this connection to create a dataset: click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(6) Enter keywords to search and select the previously created data connection.

<span id="13729c8b"></span>
## 2.2 Create a dataset from the dataset module

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and click the "New" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" /></div>


(2) When selecting a data connection, click the "Other" button.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" /></div>


The subsequent steps are the same as steps (2) and (3) in 2.1 above. After completing the configuration, the system will remain on the pop\-up window for selecting a data connection for the dataset, allowing you to proceed directly to the next step of dataset creation.

<span id="716bd899"></span>
# 3. Feature overview

The following describes the basic information required during the data connection process.


|Name |Description |
|---|---|
|Data connection name |The name of the new data connection, used to distinguish connections to different databases in the system. For example, Hetu.<br><br>The name can be modified. Please enter a standard name. Do not use special characters, and do not include spaces at the beginning or end. |
|Connection method |Two types: IP/Port and JDBC connection string |
|Server |The public network address of Hetu<br><br>For more information, refer to the official Hetu documentation |
|Port |Hetu instance port<br><br>To obtain information, refer to the official Hetu documentation |
|Authentication methods |Authentication methods support two options: username/password and Kerberos |
|Username |The username created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator responsible for the corresponding engine. |
|Password |The password created in the database engine. If you do not know how to obtain it, it is recommended to contact the administrator responsible for the corresponding engine. |
|Keytab file |Files or information related to Kerberos authentication (keytab, krb5, principal, jks) are usually located in the Hetu engine installation directory. If you do not know how to obtain them, it is recommended to contact the relevant administrator or Hetu after\-sales support. |
|Krb5 file ||
|Principal ||
|jks ||
|Database |The name of the database created in Hetu. |
