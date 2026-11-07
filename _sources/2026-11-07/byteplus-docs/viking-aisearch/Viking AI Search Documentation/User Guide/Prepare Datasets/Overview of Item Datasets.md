---
title: "Overview of Item Datasets"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Overview_of_Item_Datasets"
---

**Item Data** (also known as candidate data) is the most fundamental data source for AI search and recommendations. Viking AI Search uses "Item Datasets" to define, upload, and manage item data. Once configured, the item dataset will undergo index building within the application and be applied to search and recommendation tasks.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/96d4664fe24f4445abd8a53de58c38b8" width="421px" /></div>


An item dataset is a structured table. Each record has a unique ID and a set of fields that describe the item. Item data is represented as a nested JSON object. You can structure products, content assets, news articles, videos, and other content as field\-value pairs, and then import the data for processing and storage.

Viking AI Search supports the following item dataset types. Select a type based on the content and structure of your candidate data.


|**Dataset type** |**Schema** |**Supported content** |**Recommended use cases** |**Documentation** |
|---|---|---|---|---|
|Image\-and\-text item dataset |Custom fields; no fixed schema |* Text fields<br><br>* Image fields uploaded by URL or Base64 |* Product data<br><br>* Articles and blog posts<br><br>* News content<br><br>* Commercial image assets |[Image & Text Item Dataset](https://docs.byteplus.com/docs/viking-aisearch/Introduction_Image_Text_Dataset) |
|Video dataset |Predefined fields for required information, such as the item ID, series indicator, episode number, and video download URL |* Text fields<br><br>* Image fields for video covers or posters<br><br>* Video fields uploaded by URL |* Movies and TV series<br><br>* Video courses<br><br>* Short\-form videos |[Video Dataset](https://docs.byteplus.com/docs/viking-aisearch/Introduction_to_Video_Dataset) |
|Multimodal dataset |Custom fields with no fixed schema; predefined templates are available for General, E\-commerce, Content, and Long\-form Video scenarios |* Text fields<br><br>* Image URL fields labeled Multimodal<br><br>* Video URL fields labeled Multimodal |Records that contain both images and videos, such as products with primary images, detail images, and product videos; image\-and\-text or short\-video posts; and long\-form video series with cover images and clips |[Multimodal Dataset](https://docs.byteplus.com/docs/viking-aisearch/117710) |


Before creating an application on the platform, you need to prepare an item dataset based on the content characteristics of your search and recommendation candidate data. You can refer to the table below to select the appropriate dataset type:


|**Dataset Type** |**Data Table Definition** |**Supported Content** |**Applicable Content Genres** |
|---|---|---|---|
|Image & Text Item Dataset |Flexible fields; no fixed data schema. |* Text fields<br><br>* Image field (supports image URL and Base64 input) |* Product data<br><br>* Text and image content, such as articles and blog posts<br><br>* News content<br><br>* Commercial image asset data |
|Video Dataset |Contains pre\-set fields to store essential IDs, video series indicators, video sequence numbers, and download links. |* Text field<br><br>* Image field (video cover or poster for display)<br><br>* Video file field (supports video file URL input) |* Film and TV data<br><br>* Video courses<br><br>* Short video data |
