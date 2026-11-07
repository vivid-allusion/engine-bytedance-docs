---
title: "Multimodal Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Multimodal_Dataset"
---

A multimodal dataset is the recommended option when your candidate data—such as products, content posts, or long\-form video series—contains both images and videos, and you want to support image\-and\-text retrieval, video retrieval, image\-to\-item or text\-to\-item search, multimodal recommendations, and intelligent Q&A in the same application. Viking AI Search automatically processes and understands visual, video, and textual information, and builds a unified index for all modalities.

<span id="87a798e1"></span>
### Supported content scenarios


* **Product data:**  Each record represents a product SKU or SPU and can include primary images, detail images, and a product introduction video. Typical scenarios include e\-commerce shopping assistance and searching for products by image or video.

* **Content and social posts:**  Each record represents an image\-and\-text post or short\-video post and can include a cover image, inline images, and a short video. Typical scenarios include unified retrieval and personalized recommendations in content communities.

* **Long\-form videos and series:**  Each record can include a cover image, still images, and video clips. Typical scenarios include semantic search and companion Q&A on video platforms.

* **Other structured data:**  Any structured record that contains both image and video information.


<span id="8b52a9a7"></span>
### Content templates

Unlike an image\-and\-text dataset, a multimodal dataset requires you to select a **Content Type** when creating the dataset. Each content template provides recommended field attributes and search and recommendation settings to help you complete the configuration more efficiently. The following templates are available:


|**Content type** |**Description** |
|---|---|
|General |A general\-purpose configuration for scenarios that do not fit any of the other content types. |
|E\-commerce |A template for product data. It includes recommended mappings for product ID, name, description, image and video URLs, category, price, brand, and listing time. |
|Content |A template for image\-and\-text posts and short\-video posts. |
|Long\-form Video |A template for long\-form video scenarios such as series and courses. |


<span id="da089540"></span>
### Multimodal data requirements

A multimodal dataset supports a custom schema and does not restrict field names. You can define a JSON structure, including field names and field types, to describe the content to be searched. When creating a dataset in the console, upload one or more JSON records for schema analysis. The AI\-powered data parser automatically identifies the field structure, field types, and field semantics, and generates a dataset description.


* **Field names:**  A field name must start with a letter, can contain only letters, digits, and underscores, and cannot exceed 32 characters.

* **Field types:**  Supported types are String and Array of String; Integer and Array of Integer, with Int32 and Int64 available; Float and Array of Float; Boolean; and Object and Array of Object. Objects can contain up to three levels of nesting.

* **Unique identifier:**  Each record must contain exactly one unique ID field of the String type. Map this field to the **Product ID** attribute. The unique identifier is required for retrieval.

* **Separate image and video fields:**  Store image URLs and video URLs in separate fields. A field can contain an array of URLs. For example, if a product has multiple detail images and one introduction video, use an `image_url` array and a `video_url` string or array.


<span id="4b362234"></span>
### Predefined field attributes

Field attributes are predefined configurations. When you create a dataset, the system guides you through mapping parsed fields to item attributes. Fields mapped to specific attributes receive specialized processing and are used for content understanding and ranking in search, recommendation, and conversational experiences.

In a multimodal dataset, both **Image URL** and **Video URL** are multimodal attributes. You can map multiple fields to either attribute, such as separate primary\-image and detail\-image fields.


|**Attribute** |**Required** |**Supported field types** |**Description** |
|---|---|---|---|
|Product ID (unique identifier) |Yes |String |The primary key of a record. The schema must contain exactly one unique identifier. Only a top\-level, non\-nested field can be used. |
|Product Name |No |String |The display title of the product. Providing this field is recommended because it is used as core semantic information for search and personalized recommendations. |
|Product Description |No |String |The main product description, such as material, fit, style, and applicable scenarios. |
|Image URL (Multimodal) |No |String, Array<String\> |Download URLs of product images, such as primary and detail images. The system downloads the images and extracts visual features. Multiple fields can be mapped to this attribute. |
|Video URL (Multimodal) |No |String,  Array<String\> |Download URLs of product videos, such as a product introduction video. The system downloads and performs multimodal understanding on the videos. Multiple fields can be mapped to this attribute. |
|Category |No |String |The product category. Category information is used as a core feature for search and recommendation and for intelligent filtering in conversational search. You can provide multiple category fields, such as level\-1 and level\-2 categories. |
|Keywords/Tags |No |String,  Array<String\> |Product keywords or tags used for retrieval and query completion. |
|Price |No |Float, Int |The product sale price, which can be used for price\-range filtering and sorting. |
|Brand |No |String |The product brand. |
|Listing Time |No |String, Int64 |The time when the product was released or listed. Standard date strings and UNIX timestamps are supported. This value can be used for freshness\-based ranking in search and recommendation. |


