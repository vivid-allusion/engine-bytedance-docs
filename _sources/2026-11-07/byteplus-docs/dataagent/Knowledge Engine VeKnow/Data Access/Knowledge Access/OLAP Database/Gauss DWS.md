---
title: "Gauss DWS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Gauss_DWS_"
---

Support Gauss DWS data connection, this article describes how to access Gauss DWS data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="c416db5a"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="9df625e4"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> Gauss DWS** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00e4d8ea0e704150a25e4dcf6fc245a2~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd3568e2f037424fa65a0daeda18eeec~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Gauss_DWS_YYYYMMDDHHMMSS` |
   |connection method |Select the way to connect to the data source. The following two methods are supported:<br><br>IP/Port: Connect by server address and port number. When you select this option, you need to configure parameters such as server, port, username, password, and database.<br><br><br>* JDBC connection string: Connect through a standard JDBC URL. When this option is selected, you need to configure the JDBC connection string, username, password, and database. |
   |server |Enter the connection address for the server |
   |JDBC connection string |Enter the JDBC URL to connect to the database |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   |database |Enter the specific database name to connect to |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6816ad7eb0a247278ff6c791973e30d1~tplv-goo7wpa0wc-image.image) </span>
