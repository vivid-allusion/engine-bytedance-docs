---
title: "Image & Text Item Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Introduction_Image_Text_Dataset"
---

The Image & Text Dataset is a specialized data structure for integrating content like products, news, or design assets into an AI\-powered search, recommendation, and Q&A system. This document details the data format requirements for this dataset type, covering flexible schema definitions, image import methods (URL or Base64), image specifications, and the use of reserved field attributes to optimize multimodal understanding and search performance. This dataset type allows you to upload data containing images and corresponding text descriptions. The system automatically invokes multimodal pre\-processing and understanding capabilities to deeply analyse visual information and textual semantics, subsequently indexing the content.

&nbsp;

Image and Text Search is applicable for the following data types:


* **Product Data:**  Each entry represents a product (SKU or SPU, depending on the product level you wish to display to users in search and recommendation). This can include product ID, name, description, specifications, price, and image information such as detailed product photos or thumbnails.

* **Image and Text Design Assets:**  Each entry represents a commercial asset. This can include the asset ID, name, large thumbnails (imported via URL), description, keywords and other information.

* **Graphic and Text News Articles:**  Each entry represents a news article. This can include the ID, title, body text, and any accompanying images.

* **Other Structured Data:**  Any other data formats that combine image and text information


&nbsp;

<span id="be4cd2ab"></span>
# **Image & Text Data Format**

Our Image & Text Dataset supports a flexible schema definition. We **do not restrict data field names**; you can customise the JSON structure (field names and types) to upload any image and text information that describes the searchable content. When creating an AI Search application via the console, you can create a dataset and upload one or more JSON records for schema parsing. The console's Large Language Model (LLM) data parsing feature can automatically identify the field structure, names, special attributes, and dataset content summaries for you.

&nbsp;

**Field Names:**  Must start with a letter and can only contain letters, numbers, and underscores. Field names must not exceed 32 characters.

**Field Type**: Supports the following data types from the JSON schema \-


* String (Array<String\>)

* Integer (Array<Integer\>): supports both Int64 and Int32

* Float (Array<Float\>)

* Boolean

* Object (Array<Object\>): supports nested objects, with a maximum of three layers of nesting


&nbsp;

Below is an example of Image & Text data:

