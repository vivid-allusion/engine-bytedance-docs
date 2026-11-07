---
title: "Tableau"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-tableau-desktop-integration-with-bytehouse"
---

Tableau is a data visualization platform developed by Salesforce, used for visualizing data, interactive dashboards, and KPI scorecards. This article will guide you on how to use Tableau to connect to ByteHouse and perform data query analysis.

<span id="4ee2c94d"></span>
# Background information

ByteHouse allows you to connect to it via Tableau using either an IAM user or a database user, and you can choose one of these connection methods as needed.


* An IAM user is a user created in BytePlus Identity and Access Management (IAM). Its privileges are determined by IAM privilege policies as well as the ByteHouse resource and data privileges you grant. An IAM user can access the ByteHouse console and also supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.

* A database user is a database\-level user created in ByteHouse, to which you can grant environment, resource, and data privileges. A database user cannot access the ByteHouse console but supports accessing ByteHouse through CLI, connection drivers, ecosystem tools, APIs, and other methods.


For more introductions to IAM users and database users, please refer to the following documents:


* [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview)

* [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management)

* [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account)


<span id="3de3c7c4"></span>
# Caution


|**Breakdown Items** |**Verified Version** |
|---|---|
|Tableau Version |[2024.3](https://www.tableau.com/support/releases/desktop/2024.3) |
|ClickHouse Tableau Connector Version |[0.3.1](https://github.com/ClickHouse/clickhouse-tableau-connector-jdbc/releases/tag/v0.3.1)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Due to the maintenance and updates of the <code>bytehouse-taco</code>\-based <code>ByteHouse Tableau Connector</code>, it is currently recommended to use the open\-source <strong><code>ClickHouse Tableau Connector</code></strong> and <strong><code>ByteHouse JDBC Driver</code></strong> to connect to ByteHouse.</div><br> |
|ByteHouse JDBC Driver Version |[1.1.73](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/1.1.73/driver-java-1.1.73.jar) and above versions |


<span id="c9820998"></span>
# Configure ByteHouse

ByteHouse supports connections via IAM users or database users. Configure your user account information before using this tool. For the difference between IAM users and database users, please refer to [Overview](https://docs.byteplus.com/docs/bytehouse/access-control-overview).

<span id="4e411219"></span>
## **Step 1 Configure network domain**

After logging into the ByteHouse console, go to the **Tenant management** \> **Basic information** page. Check the **Network information** to confirm that the VPC is bound and that a public domain is linked

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7742905ea3b344f5ac1c08f915e512b7~tplv-goo7wpa0wc-image.image) </span>


* If the VPC and public domain are not bound, refer to [Network settings](https://docs.byteplus.com/docs/bytehouse/network-settings).

* After binding, click to copy the public domain name for later parameter configuration.


<span id="513f4cc6"></span>
## **step2 Set the default virtual warehouse**

Go to the **Tenant management** \> **Parameter settings** page at the top, check the set default virtual warehouse, and ensure this virtual warehouse is running and not stopped. All subsequent operations, such as data queries after connecting to ByteHouse, will use the default virtual warehouse configured here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95e5f5c8a7e349ad8155b5c213f38dee~tplv-goo7wpa0wc-image.image) </span>

<span id="e08fb056"></span>
## **step 3 Obtain user and password information for the connection string**

<span id="262ffa04"></span>
### Use an IAM user to connect

IAM users use an API Key as the connection password. You can create a new API key in the API Key module on the **Tenant management** \> **Connection information** page at the top and save the API key locally for later configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e13db982dd742a38d56b3893ab7045e~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A sub\-account supports creating up to two API Keys. If you have previously created API Keys, you can also use the existing API Keys directly.</div>


<span id="43108626"></span>
### **Use a database user to connect**

The database user's account consists of the ByteHouse account, database username, account, and optionally the environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. The password is the database user's password.

<span id="94422480"></span>
#### Obtain account information

After logging in to the ByteHouse console, click the personal center at the top right to view and copy the account ID or name.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bec2175b742244948084125e4b722c53~tplv-goo7wpa0wc-image.image) </span>

<span id="d1689d72"></span>
#### Obtain database user and password

After logging in and entering the ByteHouse console, go to the **Access control** \> **Users** page at the top. Check the user list and filter users by the **Database** category. View and copy the database username. If the database user has not been created yet, contact the administrator to create a database user by referring to [Manage database user](https://docs.byteplus.com/docs/bytehouse/manage-database-account).

The database user's password is set by the administrator. Contact the administrator to obtain the corresponding password. If the password is lost or forgotten, contact the administrator to reset it. For details, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c86f9e2b39af4adda566073e67eaf85c~tplv-goo7wpa0wc-image.image) </span>

<span id="aab061d8"></span>
#### (Optional) Retrieve environment information

If using the default environment, no configuration is needed. To use another environment, specify its name. You can log in to the ByteHouse console, then check the current environment name on the **Basic information** page under **Tenant management** at the top.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a94f89579cbb41b8b38e35a26f77b875~tplv-goo7wpa0wc-image.image) </span>

<span id="d61609b5"></span>
# Configure Tableau

<span id="e0147b09"></span>
## Step 1: Preparation


1. Download and install [Tableau Client](https://www.tableau.com/products/desktop/download).

2. Install the ByteHouse JDBC driver.

   1. Download the latest [ByteHouse JDBC driver](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/).

   2. Store the JDBC driver in the following folder (create the folder first if it does not exist).

      
      |OS |Path |
      |---|---|
      |windows |`C:\Program Files\Tableau\Drivers` |
      |mac |`~/Library/Tableau/Drivers` |
      

3. Install ClickHouse Tableau Connector.

   1. If you are using the latest `Tableau Desktop`, a ClickHouse connector should be available by default. If you are using an older version, please first download [ClickHouseConnector](https://github.com/ClickHouse/clickhouse-tableau-connector-jdbc/releases/tag/v0.3.1) (v0.3.1).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f285e92917cc45d38e88a1431aed9932~tplv-goo7wpa0wc-image.image) </span>

   2. Place the connector (taco file) in the following folder:

      
      |OS |Path |
      |---|---|
      |windows |`C:\Users\[Windows User]\Documents\My Tableau Repository\Connectors` |
      |mac |`~/Documents/My Tableau Repository/Connectors` |
      


<span id="22bb8dfb"></span>
## Step 2: Create a ByteHouse datasource


1. Launch `Tableau Desktop` and click **To a Server** \> **More**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d45fc26e1dd492cb977a633cb520207~tplv-goo7wpa0wc-image.image) </span>

2. Search for and click **ClickHouse by ClickHouse**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/110bee65cf304e1e8e38e14d1e1fca52~tplv-goo7wpa0wc-image.image) </span>

3. Click `Install and Restart Tableau` to install the ClickHouse connector. After installation, restart `Tableau Desktop`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d9287ba37546008dd3e68b355f5e81~tplv-goo7wpa0wc-image.image) </span>

