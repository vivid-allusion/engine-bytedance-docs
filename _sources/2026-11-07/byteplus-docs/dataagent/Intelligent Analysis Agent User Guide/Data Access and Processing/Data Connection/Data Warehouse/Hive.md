---
title: "Hive"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Hive"
---

<span id="_1-概述"></span>
# 1. Overview

Supports integration with Hive to create datasets.

Before connecting to the data, collect the following information:


* The IP address and port number of the server where the database is located.

* The username and password for the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Create from data connection

(1) Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

(2) Select Hive on the page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3c352fc34144a21ad98d41155327b49~tplv-goo7wpa0wc-image.image) </span>

(3) Fill in the required basic information, test the connection, and click Save after the connection is successful.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0d7ed984bde4fc9b7bb1eab3087c0c8~tplv-goo7wpa0wc-image.image) </span>

(4) After confirming that the basic information of the data connection is correct, the data connection is complete.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b0bd434276ec44e6bd581056bff3664d~tplv-goo7wpa0wc-image.image) </span>

(5) You can use this connection as a data source to create datasets: click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(6) Search or scroll through existing connections and select the previously created data source.

<span id="_2-2-从数据集新建"></span>
## 2.2 Create from dataset

(1) Enter BytePlus, click Data Preparation \-\-\> Dataset, and select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

(2) When selecting a data connection, click Create Configuration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


The subsequent steps are consistent with **steps (2) and (3) of 2.1**. After uploading is complete, the system will remain on the popup window for selecting a data connection for the dataset, allowing you to proceed directly to the next step of dataset creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3c352fc34144a21ad98d41155327b49~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能说明"></span>
# 3. Function description

<span id="_3-1-鉴权方式"></span>
## 3.1 Authentication methods

There are two authentication methods: username and password, and Kerberos.

If Kerberos is selected as the authentication method


* The server, port, Keytab, and Krb5 are provided by the data source provider.

* Principal


Here, Principal refers to the user\-level principal, which can generally be viewed through the Keytab file. The command is (using dlcdp.Keytab as an example):


* mac：`ktutil --Keytab=dlcdp.Keytab list`

* linux：`klist -kt dlcdp.Keytab`


Execution result on mac platform:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f3454f82a27db4bef05296b93b666211.png) </span>

As shown above, the Principal corresponding to the dlcdp.Keytab file is dlcdp@CDH.COM.

<span id="_3-2-连接方式"></span>
## 3.2 Connection method


* JDBC connection string


When connecting to hive server2 (JDBC) via Kerberos, you must specify the hive Principal in the JDBC connection string. Here, Principal refers to the service\-level principal for hive. The format of the connection string is:

```plaintext
jdbc:hive2://<host>:<port>/<db>;Principal=HivePrincipal
```


You can determine the hive Principal by checking hive\-site.xml. Generally, Kerberos\-related configuration is as follows:

```xml
<property>
  <name>hive.server2.authentication</name>
  <value>Kerberos</value>
</property>
<property>
  <name>hive.server2.authentication.Kerberos.Principal</name>
  <value>hive/_HOST@YOUR-REALM.COM</value>
</property>
<property>
  <name>hive.server2.authentication.Kerberos.Keytab</name>
  <value>/etc/hive/conf/hive.Keytab</value>
</property>
```


The part highlighted in red can be summarized as: **hive/ + hostname + @realm**.

> Caution: The _HOST position can only use the hostname, not the IP address.


The realm is specified in the Krb5 file. For details, refer to the example Krb5 file below:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a774b36a898fa4ba06317759e24e6280.conf" name="Krb5.conf">Krb5.conf</Attachment>


Therefore, our hive Principal is: `hive/``cdh.com@CDH.COM`.


* The JDBC connection method supports read acceleration configuration, which improves data extraction performance in single\-table and custom SQL scenarios, matching the performance of built\-in Hive.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6fa326155994b0781de882746639b69~tplv-goo7wpa0wc-image.image) </span>

**Note: SaaS products currently do not support JDBC connection string capabilities. Please use the IP/PORT method.** 

<span id="84576ddf"></span>
## 3.3 Read acceleration configuration

When a large amount of data needs to be extracted from Hive tables, it is recommended to enable the read acceleration configuration. This can effectively improve data extraction performance in single\-table, multi\-table JOIN, and custom SQL scenarios, matching the performance of built\-in Hive.

Before enabling the read acceleration configuration switch, please confirm and collect the following information:


* Confirm that the underlying file system of the Hive table is HDFS.

* Collect the IP address and port number of the HDFS NameNode corresponding to the underlying Hive table.

* Confirm that the Hive table to be synchronized is stored in Parquet or ORC format.

* If Kerberos authentication is enabled for the HDFS cluster, you also need to collect the Principal of the HDFS NameNode and upload the Keytab file and Krb5 file.


The Keytab file path and Principal can be found in the hdfs\-site.xml file of the Hadoop cluster.

```XML
<property>
    <name>dfs.namenode.keytab.file</name>
    <value>/var/security/HDFS/hdfs.keytab</value>
</property>
<property>
    <name>dfs.namenode.kerberos.principal</name>
    <value>nn/_HOST@BYTED.COM</value>
</property>
```


In the example above, the Keytab file is located at /var/security/HDFS/hdfs.keytab, and the format of the HDFS NameNode Principal is **nn/ + NameNode hostname + @BYTED.COM**. You can search for the corresponding Principal format in the Keytab file.

&nbsp;
