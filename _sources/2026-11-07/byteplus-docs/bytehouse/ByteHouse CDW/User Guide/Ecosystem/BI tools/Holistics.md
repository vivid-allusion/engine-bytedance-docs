---
title: "Holistics"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/holistics"
---

Holistics is a modern BI platform designed to provide self\-service data access to the entire organization.

Holistics enables data teams to predefine business metrics and data logic. Based on these predefined logic, business users can perform self\-service data exploration and build their own visualizations and reports.

In the background, Holistics converts these operations into SQL queries and runs them against your SQL database. The SQL results are formatted and visualized for the end user.

<span id="765c6218"></span>
# Background information

ByteHouse allows you to connect to it via DataEase using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="f9f5c9d2"></span>
# **Version requirements**


1. Log in to [Holistics Saas Service](https://www.holistics.io/).

2. Use the built\-in ClickHouse data source.


<span id="2a6ef889"></span>
# **Connect to ByteHouse**

<span id="4c72cad2"></span>
## Use ClickHouse connector


1. Add a datasource in Holistics and select the ClickHouse connector.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b27e4c8399184bf19222d58bf59499ab~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

2. Fill in the connection and verification information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c170aa8b4d3f4334b07e42bb64810623~tplv-goo7wpa0wc-image.image" width="3548px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Display Name |You can customize it. ||
   |Connection mode |Select **Direction Connection**. ||
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |8123 ||
   |Database name |Configure it as the database name you want to connect to. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Require SSL |Enable it. ||
   


<span id="c251de9d"></span>
## Use MySQL connector


1. Add a datasource in Holistics and select the MySQL connector.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fadab60d352b466b97d6f9fc5727bff4~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the connection and verification information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5e297557ca043ed91974a2fe5e77a57~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Display Name |You can customize it. ||
   |Connection mode |Select **Direction Connection**. ||
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |8123 ||
   |Database name |Configure it as the database name you want to connect to. ||
   |Username & Password |[**Recommended**] **Option 1**:<br><br>Use the API Key as both the Username and Password. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* The Username is the first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `xxxx`.<br><br>* The Password is the second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `yyyy`.<br><br><br>**Option 2**:<br><br><br>* user: defaults to `bytehouse`.<br><br>* password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Required SSL |Enable it. ||
   


<span id="c9045cc1"></span>
# Examples

<span id="3aa4b675"></span>
## Create data model

Select the table to create the data model as shown in the following image.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f111925800b4d4e854927dc583fe013~tplv-goo7wpa0wc-image.image" width="3550px" /></div>


<span id="5de41fac"></span>
## Create dataset

Select a data model to create a dataset.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed8a06f931364cb99f4dda8c663f0e23~tplv-goo7wpa0wc-image.image" width="3548px" /></div>


<span id="b2a22eab"></span>
## Create dashboard

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d5ca612ad1f472699927c44d7520f17~tplv-goo7wpa0wc-image.image" width="3552px" /></div>



* Add dashboard filters

* Add time filters

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b191cf6b072c4cbe8d751464728ee643~tplv-goo7wpa0wc-image.image" width="3550px" />   </div>
   


Data Overview

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de5885e0630748ed872033d935471faa~tplv-goo7wpa0wc-image.image" width="3556px" /></div>
