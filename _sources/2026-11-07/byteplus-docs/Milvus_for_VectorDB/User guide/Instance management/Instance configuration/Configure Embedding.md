---
title: "Configure Embedding"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/configure-embedding"
---

Provide Embedding model management capabilities for the AI center of the Milvus for VectorDB version. You can configure Embedding for the Milvus instance to convert unstructured data into vectors. This article explains how to configure Embedding for an instance.

## Prerequisites

* A dedicated instance has been created and is in **Running** status. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

* API Key has been created. For details, see [API Key management](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/api-key-management).

## Precautions

Only Dedicated instances support configuring Embedding.

## Enable Embedding

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for the instance in the top menu bar.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. On the **Instance details** page, click **Configure** next to **Embedding**, then set the parameters in the **Configure Embedding** dialog box and click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |IAM API Key ID |Select the ID of the created API Key from the dropdown list. |
   |IAM API Key Secret |Click **Get Secret** to obtain the API Key Secret.<br><br>> **warning**<br><br><br><br>* > The obtained Secret is only for this configuration.<br><br><br>* > Clicking **Get Secret** may require entering a verification code sent to the registered email to complete MFA.<br> |

## Modify Embedding configuration

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. On the **Instance details** page, click **Reconfigure** on the right of **Embedding**, then configure the following parameters in the **Configure Embedding** dialog and click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |IAM API Key ID |Select the ID of the created API Key from the dropdown list. |
   |IAM API Key Secret |Click **Get Secret** to obtain the API Key Secret.<br><br>> **tip**<br><br><br><br>* > The obtained Secret is only for this configuration.<br><br><br>* > Clicking **Get Secret** may require entering a verification code sent to the registered email to complete MFA.<br> |

## Turn off Embedding

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. In the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instance list**, select the **Dedicated** tab, then click the target instance name.

5. On the **Instance details** page, click **turn off** to the right of **Embedding**, then click **OK** in the pop\-up dialog.

   > **warning**

   > After disabling Embedding, the instance will no longer support the Embedding feature.
