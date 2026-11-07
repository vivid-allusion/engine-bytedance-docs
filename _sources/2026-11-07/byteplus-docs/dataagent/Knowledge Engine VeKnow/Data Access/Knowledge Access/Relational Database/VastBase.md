---
title: "VastBase"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/VastBase_"
---

Support VastBase data connection, this article introduces how to access VastBase data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<span id="09044985"></span>
## Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection. SaaS is not supported for the time being.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="078e4ea5"></span>
## Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connections page, select **Relational Database \- VastBase** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f23f387bcf4747fba151addcef4348d7~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/884e3eb9822f4aa2b195b6ee33d22e3f~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `VastBase_YYYYMMDDHHMMSS` |
   |connection method |* IP/Port: Support entering the server connection address and port number to connect<br><br>* JDBC connection string: Support entering JDBC connection string connection |
   |JDBC connection string |String to connect to the database through the JDBC interface |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   

4. Click **Save** after successful connection.
