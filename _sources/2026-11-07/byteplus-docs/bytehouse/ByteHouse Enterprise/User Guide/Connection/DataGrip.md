---
title: "DataGrip"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/datagrip"
---

DataGrip is a set of integrated development environments (IDE) designed by JetBrains specifically for database developers and administrators. It supports various database management systems, provides smart code completion, and facilitates version control integration.

This article will discuss how to connect ByteHouse Enterprise Edition through the JDBC driver using DataGrip.

<span id="6ba540c5"></span>
## Prerequisites


* Please install [DataGrip](https://www.jetbrains.com/zh-cn/datagrip/) in advance and acquire the corresponding commercial authorization.


<span id="e15778a5"></span>
## Connect to ByteHouse with DataGrip


1. Launch DataGrip, click on the *Database Explorer* tab, click the  **+**  icon, select *Data Source* \-\> ClickHouse\*.\*

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2143d9544574a809593ae3372451839~tplv-goo7wpa0wc-image.image) </span>

2. Switch to the Drivers tab, click the + sign in *Driver Files* , select the latest ClickHouse driver in the pop\-up window as shown, and click Apply to configure the settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1f7b865f156243d09ea8c832e5efabb1~tplv-goo7wpa0wc-image.image) </span>

3. Switch to the Data Sources tab. I set a name for the connection (e.g., ByteHouse) and fill in the following fields:

   1. `Host` and `Port`: Depending on the region where the cluster is located, please refer to [Get cluster connection information](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information).

   2. `Username` and `Password`: Fill in the username and service password. See [Reset connection password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#9f131fd8).

   3. (Optional) `Database name`.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9c9cbe6b7964708a29041df74936dda~tplv-goo7wpa0wc-image.image) </span>

4. Click **Test Connection**, if it displays 'Succeeded' the connection is successful, click **OK** to confirm the configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cda5226cceed4908954baf1e87ad5f29~tplv-goo7wpa0wc-image.image) </span>
