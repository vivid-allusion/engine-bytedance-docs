---
title: "Reference: Intelligent Analysis Agent OpenAPI Chart Consumption Instructions"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Reference_Intelligent_Analysis_Agent_OpenAPI_Chart_Consumption_Instructions"
---

When querying data using OpenAPI, you can configure the chart format for the query results (the `imageFormat` parameter). This article introduces how to parse and use the returned results for different types of charts.

<span id="a1e6fe02"></span>
# Background information

In the data query OpenAPI, you can set the `imageFormat` parameter to specify the chart format for the query results. Supported formats include:


|Returned chart format types |Description of returned result formats |Applicable scenarios |
|---|---|---|
|image_url |The returned value is the URL address of a static image. |**Rapid consumption on the PC side** (non\-interactive), no secondary development required. |
|lark_fragment (recommended) |Feishu\-format rich text. The returned result is in Feishu native fragment format. |**Feishu side** consumption, interactive charts are pushed via card and other message formats **interactive charts**, requiring minimal secondary development |
|ark_image_key |Feishu image key. The returned result is in Feishu static image format. |**Feishu side** consumption, static chart images are pushed via card and other message formats **static chart images (non\-interactive)** , requiring minimal secondary development |
|vchart_schema |The returned result is in the native format of vchart and vtable charts. |**PC side** consumption, **requiring more secondary development**<br><br>The returned chart is not a static image, but an **interactive** real chart, and you can also **customize** style themes or value formatting |


In the response returned after running the data query OpenAPI, the `charts` field contains the recommended chart list. Currently, up to the top 4 charts are returned, that is, the four charts most suitable for the scenario. The recommendation order is from top to bottom, with the first being the most recommended. You can adjust the number of top N charts returned by setting the `maxImageNumber` input parameter.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/176afd8763654163a80b4abf397819cb~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The currently supported chart types include line charts, bar charts, pie charts, and many other types. For more information about supported chart types and usage examples, see <a href="https://docs.byteplus.com/docs/dataagent/Best_Practices_Supported_Chart_Types_and_Usage_Practices">Best Practices: Supported Chart Types and Usage Practices</a>.</div>


<span id="2ff76110"></span>
# Chart result parsing and consumption

<span id="7a7f6607"></span>
## image_url format

When the `imageFormat` input parameter passed to OpenAPI is "image_url", the returned chart is in static image URL format. You can directly consume the image link without any additional processing.

<span id="5d8f81b4"></span>
## lark_fragment format


* Example of returned result:

   When the `imageFormat` input parameter passed to OpenAPI is "lark_fragment", the returned chart is in Feishu native fragment format. The example is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/87d78300fa2b47089080f0183730c28c~tplv-goo7wpa0wc-image.image) </span>

* Consumption and usage: The `larkFragment` returned by OpenAPI is only a Feishu native fragment. To display it in the style of a **message card** in the Feishu application, you need to encapsulate the `larkFragment` returned by OpenAPI in this structure with **encapsulation**.

   ```Plain
   {
     "header": {
       "template": "blue",
       "title": {
         "content": "示例",
         "tag": "plain_text"
       }
     },
     "elements": [
       charts[0].larkFragment // dataagent OpenApi returns chart content
     ]
   }
   ```
   


<span id="ed615877"></span>
## lark_image_key


* Example of returned result:

   When the `imageFormat` input parameter passed to OpenAPI is "lark_image_key", the returned chart is in Feishu image format. The example is as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea4403aa028c4ea5a2d67fb17d350a49~tplv-goo7wpa0wc-image.image) </span>

* Consumption and usage: The `imageLarkKey` returned by OpenAPI is only a Feishu image_key. To display it in the style of a **message card** in the Feishu application, you need to encapsulate the `larkFragment` returned by OpenAPI in this structure with **encapsulation**.

   ```Plain
   {
       "header": {
           "template": "blue",
           "title": {
               "content": "lark_image_key 测试",
               "tag": "plain_text"
           }
       },
       "elements": [
           {
               "tag": "img",
               "img_key": charts[0].imageLarkKey, // dataagent OpenApi 返回图表内容
               "alt": {
                   "tag": "plain_text",
                   "content": "柱状图"
               }
           }
       ]
   }
   ```
   


<span id="0c1233b4"></span>
## vchart_schema

When the `imageFormat` input parameter passed to OpenAPI is "vchart_schema", the returned chart is in the native formats of [vchart](https://github.com/VisActor/VChart) and [vtable](https://github.com/VisActor/VTable). Front\-end developers need to install the [vchart](https://github.com/VisActor/VChart) and [vtable](https://github.com/VisActor/VTable) component libraries based on the returned `chartType` for actual rendering. Examples of various chart types are as follows.


|Chart types |OpenAPI return result example |Consumption usage example |
|---|---|---|
|Pie chart |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3ee7aa6f5844cf9b1814a28ae8c8225~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. Frontend consumes via **vchart**<br><br><br>You can use [the test address](https://www.visactor.io/vchart/playground) to test and parse the returned result. An example of the consumption result is shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46a658b6401e4b13ab377cff48c501c8~tplv-goo7wpa0wc-image.image) </span> |
|Bar chart |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a86ff9a15a34beab8890d201039959f~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. Frontend consumes via **vchart**<br><br><br>You can use [the test address](https://www.visactor.io/vchart/playground) to test and parse the returned result. An example of the consumption result is shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/463dd1b5b6d34645ab7bc6a45932f56c~tplv-goo7wpa0wc-image.image) </span> |
|Metric card |None |1. Copy the returned vchartSchema content<br><br>2. Implemented on the frontend via **DOM**, with no dependency on open\-source libraries. |
|Line chart |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d97aee6f6b644cb6a09a860cb313da2f~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. Frontend consumes via **vchart**<br><br><br>You can use [the test address](https://www.visactor.io/vchart/playground) to test and parse the returned result. An example of the consumption result is shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d49f5c18d3714a38b056f4e482ed4496~tplv-goo7wpa0wc-image.image) </span> |
|Dual\-axis chart |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61c37f50c86b428294a1e74c05f472cb~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. Frontend consumes via **vchart**<br><br><br>You can use [the test address](https://www.visactor.io/vchart/playground) to test and parse the returned result. An example of the consumption result is shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81a6fc64061f42c6b1b803e859f6ff35~tplv-goo7wpa0wc-image.image) </span> |
|Combo chart |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/136717f4c10041a594c9d287687296c0~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. Frontend consumes via **vtable + vchart**<br><br><br>You can use [the test address](https://visactor.io/vtable/demo/table-type/list-table) to test and parse the returned result. An example of the consumption result is shown below.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a6c333e44e24c6abaa7ba7c1e24eef4~tplv-goo7wpa0wc-image.image) </span> |
|Table |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ee1694bad8d4ae99965a1987bdf7566~tplv-goo7wpa0wc-image.image) </span> |1. Copy the returned vchartSchema content<br><br>2. The frontend consumes via **vtable** .<br><br><br>You can use [test address](https://visactor.io/vtable/demo/table-type/list-table) to test and parse the returned results; an example of the consumption result is as follows.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12213d0e14834019aca473fe90585ce5~tplv-goo7wpa0wc-image.image) </span> |
