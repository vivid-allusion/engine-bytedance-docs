---
title: "Huawei FusionInsight"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Huawei_FusionInsight"
---

Support Huawei FusionInsight data connection, this article introduces how to access Huawei FusionInsight.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="f50e5f82"></span>
# **Premise of use**

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="46ae5803"></span>
# **Operation steps**


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the data connection interface, select **data warehouse** \- **Huawei FusionInsight** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf455370b6444f63b2b1b6ab08d07839~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f91588324eb9443ab7685c1e52d2c38f~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets the business name of the data connection to uniquely identify it. |
   |**server** |Enter the IP address or hostname of the server in the FusionInsight cluster that is used to establish the connection. |
   |**Port** |Enter the port number corresponding to the server. |
   |**Krb5 file** |Click **Upload** to upload the `krb5.conf`profile required for Kerberos authentication. |
   |**Keytab file** |Click **Upload** to upload the `keytab`key file required for Kerberos authentication. |
   |**Principal** |Enter the Principal name for Kerberos authentication, usually in the format `user/host@REALM`. |
   |**connection method** |Select the way to connect to the database.<br><br><br>* **IP/Port** : Connect by server IP/hostname and port number. When you choose this, you need to configure the **server** and **port** parameters.<br><br>* **JDBC connection string** : Connect through the full JDBC URL. When selected, the **server** and **port** parameters are hidden and the text box for the JDBC connection string is displayed. [Note: Please add sample format for JDBC connection string] |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97bdd133544f40d8a0021e62927f15a1~tplv-goo7wpa0wc-image.image) </span>
