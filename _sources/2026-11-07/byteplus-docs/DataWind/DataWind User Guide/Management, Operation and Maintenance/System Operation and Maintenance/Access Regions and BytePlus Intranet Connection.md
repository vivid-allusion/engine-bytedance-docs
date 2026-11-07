---
title: "Access Regions and BytePlus Intranet Connection"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Access_Regions_and_BytePlus_Intranet_Connection"
---

This article introduces the basic information about access regions (Region) and the fundamental features of Volcano Engine intranet connection.

<span id="b3996a51"></span>
# Access regions

The available access regions (Region) for the SaaS version include: North China 2 (Beijing), East China 2 (Shanghai), and Asia Pacific Southeast (Johor).

The regions supported by Intelligent Data Analytics are shown in the following table:


|Region |City |RegionID |
|---|---|---|
|North China 2 |Beijing |cn\-beijing |
|East China 2 |Shanghai |cn\-shanghai |
|Southeast Asia Pacific |Johor |ap\-southeast\-1 |



* If you have already purchased the product:

   * You can view the access region (Region) of the current product in the upper right corner of the product interface.

   * In general, for enterprise customers who have activated product services, the access region (Region) is North China 2 (Beijing).

* If you have not purchased the product:

   * If Intelligent Data Analytics has not been purchased yet, you can select the access region (Region) when making a future purchase.

   * The currently available access regions (Region) include North China 2 (Beijing), East China 2 (Shanghai), and Asia Pacific Southeast (Johor).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Region refers to the geographic area where the physical data center is located. After a resource is created, its region cannot be changed. The internal networks of different regions are completely isolated.</div>


* <div data-tips="true" data-tips-type="tip">From a geographical perspective, it is generally recommended to select the region closest to you or your target users to reduce network latency and improve access speed. For more information, see <a href="https://www.volcengine.com/docs/6396/67719">Regions and Availability Zones</a>.</div>


* <div data-tips="true" data-tips-type="tip">If you switch the access region from North China 2 (Beijing) to East China 2 (Shanghai), a new purchase is required, and the product interface will present the purchase page. In addition, please note that data in North China 2 (Beijing) and East China 2 (Shanghai) are isolated from each other. Data connections and datasets in Intelligent Data Insights do not support cross\-region access or usage.</div>


* <div data-tips="true" data-tips-type="tip">If access region for other products under Volcano Engine is switched to East China 2 (Shanghai), the access region for Intelligent Data Insights will also be displayed as East China 2 (Shanghai). Products under Volcano Engine do not support multiple access regions.</div>



<span id="eb05a0fd"></span>
# Volcano Engine intranet connection

<span id="33e08a10"></span>
## Feature overview


* Currently, among the data connection methods of Intelligent Data Analytics, the data sources that support intranet connection include:

   MySQL, Oracle, Bytehouse CDW, SQL Server, ClickHouse, PostgreSQL, LAS_jdbc, StarRocks, Bytehouse_CE, Trino, TIDB, OpenGauss, OceanBase Oracle, Oceanbase MySQL, Inceptor, GoldenDB, DM, Presto, Impala, Hive_jdbc, Doris, DB2.

* When a data source supports intranet connection, you need to additionally select the VPC Mode option in the connection parameters. After selecting it, you can enter the VPC ID where the database is located, and then connect to the database using the local area network IP address under that VPC.

   As shown in the following figure, you need to obtain Server IP.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/794202d0aa0246dea1e719860aea067c~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only intranet access within the same region of Volcano Cloud is supported. For example, if the access region of the purchased DataWind is North China, the VPC can only use the North China region. To establish a cross\-region connection, use Cloud Enterprise Network or similar products to connect the VPCs in the two regions, and set up a proxy node in North China for the connection.</div>


<span id="de8ed400"></span>
## **Obtain the database local area network IP**

There are two methods to obtain the database local area network IP. The first method is to query by pinging the local area network domain name, and the second method is to query through the network interface management under the VPC. The following section provides a detailed introduction.

<span id="107b4985"></span>
### Query by pinging the local area network domain name


1. Open the command line tool: In Windows, press `Windows+R`, enter `cmd` and press Enter to open the Command Prompt window; in macOS or Linux, open the Terminal application.

2. Ping the local area network domain name: Enter `ping [database local area network domain name]`, for example, `ping mysql-server.local`, and press Enter. After executing the command, the IP address corresponding to the domain name will be displayed. This IP address is the database server's IP address in the local area network.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81d0544871d348ba8e342bdb99752a9a~tplv-goo7wpa0wc-image.image" width="1178px" />   </div>
   


<span id="338fc9eb"></span>
### Query through VPC network interface management

Taking MySQL as an example, the same applies to databases deployed in environments for other products such as PostgreSQL, load balancing, ECS, and so on.


1. Go to the MySQL instance list page and click to view "Instance Information."

2. Go to the network interface page. In the Private IP Address section, you can view the LAN IP.


<span id="06269f9c"></span>
## Obtain the VPC ID

You can only query the VPC ID through the VPC's network interface management.

Taking MySQL as an example, the same applies to databases deployed in environments for other products such as PostgreSQL, load balancing, ECS, and so on.


1. Go to the MySQL instance list page and click to view "Instance Information."

2. Copy the "ID" in the "Basic Information" section as shown in the figure below to obtain the VPC ID.


<span id="4d97ee96"></span>
## Enter the server IP and VPC ID


1. Go to the data connection configuration page and enter the copied "ID" in field A "VPC ID."

2. Copy the LAN IP and enter this IP in field B "Server" on the data connection page.


&nbsp;
