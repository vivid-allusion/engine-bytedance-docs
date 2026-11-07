---
title: "Greenplum"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Greenplum_"
---

Support GreenPlum data connection, this article describes how to connect GreenPlum data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before connecting to the database, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The name of the database.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="e48fe573"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="67981d9d"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> GreenPlum** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d6942de471540788dd7166dbaf39dbe~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca26b280bad84b2098fe27d248db43d7~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `GreenPlum_YYYYMMDDHHMMSS` |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   |database |Enter the name of the target database to connect to |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f235b94c7ea4df4a13cd30851221e5c~tplv-goo7wpa0wc-image.image) </span>
