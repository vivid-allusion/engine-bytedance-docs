---
title: "EMR Serverless Spark"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/EMR_Serverless_Spark"
---

This article describes how to integrate BytePlus's EMR Serverless Spark to create datasets.

<span id="ed0bb570"></span>
# Usage restrictions


* The current product only supports integration with BytePlus's EMR Serverless Spark.


<span id="7b6c363c"></span>
# Prerequisites


* Before connecting data, contact the database administrator to collect the following information:

   * The IP address and port number of the server where the database is located

   * The username and password for the database

   * The queue and compute group of the database

* Currently, DataAgent does not support the default compute group. In EMR, you need to create a separate spark\-type compute group.


<span id="3c96b797"></span>
# Preparation

<span id="815b0d19"></span>
# **Create from data connection**


1. Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown list, and create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select EMR Serverless Spark on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a541b95cb444e0d9de0eabedfa2441f~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.

   * The parameter configuration instructions for the SaaS version are as follows:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29e5b03cf41f42c793a1cda12fffced0~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameters |Configuration description |
      |---|---|
      |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. The default is Emr_Serverless_Spark_timestamp. The name can be modified, but please enter a standardized name. Only Chinese, English, numbers, and underscores are allowed, and spaces cannot be included at the beginning or end. |
      |Connection method |There are two options: IP/Port and JDBC connection string. |
      |Server |Required when the connection method is IP/Port.<br><br>The address for connecting to EMR Serverless Spark varies by region.<br><br>North China: serverless\-spark\-jdbc.emr.cn\-beijing.volces.com<br><br>East China: serverless\-spark\-jdbc.emr.cn\-shanghai.volces.com<br><br>South China: serverless\-spark\-jdbc.emr.cn\-guangzhou.volces.com<br><br>Johor: serverless\-spark\-jdbc.emr.ap\-southeast\-1.volces.com |
      |Port |Required when the connection method is IP/Port.<br><br>The EMR instance port; for public cloud, it is usually 10009.<br><br>For details, refer to the documentation: [Cluster component port description](https://www.volcengine.com/docs/6491/110117). |
      |Username |The tenant's AccessKey.<br><br>For instructions, refer to the documentation: [Access Key (Secret) management](https://www.volcengine.com/docs/6291/65568). |
      |Password |The tenant's SecretKey.<br><br>For instructions, refer to the documentation: [Access Key (Secret) management](https://www.volcengine.com/docs/6291/65568). |
      |Queue |The name of the queue used for the connection. Currently, only dedicated queues are supported; public queues are not supported.<br><br>Path to obtain queues in EMR: "Console" \- "Resource Management" \- "Serverless" \- "Queue Details". |
      |Compute group |Compute group name.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Currently, the default compute group is not supported. You need to create a separate compute group of the Spark type.</div><br> |
      |EMR cluster region |Specify the region where the EMR cluster is located. Options include North China (Beijing), East China (Shanghai), South China (Guangzhou), or Asia Pacific (Johor). |
      |Bucket name |To accelerate extraction using TOS, enter the TOS bucket name here. For details, see [Optional: Extraction acceleration](https://docs.byteplus.com/docs/dataagent/EMR_Serverless_Spark#95a26d42). |
      

   * The parameter configuration instructions for the private deployment version are as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/540821182d0246e1a54733372b6a15d0~tplv-goo7wpa0wc-image.image) </span>

```Plain Text
  | | | \
  |Parameters |Configuration description |
  |---|---|
  | | | \
  |Data connection name |The name of the new data connection, used to distinguish between different database connections in the system. Emr_Serverless_Spark_timestamp. The name can be modified, but please enter a standardized name. Only Chinese, English, numbers, and underscores are allowed, and spaces cannot be included at the beginning or end. |
  | | | \
  |Server |Required when the connection method is IP/Port. |\
  | |The address for connecting to EMR Serverless Spark varies by region. |\
  | |North China: serverless-spark-jdbc.emr.cn-beijing.volces.com |\
  | |East China: serverless-spark-jdbc.emr.cn-shanghai.volces.com |\
  | |South China: serverless-spark-jdbc.emr.cn-guangzhou.volces.com |\
  | |Johor: serverless-spark-jdbc.emr.ap-southeast-1.volces.com |
  | | | \
  |Port |Required when selecting IP/Port as the connection method. The instance port of EMR; for public cloud, it is typically 10009. |\
  | |For details, refer to the documentation: [Cluster component port description](https://www.volcengine.com/docs/6491/110117). |
  | | | \
  |Username |The tenant's AccessKey. For instructions, refer to the documentation: [Access Key (Secret) management](https://www.volcengine.com/docs/6291/65568). |
  | | | \
  |Password |The tenant's SecretKey. For instructions, refer to the documentation: [Access Key (Secret) management](https://www.volcengine.com/docs/6291/65568). |
  | | | \
  |Connection method |Two options: IP/Port and JDBC connection string. |\
  | | |\
  | |* IP/Port: Suitable for general scenarios. |\
  | |* JDBC string connection: Suitable when users need to add connection parameters. |
  | | | \
  |JDBC connection string |Required when selecting JDBC connection string as the connection method. For details, refer to the documentation: [JDBC usage](https://www.volcengine.com/docs/6491/1263263). |
  | | | \
  |Queue |The name of the queue used for the connection. Currently, only dedicated queues are supported; public queues are not supported. |\
  | |Path to obtain the queue in EMR: "Console" - "Resource Management" - "Serverless" - "Queue Details". |
  | | | \
  |Compute group |Name of the compute group. |\
  | |:::warning |\
  | |Currently, the default compute group is not supported. You need to create a separate compute group of the Spark type. |\
  | |::: |
  | | | \
  |EMR cluster region |Specify the region where the EMR cluster is located. Options include North China (Beijing), East China (Shanghai), South China (Guangzhou), or Asia Pacific (Johor). |
  | | | \
  |Bucket name |To accelerate extraction using TOS, enter the TOS bucket name here. For details, see [Optional: Extraction acceleration](/docs/dataagent/EMR_Serverless_Spark#95a26d42). |
```


<span id="e648e1d3"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click the Other button.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" />   </div>
   

3. The subsequent steps are the same as steps 2 and 3 of **Create from data connection**. After completing the configuration, you will stay in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step to create the dataset.


<span id="6142d5c6"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. Search for or select from the dropdown the previously created data connection.


<span id="95a26d42"></span>
# Optional: Extraction acceleration

Currently, DataAgent uses a query gateway approach when connecting to EMR Serverless Spark. This approach is insufficient for large\-volume extraction scenarios. To extract large volumes of data, you can use TOS to transfer result sets.

DataAgent supports acceleration by reading result data from TOS, and the extraction speed is expected to increase by dozens of times.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Currently, if the SaaS version of DataAgent and TOS are in the same region, or if the privatized version deployed on BytePlus ECS and TOS are in the same region, TOS can be accessed via the internal network without additional traffic charges. In all other scenarios (that is, when DataAgent and TOS are not in the same region), downloads must be performed via the public network, which will incur additional traffic charges. For details, refer to TOS's <a href="https://www.volcengine.com/docs/6349/79461">traffic fee description</a>.</div>


<span id="08e5bd43"></span>
## Step 1: Create a TOS acceleration bucket

After creating the storage bucket, refer to [Create a storage bucket](https://www.volcengine.com/docs/6349/75024) for detailed steps.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Please select the same region as EMR. Currently, hierarchical namespace buckets (HNS) are not supported.</div>


<span id="f5fa95cc"></span>
## Step 2: Configure TOS to allow cross\-tenant access

After creating the storage bucket authorization policy, refer to [Cross-account authorization](https://www.volcengine.com/docs/6349/102151) for detailed steps.

<span id="bea82474"></span>
## Step 3: DataAgent configuration

When DataAgent connects to EMR Serverless Spark, enter the name of the created TOS bucket in the connection parameters to enable acceleration.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd0b20e3b4a9429a871d1e371c14315f~tplv-goo7wpa0wc-image.image" width="610px" /></div>


&nbsp;
