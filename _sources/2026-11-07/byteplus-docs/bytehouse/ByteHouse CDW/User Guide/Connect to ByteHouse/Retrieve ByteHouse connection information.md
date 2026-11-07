---
title: "Retrieve ByteHouse connection information"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-connectivity"
---

You can refer to this page to obtain the connection information for ByteHouse Cloud Data Warehouse service.

<span id="30753141"></span>
# Set up IP allowlist

If your network environment has access restrictions, please add the following IP addresses to the whitelist in advance to ensure normal access to the ByteHouse Cloud Data Warehouse service.


|**Regions** |**Public Network Exit IP** |
|---|---|
|Hong Kong |[150.5.146.60](https://console.byteplus.com/eip/region:eip+cn-hongkong/eips/detail?id=eip-3e1c8qn1jeups2h2n5oj5d89r), [150.5.168.25](http://150.5.168.25/) |
|Southeast Asia (Johor) |[101.47.140.89](https://console.byteplus.com/eip/region:eip+ap-southeast-1/eips/detail?id=eip-14w1m7g264mps3tvs80iln5no), [101.47.11.124](http://101.47.11.124/) |


<span id="7ce98893"></span>
# Step 1: Set default parameter information (Required)

The connection initialization with ByteHouse always uses the default compute group and default roles, so these values cannot be empty.

Before connecting to ByteHouse using a driver, users need to confirm these values in **Tenant management** \> **Parameter setting**.


* Default virtual warehouse: Set the default computing resources used by this account.

* Write virtual warehouse: Set up a dedicated write compute group to enhance table write performance.

* Default database: Set the default connection database.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a01dbb441724ab09ea4fc5fc869f413~tplv-goo7wpa0wc-image.image) </span>

<span id="d49d2486"></span>
# Step 2: Configure network information

Generally, connecting to ByteHouse requires the cluster's access address (HOST) and port number (PORT). You can configure and obtain the corresponding connection information through the network information module in the ByteHouse console.

On the **Tenant management** \> **Basic information** page at the top of the ByteHouse CDW console, check the network information to confirm that the VPC is bound and a public domain name is assigned. If the VPC and public domain name are not bound, refer to the [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings) documentation to complete the binding configuration.

After binding, click to copy the private or public domain name to use as the cluster access address (HOST) for subsequent parameter configuration. The default port number is 19000. For ports used by other common connection methods, please refer to [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers#18dc0302).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Public or private network domain names can meet the needs of regular connection scenarios. If you have special requirements and need to use a public network or private network IP, you can submit an order to contact the ByteHouse team for assistance.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/341aecaf1c004cf2aa4554225b213aa0~tplv-goo7wpa0wc-image.image) </span>

Meanwhile, for commonly used connection drivers (JDBC/Python/Golang/ByteHouse\-CLI), you can also obtain the connection address string for various connection methods on the Console by the path **Tenant management\-Connection information**.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd26a8dde754420dbc544190a14731a5~tplv-goo7wpa0wc-image.image) </span>

<span id="6b1d1889"></span>
# Step 3: Obtain ByteHouse connection information

You can connect to ByteHouse using an IAM user or a database user. The parameters required for the connection are as follows:


|Parameter item |Use an IAM user to connect |Use a database user to connect |
|---|---|---|
|`{HOST}` |Cluster access address. See [Step 2: Configure network information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#d49d2486) for retrieval instructions. ||
|`{PORT}` |The default port is 19000. See [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/docs-supported-regions-and-providers#18dc0302) for ports used by other common connection methods. ||
|`{USERNAME}` |Username to log in to the ByteHouse database.<br><br><br>* User for ByteHouse on BytePlus defaults to `bytehouse`.<br><br>* For ByteHouse not hosted on BytePlus, obtain `{USERNAME}` information from the platform administrator. |The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`.<br><br><br>* `{accountID_or_accountName}`: It refers to the BytePlus account UID or name. See below [Obtain account information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#78b6af42) for details.<br><br>* `{username}`: The ByteHouse database login username. See below [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90) for details.<br><br>* `{envID}`: Optional. It specifies the environment name where the database resides. See [(Optional) Retrieve environment information](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#2e2b115d) below for details. When configuring envID, `[]` is not needed.<br><br>   Examples:<br><br>   * Default env: `30xxxxxxxx:demouser`<br><br>   * Other envs `30xxxxxxxx:demouser:demoenv` |
|`{password}` |Set as the current account's API Key. See [Obtain API Key](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#50160311) below for retrieval instructions. |Obtain the database user's password by referring to [Obtain database user and password](https://docs.byteplus.com/docs/bytehouse/docs-connectivity#5464ba90) below. |


<span id="50160311"></span>
## Obtain API Key

After logging in and entering the ByteHouse console, click **Tenant management** at the top, then **Connection information**. Create a new API key in the API Key section and save it locally for subsequent configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bc71143423b745b4811202d8c0733539~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">API Key <strong>cannot be viewed again after creation</strong>. It is recommended to download and save the key locally.</div>


* <div data-tips="true" data-tips-type="warning">One sub\-account can create up to 2 API keys. If you have existing API keys created, you can use those directly.</div>


* <div data-tips="true" data-tips-type="warning">Keys must be refreshed within 90 days to ensure security.</div>



<span id="78b6af42"></span>
## Obtain account information

After logging in to the ByteHouse console, click the personal center at the top right to view and copy the account ID or name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec2175b742244948084125e4b722c53~tplv-goo7wpa0wc-image.image) </span>

<span id="5464ba90"></span>
## Obtain database user and password

After logging in and entering the ByteHouse console, go to the **Access control** \> **Users** page at the top. Check the user list and filter users by the **Database** category. View and copy the database username. If the database user has not been created yet, contact the administrator to create a database user by referring to [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account).

The database user's password is set by the administrator. Contact the administrator to obtain the corresponding password. If the password is lost or forgotten, contact the administrator to reset it. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c86f9e2b39af4adda566073e67eaf85c~tplv-goo7wpa0wc-image.image) </span>

<span id="2e2b115d"></span>
## (Optional) Retrieve environment information

If using the default environment, no configuration is needed. To use another environment, specify its name. You can log in to the ByteHouse console, then check the current environment name on the **Basic information** page under **Tenant management** at the top.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a94f89579cbb41b8b38e35a26f77b875~tplv-goo7wpa0wc-image.image) </span>
