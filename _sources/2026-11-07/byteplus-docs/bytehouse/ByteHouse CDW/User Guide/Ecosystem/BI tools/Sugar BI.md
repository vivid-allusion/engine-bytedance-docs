---
title: "Sugar BI"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/suger-bi"
---

Sugar BI supports connection to ByteHouse over the public network. Once successfully connected, you can analyze and display data on Sugar BI. This article explains how to add a ByteHouse data source in Sugar BI.

<span id="da9427ea"></span>
# Background information

ByteHouse allows you to connect to it via Sugar BI using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="57fff8b1"></span>
## Prerequisites

For information on connecting to ByteHouse, refer to [Retrieve ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity).

<span id="c72aac9f"></span>
## Steps


1. Log in to the Sugar BI Console, and enter the interface to add a data source via the create data source portal.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c2c3b95ab13f44efbc55c08a1946ca9e~tplv-goo7wpa0wc-image.image) </span>

2. Select the **public network** connection type, and in the **Configuration connection** dialog, you can complete the following configurations based on your business scenarios.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cedfd60f9b1e4da5bbbdaeef174f94fd~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Network of data source |Select ClickHouse. ||
   |Data source name |Display name for the data source configuration list. Enter a standard name without special characters or leading/trailing spaces. ||
   |Database source Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port number |Database port number. Set it as 8123. ||
   |Database |The database name customized during the deployment of ByteHouse database. ||
   |User name & Password |* User name: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User name: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Click **Test Connection** to test the connectivity of the data source.

4. After a successful test, click **Confirm** to complete the addition of the data source.

5. After creating a data source, click Preview Data, and you will be able to see the table and example data.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1756ab4a3e4140f0a2797731573156e9~tplv-goo7wpa0wc-image.image) </span>
