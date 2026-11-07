---
title: "ByteHouse CDW"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouse_CDW___"
---

Support ByteHouse cloud data warehouse version data connection. This article introduces how to access ByteHouse cloud data warehouse version data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="895142b2"></span>
# Premise of use


1. The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

2. The [ByteHouse CDW cloud data warehouse version has been opened ](https://www.volcengine.com/product/bytehouse-cloud).

   1. Apply for a [Volcano Engine account ](https://console.volcengine.com/auth/signup/?redirectURI=%2F%2Fwww.volcengine.com%2Fdocs%2F6261%2F64925); enterprise users need to go to the Volcano Engine official website to apply for a Volcano Engine main account and complete account authentication. For the steps, please refer to ["Volcano Engine Account Registration and Authentication Operation Guide" ](https://www.volcengine.com/docs/6261/64925);

   2. Carry out real\-name authentication, and refer to [real-name authentication ](https://www.volcengine.com/docs/6261/64935)in steps;

   3. Go to the Volcano Engine ByteHouse console ( [ByteHouse product page ](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/database)) to launch the product.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d62a7ce73c84752a7f60e69be2d04ce~tplv-goo7wpa0wc-image.image) </span>

      Taking the **Cell tower public data table** as an example, complete the operation of creating the data table as shown in the following figure:

> Note: Cell tower data table statistics of base station information around the world (GSM, LTE, UMTS, etc.), as well as geographical coordinates, country codes and other information.


   1. Create a new database.

   2. You can use the following SQL to build a table for trial use.

   3. You can use the following SQL to build a table for trial use.

   ```sql
   CREATE TABLE `sampledb`.`cell_towers`
   (
       radio String,
       mcc UInt16,
       net UInt16,
       area UInt16,
       cell UInt64,
       unit Int16,
       lon Float64,
       lat Float64,
       range UInt32,
       samples UInt32,
       changeable UInt8,
       created DateTime,
       updated DateTime,
       averageSignal UInt8
   )
   ENGINE = CnchMergeTree ORDER BY (radio, mcc, net, created);
   sql
   ```
   

   4. After the creation is complete, follow the steps below to import the task:

   5. Get **access keys, calculation groups, roles** :

      * Users can fill in the following parameters according to the following information items

         * **Data connection name** : Use default

         * **Region** : Use Default

         * **Access key** : [Create an Access Token ](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/account/details)in the **ByteHouse account details** and get **the API Token ID in the figure below**.

   * **Compute Group** : Get it on the [ByteHouse Compute Group page ](https://console.volcengine.com/bytehouse/region:bytehouse+cn-north-1/virtual-warehouse)and fill in the name (default_vw in the example) as shown in the figure below.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Note for the calculation group:</strong> You need to confirm that the current status is "On", or the automatic start is "On".   </div>
   

   * **Roles** : View the role acquisition in the settings button in the upper right corner of ByteHouse.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Role Note: You need to ensure that this role has SELECT and SHOW CREATE permissions on the table before you can use the table in DataWind   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If there is no [role] item to fill in in the parameters required for the data connection, the current user needs to have the AccountAdmin role permission in ByteHouse.   </div>
   

   6. Once configured, click **Test Connection** to debug connectivity.


<span id="e7094f21"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="3e08be0c"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **Volcano Engine Matrix \> ByteHouse CDW** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a318947d3d404012b12e26db2c152678~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/beb39161ad97451394ca5bc2a9839b9e~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Bytehouse_CDW_YYYYMMDDHHMMSS` |
   |area |ByteHouse cloud data warehouse version service Region, for details, please refer to [obtain ByteHouse connection information ](https://www.volcengine.com/docs/6517/1121919?lang=zh). |
   |access key |Access password, please refer to [Obtain ByteHouse connection information ](https://www.volcengine.com/docs/6517/1121919?lang=zh). |
   |calculation group |Virtual Warehouse (VW) is a computing resource cluster in ByteHouse. For details, please refer to [Obtain ByteHouse Connection Information ](https://www.volcengine.com/docs/6517/1121919?lang=zh). |
   |role |Role name, the default AccountAdmin, please refer to [role management ](https://www.volcengine.com/docs/6517/1250178?lang=zh). |
   |connection method |* Volcanic Cloud: directly select Volcanic Cloud Connection<br><br>* JDBC connection string: Enter a JDBC connection string<br><br>* Server: Enter the server name and port |
   |driverVersion |Select the driver version |
   

4. Click **Save** after successful connection.


<span id="297c3b8d"></span>
# Common problem

Without real\-name authentication, you will not be able to access the Volcano Engine ByteHouse Enterprise Edition console normally, and you need to complete [real-name authentication ](https://www.volcengine.com/docs/6261/64925).
