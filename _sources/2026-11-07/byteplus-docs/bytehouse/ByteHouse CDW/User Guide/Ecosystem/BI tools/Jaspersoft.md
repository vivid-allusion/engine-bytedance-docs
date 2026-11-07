---
title: "Jaspersoft"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Jasper"
---

<span id="859e4689"></span>
# Background information

ByteHouse allows you to connect to it via Jaspersoft using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="24a31be0"></span>
# Prepare environment

<span id="c1df0ba8"></span>
## Recommended versions


* Jaspersoft Studio Version: 6.21.3

* Jasper Server Version: bitnami/jasperreports:8.1.0


<span id="bba8786e"></span>
## Install JasperReports

Execute the following command to install. Open http://localhost:8080/ in a browser to access the JasperServer UI.

```Bash
docker network create jasperreports-network

docker run -d --name mariadb \
  --env ALLOW_EMPTY_PASSWORD=yes \
  --env MARIADB_USER=bn_jasperreports \
  --env MARIADB_PASSWORD=bitnami \
  --env MARIADB_DATABASE=bitnami_jasperreports \
  --network jasperreports-network \
  --volume /YOUR_MARIADB_DATA_PATH:/bitnami/mariadb \
  bitnami/mariadb:latest

docker run -d --name jasperreports \
  -p 8080:8080 -p 8443:8443 \
  --env JASPERREPORTS_DATABASE_USER=bn_jasperreports \
  --env JASPERREPORTS_DATABASE_PASSWORD=bitnami \
  --env JASPERREPORTS_DATABASE_NAME=bitnami_jasperreports \
  --network jasperreports-network \
  --volume /YOUR_JASPERREPORT_DATA_PATH:/bitnami/jasperreports \
  bitnami/jasperreports:8.1.0
```


For related issues, refer to the official documentation: https://hub.docker.com/r/bitnami/jasperreports

<span id="94765a4c"></span>
## Install Jaspersoft Studio

Download the installation package and execute the installation, for details please refer to the official documentation: https://community.jaspersoft.com/download\-jaspersoft/community\-edition/jaspersoft\-studio_6.21.3.

<span id="521f7f17"></span>
# Jaspersoft Studio build report

<span id="ce092e43"></span>
## Connect through ClickHouse data adapter


1. Enter the connection information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee35e3ba049d43cc95de6a19bf6ee171~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |You can customize the data adapter name. ||
   |JDBC Driver |`com.clickhouse.jdbc.ClickHouseDriver` ||
   |JDBC URL |`jdbc:clickhouse://<HOST>:8123/<database_name>`.<br><br><br>* HOST: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* Database: You can log in to the ByteHouse Console, and click Database to view and copy the database you want to connect. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set it as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

2. Fill in the connection properties

   * `compress:0`

   * `server_version:54021`

   * `ssl:true`

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/315f9bd8b0084a89871dc86c4c842daf~tplv-goo7wpa0wc-image.image) </span>

