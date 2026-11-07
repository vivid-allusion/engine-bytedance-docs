---
title: "DBeaver (MySQL)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dbeaver-mysql"
---

DBeaver Community Edition is a free cross\-platform Database tool for developers, administrators, and Data Analysts. DBeaver supports all popular SQL databases, such as MySQL, MariaDB, PostgreSQL, SQLite, and others.

<span id="cacb7ee2"></span>
## Background information

ByteHouse allows you to connect to it via DBeaver using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its permissions are determined by IAM permission policies as well as the ByteHouse resource and data permissions you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data permissions. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="213354a8"></span>
## Prerequisites


* Please [download](https://dbeaver.io/download/) and install DBeaver ahead of time through the official website.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use DBeaver version 24.2.2 or above to achieve better compatibility.   </div>
   

* You can set the default virtual warehouse/database on the **Tenant management**  **\- Parameter setting** Page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="0af5216d"></span>
## Connect to ByteHouse


1. Click **Database \- New Database Connection**, select "MySQL" on the page, and click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a580ff3ad2d14093b25219afbea1f13b~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the following fields:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f9ea2be502eb4cc78a17c8d668621ca6~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Server host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |Database port number. Set as 8123. ||
   |Username & Password |[**Recommended**] **Option 1**:<br><br>Use the API Key as both the Username and Password. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* The Username is the first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `xxxx`.<br><br>* The Password is the second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `yyyy`.<br><br>   **Option 2**:<br><br>* Username: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `accountID_or_accountName`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Switch to the SSL page, activate the SSL function, check "Activate SSL" "Require SSL", and uncheck "Verify server certificate".

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7991ef0b6a974db184d89a01ea233eae~tplv-goo7wpa0wc-image.image" width="1472px" />   </div>
   

4. Click on the lower left "test connection", if it displays **Connected** then the setup is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d8a81bc269246bc846bb1fdee5f6d84~tplv-goo7wpa0wc-image.image) </span>

5. Click **Complete**, you can then operate the ByteHouse database on the DBeaver homepage.
