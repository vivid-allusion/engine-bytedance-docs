---
title: "Search Experience Page Settings"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Search_Experience_Page_Settings"
---

To enhance the user experience of your search application, you can customize how results are presented on the search experience page. This guide provides instructions on how to configure the display of hierarchical media content, customize the information fields on result cards, and fine\-tune image search logic with custom commands. These display\-only settings allow you to tailor the search interface to your specific business needs without altering API behavior.

<span id="767d301a"></span>
# Display Media Content Hierarchy

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Scope</div>


<div data-tips="true" data-tips-type="default">This configuration only displays when applying associated video datasets.</div>


Video datasets support storing parent\-child hierarchical content, allowing the creation of series (such as a season of a TV show) and individual episodes (such as one episode of a TV show) with parent\-child relationships within the dataset. During search, depending on your platform's business strategy, you may want the search results to display both series and episodes side by side as the same\-level content; or only show parent\-level content (for example, a video platform's search results only return TV seasons, movies, and short videos, but not individual TV episodes).

The search experience configuration includes an option to display multi\-level content, allowing precise control over how content with inherent hierarchical structures (such as TV series and episodes) is returned in search results, simulating different business scenarios.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4912990336734413b53554cc0d6b2a18" width="2674px" /></div>


&nbsp;

**Configurable options include:** 


* **Display parent\-level content only:**  When a user's search query matches a child\-level media item (such as a specific episode), the search results will aggregate and display only the corresponding parent\-level media information. For example, if a user searches for an episode of a TV series, the search results will return only the overall entry of the series, without listing the episode separately. This applies to scenarios where you want to simplify the result list and avoid redundant information, especially when users are more interested in the entire series rather than specific subsets.

   * When calling the search API, you can use conditional filtering to achieve this behavior:

   ```JSON
   {
           "op": "must",
           "field": "parent_content_id",
           "conds": [
                   ""
           ]
   }
   ```
   


For detailed instructions on using the filter operator, see: [AI Search: Filter](https://docs.byteplus.com/docs/393/AI_search_filter)


* **Show all results:**  When a user's search query matches a child\-level media item, the search results will display both the parent\-level media information and the specific child\-level media information. For example, if a user searches for an episode of a TV series, the search results will include both the overall series entry and the specific episode entry. This is suitable for scenarios where you want to provide more comprehensive information, allowing users to directly locate specific subsets from the search results.


<span id="ff5707de"></span>
# Configure search result card display

This configuration area determines which information fields from the source dataset are displayed for each result in the search results list. By configuring properly, you can customize the presentation cards of search results to highlight key information and help users quickly assess relevance. This configuration usually allows independent settings for **each dataset** associated with the application.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/77569bdc63b9488c80125b6778866a7d" width="510px" /></div>


&nbsp;

The **Title ** field is **mandatory**; it defines the core identifying text of each search result (such as product name or video title). Additionally, to enrich the presentation, you can **optionally** configure the **Image ** field (must specify the data column containing image links) and **Description ** text field (used to display summaries, descriptions, or other supplementary information), providing users with a more comprehensive and intuitive search experience. Configurable display items differ by dataset type. See the table below for the detailed configurations for each data type.

<span id="33d10952"></span>
## **Display configuration items for graphic and text datasets:** 


|**Configuration** |**Field** |**Required** |**Screenshot** |**Description** |
|---|---|---|---|---|
|Search results display |Title  |Yes |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8cb01c6655c14d28b54ad9fb83bc6fdf) </span><br><br> |Which field to use for the title when displaying search results<br><br>Choose from string fields |
||Image  |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cbe4e01969d54420acbfe14de29a30a8) </span><br><br> |Which field to use for the image when displaying search results<br><br>Choose from **fields with the image link attribute** |
||Description  |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d2dd2bfddffe495097cd0a7c7267fd8d) </span><br><br> |Display description text in search results<br><br>Choose from string fields |


<span id="3dbb3eef"></span>
## **Display configuration items for video datasets:** 


|**Configuration **  |**Field** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Search result display |Title |Yes |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0dd2e505eee74f509655e060de1c2c87) </span><br><br> |Which field to use for the title when displaying search results<br><br>can be selected from string fields |
||Image |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4b1a392346b64f42a8c0c5fa02c0524e) </span><br><br> |Which field to use for the image when displaying search results<br><br>can be selected from **fields with image link attributes** |
||Description |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fdf5fb1e1f45422daa39e0220dd52afb) </span><br><br> |Show description text when displaying search results<br><br>Can be selected from the String field |
||Redirect link |No |No redirect link configured:<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/75c863bf14bb4c1394adcd6e3fc80aed) </span><br><br>Redirect link configured:<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/83f3159bf074418f967f9e302494c6bd) </span><br><br> |A redirect link for the media content. Clicking it navigates to the linked address<br><br>Can be selected from the String field |
||Tags |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4adaee6466dd4169aaf0d8e10fa51102) </span><br><br> |Field displaying the media content's tags<br><br>Selectable from Array<string\> fields |
||Release time |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/83d7f8eb56af4655a020aaca5ae9def6) </span><br><br> |Display the release time of the media content<br><br>Selectable from String field |
||Other metadata |No |&nbsp;<br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8daa2e81ff994e4b816d6bc2518f4829) </span><br><br> |Display other metadata of the media content<br><br>Selectable from String field |


<span id="3b2889ef"></span>
# Test image search instructions

In applications associated with image datasets, when using **Search by image**, you can customize image search instructions to **fine\-tune the matching logic between your query image and the images in the database**, thereby improving search result accuracy. These instructions essentially provide the system with more precise guidance, helping it better understand and compare image features to achieve better relevance in search results.

**The operation button for this feature only appears when your dataset includes fields configured with "Searchable (Image)"** 

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2a41c4b6272a4bd5ae96bb9b2e32625e" width="277px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f22708d90cbd4b939251481ba45ecb7b" width="274px" /></div>


&nbsp;

By default, the system operates in an **instruction\-free** state when performing image\-to\-image search, meaning no specific enhanced matching logic is preset.

To achieve better image search results in specific scenarios, you can add custom **image search instructions**. These instructions guide the system to focus more on certain specific features or aspects of the image for matching, effectively improving the accuracy and relevance of retrieval results.

To help you better understand and use this feature, we have summarized some best practice instructions based on internal testing and real application scenarios for your reference.

```Plain Text
Search similar images: Retrieve similar images based on the overall content of the image, rather than focusing only on local information within the image.
Search identical images: Find images that are exactly the same as this one. They may have been digitally edited, including scaling, cropping, or watermarking; please ignore these modifications.
Search same products: Find images of the exact same product appearing in this image, ignoring the background and human subjects.
```


You can pass corresponding instructions using the **image_query_instruction** field when calling the search interface, see [Use case 2:   Image search](https://docs.byteplus.com/docs/393/92223#e82a8266).