3. Enter the driver file path.

   Please download the file from [this link](https://github.com/ClickHouse/clickhouse-java/releases/download/v0.6.3/clickhouse-jdbc-0.6.3-http.jar) and load it locally.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b863498c6a5b4078b4b63f0b32ad17d0~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   

4. Test the connection. An interface prompt of "Succeed" indicates a successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da2b7998eebe4c46b2bcc45023a6f68a~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   


<span id="768d10de"></span>
## Connect using the MySQL data adapter


1. Enter the connection information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03b205ae9a4649fbb2758494e9cf85c7~tplv-goo7wpa0wc-image.image" width="3838px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Name |You can customize the data adapter name. ||
   |JDBC Driver |`com.mysql.jdbc.Driver` ||
   |JDBC URL |`jdbc:clickhouse://<HOST>:3306/<database_name>`.<br><br><br>* HOST: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* Database: You can log in to the ByteHouse Console, and click Database to view and copy the database you want to connect. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set it as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

2. Import Driver Files.

   Please download it from [the link](https://repo1.maven.org/maven2/mysql/mysql-connector-java/8.0.28/mysql-connector-java-8.0.28.jar) to your local machine and load it from there.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad096c7a5e3a4e3c903c19e42204bca9~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   

3. Test connection. An interface prompt of "Succeed" indicates a successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b03efec9171342f39e6e1e9cb9985dc5~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   


<span id="7d8ddde6"></span>
# Jaspersoft server

<span id="c0bf2d0c"></span>
## Preparation

<span id="f90c1981"></span>
### Create JasperReport server

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0edaf93c8071485cbc1f712ecd315914~tplv-goo7wpa0wc-image.image" width="3584px" /></div>



1. Enter connection information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/23711b6a04bc4aff8df1a71c2ef7584e~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Name |You can customize the server name. |
   |URL |`http://<ip>:8080/jasperserver/`. Configure `<ip>` as the domain name of the Jasper server or IP address. |
   |User |`jasperadmin` |
   |Password |`jasperserver password` |
   

2. Test Connection. An interface prompt of "Succeed" indicates a successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e87c2ae2a354ad6998051c8fd4876ed~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   


<span id="048a8182"></span>
### Create ClickHouse data source

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6031dd05e2f3478ca48a40fdecb7a8f7~tplv-goo7wpa0wc-image.image" width="3840px" /></div>



1. Upload Clickhouse JDBC driver. JDBC driver package name: com.clickhouse.jdbc.ClickHouseDriver

   Driver download URL: https://github.com/ClickHouse/clickhouse\-java/releases/download/v0.6.3/clickhouse\-jdbc\-0.6.3\-http.jar

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d4eb948efd54d77b6f56f846532670c~tplv-goo7wpa0wc-image.image" width="3832px" />   </div>
   

2. Enter the connection information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/477e68b360094e2cb01d6a680646ecb4~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |URL |`jdbc:clickhouse://<HOST>:8123/<database_name>ssl=true&compress=0&server_version=54021`<br><br><br>* HOST: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* Database: You can log in to the ByteHouse Console, and click Database to view and copy the database you want to connect. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Test connection. An interface prompt of "Succeed" indicates a successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae376c4c8c2742cbac13265a9122e085~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

4. Save this data source.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6312e0dc028a4c5fbd30037fbfcba7e6~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   


<span id="862a2b9d"></span>
### Create MySQL data source

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fdd07a86a1ca443ca9a81f1f28840e4c~tplv-goo7wpa0wc-image.image" width="3840px" /></div>



1. Upload Driver. Driver package name: `com.mysql.jdbc.Driver`

   Driver download URL: https://repo1.maven.org/maven2/mysql/mysql\-connector\-java/8.0.28/mysql\-connector\-java\-8.0.28.jar

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcb0e76b18784c4494c226979e5a1a40~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   

2. Enter the connection information.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39b21cac143f49a1aa3aa52301b124d4~tplv-goo7wpa0wc-image.image" width="3840px" />   </div>
   

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |Host |Enter the server address. Refer to [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for details. ||
   |Port |3306 ||
   |Database |The ByteHouse database you created. ||
   |URL |`jdbc:clickhouse://<HOST>:8123/<database_name>`<br><br><br>* HOST: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* Database: You can log in to the ByteHouse Console, and click Database to view and copy the database you want to connect. ||
   |Username & Password |* Username: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   

3. Test connection. An interface prompt of "Succeed" indicates a successful connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cab9884fcaa14f799b574712ae97ca80~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

4. Save this data source.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21146d0054674281be7346c467de745e~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   


<span id="6f5ae025"></span>
## Execute query

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bba8524d1084fa3bc798b762ce8ecb7~tplv-goo7wpa0wc-image.image" width="3838px" /></div>



1. Customize the query name.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62d1cccee4774fd39fb5e1c5dbdab474~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

2. Select a data source.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a71131b1b68478f8ebea6e0188672ba~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

3. Write the SQL query statement.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/911340beef434a0a9fdf65c33152e7fa~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   


<span id="72560bc3"></span>
## Publish report

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ba5af5107c84bb7973681805fe09ac6~tplv-goo7wpa0wc-image.image" width="3584px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6befee6709a44b1cb09bcd91a02c98de~tplv-goo7wpa0wc-image.image" width="3584px" /></div>



1. Select the data source created in step 2 the [Execute query](https://docs.byteplus.com/docs/bytehouse/Jasper#6f5ae025) section.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a3b705ba19064b479956ff149d73eb07~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

2. Select the query created in step 3 in the [Execute query](https://docs.byteplus.com/docs/bytehouse/Jasper#6f5ae025).

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9655e3226bb435eb77d8977826aeeab~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

3. Click Finish to pushi the report.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cff532c0ed294704aae90583dd4aa234~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
   

4. You can view the corresponding report under the Reports directory.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbc5e7dc3415478d9cbfe0bc45b3cd6c~tplv-goo7wpa0wc-image.image) </span>

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f44666c9d034419a404832387710829~tplv-goo7wpa0wc-image.image" width="3584px" />   </div>
