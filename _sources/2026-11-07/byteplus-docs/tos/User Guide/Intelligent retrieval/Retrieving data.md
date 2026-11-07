---
title: "Retrieving data"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Retrieve_data"
---

To retrieve data using the TOS console, you must first specify a dataset and then set the retrieval conditions. You can either retrieve data based on object metadata properties (basic information retrieval) or search for images or videos using images or text (image retrieval and video retrieval). This topic explains how to retrieve data.

<span id="9cc3d992"></span>
## Notes


* This feature is currently in closed beta. Please contact your account manager for access.

* Datasets that use the **basic information retrieval template** only support basic information retrieval and not image retrieval.

* Datasets using the **semantic image retrieval template** support basic information retrieval and image retrieval.

* Datasets using the **semantic video retrieval template** support basic information retrieval and video retrieval.


<span id="637e49a7"></span>
## Prerequisites

You have created a dataset. For instructions, see [Creating datasets](https://docs.byteplus.com/docs/tos/Create_dataset).

<span id="551ef1e1"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, select **Intelligent retrieve** \> **Data set management**.

3. In the dataset list, click **retrieve** in the **Actions** column of the dataset you want to use.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Alternatively, select <strong>Intelligent retrieve</strong> \> <strong>Data retrieval</strong> in the left navigation pane. Then, select the dataset from which you want to retrieve data.   </div>
   

4. Select the dataset that will be used for retrieval.

5. Enter text or upload an image.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This step only applies to <strong>image retrieval</strong> and <strong>video retrieval</strong>.   </div>
   

   * File in Bucket

      Select an existing bucket from the drop\-down menu and then select an image file within it.

   * Local files (select and upload local files)

      First, select a bucket or a specific directory within a bucket to which the local file will be uploaded. Then, select and upload a local file.

5. Set the retrieval conditions.

   
   |**Parameter** |**Description** |
   |---|---|
   |Storage type |Select the storage type(s) of the objects you want to retrieve. Supported types:<br><br><br>* Standard<br><br>* Infrequent Access<br><br>* Intelligent Tiering<br><br>* Archive Flashback<br><br>* Archive<br><br>* Cold Archive<br><br>* Deep Cold Archive |
   |Filename |Specify the object name for retrieval.<br><br><br>* **Prefix match**: Matches the prefix of the object name.<br><br>* **Equal to**: Retrieves objects with the specified name. |
   |Last modified time |Specify the range of times that the objects were last modified to retrieve them.<br><br>Enter the start and end times in the format **YYYY\-MM\-DD HH:MM:SS**. For example, 2025\-11\-07 17:13:23. |
   |File size |Specify the size of the objects you want to retrieve in B. |
   |ContentType |Specify the file type or format for retrieval.<br><br><br>* **Prefix match**: Matches the prefix of the file type or format.<br><br>* **Equal to**: Retrieves objects with the specified file type or format. |
   |Object tag |Specify the tag(s) of the objects you want to retrieve.<br><br>You can add up to 10 tags. |
   |Result output settings |Select the output mode for the retrieval results.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This step only applies to <strong>basic information retrieval</strong>.</div><br><br><br><br>* **List**<br><br>   Select a sorting method for the results.<br><br>   * **Last modified time**: Results can be sorted in ascending or descending order.<br><br>   * **Filename**: Results can be sorted in ascending or descending order.<br><br>   * **File size**: Results can be sorted in ascending or descending order.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In list mode, you can set up to five sorting criteria.   </div><br>   <br><br>* **Statistics**<br><br>   Select an aggregation method for the results.<br><br>   * **File size**: Results can be aggregated by minimum value, maximum value, or average.<br><br>   * **Storage type**: Results can be aggregated by count, deduplicate count, or group.<br><br>   * **ContentType**: Results can be aggregated by count, deduplicate count, or group. |
   

6. Click **Select**.


<span id="ca7ca065"></span>
## Related operations

After the retrieval process is complete, the results will appear at the bottom of the page.


|**Retrieval mode** |**Output mode** |**Steps** |
|---|---|---|
|Basic information retrieval |List mode |In the list of retrieval results, view the **filename**, **file size**, **storage type**, and **updated at/update time**. |
||Statistical mode |In the list of retrieval results, view the **field name**, **statistical type**, and **aggregation result value**. |
|Image retrieval |List view |Click **List view** to see the following information in the list: **filename, file size, storage type, updated at/update time, content summary, and detailed description**. |
||Preview view |Click **Preview view** to see the image and the following information in the list: **filename, file size, storage type, and updated at/update time**. |
|Video retrieval |List view |In the list of retrieval results, view the **filename, file size, storage type, updated at/update time, content summary, and detailed description**. |
