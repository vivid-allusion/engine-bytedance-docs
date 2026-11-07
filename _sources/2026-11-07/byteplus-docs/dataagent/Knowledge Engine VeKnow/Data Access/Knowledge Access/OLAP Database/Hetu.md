---
title: "Hetu"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hetu_"
---

Support Hetu data connection, this article describes how to connect Hetu data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The name of the database.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="8f020b99"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="f565dc52"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the **data connection** screen select **OLAP \> Hetu** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5bdea4d8f924291a339b7bb5740c222~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84feb69f55b24ba1bd34bb53f2c14480~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Trino_YYYYMMDDHHMMSS` |
   |connection method |* IP/Port: Support entering the server connection address and port number to connect<br><br>* JDBC connection string: Support entering JDBC connection string connection |
   |JDBC connection string |String to connect to the database through the JDBC interface.<br><br>The following JDBC URL format: `jdbc: presto://host: port jdbc: presto://host: port/catalog jdbc: presto://host: port/catalog/schema`<br><br>For example, use the following URL to connect to Presto running on a `example.net`port with a directory and schema: `jdbc: presto://example.net:8080/hive/sales`<br><br>You can use the URL above to create a connection.<br><br>`String url = "jdbc:presto://example.net:8080/hive/sales"; Connection connection = DriverManager.getConnection(url, "test", **null**);` |
   |server |Enter the connection address for the server |
   |Port |Enter the port number for the server. |
   |Authentication method |* Username and password: If you choose the form of username + password for verification, just enter it directly.<br><br>* Kerberos: If the authentication method is selected Kerberos.<br><br>   * Server, port, keytab, krb5 are provided by the data source.<br><br>   * Principal: The principal here refers to the user level, which can generally be viewed through the keytab file. The command is (take dlcdp.keytab as an example):<br><br>      * mac：`ktutil --keytab=dlcdp.keytab list`<br><br>      * linux：`klist -kt dlcdp.keytab`<br><br>         ```Plain Text```<br>```          The execution result of the Mac platform:```<br>```         ```<br>         <br><br>         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2079a3f69bbcbd822f723d1af6c2792d.png) </span><br><br><br>As can be seen from the figure above, the principal corresponding to the file dlcdp.keytab is dlcdp@CDH.COM.<br><br><br>1. Connection method: |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   |database |Enter the database name |
   

4. Click **Save** after successful connection.
