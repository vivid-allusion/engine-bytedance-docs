---
title: "Binding data sources"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Bind_data_source"
---

After creating a dataset, you can bind a data source to it. This topic describes how to do so.

<span id="8e1bde5e"></span>
## Notes


* This feature is currently in closed beta. Please contact your account manager for access.

* Currently, you can only select an FNS bucket from the same region as the dataset.

* After a data source is bound, an index will be built for it. This process takes time to complete.


<span id="bdec2c57"></span>
## Prerequisites

You have created a dataset. For instructions, see [Creating datasets](https://docs.byteplus.com/docs/tos/Create_dataset).

<span id="d54a5729"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Intelligent retrieve** \> **Data set management**.

3. In the dataset list, click **Manage** in the Actions column of the dataset you want to manage.

4. Click **Bind data source**.

5. Configure the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Select Bucket |Select an existing bucket as the data source. |
   |Index of stock data |Switch on or off the option to index existing data.<br><br><br>* On: Indexes incremental data and batch indexes all existing data.<br><br>* Off: Only indexes incremental data and does not perform batch indexing on existing data. |
   

6. Click **Select**.


<span id="2f499c2b"></span>
## Related operations


|**Operation** |**Steps** |
|---|---|
|View information about bound data sources |On the **Manage data sources** page, view details in the data source list, including **Data source address**, **Status**, **Stock Index**, and **Binding time**. |
|Unbind a data source from the dataset |On the **Manage data sources** page, find the data source list. Then, click **Unbind** in the **Actions** column of the data source you want to remove.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a data source is unbound, the existing data index is retained within the current dataset and is not deleted.</div><br> |
