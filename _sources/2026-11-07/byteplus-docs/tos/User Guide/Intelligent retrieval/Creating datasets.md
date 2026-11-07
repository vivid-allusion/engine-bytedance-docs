---
title: "Creating datasets"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create_dataset"
---

Intelligent retrieval offers comprehensive, multi\-modal search capabilities for your data stored in TOS. Before retrieving data, you must create a dataset. This topic describes how to do so.

<span id="8e1bde5e"></span>
## Notes


* This feature is currently in closed beta. Please contact your account manager for access.

* The data will be indexed according to the selected template. Both data source binding and index building are background tasks that require time to complete.

* By default, a dataset supports indexing for up to 100 million records. If your data exceeds this limit, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000245) to technical support.


<span id="bdec2c57"></span>
## Prerequisites

You have enabled the intelligent retrieval feature.

<span id="d54a5729"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Intelligent retrieve** \> **Data set management**.

3. In the upper\-left corner of the displayed page, click **Create dataset**.

4. Configure the dataset parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Dataset name |Enter a name for the dataset. The dataset names must:<br><br><br>* Contain only letters, numbers, hyphens (\-), and underscores (_).<br><br>* Be between 1 and 128 characters long.<br><br>* Start with a letter or an underscore (_). |
   |Region |Select the region where the dataset is located.<br><br>After you create a dataset, you cannot change its region. |
   |Select retrieve template |Select a data retrieval template that best fits your needs.<br><br><br>* **Basic information retrieval template**: Retrieves objects based on metadata properties.<br><br>* **Semantic image retrieval template**: Retrieves objects based on metadata properties, and searches for images using text or images.<br><br>* **Semantic video retrieval template**: Retrieves objects based on metadata properties, and searches for videos using text or images. |
   |Additional operators |Additional general\-purpose capabilities beyond the base functionality of the retrieval template.<br><br>Currently, you can only select **Content description** as an additional operator. The search results will include a summary and a detailed description of the image or video.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is only valid when the <strong>semantic image retrieval template</strong> or <strong>semantic video retrieval template</strong> is selected.</div><br> |
   

5. Click **Select**.
