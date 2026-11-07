---
title: "Getting Ark API Key"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Getting_Ark_API_Key"
---

When using the Auto Embedding feature of Document Database for MongoDB, you need to call Ark's embedding model. This topic describes how to get the Ark API Key and configure it in the MongoDB console.

## Prerequisites

* An instance of MongoDB 8.3 or later has been created. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/mongodb/creating_an_instance).

* The instance status is **Running**. For more details about instance status, refer to [Instance status](https://docs.byteplus.com/en/docs/mongodb/instance-status).

> **tip**

> Currently, MongoDB 8.3 is being rolled out in phases. If you need to use the Auto Embedding feature, or if you do not see the **AI capabilities** tab on the instance details page, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

## Precautions

An API Key is a crucial credential for invoking the Ark model service, and it remains valid long\-term after creation. Do not share key information in public environments. Keep keys secure and rotate them regularly to prevent security risks from unauthorized use.

## Procedure

### Step 1: Activate vector model service

1. Log in to the [Ark console](https://console.byteplus.com/ark).

2. In the left navigation bar, select **Model activation**.

3. On the **Model activation** page, click the **Model** tab, then select the **Embedding** sub\-tab.

4. In the model list, locate the target model **Doubao\-embedding\-vision**, and in the **Actions** column on the right, click **Activate**.

5. In the pop\-up dialog box, turn on the **Model hashrate billing** switch, check **I have read and agree to Ark Platform Special Terms, Terms of Service, Doubao Model Service Agreement, and Open\-source Model License**, and then click **Confirm activation and authorization**.

The complete process for activating the embedding service is shown in the figure below.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e19baee6c6beeb7a021ece5db7ad7c7.jpg)

After activation, if the model status is displayed as **Activated**, it means the model is ready for use. If it is no longer needed later, click **De\-activate** in the **Actions** column on the right.

### Step 2: Create and copy API Key

1. In the left navigation bar of the [Ark console](https://console.byteplus.com/ark), select **API Keys**.

2. On the **API Keys** page, click **Create API Key**. Details are shown in the figure below.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0aaa05144fe1737f20bb53ca1e3760ad.jpg)

3. In the pop\-up dialog box, confirm or modify the API Key name in the **Name** text box, then click **Create**. Details are shown in the figure below.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8540327376da010b17ecb14e82aa7faa.png)

4. In the API Key list, find the API Key you just created, click **Copy**, and save it securely. Details are shown in the figure below.![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2e63dac5163e320185055a34589a7841.png)

### Step 3: Configure to MongoDB console

1. Log on to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the top menu bar, select the project and region for the instance.

3. Select either **Replica set instances** or **Sharding instances** in the left navigation bar depending on the instance type.

4. On the target instance type list page, click the name of the target instance to enter the instance details page.

5. In the **AI Capabilities** tab's **API Key management** sub\-tab, paste the copied API Key into the **Ark API Key** input box.![图片](https://sf-bpcms.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/20261021025153-1738004129558.png)

6. Click **Validate and save**. If validation fails, confirm that the API Key is valid and has permission to call models. If the issue persists, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

## Subsequent operations

After completing the API Key configuration, you can create an Auto Embedding vector index. When writing data, MongoDB automatically calls the Ark model to generate vectors, then you can perform vector search using `$vectorSearch`. For more information, refer to [MongoDB Vector Search Quick Start Tutorial](https://www.mongodb.com/zh-cn/docs/vector-search/tutorials/quick-start/).
