---
title: "Getting started with vector databases- API V2"
product: "Vector Database Cloud"
product_code: "VikingDB"
source: "https://docs.byteplus.com/en/docs/VikingDB/Getting_started_with_vector_databases_V2"
---

> The following best practices are based on the new API V2 version, and it is recommended to use this version.


To get started with VikingDB, this guide provides step\-by\-step instructions for setting up your first vector library in minutes. You will learn how to use the console to complete the entire workflow, including creating a collection, building an index, writing data, and performing a retrieval query.

In this guide, we will guide you to quickly complete the configuration of your first vector library in just a few minutes, allowing you to go through the entire process of Collection creation, index creation, and retrieval query on our configuration page.

<span id="a0f65846"></span>
# Step 1: Create a Collection

There are **two ways to create a Collection**:


* Method 1: Click on Vector Database on the homepage to enter the console's **Get Started** page, then click **Create Collection** in the first step of the tutorial bar at the top of the page.

* Method 2: Click on Vector Database on the homepage to enter the console. Click **Collections** in the left navigation bar of the console to enter the Collection page, then click **Create Collection** in the upper left corner.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/133ef97064684038a81828d14aa61429~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae20281af7f8430b9abba4f982d186f0~tplv-goo7wpa0wc-image.image) </span>


3. You can create a Collection by **vectorizing text and image data** or **directly importing existing vectors**. The creation method you choose depends on your data preparation:

*  **"Existing Vector Data"**  is suitable for the following scenarios:

   * You have already vectorized your text or image data and have vector data ready to be imported.

   * You do not need to store your original multimodal data (such as images and videos) in the associated TOS bucket. Instead, you can call the vectorization service (such as [Embedding Calculation](https://docs.byteplus.com/en/docs/VikingDB/Embedding_Calculation_V2)) in real time and write only the resulting vectors to the Collection.

*  **"Start from Vectorization"**  is suitable for the following scenarios:

   * You have not yet vectorized the data, and the system will automatically vectorize text, image, and other fields according to the model you configure.


In this example, we use the **Start from Vectorization** method to create a Collection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcf62d2cc0924636843afaadabb10066~tplv-goo7wpa0wc-image.image) </span>


4. Fill in the relevant parameters on the [Create Collection](https://docs.byteplus.com/en/docs/VikingDB/Create_Collection) page, including basic collection information, vector configuration, and database fields. Complete the specific configuration by referring to the example on the right.

5. After filling in the parameters, click **Submit** in the lower right corner to complete the Collection creation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bec48e2d47748ad8a7c2d6bce082bb2~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f7ea73cd33342108991081ff9d66453~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
(Example)</div>



1. If you need to add sparse vector fields, you must configure dense vector fields, meaning sparse vectors cannot appear alone.

2. Do not define fields used for vectorization again in the scalar field configuration. Any text, image, or video fields defined there are used only for data storage, not for vectorization, and their names cannot be the same as the vectorization fields.


<span id="4bee9fff"></span>
## Collection Configuration Items


|**Number** |**Parameter Name** |**Parameter Description** |
|---|---|---|
|1 |Basic Information (Required) |* Name is required, alias and description are optional |
|2 |Vector Information (Required) |* Configure vector fields (existing vector fields) or fields for vectorization (starting from vectorization). |
|3 |Field Configuration (Optional) |* Configure scalar fields for metadata or raw data storage.<br><br>* Field Name: Use English letters, numbers, and underscores _, starting with an English letter, and cannot be repeated.<br><br>* Field Type: Select field type from the dropdown list, optional values: string, bool, list, int64, float32, text, image, video.<br><br>* Default: When the field type is not text, image, or video, a default value can be entered. If this default value is not provided and a field is missing data during a write operation, the system populates it with a default value.<br><br>* **Full\-text search (New):**  When the field type is text, you can optionally enable full\-text search. After it is enabled, tokenization and keyword\-based retrieval are supported and can be combined with existing vector search and filtering capabilities. A collection can enable full\-text search for up to two text fields.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63585fb30cd74611900b6a3bea157efa~tplv-goo7wpa0wc-image.image) </span> |
|4 |Primary Key (Required) |* The primary key is used to uniquely identify a row of data<br><br>* You can choose to either automatically generate a primary key or select a string/int64 field from your field configuration to serve as the primary key |
|5 |Cost Details and Collection Creation |* If a vectorization model is configured, model cost information will be displayed<br><br>* After an index is created, offline storage resource costs will be billed based on the volume of stored data |


<span id="d8f7ca08"></span>
# Step 2: Create an Index


1. There are **three ways to enter the Create Index** page:

   * Method 1: Click **Quick Start** in the left navigation bar, then click **Create Index** in the second step of the tutorial bar at the top of the page

   * Method 2: Click **Index** in the left navigation bar to enter the index page. Click **Create Index** in the upper left corner of the index list page to enter the **Create Index** page.

   * Method 3: Click **Collections** in the left navigation bar to enter the Collection page. Select the Collection you want to create an index for, then click **Create Index** under the "..." button in the upper right corner of the corresponding Collection card


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0422b2c839d24217b598911082e4a62d~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac518fce6f5440d6b702a40efe27a162~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/47068567f50047538178295f87253a03~tplv-goo7wpa0wc-image.image) </span>


