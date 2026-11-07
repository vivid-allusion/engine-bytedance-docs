---
title: "ClickHouse Client"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/clickhouse-client"
---

ClickHouse Client is a command line client provided by the ClickHouse open\-source community, and can fully interact with the ByteHouse cluster through the command line.

This article describes how to connect to the ByteHouse enterprise cluster using the ClickHouse command line tools.

<span id="6e7c4bd5"></span>
# Prerequisites


* Created ByteHouse cluster, for details, see [Create a cluster](https://docs.byteplus.com/docs/bytehouse/create-a-cluster).

* Set ByteHouse Password, for details, see [Reset connection password](https://docs.byteplus.com/docs/bytehouse/get-cluster-connection-information#9f131fd8).

* Download and install the ClickHouse Client tool.

   <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ca52ec9c2840faa0d7cedc8307facf~tplv-goo7wpa0wc-image.image" name="dp.clickhouse.ce_debian_tob_client_2.6.1.137.tar.gz">dp.clickhouse.ce_debian_tob_client_2.6.1.137.tar.gz</Attachment>
   


<span id="a984fc9e"></span>
# Steps


1. View the connection information of the cluster in **Manage clusters \> Cluster List \> Cluster \> Connect Cluster**, copy and modify the password field. The basic syntax for the connection statement is as follows.

   ```Plain
   clickhouse client
     --host <host>
     --user <user>
     --password <password>
   ```
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4effa40dac3541a9b8da71ef8027df96~tplv-goo7wpa0wc-image.image) </span>

2. Run the connection command to connect to the ByteHouse Cluster.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6695e24427cb441ea0cc65d62dac39bc~tplv-goo7wpa0wc-image.image) </span>


3. Input SQL and press Enter to send the query.


<span id="331767bd"></span>
# Use example

You can refer to the example in [Import from small files](https://docs.byteplus.com/docs/bytehouse/import-from-small-files) to complete the operation.

<span id="c1bc5091"></span>
# Parameter details

The main parameters used by clickhouse\-client are as follows, other parameters can be referred to the official document [Command-line Client](https://clickhouse.tech/docs/en/interfaces/cli/).


|Parameter |Description |
|---|---|
|\-C \-\-config\-file |Specifies the configuration file used by the client. |
|\-h \-\-host |Specify the IP<br><br>of the clickhouse\-server |
|\-\-port |Specify the<br><br>of the clickhouse\-server<br><br> |
|\-u \-\-user | |
|\-\-password | |
|\-d \-\-database | |
|\-V \-\-version |View the client version |
|\-E \-\-vertical |Display the query results in vertical format |
|\-q \-\-query |SQL statement passed in non\-interactive mode |
|\-t \-\-time |Show execution time in non\-interactive mode |
|\-\-log\-level |Client log level |
|\-\-send_logs_level |Specify the server logs level |
|\-\-server_logs_file |Specify server's log storage path |
