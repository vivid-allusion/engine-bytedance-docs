---
title: "DataEase"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dataease"
---

DataEase is an open\-source data visualization and analysis tool that helps users quickly analyze data and gain insights into business trends, thereby improving and optimizing business operations. DataEase supports a variety of data source connections, allowing users to quickly create charts through drag\-and\-drop methods, and easily share them with others.

<span id="1033525c"></span>
# Background information

ByteHouse allows you to connect to it via DataEase using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="0d4b6682"></span>
# **Version requirements**


* DataEase: Version 1

* Use the built\-in ClickHouse data source.


<span id="06282a22"></span>
# **Install DataEase**

To install DataEase version 1, use the following command:

```Bash
curl -sSL https://dataease.oss-cn-hangzhou.aliyuncs.com/quick_start.sh | sh
```


DataEase Server Edition is a B/S architecture product, that is, Browser/Server structure. After the server installation is complete, clients can access the following address through a browser to start using it.

```Plain
http://Server IP address: Service running port (if not modified, the default is 8100)
Log in with the default username "admin" and password "DataEase@123456".    
```


For other installation considerations, please visit the official document: https://community.fit2cloud.com/#/products/dataease/getstarted.

<span id="5b45268f"></span>
# **Connect to ByteHouse**

<span id="84ac7208"></span>
## Essential settings

Refer to the diagram below to adjust the database request timeout setting to 300.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e25f75cefdd4dfbae09d8f78705bc1b~tplv-goo7wpa0wc-image.image" width="3584px" /></div>


<span id="7526c720"></span>
## Use ClickHouse datasource


1. Add a datasource in DataEase, select the Clickhouse connector.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15c5c7f0c11b4a26a42073e70946d5a8~tplv-goo7wpa0wc-image.image" width="3838px" />   </div>
   

2. Fill in the connection information and verification details.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04784a0e9fd94336b16958372eaf4c5a~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Display name |You can customize it. ||
   |Driver |Default ||
   |Host name/IP address |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Database name |Configure it as the database name you want to connect to. ||
   |User Name & Password |* User Name: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User Name: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Extra JDBC connection string |`ssl=true&max_execution_time=600&socket_timeout=600000&compress=0` ||
   |Port |8123 ||
   


<span id="1a531079"></span>
## Use MySQL datasource


1. Add a datasource in DataEase, select the MySQL connector.

2. Fill in the connection information and verification details.

   
   |Parameter item |Use an IAM user to connect |Use a databse user to connect |
   |---|---|---|
   |Display name |You can customize it. ||
   |Driver |default(5,8) ||
   |Host name/IP address |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Database name |Configure it as the database name you want to connect to. ||
   |User Name & Password |* User Name: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User Name: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Extra JDBC connection string |`characterEncoding=UTF-8&connectTimeout=5000&useSSL=false&allowPublicKeyRetrieval=true` ||
   |Port |3306 ||
   


<span id="190ba25d"></span>
# Show effect

<span id="8c8820b9"></span>
## Create dataset

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7047444c80e4f3698a207c0cc9dd194~tplv-goo7wpa0wc-image.image" width="3584px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eecbfaa60c044fd7a0a259bf58e2b720~tplv-goo7wpa0wc-image.image" width="3582px" /></div>


<span id="0089503a"></span>
## Create dashboard

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b04f8bac1094904b47057264a675b0c~tplv-goo7wpa0wc-image.image" width="3576px" /></div>