```JSON
{
    "product_id": "P10092385",
    "title": "Ultra-thin laptop",
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


<span id="dc911407"></span>
# Transferring Image Data

String or Array<String\> type is supported to pass image data in Image & Text datasets. Each data record supports multiple fields to distinguish between different image types and their intended purposes.

&nbsp;

> Example: In an E\-Commerce platform scenario, a single product record may contain multiple categories of images, such as the display thumbnail for the product list page, the top carousel images, and product detail images.


> * **Display** ** Thumbnails** **: ** Usually shown in search results or category pages; these typically feature the complete appearance of the product.

> * **Top Carousel Images:**  Used at the top of a product detail page to showcase the item from multiple angles.

> * **Product Detail Images:**  Often long images containing text descriptions of specifications and close\-up details. 


> The first two are better suited for **visual search features**, whilst the detail images are better processed by **Large Language Models (LLMs)**  to assist in shopping assistant Q&A.


&nbsp;

**Transferring fields containing a single image:**  

Use a **String** type field to provide a single image. This is suitable for providing asset thumbnails in commercial image search scenarios or the main display image in product data.

**Transferring fields containing multiple images:**  

Use an **Array** type field to provide multiple images. This is suitable for uploading product detail images (containing graphic descriptions) or top carousel images (showing the product from various angles).

&nbsp;

<span id="f9504ebd"></span>
## Image Import Methods

**Import images using URL download links**

You can import images by providing a publicly accessible distribution download link (String) in the field. Once the data is imported, the AI Search Engine will download the images for subsequent image understanding and multimodal data indexing. Please ensure the links are publicly accessible.

&nbsp;

**Import images using Base64 (not recommended)** 

If your database stores raw image files but does not have an image distribution service, you can provide Base64\-encoded image files directly in the field.

To ensure the Base64 encoding is parsed correctly, please ensure that it follows the standard format, consisting of both **Data Header (Data URI Scheme)**  and **Base64\-encoded body**:


|**Component** |**Format Requirements** |**Description** |
|---|---|---|
|Data Header Prefix |Fixed as `data:` |Identifies the string as being in Data URI format; it must not be omitted or modified. |
|MIME Type |Must strictly match the actual image format. |Used by the server to identify the image type; do not use arbitrary values (e.g., do not specify the MIME type for PNG for a JPG image). |
|Separator |Fixed as `;base64,` |Connects the MIME type to the Base64\-encoded body; the semicolon, "base64", and comma must not be omitted or replaced. |
|Base64\-Encoded Body |A Base64\-encoded string complying with the RFC 4648 standard. |Generated directly from the binary data of the image file. **Must not contain spaces, line breaks, or special characters**; it must be a continuous ASCII string. |



<Tabs>
<Tab zoneid="bdv09wucAr" title="Format">
<TabTitle>Format</TabTitle>

```JSON
data:<MIME type>;base64,<Base64-encoded string>
```



</Tab>
<Tab zoneid="msqgqzNeaT" title="JPEG image">
<TabTitle>JPEG image</TabTitle>

```JSON
data:image/jpeg;base64,<Base64-encoded string>
```



</Tab>
<Tab zoneid="V7kPhLamEs" title="PNG image">
<TabTitle>PNG image</TabTitle>

```JSON
data:image/png;base64,<Base64-encoded string>
```



</Tab>
<Tab zoneid="ERTnBRBcOd" title="WebP image">
<TabTitle>WebP image</TabTitle>

```JSON
data:image/webp;base64,<Base64-encoded body>
```



</Tab>
</Tabs>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Transferring images using Base64 will result in larger request and response bodies for the data import interface, which affects the timeliness of data uploads and queries. It is recommended to use image URLs instead.</div>


<span id="d246f9d6"></span>
## Image Format Specifications

Please ensure that the image formats meet the following requirements before importing data:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Specifications</div>



1. <div data-tips="true" data-tips-type="default"><strong>Supported Formats:</strong> jpeg, png, webp, bmp, tiff, ico, dib, icns, sgi, jpeg2000</div>


   <div data-tips="true" data-tips-type="default">For tiff, sgi, icns, jpeg2000 formats, ensure metadata alignment by correctly setting file metadata in object storage; otherwise, parsing will fail.   </div>
   

   <div data-tips="true" data-tips-type="default"><strong>Animated images (.gif) and any vector format files (such as .svg, .eps, .ai) are not supported</strong>. If your source images contain vector graphics, please convert them to bitmap thumbnails before uploading.   </div>
   

2. <div data-tips="true" data-tips-type="default"><strong>Aspect Ratio (width/height):</strong> within the range [1/100, 100]</div>


   <div data-tips="true" data-tips-type="default">For optimal performance, the aspect ratio should be within the range [1/10, 10]. Extreme image ratios may affect the performance of large models in image understanding and feature search matching.   </div>
   

3. <div data-tips="true" data-tips-type="default"><strong>Edge Length: </strong>must be within [10, 6000] px</div>


   <div data-tips="true" data-tips-type="default">The shorter side must be greater than 10 px and the longer side must be less than 6000 px, or image processing will not be possible.    </div>
   

   <div data-tips="true" data-tips-type="default"><strong>For optimal model processing results, it is suggested to keep the image edge length within [300, 3600] px</strong>. Resolutions that are too low may result in loss of detail, whilst excessively high resolutions increase processing time without significantly improving recognition accuracy.   </div>
   


<span id="bb64f3ff"></span>
# Review Reserved Field Attributes

The "attributes" of a field are a set of reserved field configurations which you will be guided to set up during dataset creation. Fields configured with specific attributes will undergo specific processing and will be used in content understanding and ranking strategies during search, recommendation and conversation. When preparing your data, you can pre\-determine whether your database contains the following information. We recommend passing these attributes in the specified format to maximise the utility of Viking AI Search’s intelligent data processing and online strategies.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cc27cc5744654359ad40f17e4a2093c2) </span>


|**Attribute** |**Mandatory?**  |**Supported Field Type(s)**  |**Attribute Description** |
|---|---|---|---|
|**Item ID (unique identifier)**  |Mandatory |String |The unique identifier for a single piece of data, which is the primary key. In search and recommendation scenarios, a different item ID represents a different "candidate".<br><br>**A data schema must contain exactly one unique identifier.** <br><br><br>* Supports upload as a **String** type.<br><br>* Only an outermost, non\-nested field can be used as the unique identifier. |
|**Title** |Optional |String |A field storing the title or name of the item. Applicable to product names, content or article titles, etc.<br><br>It is recommended to upload this information, as it serves as core semantic information for search and personalised recommendations. |
|**Image URL**<br><br> |Optional |String, Array<String\> |This field stores image URLs. After uploading data, the system automatically pulls images and extracts visual features for multimodal understanding. To use URLs for multimodal search, the field must be marked as an Image URL attribute. <br><br>Supports both single string and string array fields. |
|**Image Base64** |Optional |String, Array<String\> |This field stores image Base64 strings (or a list of strings). |
|**Category** |Optional |String |The field stores the category or classification to which the item belongs.<br><br>It is recommended to upload this attribute in product data. Category information serves as a core data feature for search and recommendation, and the conversational assistant uses it to intelligently filter categories based on user queries during the decision\-making process.<br><br>Multiple classification attributes can be uploaded. If your product belongs to multiple categories (e.g., Level 1, Level 2 categories), you can use different fields to upload them. |
|**Publish Time (Date/Time Format)**  |Optional |String |Stores the publish or listing time of the item in date\-time format, used for sorting by newness in search and recommendation. <br><br>Supports formats of:<br><br><br>* Standard ISO date\-time strings (`YYYY-MM-DDThh:mm:ss+08:00`).<br><br>* Non\-standard date\-time strings (`YYYY-MM-DD hh:mm:ss` or date\-only strings). The system will automatically convert these to standard format. |
|**Publish Time (UNIX Timestamp, Seconds)**  |Optional |Int64 |Item publish time represented by a standard 10\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |
|**Publish Time (UNIX Timestamp, Milliseconds)**  |Optional |Int64 |Item publish time represented by a standard 13\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |
|**Geographical Location \- Longitude** |Optional |Float or String |Longitude and latitude information used to identify the location of an item. Supports configurations for the following field types:<br><br><br>* Single JSON object: `"location":{"lat":"12.709","long":"30.281"}`.<br><br>* JSON object array for multiple locations: `"location":[{"lat":"12.709","long":"30.281"},{...}]`. System will select the maximum or minimum distance for calculations based on strategies.<br><br><br>&nbsp;<br><br>Supports both Float or String representation (e.g., `"30.281"` or `30.281`). |
|**Geographical Location \- Latitude** |Optional |Float or String ||


<span id="19433fda"></span>
# Sample Data

The following is an example of an image\-text data entry:

```JSON
{
    "product_id": "P10092385",
    "title": "Ultra-thin laptop",
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



|**Sample Field Name** |**Data Type** |**Field Attribute** |**Field Meaning** |
|---|---|---|---|
|product_id |*String* |Unique identifier |Product's unique ID |
|title |*String* | |Product title |
|images |*Object* | |Image information included in the product |
|   * images.primary |*String* |Image URL |Product main image |
|   * images.gallery |*Array<String\>*  |Image URL |Product detail carousel, containing images of the product's main information |
|price |*Object* | |Product price information |
|   * price.current |*Float* | |Product current displayed price |
|   * price.original |*Float* | |Product original price |
|   * price.discount_percentage |*Float* | |Product discount percentage |
|specs |*Object* | |Product specifications |
|processor |*String* | |Processor Model |
|memory |*String* | |Memory Size |
|storage |*String* | |Product storage type and space |
