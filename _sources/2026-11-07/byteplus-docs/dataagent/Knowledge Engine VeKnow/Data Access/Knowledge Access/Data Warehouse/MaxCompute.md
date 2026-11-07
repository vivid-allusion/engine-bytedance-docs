---
title: "MaxCompute"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/MaxCompute_"
---

MaxCompute data connection is supported. This article describes how to access MaxCompute data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">Internet Protocol Address of the server where the database is located;</div>


* <div data-tips="true" data-tips-type="tip">The name of the project.</div>


* <div data-tips="true" data-tips-type="tip">Access ID and Access Secret for MaxCompute project access permissions.</div>



<span id="6b5dc6b1"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="5c1e326f"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the data connection interface, select **data warehouse** \- **MaxCompute** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6661c5184da4230baf38c60be520cda~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4b9d295463e43809ac64bfa52d589b7~tplv-goo7wpa0wc-image.image) </span>

   
   |name |describe |
   |---|---|
   |data connection name |The name can be modified. Please enter the standard name, do not use special characters, and do not include spaces before and after. |
   |server |The server address to connect to the MaxCompute project. |
   |Project Name |The name of the target MaxCompute project. |
   |Access ID and Access Secret |Access ID and Access Secret with access to the target MaxCompute project. |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf7e7a53ad9446a3b33455d5c097e27e~tplv-goo7wpa0wc-image.image) </span>
