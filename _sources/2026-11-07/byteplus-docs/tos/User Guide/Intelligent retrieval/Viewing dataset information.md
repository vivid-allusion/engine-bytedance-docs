---
title: "Viewing dataset information"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/View_dataset_information"
---

This topic explains how to view information about a dataset, including basic information, metadata index, and data source details.

<span id="b45b4d33"></span>
## Notes

This feature is currently in closed beta. Please contact your account manager for access.

<span id="e39d3bb4"></span>
## Prerequisites

You have created a dataset. For instructions, see [Creating datasets](https://docs.byteplus.com/docs/tos/Create_dataset).

<span id="f37380d9"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Intelligent retrieve** \> **Data set management**.

3. In the dataset list, click **Manage** in the Actions column of the dataset you want to manage.

4. View basic dataset information.

   
   |**Parameter** |**Description** |
   |---|---|
   |Dataset name |The name of the dataset. |
   |Region |The region where the dataset is located.<br><br>After you create a dataset, you cannot change its region. |
   |Template name |The name of the data retrieval template.<br><br><br>* **Basic information retrieval template**: Retrieves objects based on metadata properties.<br><br>* **Semantic image retrieval template**: Retrieves objects based on metadata properties, and searches for images using text or images.<br><br>* **Semantic video retrieval template**: Retrieves objects based on metadata properties, and searches for videos using text or images. |
   |Dataset created at/creation time |The time when the dataset was created. |
   |Dataset updated at/update time |The time when the dataset was last updated. |
   

5. View the metadata index details of the dataset.

   
   |**Parameter** |**Description** |
   |---|---|
   |Number of indexed files |The total number of objects that have been indexed. |
   |Indexed file size |The total size of the indexed objects in MiB. |
