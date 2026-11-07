---
title: "SCHEMA_LESS NAS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/SCHEMA_LESS_NAS"
---

SCHEMA_LESS NAS is commonly used in scenarios such as data backup, archiving, and video hosting, this article shows you how to access SCHEMA_LESS NAS in Enterprise Knowledge Engine.

<span id="97ab0ff3"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Unstructured Data \- SCHEMA_LESS NAS**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8192fa96d961426596d256da0d3c9114~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4f81f2f7edbd476d8dc2f2e70b804685~tplv-goo7wpa0wc-image.image) </span>

   The specific parameters are described as follows:

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Set the name of the data connection. It is recommended to set it as a unique name that is relevant to the business and easy to identify. |
   |**shareName** |Enter the name of the shared directory on the NAS (network attached storage). |
   |**server** |Enter the Internet Protocol Address or hostname of the NAS server. |
   |**Port** |Enter the port number for the NAS service. |
   |**user name** |Enter the user name for accessing the NAS shared directory. |
   |**password** |Enter the password for the specified user name. |
   |**agreement** |Select the protocol for the connection.<br><br>Currently supports **SMB** protocol. |
   |**basePath** |Sets the root path for access. All read and write operations will take place under this path. This is an optional parameter. |
   |**domain** |Specifies the domain to which the user belongs for authentication.<br><br>Default: `WORKGROUP`. |
   

4. Click **Test Connection** to take the data source connectivity test.

5. After the test is successful, click **Save** . Click on **a key access** , the system will start to perform data access tasks.

6. After the access is complete, you can click to **view the dataset** and jump to the dataset management page.

7. In the **visual knowledge processing module,**  the **data connection** of the new task, the created unstructured data SCHEMA_LESS NAS is used.


<span id="9464f3ea"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
