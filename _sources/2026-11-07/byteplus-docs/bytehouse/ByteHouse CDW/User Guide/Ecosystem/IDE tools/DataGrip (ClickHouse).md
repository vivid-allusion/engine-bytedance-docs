---
title: "DataGrip (ClickHouse)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/datagrip-clickhouse"
---

DataGrip is a specialized Integrated Development Environment (IDE) designed by JetBrains for database developers and administrators. It supports various Database Management Systems, provides intelligent code completion, and facilitates version control integration.

This document will introduce how DataGrip connects to ByteHouse Cloud Data Warehouse (CDW) through the open\-source ClickHouse driver.

<span id="5df65ae5"></span>
# Background information

ByteHouse allows you to connect to it via DataGrip using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its permissions are determined by IAM permission policies as well as the ByteHouse resource and data permissions you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data permissions. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="a2be16d6"></span>
# Prerequisites


1. Please install [DataGrip](https://www.jetbrains.com/zh-cn/datagrip/) in advance and acquire the corresponding commercial authorization.

2. You can configure the default connection virtual warehouse/database on the **Tenant management** \> **Parameter setting** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="af8ed095"></span>
# Connect to ByteHouse using DataGrip


1. Launch DataGrip, click the  **+**  icon on the Database Explorer tab, and select *Data Source \-\> ClickHouse.* 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9056c9b62ece451f8e912aa8f1ff8426~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the interface reminds you to download the driver, click "Download" to complete the driver download.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/793efae6c2d84d9299759409d8aa0e7f~tplv-goo7wpa0wc-image.image" width="226px" />   </div>
   

2. Configure the ByteHouse Data Source fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbc1aaf559bf4df48e0d139288a3fd13~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |Customize your connection name. ||
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |The default port is 8123. ||
   |User & Password |The user and password for logging in to ByteHouse.<br><br><br>* User: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |URL |```Bash```<br>```jdbc:clickhouse://{HOST}:{PORT}/?secure=true&user=bytehouse&password={API_KEY}```<br> |```Bash```<br>```jdbc:clickhouse://{HOST}:{PORT}/?secure=true&user={accountID_or_accountName}::{username}[::{envID}]&password={password}```<br> |
   

3. Switch to the SSH/SSL tab and check the `Use SSL` option.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc49c765d8364286a59bc5613ee57bb2~tplv-goo7wpa0wc-image.image) </span>

4. Switch to the Schemas tab to select the database to connect to (you may click the **Refresh** button to retrieve this).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b60a9b5bf5ce45eaa548050c9ce70f69~tplv-goo7wpa0wc-image.image) </span>

5. (Optional) Set the default virtual warehouse.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have multiple virtual warehouses, you can refer to this step to set the default virtual warehouse after connecting to ByteHouse; if not set, then the console\-configured default virtual warehouse will be used after connecting to ByteHouse.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b7c510d6e0a449e485656cc2481e254d~tplv-goo7wpa0wc-image.image) </span>

   On the Advanced tab, set custom_settings to `virtual_warehouse=your_virtualwarehouse_id`, of which `your_virtualwarehouse_id` is the default virtual warehouse ID used after connecting to ByteHouse, and you can view the ID of the corresponding virtual warehouse on the **Virtual warehouse** page in the ByteHouse Console.

6. Click **Test Connection**. If it displays 'Success', the connection is successful.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Due to differences that may arise from third\-party software's recognition of special characters in the Password field within the URL, if you still cannot connect correctly after setting up accordingly, try manually filling in the password in the password box and testing the connection again.   </div>
   

<span id="83c32252"></span>
# FAQ

<span id="ba16e1b7"></span>
### [22000] Code: 0 error

If you encounter the following error during connection:

```Bash
[22000] Code: 0. DB::Exception: <Unreadable error message> (transport error: 500).
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff327bfb68ea4452a7d0d283fc95d77f~tplv-goo7wpa0wc-image.image) </span>

You can resolve this issue by adjusting the driver version of the ClickHouse datasource:

Change the driver version of the ClickHouse datasource to 0.6.3. Under the **Drivers** tab, click **ClickHouse**, then in the right\-side **Driver Files**, click  **+** , select **Provided Driver**, choose **ClickHouse**, and select version **0.6.3**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd9a82ccd4ad4f0f98a996238b469ffa~tplv-goo7wpa0wc-image.image) </span>

<span id="e70fced5"></span>
### LZ4 is not supported error

If you encounter the following error during connection:

```Bash
LZ4 is not supported. Please disable compression(compress=0), modify the algorithm(e.g. compress_algorithm=gzip), or add the missing libraries to the classpath.
```


You can fix this by disabling the `compress` parameter:

Click the added **ClickHouse datasource** on the **Data Source** tab, go to the right\-side **Advanced** tab, and set the `compress` param to `false`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6de5c198ac0840b29a4681df20a100bc~tplv-goo7wpa0wc-image.image) </span>

<span id="f4521fbf"></span>
### Connection reset error

If you encounter the following error during connection:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/228951885c0d4a26871795737b731551~tplv-goo7wpa0wc-image.image) </span>

You can resolve the issue by enabling `ssl`:

Click the added **ClickHouse Datasource** under the **Data Source** tab, then click the **Advanced** tab on the right, and set the `ssl` parameter to `true`.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfc4bdf91e0947ce9c0efd92c2882857~tplv-goo7wpa0wc-image.image) </span>

<span id="95002950"></span>
# Reference

For more details about DataGrip, please visit [DataGrip official document](https://www.jetbrains.com/help/datagrip/getting-started.html).
