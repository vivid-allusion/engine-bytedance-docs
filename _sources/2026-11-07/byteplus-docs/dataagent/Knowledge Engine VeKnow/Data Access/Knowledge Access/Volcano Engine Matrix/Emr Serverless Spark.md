---
title: "Emr Serverless Spark"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Emr_Serverless_Spark_"
---

Emr Serverless Spark data connection is supported. This article describes how to access Emr Serverless Spark data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before connecting to the database, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<span id="2dadfc15"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="9b719907"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection screen, select **Volcano Engine Matrix** \- **Emr Serverless Spark** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08f8adbb44254b8b9d72d957c7f8fe97~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6f890fa1dd4a447380ab9cdbdd9b5f3a~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets a custom name for the data connection to uniquely identify it. |
   |**connection method** |Select the way to connect to EMR Serverless Spark, which supports **IP/Port** and **JDBC connection string** .<br><br><br>* When selecting **IP/Port** , you need to configure the **server** and **port** .<br><br>* When selecting the **JDBC connection string** , you need to configure the **JDBC connection string** . |
   |**server** |Fill in the server address for EMR Serverless Spark.<br><br>When the **connection method** is **IP/Port** , this is required. |
   |**Port** |Fill in the port number of the EMR Serverless Spark.<br><br>When the **connection method** is **IP/Port** , this is required. |
   |**JDBC connection string** |Fill in the JDBC connection string for EMR Serverless Spark.<br><br>Required when the **connection method** is a **JDBC connection string** . |
   |**user name** |Fill in the username required to access EMR Serverless Spark. |
   |**password** |Fill in the password required to access EMR Serverless Spark. |
   |**queue** |Fill in the queue name to be used. |
   |**calculation group** |Fill in the name of the calculation group to be used. |
   |**EMR cluster area** |Select the region where the EMR cluster is located from the drop\-down list. |
   |**bucket name** |Fill in the name of the bucket to be used. |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae3aa56356294675a33b8a9ee17c2694~tplv-goo7wpa0wc-image.image) </span>
