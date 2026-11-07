---
title: "Connect to the instance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Connect_to_the_instance"
---

This topic describes how to connect to a Milvus for VectorDB instance using a client.

## Prerequisites

An instance is created and is in the **Running** state. For more information, see [Create an instance](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_an_instance).

## Procedure

1. Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus).

2. in the top menu bar, select the project and region for the instance.

   > **tip**

   > If the instance is not configured with a project, select **All resources**.

3. Click **Instance list** in the left navigation pane.

4. In the **Instances** list, select the **Dedicated**, **Serverless**, or **On\-Demand** tab based on the instance type, then click the target instance name.

5. On the **Instance details** page, select the **Connection guide** tab.

6. (Optional) When selecting an On\-Demand instance, you can quickly complete resource creation before connecting to the instance.

   1. In the **Create collection** area, click **Managed Collection** or **External Collection** to create the corresponding type of collection. For information about how to create a collection, see [Create a collection](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Create_a_collection).

   2. In the **Create Query cluster** area, click **Create cluster**. For more information, see [Query cluster management](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Query_cluster_management).

7. On the **Connection guide** tab, select the connection method based on your business requirements, and view the detailed connection steps. The following methods are supported: **Python**, **Java**, **NodeJs**, **Go**, and **RESTful API**.
