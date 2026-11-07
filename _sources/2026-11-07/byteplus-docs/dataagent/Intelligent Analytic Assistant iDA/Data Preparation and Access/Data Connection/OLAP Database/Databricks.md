---
title: "Databricks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Databricks__"
---

This article shows you how to access Databricks to create datasets.

<span id="a9134198"></span>
# Feature Overview

Support accessing Databricks data sources to create datasets. Data connection supports **direct connection or offline extraction** of Databricks data sources.

<span id="bc072648"></span>
# Preparation

You need to perform the following actions to obtain the necessary connection information:


1. Log in to your Databricks workspace and go to the environment of **Data Science & Engineering** or **Databricks Machine Learning** .

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2d9c7f0cd4aa56da7da51bc3b1bce07f.png) </span>

2. To change roles, click the icon below the Databricks logo.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364bc87a7a1540f085243b1913f2793d~tplv-goo7wpa0wc-image.image) </span>

3. Click the Compute tab in the sidebar.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4a5e50b0624313b8838aaa83a479a46a.png) </span>

4. Select the cluster you want to connect to and click Enter.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31ff9d0cfb9e42479eea297102c18c68~tplv-goo7wpa0wc-image.image) </span>

5. Click on "Advanced Options".

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8092d57622f1cc2063032e2204a9d937.png) </span>

6. **Gets the JDBC connection string** . Click the JDBC/ODBC tab to copy the JDBC URL to use on subsequent connections.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6163a832000420190403b811eab934c~tplv-goo7wpa0wc-image.image) </span>

7. **Get the password** . Click "User Settings" and click "Generate new token" to generate a token.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de1e850155994aa590d55a2bbd3f72ca~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use the token of the sub\-account to connect, you need to ensure that the sub\-account has the USAGE of the corresponding database & table, READ_METADATA permissions.   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b98b6b893354ee596494e6365fbd31e~tplv-goo7wpa0wc-image.image" width="1916px" />   </div>
   

<span id="2e2a3ab1"></span>
# New from data connection


1. Enter Volcano Engine, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e287890eafc413da40a2405869979c8~tplv-goo7wpa0wc-image.image) </span>

2. Select Databricks on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d75490f39f24209a08a6eb3327f09ad~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and test the connection. Click Save after the connection is successful.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6b3143917c94b21a50cfed9e03339fe~tplv-goo7wpa0wc-image.image) </span>

   * The connection method configuration instructions are as follows:

      
      |Parameter |Configuration instructions |
      |---|---|
      |Data connection name |The name of the new data connection used to distinguish connections to different databases in the system. For example Databricks_20250724110727.<br><br>The name can be modified. Please enter the name of the specification, only the combination of Chinese, English, numbers and underscores is allowed, and no spaces can be included before and after. |
      |Connection method |* IP/Port: For general use. Click IP/Port to take this approach.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac991752efcb44a8ae147001274b369c~tplv-goo7wpa0wc-image.image) </span><br><br><br>* JDBC connection string: Suitable for scenarios where users need to add connection parameters. Default to this method.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">It is recommended to use this approach to make parameter acquisition easier.   </div><br>   <br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae7fa3def2234395a25483b0b53ecc33~tplv-goo7wpa0wc-image.image) </span> |
      |Server |Databricks computes the server hostname value of the resource, that is, the `server-hostname`, please refer to the [Databricks official website documentation ](https://docs.databricks.com/aws/en). |
      |JDBC connection string |JDBC connection string, please refer to [Preparation](https://docs.byteplus.com/docs/dataagent/Databricks__#bc072648). |
      |User name |The username created in the database engine, please fill in "token" here. |
      |Password |Databricks token, please refer to [Preparation](https://docs.byteplus.com/docs/dataagent/Databricks__#bc072648). |
      |httpPath |Databricks computes the HTTP path value for the resource. The connector constitutes the HTTP address to connect to by appending the `htpPath`value to the host and port specified in the connection URL. For example, to connect to an HTTP address `http://localhost:10002/cliservice`, you can use the following connection URL: `jdbc: databricks://localhost:10002; htpPath = cliservice`. |
      |Database |Optionally, the name of the database created in Databricks. |
      


<span id="4d570583"></span>
# Create a new dataset


1. Enter the Volcano Engine, click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2700dc012b148d59c714846a310b3cc~tplv-goo7wpa0wc-image.image) </span>

2. When selecting a data connection, click New Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/acad03d3a43641cd8c56c4da6e5b8df3~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   

3. The subsequent steps are consistent with the above\-mentioned 2 and 3 steps of **new data connection from** the above, and will stop in the pop\-up box of data set selection data connection after completing the configuration, and can directly proceed to the next step of data set creation.


<span id="a447624e"></span>
# Next steps: Create a dataset


1. Create a dataset using the previously created data connection: Click Data Preparation \-\- \> Dataset, and select the "New" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f8912b6dcc9465db18cf16a29c71ca2~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e20c36c1a3e42b8b5268df56bcaca09~tplv-goo7wpa0wc-image.image) </span>

2. Search or drop down to select the previously created data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46409e54a77f4c58a5d2756f9e904cde~tplv-goo7wpa0wc-image.image) </span>


<span id="2746f80d"></span>
# Common problem

If the test connection reports a 403 error, please first check whether the username and password are filled in correctly. If there is no error, you can try to add a whitelist to the Databricks side to solve it. "Public IP accessed by DataAgent" can be viewed [Data Connection Overview](https://docs.byteplus.com/docs/dataagent/Data_Connection_Overview).
