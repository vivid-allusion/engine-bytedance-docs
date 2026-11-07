---
title: "TablePlus (MySQL&ClickHouse)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/tableplus-mysql-clickhouse"
---

TablePlus is a cross\-platform database management tool designed to simplify database connection, querying, editing, and management processes. It supports managing MySQL, PostgreSQL, SQLite, SQL Server, Oracle, and other databases. This article explains how to connect to and use the MySQL and ClickHouse databases created in ByteHouse within TablePlus.

<span id="dd1c1e29"></span>
## Background information

ByteHouse allows you to connect to it via TablePlus using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="6916a24f"></span>
# Prerequisites

You have installed TablePlus. For details, see the [TablePlus official website](https://tableplus.com/).

<span id="b99b9837"></span>
# Configure ByteHouse

ByteHouse supports connections via IAM users or database users. Configure your user account information before using this tool. For the difference between IAM users and database users, please refer to [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview).

<span id="051dc33d"></span>
## **Step 1 Configure network domain**

After logging into the ByteHouse console, go to the **Tenant management** \> **Basic information** page. Check the **Network information** to confirm that the VPC is bound and that a public domain is linked

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7742905ea3b344f5ac1c08f915e512b7~tplv-goo7wpa0wc-image.image) </span>


* If the VPC and public domain are not bound, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings).

* After binding, click to copy the public domain name for later parameter configuration.


<span id="62918c3d"></span>
## **step2 Set the default virtual warehouse**

Go to the **Tenant management** \> **Parameter settings** page at the top, check the set default virtual warehouse, and ensure this virtual warehouse is running and not stopped. All subsequent operations, such as data queries after connecting to ByteHouse, will use the default virtual warehouse configured here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95e5f5c8a7e349ad8155b5c213f38dee~tplv-goo7wpa0wc-image.image) </span>

<span id="078934be"></span>
## **step 3 Obtain user and password information for the connection string**

<span id="8251bec0"></span>
### **Use an IAM user to connect**

IAM users use an API Key as the connection password. You can create a new API key in the API Key module on the **Tenant management** \> **Connection information** page at the top and save the API key locally for later configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e13db982dd742a38d56b3893ab7045e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A sub\-account supports creating up to two API Keys. If you have previously created API Keys, you can also use the existing API Keys directly.</div>


<span id="1bda2821"></span>
### **Use a database user to connect**

The database user's account consists of the ByteHouse account, database username, account, and optionally the environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. The password is the database user's password.

<span id="a253f17a"></span>
#### Obtain account information

After logging in to the ByteHouse console, click the personal center at the top right to view and copy the account ID or name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec2175b742244948084125e4b722c53~tplv-goo7wpa0wc-image.image) </span>

<span id="060a7ac6"></span>
#### Obtain database user and password

After logging in and entering the ByteHouse console, go to the **Access control** \> **Users** page at the top. Check the user list and filter users by the **Database** category. View and copy the database username. If the database user has not been created yet, contact the administrator to create a database user by referring to [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account).

The database user's password is set by the administrator. Contact the administrator to obtain the corresponding password. If the password is lost or forgotten, contact the administrator to reset it. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c86f9e2b39af4adda566073e67eaf85c~tplv-goo7wpa0wc-image.image) </span>

<span id="4836be2b"></span>
#### (Optional) Retrieve environment information

If using the default environment, no configuration is needed. To use another environment, specify its name. You can log in to the ByteHouse console, then check the current environment name on the **Basic information** page under **Tenant management** at the top.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a94f89579cbb41b8b38e35a26f77b875~tplv-goo7wpa0wc-image.image) </span>

<span id="636707c0"></span>
# TablePlus Configuration

You can create MySQL or ClickHouse data sources using TablePlus and connect them to ByteHouse.

<span id="070ca24f"></span>
## Connect to MySQL **database driver**


1. Launch TablePlus, right\-click in the blank area on the right side of the interface, then click **New** \> **Connection**.

