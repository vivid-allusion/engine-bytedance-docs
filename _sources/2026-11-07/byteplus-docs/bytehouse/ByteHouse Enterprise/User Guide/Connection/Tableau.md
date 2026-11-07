---
title: "Tableau"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/tableau"
---

Tableau is a data visualization platform developed by Salesforce for visualizing data, interactive dashboards, and KPI scorecards. This tutorial introduces how to use Tableau to connect to ByteHouse and perform data queries and analysis.

<span id="dc9a6d58"></span>
# Cautions


|**Subcategories** |**Version** |
|---|---|
|Tableau version |[2024.3](https://www.tableau.com/support/releases/desktop/2024.3) |
|ClickHouse Tableau Connector version |[0.3.1](https://github.com/ClickHouse/clickhouse-tableau-connector-jdbc/releases/tag/v0.3.1)<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">As the <code>ByteHouse Tableau Connector</code> based on <code>bytehouse-taco</code> is currently undergoing maintenance and updates, it is recommended to use the open\-source <code>ClickHouse Tableau Connector</code> and <code>ByteHouse JDBC Driver</code> to connect to ByteHouse.</div><br> |
|ByteHouse JDBC Driver version |The latest version of the ByteHouser JDBC Driver jar file: Go to the [ByteHouse Java Driver index](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/) page to obtain it. |


<span id="c602419b"></span>
# Obtain ByteHouse connection information

You need to obtain the cluster connection address, port number, username, and password for the ByteHouse Enterprise cluster. These details are required for subsequent configuration of the connection in Tableau. You can refer to the following sections to obtain the relevant information.


* Cluster connection address: cluster gateway information. For details, see [Obtain a network domain name](https://docs.byteplus.com/docs/bytehouse/73308#3a21a181).

* Port number: use 19000. For more information about ports, see [Cluster connection port](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#c58d5357).

* Username: The username for the ByteHouse service. For details, see [Obtain an account and password](https://docs.byteplus.com/docs/bytehouse/73308#ade162ac).

* Password: The password for the ByteHouse service. For details, see [Obtain an account and password](https://docs.byteplus.com/docs/bytehouse/73308#ade162ac).


<span id="3a21a181"></span>
## Obtain a network domain name

The cluster connection address is the cluster gateway information. After logging in to and entering the ByteHouse console, click **Cluster management** at the top, then navigate through **Cluster list** \> **Cluster Details** \> **Basic information** to view the gateway configuration of the **Cluster connection** module. Copy the private or public address according to your environment.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b34c10e9d2eb41709f60dd36300335b8~tplv-goo7wpa0wc-image.image) </span>

If you have not yet configured a public network address, you can click **Bind public IP** and select an existing public IP. If no public IP is available, you can create a public IP or refresh the page to try again. For details about creating a public IP address and associated costs, refer to the following documents:


* [Applying for an EIP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP)

* [Billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview)


<span id="ade162ac"></span>
## Obtain an account and password

ByteHouse Enterprise supports access using IAM sub\-users and database users. For the differences between the two, see [User types](https://docs.byteplus.com/docs/bytehouse/privilege-model#b7c2623a). The methods for obtaining IAM sub\-users and database users are as follows:


* **IAM sub\-user**: You can log in to the ByteHouse Enterprise console, click the ByteHouse personal center in the upper right corner, click **Account management**, and view and copy the username in **Cluster connection account**. For details, please refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).

* **Database user**: You can log in to the ByteHouse Enterprise console, click **Access control** at the top, click **User**, and in the user list, view users whose **User type** is set to Database, then copy the username.


In ByteHouse Enterprise, the password used for IAM user access and database user access is the same; both use the ByteHouse cluster connection password. The method for obtaining this password is as follows:

Log in to the ByteHouse Enterprise console. Click ByteHouse Personal Center in the upper right corner. Click **Account management**. View and copy the password in **Cluster connection account**. For details, see [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50137d09012a40e5b64bbeb6e39771bb~tplv-goo7wpa0wc-image.image) </span>

<span id="57822a22"></span>
# Tableau\-side configuration

<span id="baf14fc4"></span>
## Step 1: Preparation


1. Download and install [Tableau client](https://www.tableau.com/products/desktop/download).

2. Install the ByteHouse JDBC driver.

   1. Download the latest version of the [ByteHouse JDBC driver](https://artifact.bytedance.com/repository/releases/com/bytedance/bytehouse/driver-java/).

   2. Store the JDBC driver in the following folder. If the folder does not exist, create it first.

      
      |OS |Path |
      |---|---|
      |Windows |`C:\Program Files\Tableau\Drivers` |
      |mac |`~/Library/Tableau/Drivers` |
      

3. Install ClickHouse Tableau Connector.

   1. If you are using the latest version of `Tableau Desktop`, you should have the ClickHouse connector by default. If you are using an older version, please download [ClickHouseConnector](https://github.com/ClickHouse/clickhouse-tableau-connector-jdbc/releases/tag/v0.3.1) (v0.3.1) first.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b672c087676b40dea9ed831fd023974d~tplv-goo7wpa0wc-image.image) </span>

   2. Place the connector (`taco` file) in the following folder:

      
      |OS |Path |
      |---|---|
      |Windows |`C:\Users\[Windows User]\Documents\My Tableau Repository\Connectors` |
      |mac |`~/Documents/My Tableau Repository/Connectors` |
      


<span id="e0b734c5"></span>
## Step 2: Create a ByteHouse data source


1. Start`Tableau Desktop` and click **To a Server** \> **More**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d45fc26e1dd492cb977a633cb520207~tplv-goo7wpa0wc-image.image) </span>

2. Search for and click **ClickHouse by ClickHouse**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/110bee65cf304e1e8e38e14d1e1fca52~tplv-goo7wpa0wc-image.image) </span>

3. Click **Install and Restart Tableau** to install the ClickHouse connector. After the installation is complete, restart Tableau Desktop.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0d9287ba37546008dd3e68b355f5e81~tplv-goo7wpa0wc-image.image) </span>

4. After restarting, under **To a Server** \> **More** , search for and click **ClickHouseJDBC byClickHouse**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2fecb162536947ac913a4acf9f110521~tplv-goo7wpa0wc-image.image) </span>

5. Configure connection information on the pop\-up page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03338ce870244b079302b7a98d0172c3~tplv-goo7wpa0wc-image.image) </span>

   
   |**Parameters** |**Configuration instructions** |
   |---|---|
   |Server |The ByteHouse Enterprise cluster connection address. You can view and copy the public network gateway address in **Cluster management** \> **Cluster Name** \> **Basic information** \> **Cluster connection**. For details, please refer to [Obtain a network domain name](https://docs.byteplus.com/docs/bytehouse/73308#3a21a181) above. |
   |Port |The database port number is configured as a fixed value: 19000. |
   |Username & Password |* Username refers to the ByteHouse Enterprise username. Click the ByteHouse Personal Center in the upper right corner, then click **Account management**, and view and copy the username in **Cluster connection account**. For more information, see [Obtain an account and password](https://docs.byteplus.com/docs/bytehouse/73308#ade162ac) above.<br><br>* Password is the ByteHouse Enterprise password. Click the ByteHouse Personal Center in the upper right corner, click **Account management**, then view and copy the password from **Cluster connection account**. For more details, see [Obtain an account and password](https://docs.byteplus.com/docs/bytehouse/73308#ade162ac) above. |
   |SSL |Turn on the SSL switch.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">ByteHouse requires encrypted authentication to protect data security; therefore, you must enable SSL.</div><br> |
   

6. Click **Sign In** to complete the creation of the data source.


<span id="d0f9d2a8"></span>
## Step 3: Verify results

Once you have created the ByteHouse data source, an empty Tableau workbook will appear. You can start querying and analyzing data on this page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e44fd44b121942bb9a830f8e3879813f~tplv-goo7wpa0wc-image.image) </span>
