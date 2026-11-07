---
title: "GBase 8a"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/GBase_8a"
---

Support GBase 8a data connection, this article describes how to use GBase 8a data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="2996a6a9"></span>
# **Premise of use**

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="9a1a7ca5"></span>
# **Operation steps**


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **OLAP \> Hologres** on the data connection interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82d937288d2c4a968100d15511a79715~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa7eb9b370614d9ca99081f640aa940c~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Trino_YYYYMMDDHHMMSS` |
   |connection method |* IP/Port: Support entering the server connection address and port number to connect<br><br>* JDBC connection string: Support entering JDBC connection string connection |
   |JDBC connection string |String to connect to the database through the JDBC interface |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   |database |Enter the database name |
   

4. Click **Save** after successful connection.
