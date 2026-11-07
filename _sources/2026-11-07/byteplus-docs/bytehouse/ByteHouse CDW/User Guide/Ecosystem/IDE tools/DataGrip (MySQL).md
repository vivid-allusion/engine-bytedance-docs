---
title: "DataGrip (MySQL)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/datagrip-mysql"
---

DataGrip is an Integrated Development Environment (IDE) designed by JetBrains specifically for Database Developers and Administrators. It supports various Database Management Systems, offers smart code completion, and facilitates easy integration with version control.

This document will introduce how DataGrip connects to ByteHouse Cloud Data Warehouse (CDW) using JDBC drivers via TCP.

<span id="891d9061"></span>
# Background information

ByteHouse allows you to connect to it via DataGrip using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its permissions are determined by IAM permission policies as well as the ByteHouse resource and data permissions you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data permissions. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="f38c2569"></span>
# Prerequisites


1. Please install [DataGrip](https://www.jetbrains.com/zh-cn/datagrip/) in advance and acquire the corresponding commercial authorization.

2. You can set the default connection's virtual warehouse/database on the **Tenant management** \> **Parameter Setting** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="9d5f9b47"></span>
# Using DataGrip to connect ByteHouse


1. Launch DataGrip and click the  **+**  icon on the Database Explorer tab, select *Data Source \-\> MySQL.* 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d762818056f4b15904bd365e09c79bc~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the interface prompts a need to download drivers, please click "Download" to complete the driver download.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/793efae6c2d84d9299759409d8aa0e7f~tplv-goo7wpa0wc-image.image" width="484px" />   </div>
   

2. Fill in the fields below.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dbae6251bb14d7aae4bde7443d55fcf~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |Customize your connection name. ||
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |The default port is 3306. ||
   |User & Password |The user and password for logging in to ByteHouse.<br><br><br>* User: defaults to `bytehouse`.<br><br>* Password: Set as the <API_Key\> of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |URL |```Bash```<br>```jdbc:bytehouse://{HOST}:{PORT}/?secure=true&user=bytehouse&password={API_KEY}```<br> |```Bash```<br>```jdbc:bytehouse://{HOST}:{PORT}/?secure=true&user={accountID_or_accountName}::{username}[::{envID}]&password={password}```<br> |
   

3. Switch to the SSH/SSL tab and check `Use SSL`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c7dda3481b64178a5ce34a756945213~tplv-goo7wpa0wc-image.image) </span>

4. Click **Test Connection**, if it displays Success then the connection is successful.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to potential differences in recognizing special characters in the Password field of URLs by third\-party software, if you cannot connect correctly even after setting up as directed above, please try manually entering the password in the Password box and test the connection again.   </div>
   

<span id="bf0d48ad"></span>
# References

To learn more about DataGrip, please visit [DataGrip official documentation](https://www.jetbrains.com/help/datagrip/getting-started.html).
