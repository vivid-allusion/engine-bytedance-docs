---
title: "Alibaba Cloud OSS_ Unstructured"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Alibaba_Cloud_OSS__Unstructured"
---

This article explains how to access Alibaba Cloud OSS for unstructured data in the Enterprise Knowledge Engine.

<span id="6b05e86a"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Alibaba Cloud OSS_ Unstructured**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2321ca081dc3462c89ebe60da434c791~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be506c5c7c1d4e6cbb1cdeaf741aeacb~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |specify |
   |---|---|
   |accessKey |Request security credentials for the API. For information on how to obtain an AccessKey, please refer to the official Alibaba Cloud documentation "Creating an AccessKey". |
   |secretKey |Request security credentials for the API. |
   |Access point (endpoint) |Corresponds to the access domain name of the Endpoint, and adds https://in front of it, such as the OSS Beijing corresponding [https://oss-beijing.aliyuncs.com ](https://oss-beijing.aliyuncs.com). |
   |Bucket name (bucket) |Bucket name, such as hangzhou\-static |
   |Area (region) |Regions, such as cn\-Beijing. |
   |file directory |The storage directory for data files, such as data/test/. |
   

4. Click **Test Connection** to take the data source connectivity test.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84af7c7ee1ed4e2b9acb397e542c8e36~tplv-goo7wpa0wc-image.image) </span>

5. After the test is successful, click **Save** . Click on **a key access** , the system will start to perform data access tasks.

6. After the access is complete, you can click to **view the dataset** and jump to the dataset management page.

7. In the **data connection** of the new task of **visual modeling** , use the created unstructured data Alibaba Cloud OSS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bbc9b2f73554643888d8bb3f1ed3328~tplv-goo7wpa0wc-image.image) </span>


<span id="d0bd5e9f"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
