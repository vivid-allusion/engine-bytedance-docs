---
title: "Grafana"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/Grafana"
---

Grafana supports connecting to ByteHouse via a public network. This article introduces how to add a ByteHouse datasource in Grafana.

You can connect to Grafana using the [Altinity plugin for ClickHouse](https://grafana.com/grafana/plugins/vertamedia-clickhouse-datasource/?tab=relatedcontent) or by adding a [ClickHouse datasource](https://grafana.com/grafana/plugins/grafana-clickhouse-datasource/?tab=overview).

<span id="af6d6764"></span>
# Background information

ByteHouse allows you to connect to it via Grafana using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="1f997836"></span>
# Prerequisites


1. Have a ByteHouse account.

2. Have a Grafana Cloud account. Or have Grafana installed, and you can access it through the [official website link](https://grafana.com/docs/grafana/latest/setup-grafana/installation/).


<span id="2cb8762a"></span>
# Use Altinity plugin for ClickHouse to connect to ByteHouse

<span id="d44ebd03"></span>
## Installation

<span id="086ebc2e"></span>
### Install Altinity plugin for ClickHouse on Grafana Cloud

You can install the [Altinity plugin for ClickHouse](https://grafana.com/grafana/plugins/vertamedia-clickhouse-datasource/?tab=relatedcontent) on your Grafana Cloud instance with a single click; it may take up to 1 minute for the plugin to appear in your Grafana.


* [Register Grafana Cloud](https://grafana.com/auth/sign-up/create-user?plcmt=vertamedia-clickhouse-datasource&key=pg&value=plugins).

* For more details, please visit [plugin installation](https://grafana.com/docs/grafana/latest/plugins/installation/).


<span id="f260b1a5"></span>
### Installation on local Grafana

For local instances, install and update plugins using a simple CLI command. Plugins do not update automatically, but you will receive notifications when updates are available in your Grafana.

Install using grafana\-cli from the command line:

```Plain
grafana-cli plugins install vertamedia-clickhouse-datasource 
```


The plugin will be installed to your grafana plugins directory; the default path is /var/lib/grafana/plugins.

Click for [more information about the CLI tool](https://grafana.com/docs/grafana/latest/administration/cli/#plugins-commands).

Alternatively, you can download manually. Download the zip file and unzip it into your Grafana plugin directory, click [Download](https://grafana.com/api/plugins/vertamedia-clickhouse-datasource/versions/3.2.2/download) to obtain.

<span id="0a057820"></span>
## Connect to ByteHouse

Configure connection parameters via the Settings page.

<span id="afe884c0"></span>
### Connection Parameters

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac0320f426624fcd981eb370ee3939b1~tplv-goo7wpa0wc-image.image) </span>


|Parameter item |Use an IAM user to connect |Use a database user to connect |
|---|---|---|
|URL |Set it as `https://{host}:{port}`.<br><br><br>* Host: Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant Management** \> **Basic Information** \> **Network Information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions.<br><br>* Port: Set it as 8123 ||
|AUTH |Enable `Basic auth`. ||
|User & Password |* User: defaults to `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |* User: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |


Once configured, you can enter SQL statements in the query area.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca382fff879a410c81a5d48de5ca4ad3~tplv-goo7wpa0wc-image.image) </span>

<span id="27bd65f9"></span>
# Use ClickHouse data source to connect to ByteHouse

This function currently only supports V2 Accounts. Please contact ByteHouse support personnel to learn about Account types.

<span id="47eefd94"></span>
## Installation

<span id="d2a518db"></span>
### Install plugins on Grafana Cloud

You can install the [ClickHouse Datasource plugin](https://grafana.com/grafana/plugins/grafana-clickhouse-datasource/?tab=overview) on your Grafana Cloud instance with one click; it may take up to 1 minute to see the plugin appear in your Grafana.


* [Register for Grafana Cloud](https://grafana.com/auth/sign-up/create-user?plcmt=grafana-clickhouse-datasource&key=pg&value=plugins).

* For more details, please visit [plugin installation](https://grafana.com/docs/grafana/latest/plugins/installation/).


<span id="a0cff80f"></span>
### Install on local Grafana

For local instances, install and update plugins with simple CLI commands. Plugins do not automatically update, but you will be notified when updates are available in your Grafana.

Install using grafana\-cli tool from command line:

```Plain
grafana-cli plugins install grafana-clickhouse-datasource
```


The plugin will be installed in your grafana plugins directory; the default location is /var/lib/grafana/plugins.

Click to access [more details about the cli tool](https://grafana.com/docs/grafana/latest/administration/cli/#plugins-commands).

Or, you can manually download the .zip file appropriate for your architecture from below and unpack it into your grafana plugins directory.


* [Linux-amd64](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=linux&arch=amd64)

* [Linux-arm64](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=linux&arch=arm64)

* [Linux ARM](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=linux&arch=arm)

* [windows-amd64](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=windows&arch=amd64)

* [darwin-amd64](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=darwin&arch=amd64)

* [darwin-arm64](https://grafana.com/api/plugins/grafana-clickhouse-datasource/versions/4.5.1/download?os=darwin&arch=arm64)


<span id="8a9ef56a"></span>
## Connect to ByteHouse

Configure connection parameters through the Settings page.

Access from the Grafana main menu, where you can immediately add newly installed datasources in the Datasource section.

Next, click the "Add Datasource" button in the top right corner. The Datasource will be available for selection in the **Type** selection box.

To view the list of installed datasources, click the **Plugins item** in the main menu. **Both core and installed datasources will appear.** 

<span id="7d20dc99"></span>
### Connection Parameters


* Basic Configuration

   * Server address: Refer to [Cluster connection address {HOST}:{PORT}](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#49ca314c).

      Domain Name, corresponding to your tenant, for more details.

   * Server port: 8123

   * Protocol: HTTP

   * Secure Connection: Enable

   * Skip TLS Verify: Enable

   * Username: bytehouse

   * Password: API Key of ByteHouse. For details, refer to [Retrieve API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d9bd3430).

* Advanced configuration

   * Dial Timeout (seconds)：600

   * Query Timeout (seconds)：600

* Customize Settings

   * Virtual warehouse: Your calculation group ID



|Type |**Parameter** |**Configuration** |
|---|---|---|
|Basic settings |Server address |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant Management** \> **Basic Information** \> **Network Information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. |
||Server port |8123 |
||Protocol |HTTP |
||Secure Connection |Enable |
||Skip TLS Verify |Enable |
||Username & Password |Username and password for logging into the ByteHouse database via IAM user or database user. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889).<br><br><br>* Use IAM user<br><br>   * user: defaults to `bytehouse`.<br><br>   * password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details.<br><br>* Use database user<br><br>   * Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Step 3: Obtain ByteHouse connection information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#6b1d1889)<br><br>      * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>      * `{username}`: This is the username used to log in to the ByteHouse CDW database. You can find it in the **ByteHouse CDW Console** \> **Access control** \> **User** \> **View database username**.<br><br>      * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>         Examples:<br><br>         * Default env: `30xxxxxxxx::demouser`<br><br>         * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>   * Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
|Advanced settings |Dial Timeout (seconds) |600 |
||Query Timeout (seconds) |600 |
|Custom setting |virtual_warehouse |Your virtual warehouse ID. Go to **ByteHouse Console** \> **Tenant management** \> **Parameter settings** to view the default virtual warehouse ID. |


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d527ed19de4342e49e8242c02e1ed253~tplv-goo7wpa0wc-image.image" width="2134px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6cd3a92bd62047dc84c6423937c6f031~tplv-goo7wpa0wc-image.image" width="2052px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db71fa498fba42c0bc88a801b636df3d~tplv-goo7wpa0wc-image.image" width="1778px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01a1f6f2cf694d5ca77ed3b0ef856517~tplv-goo7wpa0wc-image.image" width="1080px" /></div>


<span id="3eb8e22e"></span>
### Run SQL statement

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd780ca9cf5a405988b0d51b140edc6b~tplv-goo7wpa0wc-image.image" width="2162px" /></div>


<span id="db26e58b"></span>
# Use MySQL data source to connect to ByteHouse


1. Go to **Home** \> **Connections** \> **Data Sources** \> **Add data source** to search and add MySQL as data source.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaed5fe52d394c86883f7fa2338ef1ad~tplv-goo7wpa0wc-image.image) </span>

2. Fill in with connection information。

   
   |**Parameter** |Description |
   |---|---|
   |Host URL |Configure it as the network domain name of ByteHouse. You can view the corresponding information in **Tenant management** \> **Basic information** \> **Network information** on the ByteHouse console. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. |
   |Database name |The database name customized during the deployment of ByteHouse database. |
   |Username & Password |Use the API Key as both the Username and Password. For details, refer to [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311).<br><br><br>* The Username is the first part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `xxxx`.<br><br>* The Password is the second part of the API Key. For example, if the obtained API Key is `xxxx.yyyy`, the User should enter `yyyy`. |
   |Use TLS Client Auth |Enable |
   |Skip TLS Verification |Enable |
   |Allow Cleartext Passwords |Optional. After enabling this function, you can configure Username & Password as follows:<br><br><br>* Username: bytehouse.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant management** \> **Connection information** on the ByteHouse console. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) for details. |
