---
title: "StarRocks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/StarRocks_"
---

StarRocks data connection is supported. This article describes how to access StarRocks data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before connecting to the database, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<span id="d632b1b7"></span>
# **Premise of use**

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="88cab3f5"></span>
# **Operation steps**


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the data connection interface, select **data warehouse** \- **StarRocks.** 

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cbab8db5806045a6918434aa2ef1efce~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** . After the connection is successful, click **Save** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0577c69a584474b88fbecda60a2d5a0~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets a unique identifying name for the data connection. |
   |**server** |Set the host name or Internet Protocol Address of the StarRocks server. |
   |**Port** |Sets the port number of the StarRocks server. |
   |**user name** |Sets the user name used to connect to the StarRocks database. |
   |**password** |Set the password used to connect to the StarRocks database. |
   |**connection method** |Select the way to connect to StarRocks. It includes the following two methods:<br><br><br>* **IP/Port** : Connect via server Internet Protocol Address/hostname and port number. When selecting this option, you need to configure the **server** , **port** , **username** , **password** and other parameters.<br><br>* **JDBC connection string** : Connect through a standard JDBC URL. When you select this, you need to provide the full JDBC connection string. |
   |**externalCatalog** |external data directory |
   |**permission mode** |Set the operation permissions for this data connection. It includes the following two modes:<br><br><br>* **Read** : The connection has data read permissions only.<br><br>* **Write** : The connection has data read and write permissions. |
