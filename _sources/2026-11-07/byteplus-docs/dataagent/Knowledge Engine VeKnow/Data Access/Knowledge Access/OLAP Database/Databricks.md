---
title: "Databricks"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Databricks_"
---

Databricks data connection is supported. This article describes how to access Databricks data.

<span id="f29d3fe5"></span>
## Premise of use


1. The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

2. To obtain the required connection information, you need to do the following to obtain the relevant information:

   1. Log in to your Databricks workspace and go to the environment of **Data Science & Engineering** or **Databricks Machine Learning** .

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_697c9d092f78450d9d36def354e9c417.png) </span>

   2. To change roles, click the icon below the Databricks logo.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a70ff2d1c20a43febafefb7ee3cecf32~tplv-goo7wpa0wc-image.image) </span>

   3. Click the **Compute** tab in the sidebar.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c138cf7673b3bd208f24cc4ba4500124.png) </span>

   4. Select the cluster you want to connect to and click Enter.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4528bc7a4804914a89acb306af6a902~tplv-goo7wpa0wc-image.image) </span>

   5. Click on **Advanced Options** .

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6e099d258b546941b5ea1cdf0602a0bc.png) </span>

   6. Click the JDBC/ODBC tab to copy the JDBC URL to use on subsequent connections.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9bb0859cc23b42b39ee0d2ef2be44125~tplv-goo7wpa0wc-image.image) </span>


<span id="b17fe6d3"></span>
## Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **Data Connection** screen select **OLAP \> Databricks** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2a32cffc8ec46a68b019298512e246c~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46994464e67743c5897bf23b9635e1d7~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The JDBC connection string here is the JDBC string that was copied in the preparation.   </div>
   

4. After the connection is successful, click **Save** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/814a31359a074b99b0c7e8f78e30ef95~tplv-goo7wpa0wc-image.image) </span>


<span id="3d8bcc7e"></span>
# Common problem

**The test connection reported a 403 error.** 

First check whether the username and password are filled in correctly. If there is no error, try to add a whitelist to the database ricks side to solve it.
