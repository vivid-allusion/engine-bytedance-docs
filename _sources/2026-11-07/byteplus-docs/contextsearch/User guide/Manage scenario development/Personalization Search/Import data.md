---
title: "Import data"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Import_data"
---

In personalization search and recommendation scenarios, you need to first import business data into the dataset to proceed with subsequent model development and performance optimization. This topic describes how to import data.

<span id="QC8fqXXa"></span>
## Prerequisites


* A personalization search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

* Dataset has been added. For more information, see [Add a dataset](https://docs.byteplus.com/en/docs/contextsearch/Add_a_dataset).


<span id="VQQmiqyW"></span>
## Precautions

The dataset used for development tasks must contain at least 1,000 records.

<span id="cWavvUk0"></span>
## Procedure


1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) </span>icon on the top\-right corner on the target personalized search and recommendation scenario page, then on the added dataset card, click **Import data**.

5. On the **Import data** tab, click **Import local files**.

6. In the **Add file** sub\-panel, select **Item file**, **User file**, or **Behavior file** to import the corresponding data.

   1. Click **JSONL file template download** or **CSV file template download** in the file upload area as needed. The file template example is as follows.

      
      <Tabs>
      <Tab zoneid="B7pCsjQdDy" title="JSONL file">
      <TabTitle>JSONL file</TabTitle>
      
      ```JSON
      {"user_id": "u1", "item_id": "i1", "label": 1, "timestamp": 1710000000}
      {"user_id": "u2", "item_id": "i2", "label": 0, "timestamp": 1710000100}
      {"user_id": "u3", "item_id": "i3", "label": 1, "timestamp": 1710000200}
      ```
      
      
      
      </Tab>
      <Tab zoneid="RZpdEKGapy" title="CSV file">
      <TabTitle>CSV file</TabTitle>
      
      ```Plain Text
      user_id,item_id,label,timestamp
      u1,i1,0.98,1710000000
      u2,i2,0.87,1710000100
      u3,i3,0.76,1710000200
      ```
      
      
      
      </Tab>
      </Tabs>
      

   2. Add the data to be imported in the downloaded template. The data fields are described in the following table.

      
      |Fields |Description |
      |---|---|
      |user_id |User ID. |
      |item_id |Item ID. |
      |label |Action label. |
      |timestamp |Action timestamp. |
      

   3. Click the upload area, select the JSONL file or CSV file containing added data, then click **OK**.


<span id="fsWacNJ2"></span>
## Subsequent operations

After importing data, you can proceed with model development. For more information, see [Model development](https://docs.byteplus.com/en/docs/contextsearch/Model_development).
