---
title: "DBeaver (ClickHouse)"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/dbeaver-clickhouse"
---

DBeaver Community Edition is a free cross\-platform database tool for developers, database administrators, and data analysts. DBeaver supports all popular SQL databases, such as MySQL, MariaDB, PostgreSQL, SQLite series, and others.

<span id="87d5e963"></span>
## Background information

ByteHouse allows you to connect to it via DBeaver using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its permissions are determined by IAM permission policies as well as the ByteHouse resource and data permissions you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data permissions. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="20928aee"></span>
## Prerequisites


* Please download and install DBeaver in advance through the [official website](https://dbeaver.io/download/).

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use DBeaver version 24.2.2 and above for better compatibility.   </div>
   

* You can set the default connection's virtual warehouse/database on the **Tenant management \- Parameter settings** page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2096bc67168f4254bb3ba65ec67fb083~tplv-goo7wpa0wc-image.image) </span>


<span id="802a301c"></span>
## Connect to ByteHouse


1. Click **Database \- New Database Connection** and select "ClickHouse" on the page, then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d29447d01b9a4ae5a697b1d2f4ddfe37~tplv-goo7wpa0wc-image.image) </span>

2. Fill in the following fields:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c304a634e0854cb59f04c66cfb607bd4~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |Port |Database port number. Set as 8123. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the <API_Key\> of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>   * Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Switch to the SSL page and activate the SSL function.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/403515dfcc224fd08442d0e59d3f056f~tplv-goo7wpa0wc-image.image) </span>

   If your version differs from the above interface, set the ssl parameter to true on the Driver properties page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/724df9ff0a574ad3a5485d20b856e588~tplv-goo7wpa0wc-image.image) </span>

4. (Optional) Configure the default virtual warehouse on the driver properties tab.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you have multiple virtual warehouses, you can refer to this step to set the default virtual warehouse to be used after connecting to ByteHouse; if not set, then the console settings default virtual warehouse will be used after the connection.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fdcfb1ac5a84e6299546e43e9ff4bb4~tplv-goo7wpa0wc-image.image) </span>

   * Set custom_settings to `virtual_warehouse=your_virtualwarehouse_id`.

   * Of which `your_virtualwarehouse_id` is the default virtual warehouse ID used after connecting to ByteHouse, and you can view the corresponding virtual warehouse ID on the **Virtual warehouse** page in the ByteHouse console.

5. Click on the bottom left "Test Connection"; if it **displays 'Connected'** , then the setup is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06c55d0912874461a25bba1fa6e98c44~tplv-goo7wpa0wc-image.image) </span>

6. Click **Complete** to operate the ByteHouse database on the DBeaver program homepage.


<span id="1c7efaeb"></span>
## FAQ

<span id="87d312a8"></span>
### Transport error: 500

If you are using a newer version of DBeaver, you may encounter the following error:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5199da363e8741b880b082bd4ce21c96~tplv-goo7wpa0wc-image.image) </span>

You can resolve this issue by configuring the DBeaver driver manager. The operations are as follows:


1. Download the [JDBC Driver v0.4.6 file](https://github.com/ClickHouse/clickhouse-java/releases/download/v0.4.6/clickhouse-jdbc-0.4.6.jar).

2. In DBeaver, go to **Database** \> **Driver Manager** to enter the Driver Manager interface. Click **ClickHouse**, then click **Edit**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/051077884ad54729811d623826199412~tplv-goo7wpa0wc-image.image) </span>

3. In the edit driver interface, click the **Libraries** tab.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1d7d19668d074103b9328a6f7ecbc111~tplv-goo7wpa0wc-image.image) </span>

4. Click **Add File** and upload the JDBC Driver v0.4.6 file downloaded in step 1.

5. Select `com.clickhouse:clickhouse-jdbc:RELEASE [0.x.x]` and click **Delete**.

6. Click **OK**.


<span id="537be46a"></span>
### LZ4 is not supported error

If you encounter the following error during connection:

```Bash
LZ4 is not supported. Please disable compression(compress=0), modify the algorithm(e.g. compress_algorithm=gzip), or add the missing libraries to the classpath.
```


You can resolve this issue by configuring the driver property in the connection settings and setting `compress` to false.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe5d87f98ba749fb8c0cd349cce5497e~tplv-goo7wpa0wc-image.image) </span>

<span id="ed111ca3"></span>
### Connection reset error

If you encounter the following error during connection:

```Bash
Connection reset
```


You can resolve this issue by configuring the driver property in the connection settings and setting `ssl` to true.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/19186ed855e94d4eabd89c1ed3b100b5~tplv-goo7wpa0wc-image.image) </span>

<span id="1142fba5"></span>
### Version incompatibility error: only works with ClickHouse servers 20.7 and above

If you encounter the following error during the connection process:

```Bash
We apologize, but this driver only works with ClickHouse servers 20.7 and above. Please consider to upgrade your server to a more recent version.
```


You can resolve this issue by setting the `server_time_zone` and `server_version` parameter values in the **Driver properties** as shown below.


* **server_time_zone**: Set to `Asia/Shanghai`. If you are in a different time zone, set it to the corresponding time zone based on your actual situation.

* **server_version**: Set to 21.8.7.1.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ec2b9a60cc74d15b179e535d2e1f088~tplv-goo7wpa0wc-image.image) </span>
