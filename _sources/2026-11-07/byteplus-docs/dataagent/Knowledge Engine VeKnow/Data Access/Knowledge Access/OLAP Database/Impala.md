---
title: "Impala"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Impala_"
---

Support Impala data connection, this article describes how to access Impala data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="36bdd9a0"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="25246080"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the **data connection** screen select **OLAP \> Impala** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df437f4367b54af3833abe92b49c41e1~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a74336540a34c649f036dba9c028dfe~tplv-goo7wpa0wc-image.image) </span>

   There are currently two authentication methods:

   * If you choose a username and password, you can choose to log in and verify by username + password according to your needs.

   * If you choose Kerberos, you need to upload the Keytab file and Krb5 file and fill in the principal.

      * Server, port, keytab, krb5 are provided by the data source.

      * Principal: The principal here refers to the user level, which can generally be viewed through the keytab file. The command is (take dlcdp.keytab as an example):

         * mac：`ktutil --keytab=dlcdp.keytab list`

         * linux：`klist -kt dlcdp.keytab`

            The execution result of the Mac platform:

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_18865b66eac7b6522a7a481f658631f8.png) </span>

            As can be seen from the figure above, the principal corresponding to the file dlcdp.keytab is dlcdp@CDH.COM.

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b03937d9cfa44eacac1fd1df9e6792d8~tplv-goo7wpa0wc-image.image) </span>
