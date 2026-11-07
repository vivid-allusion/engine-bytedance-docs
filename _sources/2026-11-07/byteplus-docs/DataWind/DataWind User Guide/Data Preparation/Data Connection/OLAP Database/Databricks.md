---
title: "Databricks"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Databricks"
---

This article explains how to integrate Databricks for dataset creation.

<span id="f0acedbf"></span>
# Functionality overview

Supports integrating Databricks data sources to create datasets. Data connections support **direct connection or offline extraction** of Databricks data sources.

<span id="54139225"></span>
# Preparation

You need to perform the following actions to obtain the necessary connection information:


1. Log in to your Databricks workspace and navigate to the **Data Science & Engineering** or **Databricks Machine Learning** environment.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d9c7f0cd4aa56da7da51bc3b1bce07f.png) </span>

2. To change roles, click the icon below the Databricks logo.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be0ed85bbc5843d6a6cc3f50953589a5~tplv-goo7wpa0wc-image.image) </span>


3. Click the "Compute" tab in the sidebar.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a5e50b0624313b8838aaa83a479a46a.png) </span>

4. Select the cluster you want to connect to and click to enter.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97806be06ca04e6f87edf8cd69835a3e~tplv-goo7wpa0wc-image.image) </span>


5. Click "Advanced Options".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8092d57622f1cc2063032e2204a9d937.png) </span>

6. **Obtain the JDBC connection string**. Click the JDBC/ODBC tab and copy the JDBC URL for use in subsequent connections.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea62cc9e04ee41e69a3ff1cf06773592~tplv-goo7wpa0wc-image.image) </span>


7. **Obtain the password**. Click "User Settings" and then "Generate new token" to generate a token.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8a3103648c424f609520c4cd77bb8757~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To connect using a sub\-account token, ensure that the sub\-account has USAGE and READ_METADATA permissions for the relevant databases and tables.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65ca2895f2c14e55b833b00fcdb82ff8~tplv-goo7wpa0wc-image.image" width="1916px" />   </div>
   

<span id="4018e4ba"></span>
# Create from data connection


1. Go to BytePlus, select a specific project, click Data Preparation, find Data Connection in the dropdown, and click it.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

2. Select Databricks on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c835fdb3c0fd487ea8f04439dc6dda11~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information, test the connection, and click Save after the connection is successful.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16a1f707528947e1b1b59c54fe87c85f~tplv-goo7wpa0wc-image.image) </span>


* The configuration instructions for connecting in the SaaS version are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name for the new data connection, used to distinguish between different database connections in the system. For example, Databricks_20250724110727.<br><br>The name can be modified. Please enter a valid name. Only combinations of Chinese characters, English letters, numbers, and underscores are allowed, and the name must not start or end with a space. |
   |Connection method |* IP/Port: Suitable for general scenarios. Click IP/Port to use this method.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8c2d6d3bcba4944b59e68606910455d~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters. This method is used by default.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This method is recommended, as retrieving parameters is simpler.   </div><br>   <br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd95da485e0742edb1b560770acdef3b~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The server hostname value of Databricks compute resources, that is, `server-hostname`. For details, refer to [the Databricks official documentation](https://docs.databricks.com/aws/en). |
   |JDBC connection string |JDBC connection string. For details, refer to [Preparation](https://docs.byteplus.com/docs/DataWind/Databricks#54139225). |
   |Username |The username created in the database engine. Enter "token" here. |
   |Password |The Databricks token. For details, refer to [Preparation](https://docs.byteplus.com/docs/DataWind/Databricks#54139225). |
   |httpPath |The HTTP path value of Databricks compute resources. The connector constructs the HTTP address to connect to by appending the `httpPath` value to the host and port specified in the connection URL. For example, to connect to the HTTP address `http://localhost:10002/cliservice`, you can use the following connection URL: `jdbc:databricks://localhost:10002;httpPath=cliservice`. |
   |Database |Optional. The database name created in Databricks. |
   

* The configuration instructions for connecting in the privatized version are as follows:

   
   |Parameters |Configuration instructions |
   |---|---|
   |Data connection name |The name for the new data connection, used to distinguish between different database connections in the system. For example, Databricks_20250724110757.<br><br>The name can be modified. Please enter a valid name. Only combinations of Chinese characters, English letters, numbers, and underscores are allowed, and the name must not start or end with a space. |
   |Connection method |* IP/Port: Suitable for general scenarios.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8c2d6d3bcba4944b59e68606910455d~tplv-goo7wpa0wc-image.image) </span><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This method is recommended, as retrieving parameters is simpler.   </div><br>   <br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd95da485e0742edb1b560770acdef3b~tplv-goo7wpa0wc-image.image) </span> |
   |Server |The server hostname value of Databricks compute resources, that is, `server-hostname`. For details, refer to [the Databricks official documentation](https://docs.databricks.com/aws/en). |
   |JDBC connection string |JDBC connection string. For details, refer to [Preparation](https://docs.byteplus.com/docs/DataWind/Databricks#54139225). |
   |Username |The username created in the database engine. Enter "token" here. |
   |Password |The Databricks token value. For details, refer to [Preparation](https://docs.byteplus.com/docs/DataWind/Databricks#54139225). |
   |httpPath |The HTTP path value of Databricks compute resources. The connector constructs the HTTP address to connect to by appending the `httpPath` value to the host and port specified in the connection URL. For example, to connect to the HTTP address `http://localhost:10002/cliservice`, you can use the following connection URL: `jdbc:databricks://localhost:10002;httpPath=cliservice`. For details, refer to the [Databricks official documentation](https://docs.databricks.com/aws/en). |
   |Database |Optional. The name of the database created in Databricks. |
   


<span id="acb08e51"></span>
# Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6753b4124394ae8aec91b6d92e22524~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click Create new configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The subsequent steps are consistent with steps 2 and 3 of **Create from data connection** above. After completing the configuration, you will remain in the popup window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.


<span id="be14e9cc"></span>
# Subsequent steps: Create a dataset


1. Use the previously created data connection to create a dataset: Click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select from the dropdown the previously created data connection.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf3a9affdf50433ab138a6f376e4078c~tplv-goo7wpa0wc-image.image" width="450px" /></div>


<span id="4b95d3c3"></span>
# Frequently asked questions

If a 403 error occurs during connection testing, first check whether the username and password are entered correctly. If they are correct, try adding an allowlist on the Databricks side to resolve the issue. The "public IP accessed by DataWind" can be viewed at [Data Connections Overview](https://docs.byteplus.com/docs/DataWind/Data_Connections_Overview).
