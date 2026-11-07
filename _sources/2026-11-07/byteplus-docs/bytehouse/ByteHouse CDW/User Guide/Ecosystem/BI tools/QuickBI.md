---
title: "QuickBI"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/quickbi"
---

Quick BI supports connecting to BytePlus ByteHouse over the public network. As ByteHouse supports both ClickHouse and MySQL drivers, you can choose the connection method according to your preference. Once connected, you can analyze and display data on Quick BI. This article introduces how to add ByteHouse (ClickHouse driver) and ByteHouse (MySQL driver) data sources in QuickBI.

<span id="523d19e5"></span>
# Background information

ByteHouse allows you to connect to it via QuickBI using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="7ab538e7"></span>
# Configure ByteHouse

As Alibaba Cloud QuickBI is a SaaS cloud\-based BI tool, it only supports data interfacing via the public network. Therefore, before interfacing with QuickBI, you need to follow the steps below to prepare for the public network interfacing on the ByteHouse side.

<span id="065477a2"></span>
## Step 1: Configure public domain name

After logging in to the ByteHouse console, go to the **Tenant management** \> **Basic information** page at the top, check the network group configuration, and ensure it is linked to a VPC and associated with a public domain name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/504bc95096414d22bb24d8cbd2ca8fbe~tplv-goo7wpa0wc-image.image) </span>


* If not linked to a VPC and public domain name, you need to follow instructions in [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) to complete the configuration.

* After completing the binding, you can click to copy the public Domain Name for subsequent configuration of QuickBI parameters.


<span id="0f023eca"></span>
## Step 2: Obtain API key

Go to the **Tenant management** \> **Connection information** page at the top, create a new API key in the API Key module, and save the API key locally for later Configuration use.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba9bc7147a694d239cbc283aaf0f987b~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">An account can create at most two API Keys. If you have previously created an API Key, you can also use the already created API Key.</div>


<span id="be259aae"></span>
## Step 3: Set default virtual warehouse

Go to the **Tenant management** \> **Parameter setting** page at the top, view the default virtual warehouse that has been set, and ensure that this virtual warehouse is in a running state and has not been stopped. The data query and other operations after QuickBI integrates with ByteHouse will use the default virtual warehouse configured here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0000f7fa9cf34059a216fd9b01ceb16f~tplv-goo7wpa0wc-image.image) </span>

<span id="26bf943f"></span>
# Configure QuickBI

ByteHouse supports both ClickHouse and MySQL drivers. When integrating with QuickBI, based on usage preferences, you can choose to use either ClickHouse or MySQL driver. Both integration methods have similar Configuration settings. The key points of the integration configuration are shown below, with detailed interfaces as per QuickBI's product specifications.

<span id="b9cd77eb"></span>
## Step 1: Create data source


1. Log in to the Quick BI Console, enter the data source creation interface from the Create Data Source entry, and select a MySQL data source or ClickHouse data source based on usage preferences.

2. Configure data source integration parameters. You can refer to and change the following core integration parameters; keep other parameters at their default settings.

   
   |**Name** |**Configuration Description: MySQL Datasource** |**Configuration Description: ClickHouse Datasource** |
   |---|---|---|
   |**Database Source** |Select: **Self\-built**. ||
   |**Display Name** |Customize the display name of the datasource. Please type in a standard name; avoid using special characters and do not include spaces before or after. ||
   |**Database address** |Configuration is as set on the ByteHouse side, obtained from **Tenant management** \> **Basic information** \> **Network information** in the public domain name. ||
   |**Port** |The corresponding port number of the database, keep the default `3306`. |The corresponding port number of the database, keep the default `8123`. |
   |**Database** |Custom database name when deploying the ByteHouse database. ||
   |**Username** and **Password** |Username and password for logging into the ByteHouse database via IAM user or database user. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).<br><br><br>* Use an IAM user<br><br>   * user: defaults to `bytehouse`.<br><br>   * password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details.<br><br>* Use a database user<br><br>   * Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>      * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>      * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>      * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>         Examples:<br><br>         * Default env: `30xxxxxxxx::demouser`<br><br>         * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>   * Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). ||
   |**Database Version** |Suggestion: Select **8.0**. The current version MySQL 8.0 has been verified and can function normally; it is recommended to use this version. |No involvement |
   |**SSL** |Activate the Security Agreement SSL.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encrypted authentication to protect data security; therefore, you need to enable SSL.</div><br> ||
   

3. Click **Connection Test** to conduct a connectivity test for the data source. After a successful test, click **Confirm** to complete adding the data source.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the connection test failed, please check if the configuration parameters are correct and if ByteHouse's default calculation group is functioning properly. If the default calculation group has not been set up or if its state is abnormal, it might cause the connection test to fail.   </div>
   

<span id="b2b1ed61"></span>
## Step 2: Validate QuickBI


1. You can verify the integration of QuickBI with ByteHouse by creating datasets.

   On the QuickBI Create Dataset page, you can select the ByteHouse MySQL or ClickHouse data source created in the steps above and create datasets based on the data source. For more details on dataset operations, please see [Alibaba Cloud Help Documentation](https://www.alibabacloud.com/help/en/quick-bi/user-guide/create-a-dataset?spm=a2c63.l28256.help-menu-30343.d_2_1_0.411c1b76HOWUps).

2. You can also create data analysis dashboards based on ByteHouse datasets, with operation details available in [Alibaba Cloud Help Documentation](https://www.alibabacloud.com/help/en/quick-bi/user-guide/create-a-dataset?spm=a2c63.l28256.help-menu-30343.d_2_1_0.411c1b76HOWUps).
