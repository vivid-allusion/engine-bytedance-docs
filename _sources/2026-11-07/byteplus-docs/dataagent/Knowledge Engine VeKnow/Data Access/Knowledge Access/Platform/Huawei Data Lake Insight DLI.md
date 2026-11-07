---
title: "Huawei Data Lake Insight DLI"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Huawei_Data_Lake_Insight_DLI"
---

This article shows you how to connect to Huawei Data Lake to explore DLI data.

<span id="5f4365a4"></span>
# Conditions of use

Users need to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to use this function.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="5f8d74e1"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the **data connection** interface select **Platform \- Huawei Data Lake Explore DLI** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/728e9c5fd17a4f51a36d10245bfafbe7~tplv-goo7wpa0wc-image.image) </span>

3. On the edit page, configure the corresponding parameters.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/883d467d8b854b68b7a12a800e22d45f~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Set the name of the data connection for easy identification and management. Name suggestions have business significance. |
   |**connection method** |Select the way to connect to the database. The following two methods are supported:<br><br><br>* **Configuration Items** : Configure connection parameters by filling out the form below.<br><br>* **JDBC connection string** : Configure the connection with the full JDBC URL. [Note: Please add the configuration item that appears after selecting "JDBC connection string"] |
   |**server** |Enter the address of the database server. |
   |**ProjectId** |Enter your project ID. |
   |**user name** |Enter the user name for database authentication. |
   |**password** |Enter the password for database authentication. |
   |**database** |Enter the name of the database to connect to. |
   |**queue** |Enter the name of the calculation queue to use. |
   |**Region (Region)**  |Enter the geographical region where the resource is located. |
   |**obsEndpoint** |Enter the end point node address for the Object Storage Service (OBS). |
   

4. Click **Test Connection** , and after the test is successful, click **Save** .
