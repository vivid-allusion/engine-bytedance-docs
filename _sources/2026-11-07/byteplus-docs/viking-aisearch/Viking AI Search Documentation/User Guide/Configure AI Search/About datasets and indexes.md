---
title: "About datasets and indexes"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/About_datasets_and_indexes"
---

<span id="7a0d983e"></span>
# Building indexes in the app

To achieve fast and high\-performance retrieval, you must properly configure your dataset fields to build an effective index.

This guide explains what an index is and provides detailed instructions and best practices for setting field usages, such as Searchable, Filterable, and Autocomplete, to optimize search accuracy and relevance.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b8122fa73a584178bef4c88bdb7ff1c2) </span>

<span id="cff6b112"></span>
# Preparation: Dataset field configuration

Index configuration is critical for search accuracy and relevance coverage. When associating or creating a dataset in the app, you will see the dataset field configuration interface where you can set or adjust the field strategies for various search functions.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dfb7e6cdda2c40b08a7f839e205976b2) </span>


* **Field name:**  the name of the field automatically parsed from sample data. Once the field name is set, it cannot be modified in the app or dataset management.

* **Field Data type:**  the type of the field automatically detected from sample data. If the sample data contains fields with all null values, the platform cannot automatically infer the type; you must manually specify the field type to save and apply the configuration. Once a field type is configured, it cannot be modified in the app or dataset management.

* **Field Description:**  The meaning of the value stored in the field automatically interpreted by the large model based on sample data. You can review, supplement, and modify it further.

* **Field Attributes:**  Special field attribute tags used to mark fields storing specific information in the dataset (title, timestamp, image content, etc.) for special indexing processing. See details at [Image & Text Item Dataset](https://docs.byteplus.com/docs/393/Introduction_Image_Text_Dataset)[Video Dataset](https://docs.byteplus.com/docs/393/92244). Once a field attribute is configured, it cannot be modified in the app or dataset management.

* **Field Usage:**  Configure the indexing purpose of the field. When the same dataset is linked to different apps, you can configure different field usages. Field usage affects indexing strategy and search performance, so please check the configuration carefully.



|**Purpose** |**Parameter description** |
|---|---|
|**Searchable (Text)**  |The semantic information in the field will be included in the item's semantic representation for retrieval.<br><br>It is recommended to select key searchable information such as product name, key features, and categories. If your scenario involves image search, select the image (marked as image attribute) field as a search matching field. |
|**Searchable (Image)**  |Selecting this option enables images in this field to support "**Image\-to\-Image Search**".<br><br>You can **optionally enable** this feature to precisely control which types of images respond to users' image search requests. You can decide based on the specific application scenario: for all image link fields in the data that meet the conditions (such as "product main image," "user avatar," "scene photo," etc.)<br><br>**Note**: this field must be marked as "**searchable**" and its **field attribute** must be "**image link".**  |
|**Filterable** |When calling search and conversation APIs, selected fields can be used to filter search results.<br><br>It supports numeric fields (Float, Int), boolean (Bool), string (String), and string list (Array<String\>).<br><br>It is recommended to select numeric or enumerating fields such as category and price. |
|**Autocomplete** |Selected field values in each record serve as suggestion terms for indexing to be used by the **Autocomplete** API.<br><br>It supports string and string list data formats. |


After importing a data sample, the platform uses a large model for intelligent data understanding, automatically determining field information based on the sample data's field names and values.

<span id="df28589a"></span>
# Best practices for data configuration

<span id="ae3855b1"></span>
## Write concise field descriptions

Field descriptions briefly introduce the content stored in each field. During search matching, the model semantically represents both the field description and the field's value together. When configuring fields for search, to enable the model to accurately understand and match the data content, please check the field description interpreted by the large model. If the model's understanding is incorrect, modify it before completing the configuration.

Field descriptions should be concise and summarizing. It is recommended to keep them within 10 characters, accurately describing the essential characteristics of the field content, for example:

```JSON
{
    "product_id": "P10092385",
    "title": "Ultra-thin Laptop",
    "images": {
      "primary": "https://example.com/images/laptop_main.jpg",
      "gallery": [
        "https://example.com/images/laptop_angle1.jpg",
        "https://example.com/images/laptop_angle2.jpg"
      ]
    },
    "price": {
      "current": 4999,
      "original": 5899,
      "discount_percentage": 15
    },
    "specs": {
      "processor": "Intel i7",
      "memory": "16GB",
      "storage": "512GB SSD"
    }
  }
```



|**example field** |**field type** |**Field meaning** |
|---|---|---|
|product_id |String |Unique product ID |
|title |String |Product name |
|images |Object |Image content |
|    images.primary |String |Main product image |
|    images.gallery |Array<String\> |Product detail page content |
|price |Object |Price information |
|    price.current |Float |Current price |
|    price.original |Float |Original price |
|    price.discount_percentage |Float |Product discount (percentage) |
|specs |Object |Product parameters |
|    specs.processor |String |Processor |
|    specs.memory |String |Memory |
|    specs.storage |String |Computer storage space and media |


<span id="3f597c4f"></span>
## Select fields accurately for search

Fields used for search are content fields matched with user input (image or text query). To make information in item data searchable by users, set these fields as "Searchable".

You may configure according to the following recommendations


|**field purpose** |**supported fields** |**configuration guide** |
|---|---|---|
|**Searchable (Text)**  |all fields.<br><br>includes text fields, image fields (fields with "image link" or "image base64" attributes), and other numeric and boolean fields |* **Product data:**  product names, descriptions, key attributes, category tags, and other information that directly reflects core product features. Product detail images can be set for text search to allow the model to read and search\-match the descriptions within the images.<br><br>* **Content data:**  fields containing core text information of the content, such as titles, body text, tags, and categories.<br><br>* **Image asset library:**  setting asset titles, keywords, and descriptions as "**Searchable (Text)** " fields supplements essential operational and editorial information for image assets.<br><br>* **Video platform:**  The video URL field in the video platform is selected by default for text search. After the audio\-visual text information in the video file is interpreted and represented, it can be used for direct video search or for video content Q&A in the Conversation Experience. |
|**Searchable (Image)**  |Image fields (fields marked with "image link" or "image base64" attributes) |Image search means "Image\-to\-Image Search" where users upload a picture to find data with similar or identical image features.<br><br>Recommended configuration:<br><br><br>* **Product data:**  The product's appearance images (usually thumbnail images on listing pages or top carousel images) can be set "**Searchable (Image)** " to enable e\-commerce image search.<br><br>* **Content data:**  Content images can be set "**Searchable (Image)** " to enable search by image.<br><br>* **Image asset library:**  Asset thumbnails need to be set "**Searchable (Image)** " to achieve similar style asset image search. |


<span id="34496c1c"></span>
## Select fields for filtering

Fields that are selected as "**Filterable"**  are stored in the index as preset filters and can be used to pre\-filter search results during search invocation. Key business data and tags (such as date and time, price, item status, category) are recommended to be configured as filterable fields.

The following contents can be configured for filterable fields:


|**Field data type** |**Configuration guide** |
|---|---|
|Boolean fields |Typically used for filtering, such as fields indicating listing status, which can serve as filters in real\-time business rule filtering. |
|Text fields (String) |It is recommended to configure enumer\-type fields for filtering, typically categories and classifications of products and content.<br><br>Note: Fields marked as "category/classification" in the data are automatically set as **Filterable ** information |
|Numeric fields (Float, Int32, Int64) |Fields such as price and timestamps are recommended for filtering, typically used in scenarios like product price ranges and time intervals. |


&nbsp;

&nbsp;

&nbsp;
