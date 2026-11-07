---
title: "API Key management"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/api-key-management"
---

Provide an API Key as access credentials when calling the Embedding model for data vectorization in Milvus for VectorDB. This topic describes how to manage API Key.

## Create an API Key

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select **AI center \> API Key** in the left navigation pane, then click **Create an API Key**.

3. In the **Create an API Key** panel, configure the parameters below and then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Name |Enter the name of the API Key. |
   |Permission boundary (optional) |Enter the permission boundary policy JSON. If left blank, the default IAM policy is applied.<br><br>> **tip**<br><br><br>> Supported only for Active account API Keys. It is recommended to enter the Min IAM policy JSON based on Milvus Embedding.<br> |

   > **tip**

   > After creating the API Key, use it to configure Embedding for the Instance. For specific steps, see [Configure Embedding](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/configure-embedding).

## View an API Key

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select **AI center \> API Key** in the left navigation bar, then click the show icon next to the target API Key.

3. Click **confirm** in the pop\-up dialog.

   The API Key becomes visible. You can click the copy button on the right to copy the API Key.

## Disable API Key

You can disable the API Key when it is not in use temporarily.

> **warning**

> Make sure the API Key is not used by any instance before disabling it, to avoid instance errors.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the left navigation bar, select **AI center \> API Key**, then under the **actions** column of the target API Key, click **disable**.

## Delete an API Key

You can delete the API Key when it is no longer in use.

> **warning**

> Confirm the API Key is not used by any Instance before deleting it; otherwise, it may cause Instance errors.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select **AI center \> API Key** from the left navigation bar, then click **Disable** under the **actions** column for the target API Key.