<span id="2e45ea42"></span>
### Data example

The following example shows one multimodal product record that contains both image and video fields:

```JSON
{
  "product_id": "P20231001",
  "product_name": "Lightweight Athletic Skin-Friendly Dress",
  "description": "Lightweight, skin-friendly fabric with a tailored fit for commuting and travel.",
  "image_url": [
    "https://example.com/images/dress_main.jpg",
    "https://example.com/images/dress_detail.jpg"
  ],
  "video_url": "https://example.com/videos/dress_intro.mp4",
  "product_category_tree": ["Women's Clothing", "Dresses", "Skirts"],
  "product_color": "Light Pink",
  "retail_price": 399,
  "discounted_price": 299,
  "overall_rating": 4.8
}
```


<span id="5e3faf0a"></span>
### Image data transfer

The image transfer rules are the same as those for image\-and\-text datasets. Provide publicly accessible image URLs in fields of the String or Array type. The system downloads the images and extracts visual features for multimodal understanding. Base64 input is also supported but is not recommended. Base64 input must include the data header, MIME type, and Base64\-encoded body.


* **Supported formats:**  JPEG, PNG, WebP, BMP, TIFF, ICO, DIB, ICNS, SGI, and JPEG 2000. For TIFF, SGI, ICNS, and JPEG 2000 files, make sure the file content matches its metadata.

* **Unsupported formats:**  Animated GIFs and vector formats such as SVG, EPS, and AI. Convert vector assets to bitmap thumbnails before importing them.

* **Aspect ratio:**  The width\-to\-height ratio must be within [1/100, 100]. A ratio within [1/10, 10] is recommended.

* **Dimensions:**  Each side must be between 10 px and 6,000 px. For optimal understanding quality, use dimensions between 300 px and 3,600 px.


<span id="418bec6a"></span>
### Video data transfer

Video input is an additional capability of multimodal datasets. Provide video download URLs in fields of the String or Array type, such as URLs for product introduction videos, short\-form content, or series clips. The system downloads the video files and performs multimodal understanding and indexing. After processing is complete, you can view results such as **Valid Video Duration** on the dataset details page.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">说明</div>


<div data-tips="true" data-tips-type="default">For detailed image and video limits, including resolution, duration, and file size, refer to <strong>Multimodal Data Format Requirements</strong> on the dataset creation page in the console. Before importing a full dataset, use a small sample to verify that your data meets the format requirements.</div>


&nbsp;

<span id="8e6e5716"></span>
### Invalid data handling policy

Images and videos may be unavailable because of expired URLs, unsupported formats, oversized files, or other errors. When you create a multimodal dataset, configure an **Invalid Data Handling Policy** to specify how records with invalid multimodal content are processed.


|**Policy** |**Billing** |**Processing behavior** |
|---|---|---|
|Do not process and mark as invalid data (default) |No charges |If image or video processing fails, the entire record is excluded from the index. |
|Skip invalid modalities and continue processing |Charges apply only to text and video processing |The system skips the modality that failed processing and writes the remaining processable content to the index. |


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cc59d5db84ad4a81be9dbc7c9989d74f) </span>

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d15bbcd62c414020ab0944a1bdd5f458) </span>

You can change this policy after the dataset is created. On the dataset details page, open the **Data Details** tab and click **Invalid Data Handling Policy**.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ed8ce7227a71444f94a4d6c47360fcff) </span>
