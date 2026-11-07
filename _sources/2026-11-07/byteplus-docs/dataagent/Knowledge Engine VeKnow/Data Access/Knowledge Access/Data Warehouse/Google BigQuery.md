---
title: "Google BigQuery"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Google_BigQuery"
---

Support Google BigQuery data connection. This article explains how to connect Google BigQuery data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The name of the database.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="971f1d0e"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="b0565e61"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> Google BigQuery**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/98de9e62a7ea4ea3acec4fd73fdccd15~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6b7989281ec44a98c0e2bd6523a43c4~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets the name of the data connection, which is unique within the current project. For example, `Google_BigQuery_20240101`. |
   |**ProjectId** |Enter your Google Cloud Platform project ID. This is the unique device identifier that you assign when you create the project in the GCP console. |
   |**OAuthServiceAcctEmail** |Enter the service account email address for authentication. |
   |**OAuthPvtKeyFile** |Click to upload the JSON file containing the private key of the service account. This file is used to authenticate Google BigQuery with OAuth 2.0. |
   

4. Click **Save** after successful connection.
