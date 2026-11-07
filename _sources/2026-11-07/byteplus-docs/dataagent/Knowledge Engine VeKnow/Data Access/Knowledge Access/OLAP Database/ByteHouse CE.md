---
title: "ByteHouse CE"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/ByteHouse_CE_"
---

Support ByteHouse CE data connection, this article introduces how to access ByteHouse CE data.

<span id="3db6f2b0"></span>
# Premise of use


1. The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

2. The [ByteHouse CE Enterprise Edition has been opened ](https://www.byteplus.com/en/product/bytehouse).

   1. Apply for a [BytePlus account ](https://console.byteplus.com/auth/signup); enterprise users need to go to the Volcano Engine official website to apply for a Volcano Engine main account and complete account authentication. For the steps, please refer to the ["Volcano Engine Account Registration and Authentication Operation Guide" ](https://www.volcengine.com/docs/6261/64925).

   2. For real\-name authentication, please refer to [real-name authentication ](https://www.volcengine.com/docs/6261/64935).

   3. Activate [ByteHouse CE Enterprise Edition ](https://www.byteplus.com/en/product/bytehouse).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6f6311d9079434399afa131200fbd40~tplv-goo7wpa0wc-image.image) </span>

3. The steps to create a database and data table in ByteHouse CE can refer to the following operations:

   1. Create a new cluster.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f995a0e2e1d49f58dbc0a0ae2cfdb52~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf5a4c4d73aa47f8a490a262ce0d2301~tplv-goo7wpa0wc-image.image) </span>

   2. Select the cluster you created earlier and click Create Database.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ff39c3ec27a468b8c63e6542aae2d2b~tplv-goo7wpa0wc-image.image) </span>

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41e6866920124e1caf00f376d920058d~tplv-goo7wpa0wc-image.image) </span>

   3. Import data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f15947ca19984a6f9cd7d322cb9ba82a~tplv-goo7wpa0wc-image.image) </span>

   4. Click OK to submit the information.


<span id="c386b6a0"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> ByteHouse CE** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bf4ddf743f54f7ea6d6f69acee1b3bd~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ebf2b09fbc6d4d6080bda3e284f47431~tplv-goo7wpa0wc-image.image) </span>

   
   |configuration item |explain |
   |---|---|
   |data connection name |Support custom name, or use the system default name, the default format is `Bytehouse_CE_YYYYMMDDHHMMSS` |
   |server |Enter the connection address for the server |
   |Port |Enter the port number of the server |
   |user name |Enter the account name used to log in |
   |password |Enter the password corresponding to the specified username |
   

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e51e3bdb638344b1b91dd76156909061~tplv-goo7wpa0wc-image.image) </span>


<span id="f27e9f62"></span>
# Common problem

Without real\-name authentication, you will not be able to access the Volcano Engine ByteHouse Enterprise Edition console normally, and you need to complete [real-name authentication ](https://www.volcengine.com/docs/6261/64935).
