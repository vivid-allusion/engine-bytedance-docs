---
title: "Data Preparation"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Data_Preparation"
---

Before using the unstructured data marking function, you need to create the unstructured data to be labeled as a dataset of VeCDP. At present, it is not supported to directly import unstructured data into VeCDP as a dataset. You need to store unstructured data in database & table first, and then create a dataset of VeCDP by docking with database & table. This article explains how to prepare your data.

<span id="1c0c9475"></span>
# Operating instructions

When importing unstructured data into a database & table, ensure that the database & table contains any of the following types of fields:


* Text field: Stored directly as text content.

* Audio & video/file URL field: the access address of the audio & video file (i.e. converted to text, recommended), and the original audio & video file is stored (not recommended).


<span id="aa65422a"></span>
# Operation steps


1. Log into **the Customer Data Platform** and select **Data Management \- Data Connections.** 

2. Click the **New Data Connection** icon, select **Unstructured Data** , and select Upload File or the corresponding object storage.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2301ee3ef5e4d478fc9d26457091fc7~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   * **Upload file** : Fill in the data connection name, upload the file, the file supports docx, doc, pptx, ppt and other formats, and there is no limit to the number and size.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e62787e74f14a2cbbb3fdfdcb67df52~tplv-goo7wpa0wc-image.image) </span>

   * **Volcanic cloud TOS_ meta information** :

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b49c3b59388481a9a1a807b55c28aae~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |specify |
      |---|---|
      |AccessKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
      |SecretKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
      |Access point (endpoint) |Corresponding to the access domain name of S3Endpoint, and add https://in front of it, for example, TOS Beijing corresponds to https://tos\-s3\-cn\-beijing.volces.com.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09150cf5d40f47c08d97320bd68803e5~tplv-goo7wpa0wc-image.image) </span> |
      |Bucket name (bucket) |Bucket name, such as test\-bucket\-123 |
      |Area (region) |Regions, such as cn\-Beijing. |
      |File directory |The storage directory for data files, such as data/test/. |
      

   * **Tencent Cloud COS_ Meta Information:** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/619cfb151eac4c42adb9032ad9925f5d~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |specify |
      |---|---|
      |AccessKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
      |SecretKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
      |Access point (endpoint) |Corresponding to the access domain name of the Endpoint, and add https://in front of it, such as COS Beijing corresponding [https://cos.ap-beijing.myqcloud.com ](https://cos.ap-beijing.myqcloud.com). |
      |Bucket name (bucket) |Bucket names, such as my\-cos\-bucket\-125xxxx0000 |
      |Area (region) |Region, the distribution area of Tencent cloud hosting computer room |
      |File directory |The storage directory of the data file, be careful not to start with/when filling in here |
      

   * **Alibaba Cloud OSS_ information:** 

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94b288332b88486aa7b564d5aaf38c07~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameter |specify |
      |---|---|
      |AccessKey |Request security credentials for the API. For information on how to obtain an AccessKey, please refer to the official Alibaba Cloud documentation "Creating an AccessKey". |
      |SecretKey |Request security credentials for the API. |
      |Access point (endpoint) |Corresponds to the access domain name of the Endpoint, and adds https://in front of it, such as the OSS Beijing corresponding [https://oss-beijing.aliyuncs.com ](https://oss-beijing.aliyuncs.com). |
      |Bucket name (bucket) |Bucket name, such as hangzhou\-static |
      |Area (region) |Regions, such as cn\-Beijing. |
      |File directory |The storage directory for data files, such as data/test/. |
      

4. Click **Test Connection** to take the data source connectivity test.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/803a5174d0d74db599e712e235be5159~tplv-goo7wpa0wc-image.image) </span>

5. After the test is successful, click **Save** . Click on **one\-click access** and the system will automatically create a dataset and start synchronizing meta information according to your configuration.

6. After the access is complete, you can click to **view data sets** , jump to the data set management page, unstructured data has been written into a structured table.


The following is an example of an enterprise customer service conversation to illustrate the data preparation work in several typical scenarios.

<span id="51c13d14"></span>
# Outbound call conversation extraction (converted to text, recommended)

If the conversation data has converted speech to text, the conversation content text can be stored directly in the database & table, and at least 2 fields, the id column and the content column, need to be retained, as shown below.

In the Customer Data Platform CDP console, select **Data Management \- Data Connection**, see [Excel/CSV Data Connection](https://docs.byteplus.com/docs/dataagent/Excel_CSV_Data_Connection)[ ](https://www.volcengine.com/docs/6356/130758)and [Data Access Overview](https://docs.byteplus.com/docs/dataagent/Data_Access_Overview).

<span id="dea841e2"></span>
# Outbound call conversation extraction (original audio)

If the conversation data is only the original voice, you can follow the following steps:


1. Import voice files into object storage (e.g. TOS) and store URLs in database & table with at least 2 fields, id column and content column. In the Customer Data Platform CDP console, select **Data Management \- Data Connection** , see [Excel/CSV Data Connection](https://docs.byteplus.com/docs/dataagent/Excel_CSV_Data_Connection)[ ](https://www.volcengine.com/docs/6356/130758)and [Data Access Overview](https://docs.byteplus.com/docs/dataagent/Data_Access_Overview).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80ce2314248f4428810f60f0dd55db9d~tplv-goo7wpa0wc-image.image) </span>

2. In the visual modeling step, select the data and store the URL in database & table with at least two fields, the id column and the content column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78c4d9098fe94e32b89d089d7e1c85ec~tplv-goo7wpa0wc-image.image) </span>

3. Connect a REST API 2.0 call operator (call the ASR plug\-in) to complete the speech to text, please refer to the [Rest API 2.0](https://docs.byteplus.com/docs/dataagent/Rest_API_2_0).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/287d52659b1f4d9bb81404efcf7c09bc~tplv-goo7wpa0wc-image.image) </span>


<span id="2e0e1939"></span>
# WeCom Session Extraction


* If the WeCom session archive data has been previously connected to VeCDP, it can be read directly from the data database & table, and at least 2 fields, the id column and the content column, need to be retained. In the Customer Data Platform CDP console, select **Data Management \- Data Connection**, see [Excel/CSV Data Connection](https://docs.byteplus.com/docs/dataagent/Excel_CSV_Data_Connection)[ ](https://www.volcengine.com/docs/6356/130758)and [Data Access Overview](https://docs.byteplus.com/docs/dataagent/Data_Access_Overview).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de086d69f92e45ca83b7952fb4f4f26a~tplv-goo7wpa0wc-image.image) </span>


<span id="13294c63"></span>
# Next step

See [Task Creation](https://docs.byteplus.com/docs/dataagent/Task_Creation_).
