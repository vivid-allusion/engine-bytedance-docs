---
title: "SCHEMA_LESS FTP"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/SCHEMA_LESS_FTP"
---

SCHEMA_LESS FTP is commonly used in scenarios such as data backup, archiving, and video hosting, this article shows you how to access SCHEMA_LESS FTP in Enterprise Knowledge Engine.

<span id="f9a2fd0c"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection page, select **Unstructured Data \- SCHEMA_LESS FTP**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25d3a29c510442ab867fc743f3118952~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/894e4d44243545a18d00456a9f4e5815~tplv-goo7wpa0wc-image.image) </span>

   The specific parameters are described as follows:

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets the name of the data connection to uniquely identify it. The system will generate a name by default, and you can also customize it according to your business requirements. |
   |**server** |Fill in the hostname or IP address of the FTP or SFTP server. |
   |**Port** |Fill in the port number of the server. |
   |**user name** |Fill in the account name used to log in to the server. |
   |**password** |Fill in the password corresponding to the specified account. |
   |**agreement** |Select the protocol used to communicate with the server.<br><br>Supports **FTP** (File Transfer Protocol) and **SFTP** (SSH File Transfer Protocol). |
   |**connection mode** |Select the mode for connecting to the server. Currently displayed as **Pasv (passive mode)**  . |
   |**basePath** |Sets the default starting directory path to access after successfully connecting to the server.<br><br>Default value: `/` |
   

4. Click **Test Connection** to take the data source connectivity test.

5. After the test is successful, click **Save** . Click on **a key access** , the system will start to perform data access tasks.

6. After the access is complete, you can click to **view the dataset** and jump to the dataset management page.

7. In the **visual knowledge processing module,**  the **data connection** of the new task is used to create unstructured data SCHEMA_LESS FTP.


<span id="75a95ab1"></span>
# Related Documentation


* [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)

* [Real-Time Task](https://docs.byteplus.com/docs/dataagent/Real-time_Task)
