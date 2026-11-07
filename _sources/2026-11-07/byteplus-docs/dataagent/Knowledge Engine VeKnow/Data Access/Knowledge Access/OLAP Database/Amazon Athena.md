---
title: "Amazon Athena"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Amazon_Athena_"
---

Support Amazon Athena data connection. This article explains how to connect Amazon Athena data.

<span id="77632193"></span>
# Premise of use

The user needs to have **project editing** or **permissions \- by user management \- module \- data connection \- new connection** permissions to create a new data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="9efdcbdd"></span>
# Operation steps


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. In the **data connection** interface select **OLAP \> Amazon Athena** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5087ed2cb80a41daaa7f3a6223f2e7b2~tplv-goo7wpa0wc-image.image) </span>

3. Fill in the required basic information and make a **test connection** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22a9bbc269064a6abb9d03df05c589eb~tplv-goo7wpa0wc-image.image) </span>

   1. Access Key **AK and SK** : The Access Key ID and Secret Access Key in Basic Information for Data Connections are Amazon's AK and SK information.

      * You can log in to Amazon, and then click " [My Security Credentials ](https://console.amazonaws.cn/iam/home#/security_credentials)" under the avatar

      * Click on the Amazon IAM certificate, find [ **Access Key ID** ] (choose one), and **generate the ID corresponding to SK** (generate AK generated when the self\-saved information)

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c1a67580e7dfa92e931d623160347b8.png) </span>

   2. Fill in [ **Access Key ID** ] on the Access Key ID (Access Key ID), and fill in [ **This ID corresponds to SK** ] on the Access Key (Secret Access Key).

   3. **Region (Region)**  : Use the above account to click to enter the S3 to be docked, and you can get the region information of the data source on the URL. For example, https://console.amazonaws.cn/s3/buckets?region=cn\-north\-1, its region is cn\-north\-1

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f6955091373f3424f421ce60cf359ee9.png) </span>

      You can fill in the region information into the data connection information

   4. **S3 Temporary Directory (S3OutputLocation)**  :

      * Since Athena is a SQL engine, intermediate computation results need to be stored, so this space is required

      * Users can define the location on their S3. Note that the current user account needs to have read and write permissions to this directory.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ce31f88ccfdd3a0e960c7919637402a.png) </span>

4. Click **Save** after successful connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/39b688fce0c3498d98d78b5ec1b7dc64~tplv-goo7wpa0wc-image.image) </span>
