---
title: "SCHEMA_LESS S3"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/SCHEMA_LESS_S3"
---

SCHEMA_LESS S3 supports the convenient access of a large number of internal knowledge assets (such as product manuals, market analysis reports, customer service dialogue recordings, etc.) to the platform for subsequent AI applications such as document analysis, vectorization, intelligent retrieval and content generation. This article shows you how to access SCHEMA_LESS S3 in the Enterprise Knowledge Engine.

<span id="8562d872"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Unstructured Data \- SCHEMA_LESS S3**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/33b447eaa06f4378bb088d0e9de22585~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3618eb36dcb440bca5e2f6c99b73aacf~tplv-goo7wpa0wc-image.image) </span>


The specific parameters are described as follows:


|parameter |specify |
|---|---|
|accessKey |Request security credentials for the API. |
|secretKey |Request security credentials for the API. |
|Access point (endpoint) |Corresponds to the access domain name of the Endpoint, and adds https://in front of it. |
|Bucket name (bucket) |Bucket name, such as hangzhou\-static |
|Area (region) |Regions, such as cn\-Beijing. |
|file directory |The storage directory for data files, such as data/test/. |
|permission mode |Support for selecting whether to write or read\-only. |
|basePath |The underlying path prefix when accessing object storage |



4. Click **Test Connection** to take the data source connectivity test.

5. After the test is successful, click **Save** . Click on **a key access** , the system will start to perform data access tasks.

6. After the access is complete, you can click to **view the dataset** and jump to the dataset management page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3816c50c99648489e5c52a48ef9299a~tplv-goo7wpa0wc-image.image) </span>

7. In the **data connection** of the new task of **visual knowledge processing** , use the created unstructured data SCHEMA_LESS S3.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a89c51a3f7b47298598e13b56fe3d3b~tplv-goo7wpa0wc-image.image) </span>


<span id="8af935bc"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
