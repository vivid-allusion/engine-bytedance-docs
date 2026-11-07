---
title: "Hive"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hive_"
---

Support Hive data connection, this article introduces how to access Hive data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">Internet Protocol Address and Port Number of the server where the database is located;</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="b3e1af23"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="c8c75b6c"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. Select **data warehouse** \- **Hive** in the data connection interface.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe919c9d4ea84000ac41db5f0712c0e1~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f826cb48420b41a9a60523f56a9f7d71~tplv-goo7wpa0wc-image.image) </span>

   1. **There are two authentication methods: username and password, kerberos**

      * If the authentication method is kerberos

         * Server, port, keytab, krb5 are provided by the data source.

         * Principal: Refers to the user level, which can generally be viewed through the keytab file. The command is (take dlcdp.keytab as an example):

            * mac：`ktutil --keytab=dlcdp.keytab list`

            * linux：`klist -kt dlcdp.keytab`

               The execution result of the Mac platform:

               <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d00449914e48126d3ce697dc6aa2634.png) </span>

               As can be seen from the figure above, the principal corresponding to the file dlcdp.keytab is dlcdp@CDH.COM.

   2. **connection method**

      * JDBC connection string: Connecting to hive server2 (JDBC) through kerberos must specify the hive principal in the JDBC connection string, where the principal refers to the hive service level. The format of the connection string is:

         ```plaintext
         jdbc:hive2://<host>:<port>/<db>;principal=HivePrincipal
         ```
         

      You can determine the hive principal by looking at the hive\-site.xml. In general, the kerberos\-related configuration will look like this:

      ```xml
      <property>
        <name>hive.server2.authentication</name>
        <value>KERBEROS</value>
      </property>
      <property>
        <name>hive.server2.authentication.kerberos.principal</name>
        <value>hive/_HOST@YOUR-REALM.COM</value>
      </property>
      <property>
        <name>hive.server2.authentication.kerberos.keytab</name>
        <value>/etc/hive/conf/hive.keytab</value>
      </property>
      ```
      

      The red highlight is simply: **hive** \*\*/begins with + machine name + @realm \*\*.

> Note that _HOST location can only use the machine name, not ip.

> Realm is available in the krb5 file. For details, please refer to the following example krb5 file:

> <Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d0e1b48855bdef8e6d285baac1575052.conf" name="krb5.conf">krb5.conf</Attachment>


> 

> Therefore, our hive principal is: `hive/cdh.com@CDH.COM`.


4. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb181494ac77405f891813aa1756d059~tplv-goo7wpa0wc-image.image) </span>
