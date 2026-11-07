---
title: "Embedding model management"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/embedding-model-management"
---

Milvus for VectorDB’s AI center provides embedding model management to convert unstructured data into vectors. You can add, call, test, and compare models all in one place on the console. This article explains how to manage embedding models.

## Add model

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for the new model from the top menu bar.

3. In the left navigation bar, select **AI center \> Embedding model**, then click **Add model** on the **Model management** tab.

4. In the **Create backup** dialog, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Model source |Select **ContextSearch** or **Volcano Ark**. |
   |Embedding model |Select an Embedding model from the drop\-down list. |
   |Inference service |Select an inference service from the dropdown list.<br><br>> **tip**<br><br><br><br>* > This parameter is visible only when the model source is set to ContextSearch.<br><br><br>* > To create a new inference service, see [Create Custom Inference Service](https://docs.byteplus.com/en/docs/contextsearch/create_a_custom_inference_service).<br> |
   |Model configuration |* **Modality**: select the model modality from the drop\-down list; multiple selections are supported.<br><br>* **Vector type**: select the vector type from the drop\-down list; multiple selections are supported.<br><br>* **Dimension**: enter the vector dimension.<br><br><br>> **tip**<br><br><br>> Common models can use the default configuration.<br> |

## Configure model

After adding ContextSearch or Volcano Ark model for the first time, configure the corresponding API Key for the model source.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for the model configuration in the top menu bar.

3. In the left navigation bar, select **AI center \> Embedding model**, then click **API Key management** in the **Model management** tab or click **Model service configuration** in the **actions** column for the target model.

4. In the **API Key management** dialog box, click **edit** in the **ContextSearch** or **Volcano Ark** section according to the new model source.

5. Enter the API Key for the corresponding model source in the text box, click **Save**, then click **Close**.

## View model

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for the model view in the top menu bar.

3. Select **AI center \> Embedding model** in the left navigation bar, then click the target model name on the **Model management** tab.

   * On the **Basic information** tab, you can view the following details of the model.

      |**Parameter** |**Description** |
      |---|---|
      |Basic information |Basic information includes model ID, model type, model source, status, and creation time. |
      |Vector specifications |Vector specifications include vector type, dimension, and modality. |

   * On the **API call** tab, you can see examples of model calls.

      > **tip**

      > API calls only support Milvus 2.6 and above.

## Test model

After adding an Embedding model, you can test it online by entering text or uploading files to see the generated vector results and time consumed.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region for testing the model from the top menu bar.

3. Select **AI center \> Embedding model** in the left navigation bar, then click the **Model testing** tab.

4. In the **Model selection** area, enter the API Key used to call the model, then select the input type and corresponding model.

   > **tip**

   > If you need a new API Key, refer to [API Key management](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/api-key-management).

5. In the **Test content** area, enter text or upload files according to the selected input type, then click **Generate vector**.

6. View the generated vector results and time consumed in the **Vector result** area.

## Compare models

You can filter models by modality and calculate similarity matrices for the same input set to compare side by side.

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. Select the project and region to add a model from the top menu bar.

3. Select **AI center \> Embedding model** in the left navigation bar, then click the **Model comparison** tab.

4. In the **Model selection** area, enter the API Key used to call the model, then select the input type and models to compare.

   > **tip**

   > If you need to create a new API Key, see [API Key management](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/api-key-management).

5. Enter text or upload a file in the **Comparison content** area according to the selected input type, then click **Start comparison**.

6. View the generated comparison results in the **Comparison results** area.

   > **tip**

   > The closer the numerical value in the comparison results is to 1, the more similar the semantics are; the deeper the color.
