---
title: "Tencent Cloud COS_ Unstructured"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Tencent_Cloud_COS__Unstructured"
---

This article explains how to access the unstructured data in Tencent Cloud COS in the data connection of the enterprise knowledge engine.

<span id="8853c014"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Unstructured Data \- Tencent Cloud COS_ Unstructured**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6b7c848c9574074b2971e2d95ab5d65~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ca34e4c45974733a06e8b01361c4955~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |specify |
   |---|---|
   |accessKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
   |secretKey |To request an API security credential, please go to the API Key Management page of Tencent Cloud Access Management Console to create and obtain it. |
   |Access point (endpoint) |Corresponding to the access domain name of the Endpoint, and add https://in front of it, such as COS Beijing corresponding [https://cos.ap-beijing.myqcloud.com ](https://cos.ap-beijing.myqcloud.com). |
   |Bucket name (bucket) |Bucket names, such as my\-cos\-bucket\-125xxxx0000 |
   |Area (region) |Region, the distribution area of Tencent cloud hosting computer room |
   |file directory |The storage directory of the data file, be careful not to start with/when filling in here |
   

4. Click **Test Connection** to take the data source connectivity test.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ea1657a6f1e4b39a514d7d7d2ecb0fc~tplv-goo7wpa0wc-image.image) </span>

5. After the test is successful, click Save. Click "One\-Click Access" and the system will start configuring and creating the dataset.

6. After successful access, you can click to **view data sets** , jump to the data set management page.

7. In the **data connection** of the **visual modeling** new task, use the created unstructured data Tencent Cloud COS.


<span id="480557fd"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
