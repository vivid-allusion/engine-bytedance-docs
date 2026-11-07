---
title: "Integrate AI Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Integrate_AI_Search"
---

After configuring and testing the search strategy on the experience configuration page, you can apply the configuration to the online search engine through the console and then integrate the configured AI search scenario into your platform via the API.

<span id="82f9cf52"></span>
# Apply AI Search Configuration

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b02e13dd266f4006b5208ca59f43f5c6) </span>

&nbsp;

On the right configuration panel of **Application \> Experience Center \> Search**, click  **[Sync Changes to API]**  to activate the configuration for the official API call to the online engine. After activation, you can start integrating the search API and incorporate AI search capabilities into your platform.

<span id="a4ec1bf4"></span>
# Calling the Search API

Before calling the Search API, go to the [Cloud Search console](https://console.volcengine.com/es), navigate to AI Search \> open the target service \> API Key, then create or view an available API key and replace <API key\> in the example with it. For details, see [Create API Key](https://www.volcengine.com/docs/6465/1359479?lang=en) and [View API key](https://www.volcengine.com/docs/6465/1359481?lang=en). Please keep your API key secure and do not expose it in frontend code, public repositories, or other public environments.

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{configuration_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API_KEY>' \
  -d '{
    "query": {
      "text": "query text string",
      "image_url": "image file",
      "image_query_instruction": "Image Search Instructions"
    },
    "dataset_id": "target dataset id",
    "page_number": search page number,
    "page_size": number of search results per page,
    "user": {
      "user_id": "user ID"
    },
    "context": {
      "location": {
        "latitude": "12.1243",
        "longitude": "-012.1223"
      }
    },
    "filter": "search filter conditions",
    "sort_by": "specified sort field",
    "sort_order": "asc"
  }'

```



|**Parameter** |**Description** |
|---|---|
|`application_id` |**Required**<br><br>ID of the application created |
|`query.text` |**Required (if query.image_url is not provided)** <br><br>User input query text passed as a string |
|`query.image_url` |**Required (if query.text is not provided)** <br><br>User\-uploaded image for image search, passed as a URL string or base64 string. Can be used in conjunction with `query.text`. |
|`page_number` |Page number for search, used for list pagination, required, starting from 1 |
|`page_size` |Search results count per page, required |
|`user.user_id` |User ID corresponding to this call, optional but recommended |
|`context.location` |Upload user location as a JSON object. <br><br>For example:`{"latitude": "12.1243","longitude": "-012.1223"}` |
|`filter` |Filter conditions in JSON format to filter retrieved items during a search; ensure filtered fields are configured as filterable in the app before use. <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">For how to pass filters in API parameters, see: <a href="https://docs.byteplus.com/docs/393/AI_search_filter"> </a></div><br> |
|`sort_by`<br><br> |Specify a dataset field to sort the search list.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">For more details, see: <a href="https://docs.byteplus.com/docs/393/92235">AI Search: Search Results Sorting</a></div><br> |
|`sort_order` ||
|`dataset_id` |**Required**<br><br>Your created dataset ID  |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">API Reference</div>


<div data-tips="true" data-tips-type="default">For complete API usage instructions, see: <a href="https://www.volcengine.com/docs/85296/1544974">API Reference \> Search</a></div>



---



<span id="7d71b2f0"></span>
# Use case 1:  Text search

When the user enters text in the search box, pass the user's input text to the `query.text` field.

<span id="4f4084c6"></span>
## Required Parameters

<span id="a9fbf127"></span>
### query.text


|**Data Type** |**Description** |
|---|---|
|String |The query text entered by the user |


<span id="d98ed222"></span>
## Sample API Call

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/{application_id}/search/{configuration_id}' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "query": {
        "text": "sneakers suitable for mountain climbing in rainy season"
     },
    "user_id":"<user_id>",
    "context":{
        "location":{
            "latitude": "12.1243",
            "longitude": "-012.1223"
        }
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 50
}'
```


&nbsp;


---



<span id="e82a8266"></span>
# Use case 2:   Image search

You can pass a base64\-encoded image file or URL in query.image for image search.

<span id="a5789663"></span>
## Required Parameters

<span id="c0fe1812"></span>
### query.image_url


|**Data Type** |**Description** |
|---|---|
|String |Image content input by the user, passed as a web\-accessible image URL or base64 format. |


When uploading image data, you must upload image files that meet the format and restrictions described below for Viking AI search to be able to process the image.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">The input image must meet the following requirements:</div>



1. <div data-tips="true" data-tips-type="default"><strong>Supported formats:</strong> jpeg, png, webp, bmp, tiff, ico, dib, icns, sgi, jpeg2000. For tiff, sgi, icns, and jpeg2000 formats, the image must align with metadata. For example, properly set the file metadata in object storage; otherwise, parsing will fail.</div>


2. <div data-tips="true" data-tips-type="default"><strong>Aspect ratio (width/height):</strong> within the range [1/100, 100].</div>


3. <div data-tips="true" data-tips-type="default"><strong>Side length:</strong> [10, 6000] px; the shorter side must be greater than 10 px, and the longer side must be less than 6000 px.</div>



<div data-tips="true" data-tips-type="default"><strong>The optimal image side length is between 300 and 3600 pixels, and the file size should be under 300 KB. Larger images will lead to longer response times for the search API.</strong></div>


&nbsp;

If using base64 encoding, ensure that it follows the standard format, containing both **data header (Data URI Scheme)**  and **Base64 encoded body**:


<Tabs>
<Tab zoneid="XRIKqIMUSj" title="Format">
<TabTitle>Format</TabTitle>

```Plain Text
data:<MIME-type>;base64,<Base64-encoded-string>
```



</Tab>
<Tab zoneid="wIDoWIrrfW" title="JPEG image">
<TabTitle>JPEG image</TabTitle>

```Plain Text
data:image/jpeg;base64,<Base64-encoded-string>
```



</Tab>
<Tab zoneid="FlcpBmPvdc" title="PNG image">
<TabTitle>PNG image</TabTitle>

```Plain Text
data:image/png;base64,<Base64-encoded-string>
```



</Tab>
<Tab zoneid="zHYDyicC1X" title="WebP image">
<TabTitle>WebP image</TabTitle>

```Plain Text
data:image/webp;base64,<Base64-encoded-content>
```



</Tab>
</Tabs>


<span id="94010078"></span>
### query.image_query_instruction


|**Data Type** |**Description** |
|---|---|
|String |A text instruction for image search, which guides the model on how to match the query image with candidate images. A fixed instruction can be used in specific image search scenarios to improve retrieval accuracy. |


Validated image search commands include identical image search, similar product search, and similar material search. Below are some best practice commands summarized from our internal tests and real\-world scenarios for your reference. 

<span id="ae9c77cb"></span>
#### **Best Practices**


<Tabs>
<Tab zoneid="NKY8BizZfv" title="Search Similar Images">
<TabTitle>Search Similar Images</TabTitle>

```Plain Text
Search similar images: Retrieve similar images based on the overall content of the picture, rather than focusing only on local information within the image.
```



</Tab>
<Tab zoneid="MQleKc10cP" title="Search Identical Images">
<TabTitle>Search Identical Images</TabTitle>

```Plain Text
Search identical images: Find images that are exactly the same as this one. They may have been modified with image editing software (for example, by scaling, cropping, or watermarking); please ignore these modifications.
```



</Tab>
<Tab zoneid="LD7XroT6Gy" title="Find exact product">
<TabTitle>Find exact product</TabTitle>

```Plain Text
Find Exact Product: Find images of the exact same product in this image, ignoring the background and human subjects.
```



</Tab>
</Tabs>


<span id="44d82c72"></span>
### Sample API Call

**Scenario: E\-commerce product search via image upload**

```Bash
curl -X POST 'https://aisearch.cn-beijing.volces.com/api/v1/application/your_app_id/search' \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer <API Key>' \
  -d '{
    "query": {
        "image_url":<image in URL format>,
        "image_query_instruction":"Find images of the exact same product in this image, ignoring the background and human subjects."
    },
    "dataset_id": "<your_dataset_id>",
    "page_number": 1,
    "page_size": 50
}'
```
