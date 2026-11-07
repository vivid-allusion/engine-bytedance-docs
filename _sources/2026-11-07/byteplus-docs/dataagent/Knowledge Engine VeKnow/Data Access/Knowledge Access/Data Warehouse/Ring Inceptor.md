---
title: "Ring Inceptor"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Ring_Inceptor"
---

Support star ring inceptor data connection, this article introduces how to access star ring inceptor data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<span id="5d19dcc3"></span>
# **Premise of use**

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="e21ba8e2"></span>
# **Operation steps**


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the data connection interface, select **data warehouse** \- **star ring** **inceptor**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eea0db892a8340b1819a9a1716185db3~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a32a8d5572da460bba562bf89c01bcbd~tplv-goo7wpa0wc-image.image) </span>



|configuration item |explain |
|---|---|
|**data connection name** |Sets the display name for the data connection, which must be unique within the system.<br><br>Default: `Ring _Inceptor_ [timestamp]` |
|**connection method** |Select the way to connect to the database, support **IP/Port** and **JDBC connection string** two ways.<br><br>When selecting **IP/Port** , you need to configure the **server** and **port** .<br><br>When you select the **JDBC connection string** , you need to configure the **JDBC connection string** . |
|**server** |Enter the IP address or hostname of the server where the database service is located.<br><br>When the **connection method** is **IP/Port** , this is required. |
|**JDBC connection string** |Enter the full JDBC connection string to connect to the database.<br><br>Required when the **connection method** is a **JDBC connection string** . |
|**password** |Enter the password for database authentication.<br><br>When the **authentication method** is a **user name password** , this item is required. |
|**Port** |Enter the port number on which the database service is listening.<br><br>When the **connection method** is **IP/Port** , this is required. |
|**user name** |Enter the user name for database authentication.<br><br>When the **authentication method** is a **user name password** , this item is required. |
|**Authentication method** |Select the authentication method to connect to the database, support **user name password** and **Kerberos** two ways.<br><br>When selecting **a username password** , provide a **username** and **password** .<br><br>When selecting **Kerberos** , you need to configure Kerberos relevant authentication documents and parameters. |
|**Keytab file** |Upload Kerberos Keytab authentication file.<br><br>When the **authentication method** is **Kerberos** , this item is required. |
|**Krb5 file** |Upload Kerberos krb5 configuration file.<br><br>When the **authentication method** is **Kerberos** , this item is required. |
|**Principal** |Enter Kerberos Principal.<br><br>When the **authentication method** is **Kerberos** , this item is required. |
|**kuser** |Enter the kuser information.<br><br>When the **authentication method** is **Kerberos** , this item is required. |
|**permission mode** |Sets the default operating permissions for this data connection.<br><br>**Read** : Allow read operations to be performed.<br><br>**Write** : Allows write operations to be performed.<br><br>Default: **read** |



4. Click **Save** after successful connection.


&nbsp;