2. Search for and select MySQL in the popup window, then click **Create**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44ce3f03bae941e994271a9871073fdd~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

3. In the MySQL Connection popup, fill in the configuration information according to the connection details obtained from [ByteHouse Configuration](https://docs.byteplus.com/docs/bytehouse/tableplus-mysql-clickhouse#b99b9837).

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/833b2896d4c446768a0616fa9ff1371c~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

   
   |Parameter |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |Customize your connection name. ||
   |Host/IP |Set as ByteHouse network domain name in the format: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can find this in ByteHouse Console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). ||
   |Port |Database port number, set to the fixed value: 3306. ||
   |User & Password |Use the API Key as both the User and Password. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* The User is the first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `xxxx`.<br><br>* The Password is the second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `yyyy`. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Database |Enter your database name or leave blank. ||
   |SSL |Select REQUIRED. ||
   

4. Click **Test** to check if the connection is successful. When the input box background turns green, it indicates a successful connection.

   The example of a successful connection is shown below:

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46314186885a45d28b71b256b02a0614~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

5. After successfully testing the connection, click **Connect** to create the connection.

6. (Optional) Configure the virtual warehouse information. Click **Bootsrap commands** to add the `set virtual_warehouse='virtual_warehouse_id'` bootstrap command.

   `'virtual_warehouse_id'` should be set to the ByteHouse virtual warehouse ID you use. You can find the required virtual warehouse ID by logging into the ByteHouse console and clicking the **Virtual warehouse** tab at the top.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79470eba509a4c818073417872d5db74~tplv-goo7wpa0wc-image.image) </span>

   Before using the SQL editor each time, run `set virtual_warehouse='virtual_warehouse_id'`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da26e9c151df4c03a8da3105e5fb44a2~tplv-goo7wpa0wc-image.image) </span>


<span id="97947124"></span>
## **Connect to ClickHouse database driver**


1. Launch TablePlus, right\-click on the blank area on the right side of the interface, then click **New** \> **Connection**.

2. Search for and select ClickHouse in the pop\-up window, then click **Create**.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a4f0bae0113240779f16c74f0cc8ee29~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

3. In the ClickHouse Connection pop\-up, fill in the configuration according to the connection information obtained from [Configure ByteHouse ](https://docs.byteplus.com/docs/bytehouse/tableplus-mysql-clickhouse#b99b9837):

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4afe9cc4d9645abb665cedbe1ed8035~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

   
   |Parameters |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |Customize your connection name. ||
   |Host |Set as the ByteHouse network domain name in this format: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can find it in ByteHouse console under **Tenant management** \> **Basic information** \> **Network information**. For details, see [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486). ||
   |Port |The database port, set to the fixed value: 19000. ||
   |User & Password |The User and Password for logging into the ByteHouse database.<br><br><br>* User: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `accountID_or_accountName`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `username`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `envID`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>   * Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |Database |Enter your database name or leave empty. ||
   |SSL |Select `USE SSL(SKIP VALIDATE)`. ||
   

4. Click **Test** to verify the connection. When the input box background turns green, the connection is successful.

   An example of a successful connection is shown below:

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a56f0847262c496c9fd6ec27a9ffffaa~tplv-goo7wpa0wc-image.image" width="3830px" />   </div>
   

5. After the connection test succeeds, click **Connect** to create the connection.

6. (Optional) Configure virtual warehouse information. Click **Bootstrap commands** to add the bootstrap command `set virtual_warehouse='virtual_warehouse_id'`.

   `'virtual_warehouse_id'` is set to the ByteHouse virtual warehouse ID you use. You can find the required virtual warehouse ID by logging into the ByteHouse console and clicking the **Virtual warehouse** tab at the top.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79470eba509a4c818073417872d5db74~tplv-goo7wpa0wc-image.image) </span>

   Before each use of the SQL editor, run `set virtual_warehouse='virtual_warehouse_id'`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da26e9c151df4c03a8da3105e5fb44a2~tplv-goo7wpa0wc-image.image) </span>
