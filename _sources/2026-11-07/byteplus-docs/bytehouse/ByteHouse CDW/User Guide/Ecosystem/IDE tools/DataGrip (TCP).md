---
title: "DataGrip (TCP)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-DataGrip"
---

DataGrip is an integrated development environment (IDE) designed by JetBrains for database developers and administrators. It supports various database management systems, offers intelligent code completion, and facilitates version control integration.

This tutorial introduces how DataGrip connects to ByteHouse Cloud Data Warehouse (CDW) via JDBC driver, using TCP.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Pagination is not supported in the current TCP mode; if you view data in tools and the data volume is large, the preview will be slow.</div>


<div data-tips="true" data-tips-type="warning">In this case, it is recommended to connect using the HTTP protocol method, refer to <a href="https://docs.byteplus.com/docs/bytehouse/datagrip-clickhouse">DataGrip (ClickHouse)</a>.</div>


<span id="25504b9b"></span>
# Background information

ByteHouse allows you to connect to it via DataGrip using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="32861b00"></span>
# Prerequisites


* Please install [DataGrip](https://www.jetbrains.com/zh-cn/datagrip/) in advance and acquire the corresponding commercial authorization.

* Click [here](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) to download the jar file of the latest version of ByteHouser JDBC Driver.

* You can set the default virtual warehouse/database on the **Parameter setting** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="5153f173"></span>
# Usage restrictions

When using the Bytehouse JDBC TCP driver to connect, the setting `max_result_rows` may not activate. Therefore, the pagination function is not well supported. The expected returned rows may differ from the actual returned rows.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f9f016bc7134b59809e118201ccf408~tplv-goo7wpa0wc-image.image" width="3128px" /></div>


This issue can be solved by setting up as follows on DataGrip:


1. Enter **DataGrip\-Settings\-Database\-Data Editor and Viewer** tab.

2. Uncheck the first item "Limit page size to:" under **Limitations** .

3. Click the OK button to save the settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e50f9fa238b4a5a8562e9a440b6e4bc~tplv-goo7wpa0wc-image.image) </span>


<span id="b2be3b6e"></span>
# Connect to ByteHouse using DataGrip


1. Launch DataGrip, in the Database Explorer tab, click the  **+**  icon, and select **Driver** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/825ac2ad07dd411bbdc4fbb222053b7c~tplv-goo7wpa0wc-image.image) </span>

2. Name the driver, such as "*ByteHouse JDBC Driver*". Click the + sign in *Driver Files*, select *Custom JARs* in the pop\-up window, and choose the locally downloaded JDBC driver jar file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f2b891b4645a479fa3a4628f8122c387~tplv-goo7wpa0wc-image.image) </span>

3. In **Class**, select `*com.bytedance.bytehouse.jdbc.ByteHouseDriver*`, and click Apply to save.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acce13e61a764ba8bfd8fc65cb958517~tplv-goo7wpa0wc-image.image) </span>

4. In the *Database Explorer* tab, click the  **+**  icon, select *Data Source* \-\> *ByteHouse JDBC Driver*.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e7f398f314849878d5353b58aa0e0fb~tplv-goo7wpa0wc-image.image) </span>

5. Configure data source connection information. You can use either an IAM user or a database user for connection. Configuration parameter descriptions are shown in the table below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4d055aaaeea48dd86f27f9c5cd61d35~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |Customize your connection name. ||
   |User & Password |The user and password for logging in to ByteHouse.<br><br><br>* User: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |URL |Format:<br><br>```Bash```<br>```jdbc:bytehouse://{HOST}:{PORT}/?secure=true&user=bytehouse&password={API_KEY}```<br><br><br><br>* `{HOST}`: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* `{PORT}`: Set as 19000. |Format:<br><br>```Bash```<br>```jdbc:bytehouse://{HOST}:{PORT}/?secure=true&user={accountID_or_accountName}::{username}[::{envID}]&password={password}```<br><br><br><br>* `{HOST}`: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* `{PORT}`: Set as 19000. |
   

6. Click **Test Connection**, if it displays Succeeded, the connection is successful.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you properly configure settings according to the above guidelines and still cannot connect due to third\-party software not recognizing special characters in the Password field of the URL, try filling in the password manually in the Password field and testing the connection again.   </div>
   

<span id="8bcb969a"></span>
## Reference

To learn more about DataGrip, please visit [DataGrip official documentation](https://www.jetbrains.com/help/datagrip/getting-started.html).
