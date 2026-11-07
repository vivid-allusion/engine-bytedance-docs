---
title: "Metabase"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-metabase"
---

<span id="a8753c8d"></span>
# Background information

ByteHouse allows you to connect to it via Metabase using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="1838d938"></span>
# Environment preparation

<span id="7d25b4a2"></span>
## Run Metabase `Docker`

```Bash
docker run -d -p 3000:3000 --name metabase metabase/metabase
```


For specific usage, refer to the official Metabase website: https://www.metabase.com/start/oss/

Open http://localhost:3000/ in your browser to access the Metabase interface.

<span id="76bbfac4"></span>
## Download the Clickhouse plugin jar file

Because Metabase is deployed through a Docker container, you need to enter the container to download the Clickhouse Metabase plugin jar file to the plugins directory.

```Bash
docker exec -it <container_id> bash
cd plugins
wget https://github.com/ClickHouse/metabase-clickhouse-driver/releases/download/1.3.3/clickhouse.metabase-driver.jar
```


Log out and restart the container

```Bash
docker restart <container_id>
```


Reopen http://localhost:3000/ to access the Metabase interface.

<span id="ef1d5638"></span>
# ByteHouse data preparation

Here, taking the SSB dataset as an example, execute the following command to generate data. Please note, if you do not need to perform performance tests, you can reduce the data amount.

```SQL
./dbgen -s 1 -T c 
./dbgen -s 1 -T l 
./dbgen -s 1 -T p 
./dbgen -s 1 -T s
```


<span id="ae9aef08"></span>
# Connect to Metabase


1. Click the gear icon in the top right corner and select **Admin Settings** to access your [Metabase administration page](http://localhost:3000/admin/settings/setup).

2. Click **Add a database**. Or, you can click the "**Database**" tab and select the "**Add database**" button.

3. If your driver is installed successfully, you will see **ClickHouse** in the dropdown menu under **Database type**:

   <span>![图片](https://clickhouse.com/docs/assets/images/metabase_01-f3b14b02c32d28eca9015a4161bd57ef.png) </span>

4. Specify a **Display name** for your database; you can use any name you like.

5. Input the connection details for your ByteHouse database.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c71625f5ef54110b97fd32624e67745~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |host |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
   |port |Database port number. Set it as 8123. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}:`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |database |Configure as the database name created in ByteHouse. ||
   |Use a secure connection (SSL) |Enable secure connection (SSL).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encrypted authentication to protect data security. Therefore, you need to enable SSL.</div><br> ||
   

6. Click the "**Save**" button, and Metabase will scan the tables in the database.
