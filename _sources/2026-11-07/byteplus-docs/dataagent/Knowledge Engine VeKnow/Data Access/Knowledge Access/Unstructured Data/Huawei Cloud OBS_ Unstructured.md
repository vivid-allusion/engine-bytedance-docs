---
title: "Huawei Cloud OBS_ Unstructured"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Huawei_Cloud_OBS__Unstructured"
---

Huawei Cloud OBS (Object Storage Service) is usually used in scenarios such as data backup, archiving, and video hosting. This article introduces how to access Huawei Cloud OBS unstructured data in Enterprise Knowledge Engine.

<span id="8f22079b"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Unstructured Data \- Huawei Cloud OBS_ Unstructured**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84a235fb012e4341b9572723dfe3f546~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb4cbc63638a4fadac6a3175fe68b173~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |specify |
   |---|---|
   |accessKey |Request security credentials for the API... |
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

7. In the **data connection** of the new task of **visual modeling** , use the created unstructured data Huawei Cloud OBS.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15690f221d1a4af6a44bdf04bea5eb83~tplv-goo7wpa0wc-image.image) </span>


<span id="e2d6b05e"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
