---
title: "Analyze StarRocks data using Intelligent Data Insights"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Analyze_StarRocks_data_using_Intelligent_Data_Insights"
---

<span id="支持的版本"></span>
## **Supported versions**

Supports collecting data from EMR\-3.1.1 and above StarRocks clusters, as well as fully managed StarRocks engines of version 1.1.0 and above in OLAP services.

Currently, to access StarRocks in EMR, the FE node must be bound to a public IP and the security group ingress must enable port 9030.

<span id="使用前提"></span>
## **Prerequisites**


1. When configuring the StarRocks data source, ensure that the EMR cluster information and database username and password are entered correctly:

2. Important: The database username provided must have read and write permissions for the relevant database tables to ensure task data can be properly read from or written to StarRocks. To obtain the username and password, you can view the **EMR cluster details ＞ Service list ＞ StarRocks service name ＞ Service parameters ＞ starrocks\-env** parameter file, where StarRocks has a preset account and password. It is recommended to use this account/password to configure the StarRocks data source. For other user creation methods, see [CREATE USER](https://docs.starrocks.io/zh-cn/latest/sql-reference/sql-statements/account-management/CREATE%20USER)

3. EMR StarRocks requires that one FE node enables public access and opens port 9030 in the security group.

   1. FE node [binds Elastic EIP](https://console.volcengine.com/eip/). For details, see: [Bind public IP](https://www.volcengine.com/docs/6401/68687).

   2. FE node [security group](https://console.volcengine.com/vpc/) allows access to port 9030. For details, see: [Add access rule](https://www.volcengine.com/docs/6401/68895).

   3. In the EMR StarRocks cluster details page, enter the security group for the cluster and add inbound rules.

4. Supports connecting to StarRocks to create datasets.

> The StarRocks data source currently supports extraction mode, and direct connection mode will be available soon.


Before connecting data, please collect the following information:


* The IP address and port number of the server hosting the database. You need to allocate a public IP address in advance..

* The database username and password


<span id="从数据洞察新建数据连接"></span>
## Create a new data connection in Data Insights

In Volcano Engine Intelligent Data Insights, create a data connection. Refer to [Data connection overview](https://www.volcengine.com/docs/4726/47756).
