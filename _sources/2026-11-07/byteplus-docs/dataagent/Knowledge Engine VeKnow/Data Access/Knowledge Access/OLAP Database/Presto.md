---
title: "Presto"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Presto_"
---

Supports Presto data connection. This article explains how to connect Presto data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The name of the database.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="e211fb88"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="f00f8445"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> Presto** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32b7bcf59d5b4708bf807c8d825bff3b~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/048b143b59c74ca59618be61e99a422a~tplv-goo7wpa0wc-image.image) </span>

   1. There are two authentication methods:

      * Username and password: If you choose the form of username + password for verification, just enter it directly.

      * Kerberos: If the authentication method is selected Kerberos

         * Server, port, keytab, krb5 are provided by the data source.

         * principal:

            The principal here refers to the user level, which can generally be viewed through the keytab file. The command is (take dlcdp.keytab as an example):

            * mac：`ktutil --keytab=dlcdp.keytab list`

            * linux：`klist -kt dlcdp.keytab`

               The execution result of the Mac platform:

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2079a3f69bbcbd822f723d1af6c2792d.png) </span>

               As can be seen from the figure above, the principal corresponding to the file dlcdp.keytab is dlcdp@CDH.COM.

   2. Connection method: JDBC connection string. The following JDBC URL format:

      `jdbc:presto://host:port jdbc:presto://host:port/catalog jdbc:presto://host:port/catalog/schema`

      For example, use the following URL to connect to Presto running on a `example.net`port with a directory and schema:

      `jdbc:presto://example.net:8080/hive/sales`

      You can use the URL above to create a connection.

      `String url = "jdbc:presto://example.net:8080/hive/sales"; Connection connection = DriverManager.getConnection(url, "test", **null**);`

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4130457a300b4629a900690db3864235~tplv-goo7wpa0wc-image.image) </span>