2. Fill in the relevant parameters on the [Create Index](https://docs.byteplus.com/en/docs/VikingDB/Create_an_index) page, including basic index information and specific index configuration

3. After filling in the parameters, click **Submit** in the lower right corner to complete the index creation.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d90dd09bfe3149448d14746ae9cb0d3e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/849a3be5ff154f1da5c6a98637504e8b~tplv-goo7wpa0wc-image.image) </span>

<span id="34f749a7"></span>
# Step 3: Write Data


1. After creating the Collection, you can write data to it by following the data writing guide that appears.

2. On the **Collections** page, you can also click the **Write Data** button on the corresponding Collection card to find this popup window.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/32b1f7100bf64598826ddd34629dc79f~tplv-goo7wpa0wc-image.image) </span>

Data writing supports four methods: online writing, local data import, adding from TOS, and single data insertion (currently, videos only support online writing).

Click [**Write Data**] to enter the write page

**Online Writing**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a8d6422b0f241a4b8dd87fe5f6f387e~tplv-goo7wpa0wc-image.image) </span>

<span id="38674cd5"></span>
## **Category 1: Online Writing**


* ### **Synchronous Writing**   <span id="synchronous-writing"></span>


This method is for scenarios that require data to be written and available in real time, and it provides a streaming write interface

**Writing Data:**  When writing data, the parameters you need to upload depend on whether you chose  **"Start from Vectorization"**  or  **"Existing Vector Data"**  during collection creation.


