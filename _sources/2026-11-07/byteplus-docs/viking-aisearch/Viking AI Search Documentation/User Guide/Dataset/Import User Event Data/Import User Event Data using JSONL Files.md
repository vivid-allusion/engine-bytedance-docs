---
title: "Import User Event Data using JSONL Files "
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Import_Behavior_Data_JSONL_Files_using_Console"
---

After creating the dataset, you can perform small\-batch uploads of behavior data using JSONL files via the **Console / Behavior Dataset / Import Data** tab. This is suitable for importing bulk historical behavior during the testing phase, and for building user profiles or implementing interest\-based and popularity\-based recall during the cold\-start phase.

&nbsp;

<span id="f35010e6"></span>
## Operational Steps

To begin importing data into your dataset, first navigate to the corresponding data import interface. Follow these steps:


1. Navigate to your **Dataset** list

2. Find the **target dataset** where you want to add data.

3. Click **View** in the action column to enter the dataset detail page.

4. On this page, locate and switch to the **Data import** tab.


Here, you will see the option to import a local Jsonl file. Clicking it will bring up the file upload page

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b2a11454c30745a587ff9fd1cabbcc73) </span>

&nbsp;

You can import locally stored JSONL files on this page. Before importing, please ensure the following:


1. The data in the JSONL file must follow the JSON Lines format specification. Each line must be a valid JSON object, and the file extension must be `.jsonl`.

2. The data fields must match the schema definition you established during dataset creation. Ensure every record includes the corresponding field for the Item ID (Unique Identifier). Records missing an Item ID will fail to import.


&nbsp;

**File Size Requirement:**  


* Each JSONL file must not exceed 10MB.
