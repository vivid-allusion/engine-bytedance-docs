---
title: "Databricks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Databricks"
---

This article describes how to integrate Databricks to create datasets.

<span id="4d63056b"></span>
# Feature overview

Supports integrating Databricks data sources to create datasets. Data connections support **direct connection or offline extraction** of Databricks data sources.

<span id="06708397"></span>
# Preparation

You need to perform the following actions to obtain the necessary connection information:


1. Log in to your Databricks workspace and navigate to the **Data Science & Engineering** or **Databricks Machine Learning** environment.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d9c7f0cd4aa56da7da51bc3b1bce07f.png) </span>

2. To change roles, click the icon below the Databricks logo.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c3c3b94109f4f6fba827289f5a281f3~tplv-goo7wpa0wc-image.image) </span>

3. Click the "Compute" tab in the sidebar.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a5e50b0624313b8838aaa83a479a46a.png) </span>

4. Select the cluster you want to connect to and click to enter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1e9fd46d30b4adeb0e3b96086091134~tplv-goo7wpa0wc-image.image) </span>


5. Click "Advanced Options".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8092d57622f1cc2063032e2204a9d937.png) </span>

6. **Obtain the JDBC connection string**. Click the JDBC/ODBC tab and copy the JDBC URL for use in subsequent connections.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90712a8574aa44d6b582508a0e0ddf37~tplv-goo7wpa0wc-image.image) </span>

7. **Obtain the password**. Click "User Settings" and then click "Generate new token" to generate a token.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fccc97a033e843faa9e909e36e7c0ae9~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">When connecting using a sub\-account token, ensure that the sub\-account has USAGE and READ_METADATA permissions for the corresponding database tables.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f21cbdbc8594c88ae04765d34b4d9d4~tplv-goo7wpa0wc-image.image" width="1916px" />   </div>
   

<span id="7ad51906"></span>
# Create from data connection


1. Go to BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Databricks on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1294e7cd87494982a0cb78cafcab9d44~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e59433a49cf347c0b0030a60472aada1~tplv-goo7wpa0wc-image.image) </span>

   * The configuration instructions for the connection method are as follows:

      
      |Parameters |Configuration instructions |
      |---|---|
      |Data connection name |Name for the new data connection, used to distinguish between different database connections in the system. For example, Databricks_20250724110727.<br><br>The name can be modified. Please enter a standardized name. Only combinations of Chinese, English, numbers, and underscores are allowed. Spaces are not allowed at the beginning or end. |
      |Connection method |* IP/Port: Suitable for general situations. Click IP/Port to use this method.<br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters. This method is used by default.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This method is recommended, as parameter acquisition is simpler.   </div><br>    |
      |Server |The server hostname value of Databricks compute resources, that is, `server-hostname`. For details, refer to [the official Databricks documentation](https://docs.databricks.com/aws/en). |
      |JDBC connection string |JDBC connection string. For details, refer to [Preparation](https://docs.byteplus.com/docs/dataagent/Databricks#06708397). |
      |Username |Please enter "token" here as the username created in the database engine. |
      |Password |The Databricks token. For details, refer to [Preparation](https://docs.byteplus.com/docs/dataagent/Databricks#06708397). |
      |httpPath |The HTTP path value of Databricks compute resources. The connector constructs the HTTP address to connect to by appending the `httpPath` value to the host and port specified in the connection URL. For example, to connect to the HTTP address `http://localhost:10002/cliservice`, you can use the following connection URL: `jdbc:databricks://localhost:10002;httpPath=cliservice`. |
      |Database |Optional. The name of the database created in Databricks. |
      


<span id="eb76591e"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click Create Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" />   </div>
   

3. The subsequent steps are consistent with steps 2 and 3 of **Create from data connection** above. After completing the configuration, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.


<span id="7fc23a9d"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

2. Search for or select from the dropdown the previously created data connection.


<span id="0a83b967"></span>
# Frequently asked questions

If the connection test returns a 403 error, first check whether the username and password are entered correctly. If they are correct, try adding an allowlist on the Databricks side to resolve the issue. The "public IP accessed by DataAgent" can be viewed at [Overview of Data Connection](https://docs.byteplus.com/docs/dataagent/Overview_of_Data_Connection) .
