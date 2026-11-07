---
title: "EMR Serverless Spark"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/EMR_Serverless_Spark"
---

This article shows you how to connect to BytePlus' EMR Serverless Spark to create a dataset.

<span id="6737f172"></span>
# Usage restrictions


* This function currently supports SaaS or private deployment V2.75.0 and above products. If you want to buy it, please contact the business staff for consultation.

* The current product only supports access to BytePlus' EMR Serverless Spark.


<span id="680b631f"></span>
# Prerequisite


* Before connecting to data, please contact your database administrator to collect the following information:

   * The IP address and port number of the server where the database is located

   * The username and password of the database

   * Queues and calculation groups for databases

* At present, DataWind does not support default calculation groups, and a separate calculation group of spark type needs to be created in EMR.


<span id="51c3fb28"></span>
# Preparation

<span id="561cab49"></span>
# **Create from data connection**


1. Enter BytePlus, click to enter a specific project, click Data Preparation, find the data connection in the drop\-down list, and create a new data connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c9ca6ba2217441b98123b7017753ac0~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select EMR Serverless Spark on the page.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7842e43228db4b3c9eed4bd98c5f53fc~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   * The configuration instructions for the relevant parameters of the SaaS version are as follows:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08a7e53d99b94d36856d462d6e3826c7~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection used to distinguish connections to different databases in the system. Default is Emr_Serverless_Spark_ timestamp. The name can be modified, but please enter the standard name. Only combinations of Chinese, English, numbers and underscores are allowed, and spaces cannot be included before and after. |
   |Connection method |IP/Port and JDBC connection strings. |
   |Server |Required when selecting the connection method as IP/Port.<br><br>The address to connect to EMR Serverless Spark is different for each region.<br><br>North China: serverless\-spark\-jdbc.emr.cn\-beijing.volces.com<br><br>East China: serverless\-spark\-jdbc.emr.cn\-shanghai.volces.com<br><br>South China: serverless\-spark\-jdbc.emr.cn\-guangzhou.volces.com<br><br>Johor: serverless\-spark\-jdbc.emr.ap\-southeast\-1.volces.com |
   |Port |Required when selecting the connection method as IP/Port.<br><br>The instance port for EMR, the public cloud, is typically 10009.<br><br>For details, please refer to the document: [Cluster Component Port Description](https://docs.volcengine.com/docs/E-MapReduce/Clustercomponentportdescription?lang=en). |
   |User name |Tenant's AccessKey.<br><br>Get the reference document: [Access Key (key) management](https://docs.volcengine.com/docs/IAM/APIAccessKeyManagement?redirect=1&lang=en). |
   |Password |Tenant's SecretKey.<br><br>Get the reference document: [Access Key (key) management](https://docs.volcengine.com/docs/IAM/APIAccessKeyManagement?redirect=1&lang=en). |
   |Queue |The queue name used by the connection currently only supports the use of exclusive queues, not public queues.<br><br>Queue acquisition path in EMR: "Console" \- "Resource Management" \- "Serverless" \- "Queue Details". |
   |Calculation group |Calculate the group name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default calculation group is not currently supported, and a separate calculation group of type Spark needs to be created.</div><br> |
   |EMR cluster area |Specify the region where the EMR cluster is located, optionally North China (Beijing), East China (Shanghai), South China (Guangzhou) or Asia Pacific (Johor). |
   |Bucket name |When you need to use TOS to accelerate the extraction, you can fill in the TOS bucket name here, please check it for details [Optional: Extraction acceleration](https://docs.byteplus.com/docs/DataWind/EMR_Serverless_Spark#0251c4cb). |
   |Catalog |Used to specify the catalog used by the EMR data connection, determining the range of databases & tables that can be viewed on the left side of the canvas. Not required, empty is equivalent to'default ', only the database & table under default is displayed; when filling in other values, only the database & table under the corresponding catalog is displayed. Validity will be checked when saving or testing connectivity, and an error will be reported if it is not valid. |
   

   * The configuration instructions for the relevant parameters of the privatized version are as follows:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9aa187d7954141898c9bf7464dd76af6~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Data connection name |The name of the new data connection used to distinguish connections to different databases in the system. Emr_Serverless_Spark_ timestamp. The name can be modified, but please enter the standard name. Only combinations of Chinese, English, numbers and underscores are allowed, and spaces cannot be included before and after. |
   |Server |Required when selecting the connection method as IP/Port.<br><br>The address to connect to EMR Serverless Spark is different for each region.<br><br>North China: serverless\-spark\-jdbc.emr.cn\-beijing.volces.com<br><br>East China: serverless\-spark\-jdbc.emr.cn\-shanghai.volces.com<br><br>South China: serverless\-spark\-jdbc.emr.cn\-guangzhou.volces.com<br><br>Johor: serverless\-spark\-jdbc.emr.ap\-southeast\-1.volces.com |
   |Port |Required when selecting the connection method as IP/Port. The instance port for EMR, the public cloud, is typically 10009.<br><br>For details, please refer to the document: [Cluster Component Port Description](https://docs.volcengine.com/docs/E-MapReduce/Clustercomponentportdescription?lang=en). |
   |User name |Tenant's AccessKey. Get the reference document: [Access Key (key) management](https://docs.volcengine.com/docs/IAM/APIAccessKeyManagement?redirect=1&lang=en). |
   |Password |Tenant's SecretKey. Get the reference document: [Access Key (key) management](https://docs.volcengine.com/docs/IAM/APIAccessKeyManagement?redirect=1&lang=en). |
   |Connection method |IP/Port and JDBC connection strings:<br><br><br>* IP/Port: For general use.<br><br>* JDBC string connection: Suitable for scenarios where users need to add connection parameters. |
   |JDBC connection string |Required when selecting the connection method as JDBC connection string. For details, please refer to the document: [JDBC Use](https://docs.volcengine.com/docs/E-MapReduce/JDBCusage?lang=en). |
   |Queue |The queue name used by the connection currently only supports the use of exclusive queues, not public queues.<br><br>Queue acquisition path in EMR: "Console" \- "Resource Management" \- "Serverless" \- "Queue Details". |
   |Calculation group |Calculate the group name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The default calculation group is not currently supported, and a separate calculation group of type spark needs to be created.</div><br> |
   |EMR cluster area |Specify the region where the EMR cluster is located, optionally North China (Beijing), East China (Shanghai), South China (Guangzhou) or Asia Pacific (Johor). |
   |Bucket name |When you need to use TOS to accelerate the extraction, you can fill in the TOS bucket name here, please check it for details [Optional: Extraction acceleration](https://docs.byteplus.com/docs/DataWind/EMR_Serverless_Spark#0251c4cb). |
   


<span id="493cd3e7"></span>
# Create a new dataset


1. Enter BytePlus, click Data Preparation \-\- \> Create, and select the "New Dataset" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6c91b1a11aa64544b4ed04797ec59627~tplv-goo7wpa0wc-image.image) </span>

2. When selecting Data Connection, click the Other button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcb78051a35a460c9d847ee361927de2~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   

3. The subsequent steps are consistent with the above\-mentioned 2 and 3 steps of \*\*create from data connection \*\*above, and will stop in the pop\-up box of data set selection data connection after completing the configuration, and can directly proceed to the next step of data set creation.


<span id="451e3b3a"></span>
# Next steps: Create a dataset


1. Create a dataset using the previously created data connection: Click Data Preparation \-\- \> Create, and select the "New Dataset" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8617c69a8244019a1200ab142dd9f68~tplv-goo7wpa0wc-image.image) </span>

2. Search or drop down to select the previously created data connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7a9ef002d6c4c53a326028618d2bff6~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


<span id="0251c4cb"></span>
# Optional: Extraction acceleration

At present, DataWind uses the query gateway method when docking with EMR Serverless Spark, which is insufficient in the scenario of large data volume extraction; if large data volume extraction is required, the result set can be transferred with the help of TOS.

DataWind supports acceleration by reading the resulting data in the TOS, and the extraction speed is expected to increase by dozens of times.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">At present, if the SaaS version of DataWind is in the same region as TOS, or if the privatized version deployed in Volcano Cloud ECS is in the same region as TOS, TOS can be read through the intranet without additional traffic costs; all other scenarios(that is, DataWind and TOS are not in the same region) need to be downloaded through the public network, which will generate additional traffic costs. For details, please refer to the <a href="https://docs.volcengine.com/docs/TorchObjectStorage/Datatransfer?lang=en">traffic cost description </a>of TOS.</div>


<span id="a3763617"></span>
## Step 1: Create the TOS Accelerator Bucket

Complete the creation of the bucket, please refer to [Create a bucket ](https://docs.volcengine.com/docs/TorchObjectStorage/Creatingbuckets?lang=en)for specific steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please select the same region as the EMR. Hierarchical namespace buckets (HNS) are not currently supported.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/800ffe3a1f2b4b5bacab9ddf7c78c34e~tplv-goo7wpa0wc-image.image) </span>

<span id="63757067"></span>
## Step 2: Configure TOS to allow cross\-tenant access

Complete the creation of the bucket authorization policy. For specific steps, please refer to [Cross-Account Authorization](https://docs.volcengine.com/docs/TorchObjectStorage/Authorizingotheraccounts?lang=en).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a254ce2b76e544458f8fd6ea63886d03~tplv-goo7wpa0wc-image.image) </span>

<span id="99328d92"></span>
## Step 3: DataWind side configuration

When DataWind accesses EMR Serverless Spark, fill in the created TOS bucket name in the connection parameters for acceleration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6618685d8c2240398ee9d8dd631ca712~tplv-goo7wpa0wc-image.image" width="600px" /></div>
