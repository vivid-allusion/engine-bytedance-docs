---
title: "ByteHouse CE"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouse_CE___"
---

Support ByteHouse CE data connection, this article introduces how to access ByteHouse CE data.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Before you connect to the data, collect the following information:</div>



* <div data-tips="true" data-tips-type="tip">The IP address and port number of the server where the database is located.</div>


* <div data-tips="true" data-tips-type="tip">The username and password for the database.</div>



<span id="8f43b2eb"></span>
# Premise of use


1. The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

2. The [ByteHouse CE Enterprise Edition has been opened ](https://www.byteplus.com/en/product/bytehouse).

   1. Apply for a [BytePlus account ](https://console.byteplus.com/auth/signup); enterprise users need to go to the BytePlus official website to apply for a BytePlus main account and complete account authentication. For the steps, please refer to the ["Volcano Engine Account Registration and Authentication Operation Guide" ](https://www.volcengine.com/docs/6261/64925).

   2. For real\-name authentication, please refer to [real-name authentication ](https://www.volcengine.com/docs/6261/64935).

   3. Activate [ByteHouse CE Enterprise Edition ](https://www.byteplus.com/en/product/bytehouse).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1851ddec9714456cae093b474dd786f0~tplv-goo7wpa0wc-image.image) </span>

3. The steps to create a database and data table in ByteHouse CE can refer to the following operations:

   1. Create a new cluster.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/97c7dd8738614467b7d6eccd089645f3~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/551403a15f584441bf3b49457ecdeec1~tplv-goo7wpa0wc-image.image) </span>

   2. Select the cluster you created earlier and click Create Database.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/295fd142d09c45599981e5bf1b8b8f75~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1612e06844ed413fba9ddaef370aa33f~tplv-goo7wpa0wc-image.image) </span>

   3. Import data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63461cd513e141b693b961dd4a8f4c37~tplv-goo7wpa0wc-image.image) </span>

   4. Click OK to submit the information.


<span id="28bbf965"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **BytePlus Matrix \> ByteHouse CE** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4922a0d5724149389657470a6f984b0e~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbab3a641eab435fac822e0ef02e78da~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Bytehouse_CE_YYYYMMDDHHMMSS` |
   |server |Enter the connection address for the server |
   |Port |Enter the port number of the server |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0439475d5c8c40ec972b2aefb9bec7a4~tplv-goo7wpa0wc-image.image) </span>


<span id="54307e9e"></span>
# Common problem

Without real\-name authentication, you will not be able to access the BytePlus ByteHouse Enterprise Edition console normally, and you need to complete [real-name authentication](https://www.volcengine.com/docs/6261/64935).
