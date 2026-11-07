---
title: "DBeaver (TCP)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-DBeaver"
---

DBeaver Community Edition is a free cross\-platform database tool for developers, database administrators, and data analysts. DBeaver supports all popular SQL databases such as MySQL, MariaDB, PostgreSQL, SQLite series, and others.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Paging is not supported under the current TCP mode; previewing data in tools might be slower if the volume is large.</div>


<div data-tips="true" data-tips-type="tip">In this case, it is suggested to use HTTP method and you can refer to <a href="https://docs.byteplus.com/docs/bytehouse/dbeaver-clickhouse">DBeaver (ClickHouse)</a>.</div>


<span id="2cb6a729"></span>
## Background information

ByteHouse allows you to connect to it via DBeaver using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its permissions are determined by IAM permission policies as well as the ByteHouse resource and data permissions you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data permissions. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="c5f55252"></span>
## Prerequisites


1. Please download and install DBeaver in advance through the [official website](https://dbeaver.io/download/).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use DBeaver version 24.2.2 or above for better compatibility.   </div>
   

2. Click [here](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) to acquire the latest version of the ByteHouser JDBC Driver jar file.

3. You can set the default connection virtual warehouse/database on the **Tenant management**  **\- Parameter settings** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="a43b8875"></span>
## Configure ByteHouse Driver


1. Launch DBeaver, under the **Database** tab, select **Driver Manager.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b73fc722e33f4b17b84cf099bb9c0a2e~tplv-goo7wpa0wc-image.image) </span>

2. Click "New."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/277169c7e7eb424a899a15583a3f408d~tplv-goo7wpa0wc-image.image) </span>

3. In the settings tab, enter the following information as shown:

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Class name: <code>com.bytedance.bytehouse.jdbc.ByteHouseDriver</code>   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">URL Template: <code>jdbc:bytehouse://{host}:{port}/?secure=true</code>   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Default Port: <code>19000</code>   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c259943dad15402eb0dcd0876aad0e55~tplv-goo7wpa0wc-image.image) </span>

   * Class name: `com.bytedance.bytehouse.jdbc.ByteHouseDriver`.

   * URL Template: `jdbc:bytehouse://{host}:{port}/?secure=true`. The `{HOST}:{PORT}` parameter depends on the region where the cluster is located. Please refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for relevant information.

   * Default Port: `19000`.

4. Switch to the "Libraries" tab, click **Add File**, and select the ByteHouse JDBC Driver file prepared earlier.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19cbc9be7fe8404f82c9e1abe91eb598~tplv-goo7wpa0wc-image.image) </span>

5. Switch to the "Advanced Parameters" tab and deselect the two settings shown in the image below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If this item is ignored, querying tables with many rows may result in errors, such as:   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><code>SQL Error [396]: DB::ExceptionDB::Exception: Limit for result exceeded, max rows: 200.00, current rows: 8.19 thousand SQLSTATE: 54000. Stack trace:...</code>   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9752bd65070c41099099ec9a210fb0ee~tplv-goo7wpa0wc-image.image) </span>

6. Click Confirm to save.


<span id="fd943013"></span>
## Connect to ByteHouse


1. Click **Database \- New Database Connection**, and on the page, select "**ByteHouse**" then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc501ac7efdf41f488cc340238c47f0b~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the following fields:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2298e96983bd4e9d84effbdd1517a335~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |Database port number. Set as 19000. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the <API_Key\> of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Click on the bottom left "Test Connection", if it displays **Connected,**  then the setup is successful.

4. Click **Finish**, to then operate the ByteHouse Database on the DBeaver program homepage.
