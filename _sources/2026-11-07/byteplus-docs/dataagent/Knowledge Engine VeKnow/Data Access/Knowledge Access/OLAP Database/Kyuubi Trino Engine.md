---
title: "Kyuubi Trino Engine"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Kyuubi_Trino_Engine"
---

Kyuubi Trino Engine data connection is supported. This article describes how to connect Kyuubi Trino Engine data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The name of the database.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="46e296ed"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="16107c38"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> Kyuubi Trino Engine** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00ac710d7aac4d7f925a6143aa1c5b5b~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/321dc111951542e2ba94d87853f8aa48~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Kyuubi_Trino_Engine_YYYYMMDDHHMMSS` |
   |connection method |* IP/Port: Support entering the server connection address and port number to connect<br><br>* JDBC connection string: Support entering JDBC connection string connection |
   |JDBC connection string |String to connect to the database through the JDBC interface |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   |database |Enter the database name |
   

4. Click **Save** after successful connection.
