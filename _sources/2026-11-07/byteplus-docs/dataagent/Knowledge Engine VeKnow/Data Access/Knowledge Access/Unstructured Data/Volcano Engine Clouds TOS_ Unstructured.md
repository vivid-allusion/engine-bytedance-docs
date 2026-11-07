---
title: "Volcano Engine Clouds TOS_ Unstructured"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Volcano_Engine_Clouds_TOS__Unstructured"
---

Volcano Engine object storage TOS (Torch Object Storage) is a massive, secure, low\-cost, easy\-to\-use, highly reliable and highly available distributed cloud storage service provided by Volcano Engine. This article shows you how to access unorganized data in Volcano Cloud TOS in the data connection of the Enterprise Knowledge Engine.

<span id="6c4c99fd"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection screen, select **Unstructured Data \- Volcano Cloud TOS_ Unstructured**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d06bd583fb34d82ac5c79bafd0c1269~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8047dbfc8a1742e4949b6a56e7f89890~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |specify |
   |---|---|
   |accessKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
   |secretKey |Request security credentials for the Volcano Engine API, which you can obtain through the **System Configuration \- Access Control \- API credentials** in the upper right corner of the avatar, see [Access Key Management ](https://www.volcengine.com/docs/6291/65568)for details. |
   |Access point (endpoint) |Corresponding to the access domain name of S3Endpoint, and add https://in front of it, for example, TOS Beijing corresponds to https://tos\-s3\-cn\-beijing.volces.com. |
   |Bucket name (bucket) |Bucket name, such as test\-bucket\-123 |
   |Area (region) |Regions, such as cn\-Beijing. |
   |file directory |The storage directory for data files, such as data/test/. |
   

4. Click **Test Connection** and the data source connectivity test will take place.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87b2ca7a55ff4b6cbab8710d7ce52848~tplv-goo7wpa0wc-image.image) </span>

5. After the test is successful, click **Save** . Click on **one\-click access** and the system will automatically create a dataset and start synchronizing data according to your configuration.

6. After the access is completed, you can click **View Dataset** in the upper right corner to jump to the dataset management page.

7. In the **data connection** of the new task of **visual modeling** , use the created unstructured data volcano cloud TOS.


<span id="29f4f7fb"></span>
# Related Documentation


* [What is object storage TOS?](https://www.volcengine.com/docs/6349/74820)

* [Common concepts of TOS](https://www.volcengine.com/docs/6349/74822)

* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