* For the specific writing process, refer to the [Data Plane API Calling Process](https://docs.byteplus.com/en/docs/VikingDB/Data_Plane_API_Calling_Process). For the data writing API, refer to [InsertData](https://docs.byteplus.com/en/docs/VikingDB/Insert_Data)

* For multimodal data writing, please see best practices for details


**Writing Example:** 

Please create a Collection, fill in the Collection name, AK SK, field, and host

```Python
      \n\"\"\"\npip3 install volcengine\n\"\"\"\nimport os\n\nfrom volcengine.auth.SignerV4 import SignerV4\nfrom volcengine.Credentials import Credentials\nfrom volcengine.base.Request import Request\nimport requests, json\n\nclass ClientForDataApi:\n    def __init__(self, ak, sk, host):\n        self.ak = ak\n        self.sk = sk\n        self.host = host\n\n    def prepare_request(self, method, path, params=None, data=None):\n        r = Request()\n        r.set_shema(\"https\")\n        r.set_method(method)\n        r.set_connection_timeout(10)\n        r.set_socket_timeout(10)\n        mheaders = {\n            \'Accept\': \'application/json\',\n            \'Content-Type\': \'application/json\',\n            \'Host\': self.host,\n        }\n        r.set_headers(mheaders)\n        if params:\n            r.set_query(params)\n        r.set_host(self.host)\n        r.set_path(path)\n        if data is not None:\n            r.set_body(json.dumps(data))\n        credentials = Credentials(self.ak, self.sk, \'vikingdb\', \'cn-beijing\')\n        SignerV4.sign(r, credentials)\n        return r\n        \n    def do_req(self, req_method, req_path, req_params, req_body):\n        req = self.prepare_request(method=req_method, path=req_path, params=req_params, data=req_body)\n        return requests.request(method=req.method, url=\"http://{}{}\".format(self.host, req.path),\n                                  headers=req.headers, data=req.body, timeout=10000)\n\nif __name__ == \'__main__\':\n    client = ClientForDataApi(\n        ak = \"*\",#your ak\n        sk = \"*\",#your sk\n        host = \"api-vikingdb.vikingdb.ap-southeast-1.bytepluses.com\",#your region host\n    )\n    req_method = \"POST\"\n    req_params = None\n    req_path = \"/api/vikingdb/data/fetch_in_collection\"# url\n    req_body = {\n        \"collection_name\": \"my_collection\", #your collection name\n        \'ids\': [1, 2, -1]\n    }\n    result = client.do_req(req_method=req_method, req_path=req_path, req_params=req_params, req_body=req_body)\n    print(\"req http status code: \", result.status_code)\n    print(\"req result: \\n\", result.text)\n
```


<span id="6796f729"></span>
## **Category 3: Import from TOS**

Images and text are supported. Video data is not supported for importing from TOS yet.


1. **Enable and authorize TOS**

   * Enable TOS service

      * Create a TOS bucket: [Create Bucket](https://console.byteplus.com/tos/bucket/create?)

   * Authorize VikingDB access

      * Authorize the VikingDB service to access your TOS: [TOS console](https://console.byteplus.com/tos/bucket). Skip this step if you have activated TOS.


If you need to import multimodal data, upload the image files to TOS first, and pass the TOS object path in the image field. Example:

```Python
{\"animal_image\": \"tos://best-practice-pic-search-tos/pic_search_1000_images/0009fc27d9.jpg\"}\n
```



2. **Import data from TOS**

   1. **Direct import**

      * Select a json/parquet file from your TOS bucket in the console.

   2. **Import via API**

      * Create an offline task with TaskType = data_import to import a json/parquet file. See CreateVikingdbTask for details.


<span id="3c981c40"></span>
# Step 4: Retrieval Query


1. On the **Index List** page operation column, click the **Retrieval Test** button of the specified index to enter the **Retrieval Test** page.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0017da3ade154bb5b73b4bacb4c16dec~tplv-goo7wpa0wc-image.image) </span>


2. The options on the retrieval test page depend on your Collection's configuration.

   * You can input **query vectors**, **limits (Top\-K)** , and **sub\-indices** for retrieval testing

   * If you configured according to the above example, with a vectorization model configured when creating the Collection, you can input text in the input box for end\-to\-end text retrieval.

   * If you enabled full\-text search, you can select your preferred retrieval method from the filter bar above the dialog box, and choose Text search or Keyword search.

   * The retrieval test will have a **dense_weight parameter** to control the weight of dense vectors in hybrid retrieval.

3. After you click Query, the results on the right side of the page will show the K most similar vectors based on your query. The query results are sorted by score from high to low by default.

4. If you created a collection by directly importing vectors and included a hybrid index of dense and sparse vectors, you need to input both dense and sparse vectors for retrieval.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9ee257b63da3491db536fee6f07f306d~tplv-goo7wpa0wc-image.image) </span>

<div style="text-align: center">
(Configured with image\-text vectorization model for direct multimodal retrieval)</div>


An Exploration Guide is also available on the **Get Started** page to help you explore the VikingDB vector database in more depth:


* **Quick Start:**  Learn how to start using and quickly create your vector database.

* **Best Practices:**  Learn best practices for vector databases in high\-frequency scenarios such as multimodal search and multimodal annotation to help you find methods that fit your use case.

* **FAQ:**  Find answers to common questions, along with solutions and suggestions.

* **API Reference:**  Review detailed API documentation, including sample code and integration guides, to help you develop efficiently.