4. After restarting, under **To a Server** \> **More** , search for and click `ClickHouseJDBC byClickHouse`.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fecb162536947ac913a4acf9f110521~tplv-goo7wpa0wc-image.image) </span>

5. In the pop\-up page, configure the connection information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d1d3c8e5749483ca78fd225640afd29~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter item |Use an IAM user to connect |Use a database user to connect |
   |---|---|---|
   |host |Tenant\-{TENANT_ID}\-{Region}\-public.bytehouse.bytepluses.com<br><br>Configured as ByteHouse's public domain name, the format is: `tenant-{TENANT_ID}-{REGION}-public.bytehouse.bytepluses.com`. You can obtain it in ByteHouse console via **Tenant management** \> **Basic information** \> **Network Information**. Refer to [Step 1 Configure network domain](https://docs.byteplus.com/docs/bytehouse/docs-tableau-desktop-integration-with-bytehouse#4e411219) above. ||
   |port |The default port is 19000. ||
   |Username & password |* Username: Fixed at `bytehouse`.<br><br>* Password: Set as the API Key of ByteHouse. You can obtain the API Key in **Tenant Management** \> **Connection Information** on the ByteHouse console. Refer to [Connect using an IAM user](https://docs.byteplus.com/docs/bytehouse/docs-tableau-desktop-integration-with-bytehouse#262ffa04) above. |* Username: The database user's account combines the ByteHouse account, database username, and optional environment ID, formatted as `{accountID_or_accountName}::{username}[::{envID}]`. For details, refer to [Connect using a database user](https://docs.byteplus.com/docs/bytehouse/docs-tableau-desktop-integration-with-bytehouse#43108626) above.<br><br>   * `{accountID_or_accountName}`: It refers to the BytePlus user account ID or name. You can log in to the ByteHouse console, click **Personal Center** in the upper right corner to view and copy the account ID or name.<br><br>   * `{username}`: It refers to the username for logging into the ByteHouse database. You can view the database username in **ByteHouse Console** \> **Access control** \> **Users**.<br><br>   * `{envID}`: Optional. It specifies the name of the environment where the database is located. If you use the default environment, no configuration is required. If you need to use another environment, you must specify the environment name. You can log in to the **ByteHouse CDW console** and obtain it in **Tenant management** \> **Basic information** \> **Current environment**.<br><br>      Examples:<br><br>      * Default env: `30xxxxxxxx::demouser`<br><br>      * Other env: `30xxxxxxxx::demouser::demoenv`<br><br>* Password: You can contact your administrator to obtain the password for your database account. If the password is lost or forgotten, please contact your administrator to reset it. For detailed instructions, refer to [Reset password](https://docs.byteplus.com/docs/bytehouse/manage-database-account#a6a3e043). |
   |SSL |Enable SSL toggle.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encrypted authentication to protect data security; therefore, you need to enable SSL.</div><br> ||
   

6. (Optional) If you have multiple virtual warehouses and you want to use a specific virtual warehouse for subsequent queries of ByteHouse data, you can specify the specific virtual warehouse in Advanced. Configuration examples are as follows.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bfceafb7b54344bda362b3a007d4875a~tplv-goo7wpa0wc-image.image) </span>

7. Click **Sign In** to complete the creation of the datasource.


<span id="9e2e30f8"></span>
## Step 3: Verify results

After completing the creation of the ByteHouse datasource, you can see an empty Tableau workbook in the ByteHouse datasource, where you can start data queries and analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e44fd44b121942bb9a830f8e3879813f~tplv-goo7wpa0wc-image.image) </span>
