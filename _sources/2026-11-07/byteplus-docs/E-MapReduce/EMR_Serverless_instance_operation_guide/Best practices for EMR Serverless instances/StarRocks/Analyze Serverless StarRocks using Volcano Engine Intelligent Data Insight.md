---
title: "Analyze Serverless StarRocks using Volcano Engine Intelligent Data Insight"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Analyze_Serverless_StarRocks_using_Volcano_Engine_Intelligent_Data_Insight"
---

<span id="_1-支持的版本"></span>
## 1 **Supported versions**

Supports collecting data from EMR\-3.1.1 and later StarRocks clusters, as well as fully managed StarRocks engines of version 1.1.0 and above in OLAP services.

Currently, to access StarRocks in EMR, the FE node must be bound to a public IP address and the security group ingress must enable port 9030.

<span id="_2-使用前提"></span>
## 2 **Prerequisites**


1. When configuring the StarRocks data source, ensure that the cluster information and database username and password for the corresponding EMR cluster are entered correctly:

2. The database username provided must have read and write permissions for the relevant database tables to ensure that task data can be properly read from or written to StarRocks.

3. An account password is required. The root account does not have a password, which does not comply with security standards and cannot be used when configuring the data source.

4. You can go to the [EMR Serverless OLAP](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/list) user management page

* Log in to the [EMR Serverless OLAP](https://console.volcengine.com/emr-next/region:emr-next+cn-beijing/list) console.

* In the menu bar at the top left, select the region as appropriate.

* Click the instance name of the target instance.

* Click the **User management** tab.

* When adding a user in the pop\-up dialog box, configure the following information and click **OK**.


<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df80f08891e4180285f432e3c0a5d7a6.png) </span>


3. EMR StarRocks requires that one FE node enables public access and that port 9030 is open in the security group.

   1. Select to enable public access

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_fed090d07968cc778bad7d3390873286.png) </span>

   2. In the EMR StarRocks cluster details page, go to the security management \- allowlist group for the cluster, and add inbound rules.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7ab01b2e95d6aef86e7e39f93daecf9f.png) </span>

4. Before connecting ABI to data, collect the following information:

* The IP address and port number of the server where the database is located. You need to assign the public IP address in advance.

* The database username and password


<span id="_3-从数据洞察新建数据连接"></span>
## 3 Create a data connection from Data Insight

In Volcano Engine Intelligent Data Insight, create a data connection. Refer to [Data connection overview](https://www.volcengine.com/docs/4726/47756).
