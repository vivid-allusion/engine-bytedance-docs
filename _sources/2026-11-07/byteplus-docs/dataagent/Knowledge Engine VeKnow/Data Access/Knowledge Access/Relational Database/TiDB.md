---
title: "TiDB"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/TiDB_"
---

TiDB data connection is supported. This article explains how to connect TiDB data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<span id="f8a9cd76"></span>
# **Premise of use**

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="a931925b"></span>
# **Operation steps**


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **Relational Database \- TiDB** in the Data Connection screen.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73bc818601cc49cf906f3e4ff46eaaed~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac2369d162ae4f7d8784f706214b73a4~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `TiDB_YYYYMMDDHHMMSS` |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   

4. Click **Save** after successful connection.
