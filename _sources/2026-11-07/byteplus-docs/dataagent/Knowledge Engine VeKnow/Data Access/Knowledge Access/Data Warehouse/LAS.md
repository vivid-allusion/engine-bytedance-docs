---
title: "LAS"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/LAS_"
---

LAS data connection is supported. This article describes how to access LAS data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before connecting to the database, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password of the database.</div>



<div data-tips="true" data-tips-type="tip">For the IP address and port number of the server, please refer to <a href="https://www.volcengine.com/docs/6492/101901">https://www.volcengine.com/docs/6492/101901</a></div>


<span id="79d40334"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="e65a9b95"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the Data Connection screen, select **Data Warehouse** \- **LAS** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/941ed2baf50f430ea60da2e773e636af~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8735a3856e3b4e77bba366be4689cd63~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |**data connection name** |Sets a unique name for the data connection for identification and management. |
   |**server** |Enter the address of the database or service. It can be an IP address or a domain name. Example: `192.0.0.1` |
   |**Port** |Enter the port number for the service. |
   |**user name** |Enter the user name to log in to the database or service. |
   |**password** |Enter the password to log in to the database or service. |
   |**deployment method** |Select the deployment method of the service, **public cloud** , **privatization** , **privatization 2.0** . The default choice is **public cloud** . |
   |**permission mode** |Select the permission mode for this data connection, **read** and **write** . **Read** is selected by default . |
   |**Region (Region)**  |Select the region where the service is located from the drop\-down list. |
   |**queue** |Enter queue name |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83727f6073c244fd8ccb2bccfe441537~tplv-goo7wpa0wc-image.image) </span>
