---
title: "Building an E-commerce agent with Viking AI Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Building_an_E-commerce_agent_with_Viking_AI_Search"
---

*To learn more about Viking AI Search product capabilities, see * [Viking AI Search, the unified intelligent engine for enterprise search, recommendation, and conversational search](https://www.volcengine.com/product/AI-Search-Rec) *.* 


---



This document provides business, product, operations, and technical teams in the e\-commerce industry with a detailed guide to implementing the **Viking AI Search AI shopping assistant**. We will systematically introduce the best practices for the entire process, from data processing and experience configuration to building an intelligent conversational assistant, based on the specific needs of e\-commerce shopping assistant scenarios.

&nbsp;

<span id="872ca2bc"></span>
# Business background: From keyword search to scenario\-based intelligent shopping guidance

In the current e\-commerce environment, consumer shopping behavior has undergone profound changes. Users are no longer satisfied with searching for items using specific keywords, and increasingly prefer to express their needs more naturally and conversationally in specific scenarios. For example:


<columns>
<columnsItem zoneid="qMRoTjvqzz">

* **Scenario\-based shopping**: "I'm going on a beach vacation next week. Can you recommend a photogenic, sun\-protective outfit?"


&nbsp;



</columnsItem>
<columnsItem zoneid="f1gw0MDSDS">

* **Multi\-condition search**: "I'm looking for a birthday gift for my girlfriend. **My budget is around 200**, she **likes pink**, and I'd prefer **a dress**."




</columnsItem>
<columnsItem zoneid="Gx2D2Xmrse">

* **Image\-text search**: "Do you have any dresses in a French retro style like this?" (accompanied by an image)




</columnsItem>
</columns>


&nbsp;

You can use Viking AI Search to quickly build an  **"e\-commerce guide assistant"**  that understands natural language, parses images, and provides intelligent recommendations and conversational search based on user preferences to improve user experience and increase conversion rates.

<span id="d74805b6"></span>
# Preliminary data preparation

High\-quality, well\-structured data is the foundation for building any intelligent shopping guide experience. Viking AI Search analyzes every field you provide in\-depth to build rich semantic and image indexes, so you should **prepare your data thoroughly**.

<span id="8bac3993"></span>
## Data field selection: From "what's available" to "how to use it"

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Field selection strategy:</strong> Do not import all database fields directly. Focus on the "user perspective" rather than simple "archival needs."</div>


<div data-tips="true" data-tips-type="default"><strong>Filtering criteria:</strong> Retain only the information users actually care about when they search, filter, and make decisions (e.g., core specifications, brand, features).</div>


<div data-tips="true" data-tips-type="default"><strong>Clean up noise:</strong> Remove verbose HTML code, duplicate, or low\-value data<strong>.</strong></div>


Below is a general **list of core fields for the e\-commerce industry**. Including these key fields is recommended to improve overall performance. If you are missing some fields, filter by your existing fields before uploading.

⚠️**Your actual field names do not need to match this list exactly. Viking AI Search automatically performs semantic mapping during import**.


|**Field name (Example)**  |**Purpose and description** |**Attribute recommendation** |**Configuration (see Step Two for details)**  |
|---|---|---|---|
|`item_id` |**Product data unique identifier (required)** . Used to uniquely identify a product. It is the unique credential for data updates, user event association, and click reporting. Can be an SKU ID OR a Product ID. |Unique identifier | |
|`title` |**Product title**. The most important text information and the primary source for semantic item retrieval. |Title |Searchable (Text) |
|`content` |**Product details/description**. Includes unstructured text such as detailed product introductions, marketing copy, materials, styles, design concepts, applicable scenarios, and target audiences. **This is key for the AI to understand product data**; the richer the content, the better the semantic item retrieval results. | |Searchable (Text)<br><br> |
|`images`<br><br> |A list of **product image URLs**. Includes main images, detail shots, in\-context shots, on\-model shots, etc. **This is the foundation for enabling multimodal search (image search and text\-to\-image search)** . Provide publicly accessible image URLs.<br><br>For optimal vectorization performance, use clear images with prominent subjects. Recommended image size is at least 300x300 pixels, with a file size under 5 MB. Images that are too large or too small will affect processing efficiency and performance. |Image URL<br><br> |Searchable (Text), Searchable (Image)<br><br> |
|`category` |**Category**. You can have multiple category fields. For example, "Women's Clothing/Dresses/Long\-Sleeve Dresses". Used for filtering and analytics. |Category/Type |Searchable (Text), Filterable<br><br> |
|`brand`<br><br> |**Brand**. Upload the brand name in **plain text**, not the corresponding numeric code for the brand. This allows the model to understand and use it for matching user queries. Users may also ask about a specific brand during conversational search, so we recommend setting this field as a **Category/Type** attribute to improve model retrieval. |Category/Type |Searchable (Text), Filterable<br><br> |
|`price` |**Price**. Used for filtering (e.g., "phones from 500 to 1000") and sorting (e.g., "price low to high"). | |Filterable |
|`tags` |**Product tags**. Tags like "slimming," "new arrival," "designer style," and "summer bestseller" are an effective supplement to the `title` and `content`, and are ideal for semantic item retrieval and filtering. | |Searchable (Text), Filterable<br><br> |
|`status` |**Product status**. e.g., "in_stock" or "out_of_stock". Used to filter out unavailable products during search. | |Filterable<br><br> |
|`publish_time` |**Product update time.**   ** ** The product's listing or update time, which allows for the interpretation of temporal semantics such as "latest products". |Release time |Filterable<br><br> |


<span id="08b34d01"></span>
## Sample data

Before a full data import, we recommend running an end\-to\-end test with 50\-100 representative items to verify that the entire process (field configuration, import, index building, and basic Search) runs smoothly.

<Attachment link="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1d176d2ed7f54fb0b6df3726a5396c90" name="ecommerce_data_sample.jsonl">ecommerce_data_sample.jsonl</Attachment>


&nbsp;

**Other data specifications and recommendations:** 


|**Specification type** |**Details** |
|---|---|
|Nesting structure limitations |The system supports a deepest nesting of 3 levels for objects. Filterable fields can only be on the first and second levels. Filtering is not supported on the third level. If your SKU data structure is too complex, flatten it before importing. |
|Data type consistency |Within the same dataset, fields with the same name must have a consistent data type (for example, the price field cannot be an Int in one record and a String in another), otherwise index construction will fail. |


<span id="af5841e8"></span>
# Build an AI shopping guide assistant in three to four easy steps

Following the [Volcano Engine Quick Start](https://www.volcengine.com/docs/85296/2222393?lang=zh) guide, we simplified the process of building a complex AI shopping guide assistant into four core steps.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8dd80a19c75042ff9b9058a0d14839b4) </span>

<span id="04ff625a"></span>
## Step one: Create a new application


<columns>
<columnsItem zoneid="RRyJfcL02R">

1. Log in to the [Viking AI Search console](https://console.volcengine.com/aisearch/platform/region:aisearch-platform+cn-beijing/home/app-list) and click "New application". 

2. The system provides pre\-configured industry templates (such as E\-commerce, content communities, etc.). For shopping guide scenarios, you must select the **E\-commerce** industry. This preloads strategy configurations suitable for e\-commerce scenarios. 

3. After entering the Application name, you can proceed to the next step: "Dataset creation and import".

</columnsItem>
<columnsItem zoneid="jVGk3TIKNg">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/05f1bc7e7c234e05bc3d56317c25015d" controls></video>




</columnsItem>
</columns>



<columns>
<columnsItem zoneid="QWBZhO2EnW">

<span id="fc5c0a47"></span>
## Step Two: Import sample data and configurations from the console


1. Create a new Image and text dataset, select **Product Tags**, and import the sample data. You can import previously prepared JSONL format files.

2. For Field attributes and index configuration, the large model automatically scans the sample data to infer the data type, meaning, and configuration method for each field. You can **manually calibrate** these settings. This process directly determines search performance and, in turn, affects the performance of shopping guide scenarios.

3. After data import, the system will begin parsing the data with the large model and building the index. This process may take some time. Once complete, the dataset Status will show **Configuration active**. You can then go to the Experience center to try out multimodal search and conversational search.

</columnsItem>
<columnsItem zoneid="ns3Otli6ih">

&nbsp;



</columnsItem>
</columns>


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Data configuration</div>


<div data-tips="true" data-tips-type="default"><strong>Unique identifier</strong>: <strong>You must specify one</strong>. This is the unique identifier for the entire system. All data updates and associations depend on this ID.</div>


<div data-tips="true" data-tips-type="default"><strong>Searchable (Text)</strong>: When selected, the search matches the user's query against the semantic and keyword information in the field content. Supports text. Typically, all fields containing rich semantic information (such as <code>title</code>, <code>content</code>, <code>tags</code>) should be set as searchable.</div>


<div data-tips="true" data-tips-type="default"><strong>Searchable (Image):</strong> To enable image search, select both Searchable (Text) and Searchable (Image) for the product image field. The system will then vectorize the image and apply VLM understanding.</div>


<div data-tips="true" data-tips-type="default"><strong>Filterable</strong>: When selected, this field can be used as a filter during search. Suitable for fields with clear, enumerable values, such as <code>category</code>, <code>status</code>, and <code>brand</code>, and the numeric field <code>price</code>.</div>


<div data-tips="true" data-tips-type="default"><strong>Autocomplete</strong>: When selected, this field's values are used for search box suggestions (suitable for brand names, popular tags, category names, etc.).</div>


&nbsp;

<span id="b9cbba80"></span>
## **Evaluate experience and optimize**

After completing the steps above, you have finished the **initial setup of Search and conversational search capabilities**. The next stage is primarily for "experience optimization". The conversational assistant's underlying capabilities depend on the results returned by Search. **To configure a good e\-commerce shopping guide, you typically need to adjust both Search and conversational search strategies**.

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Recommendation</div>


<div data-tips="true" data-tips-type="default"><strong>Avoid using a one\-size\-fits\-all "template" configuration</strong>. </div>


<div data-tips="true" data-tips-type="default">Optimal search strategies can vary across different E\-commerce verticals (e.g., apparel, electronics, fresh produce) and for different inventory sizes. For example, the beauty industry may prioritize "new arrivals" and "brand," while the consumer electronics industry may focus more on "spec matching" and "price." </div>


<div data-tips="true" data-tips-type="default">We strongly recommend <strong>viewing experience configuration as a continuous iterative process and using online experience and user feedback to evaluate and select the optimal strategy</strong>.</div>


&nbsp;

<span id="def29534"></span>
### Search strategy configuration recommendations

The following are some of the most commonly used Experience center capabilities for e\-commerce shopping guides. You can configure them to meet your business needs:


<columns>
<columnsItem zoneid="wiFt6UCIKu">

<span id="3c6fc070"></span>
#### Boost/Demote rules

You can dynamically boost or demote the sorting weight for specific products based on a series of conditions.

**Common use cases:** 


* **Boost high\-quality products:**  Apply a higher sorting weight to products where the `product_rating` is greater than 4.5 (assuming a maximum score of 5).

* **Boost new products**: Apply a higher sorting weight to products with a `publish_time` within the last 7 days.

* **Boost promotional/event products**: Boost products where `tags` includes "Big Sale" OR that belong to a specific event ID.

* **Prioritize in\-stock items**: Boost products where `stock` is greater than 0, OR demote products where `stock` equals 0.

* **Boost high\-profit/featured products**: Boost specific products based on internal profit margins or strategic priority.

* **Location\-based boost and demote configuration:**  When your use case requires dynamically adjusting search results based on user proximity, you can configure a location\-based boost and demote strategy.


<span id="b29e1cc0"></span>
#### 

</columnsItem>
<columnsItem zoneid="fnXJuPeVHS">

Example: Boosting high\-quality product data

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a50d5962323b4330a0bbd7d4bbe51b7b) </span>



</columnsItem>
</columns>



<columns>
<columnsItem zoneid="iRPBjMhkcm">

<span id="80059f81"></span>
#### Field sorting

In addition to the default relevance sorting, you can also set a custom sort order. For example:


* **Price sorting**: Select the Price field and set the order to high to low OR low to high.

* **Sort by sales volume**: Sort by the `sales_volume` field in descending order.

* **Sort by release time**: Sort by the `publish_time` field in descending order, i.e., new items first.

</columnsItem>
<columnsItem zoneid="DyOwcEWywD">

<div style="text-align: center">
Example: Price sorting</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/15c416b61a3a42bea561e9deda29b242) </span>



</columnsItem>
</columns>


To learn more about Search configuration details, refer to the official documentation: [Quickly create a Viking AI Search application](https://www.volcengine.com/docs/85296/2222393?lang=zh).

&nbsp;

<span id="49544ce3"></span>
### Conversational search (AI shopping assistant) configuration

Viking AI Search uses a conversational agent to combine powerful Multimodal search, personalized recommendations, and the conversational capabilities of large language models (LLMs). This lets you quickly build an intelligent shopping assistant that can chat, understand Product data, and guide users. In conversational search scenarios, we recommend configuring the following strategies.

<span id="1588ed4c"></span>
#### Agent persona

You can define a unique "identity and persona" for your shopping assistant. Although this does not directly change the Product data retrieved by search, it greatly affects the user experience and brand perception.

**Prompt example:** 


<columns>
<columnsItem zoneid="FVF1S2VaTR">

<div style="text-align: center">
Professional shopping guide (Default example)</div>


```Plain Text
As a trusted search assistant, you maintain a rigorous and objective stance, dedicated to providing insightful content recommendations and comprehensive answers. No matter how complex or detailed a user's query may be, you will do your utmost to help users find what they need in an efficient and friendly manner.
```




</columnsItem>
<columnsItem zoneid="CkkDHnhO2M">

<div style="text-align: center">
Fashion and style expert (Stylized example)</div>


```Plain Text
You are {Brand Name}'s e-commerce fashion shopping assistant, {Assistant Name} — the user's personal "styling partner" and "style advisor."
You have a keen eye for clothing, accessories, fabrics, cuts, trends, and styling occasions, and you excel at making fashion easy to understand, easy to choose, and easy to wear.
You have a warm, enthusiastic personality with a strong sense of aesthetic judgment. You are skilled at empathizing with users' real needs — equally at home, with trends and everyday dressing. You don't just recommend products; you help users think through the question of "what to wear."
Your goal is to help users shop with confidence, look great, and avoid costly mistakes — making every shopping experience easier, more stylish, and more understood.
```


</columnsItem>
</columns>


<span id="1555f70d"></span>
#### Response style settings

Configure the structure, tone, and language of the agent's responses. For example: principles for product recommendations, quantity, scope, and response methods. We recommend further optimizing these based on your business needs.

&nbsp;

<span id="ab3a0745"></span>
#### Conversation opening configuration: The first impression of the interaction

The opening remarks are the first touchpoint in the user's interaction with the assistant and directly determine the user's willingness to engage. A good opening can effectively lower the user's decision\-making barrier and increase the interaction rate. We recommend that you configure good opening remarks based on your business strategy. Viking AI Search provides three configurable opening modes:

**Plain text opening**


<columns>
<columnsItem zoneid="yilV8qQzw2">

* **Use cases**: The simplest and most direct way to start.

* **Example script**: "Hello! I'm your personal AI shopping assistant. What can I help you find? Feel free to ask me anything."




</columnsItem>
<columnsItem zoneid="CdsEthFU1H">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/eefd22e3cb0548a49238343d2c637f88) </span>



</columnsItem>
</columns>


&nbsp;

**Starter questions**


<columns>
<columnsItem zoneid="BzdsTpmOHW">

* **Use cases**: Lower the barrier to entry for users by providing popular or interesting question "bubbles" to proactively guide them as they explore.

* **Question source:**  The system automatically generates related question recommendations the day after you configure the conversational search scenario. You can also customize the opening questions based on your business needs.

* **Example custom question configuration**: For example, "Recommend some outfits for the Spring Festival."

</columnsItem>
<columnsItem zoneid="TaA4pzQH5o">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/91f6926fab8a4a42957194ae18b3131f) </span>



</columnsItem>
</columns>


&nbsp;

**Starter product recommendations: Personalized opening recommendations**


<columns>
<columnsItem zoneid="oWqEGypv13">

* **Use cases**: Implement proactive marketing and provide an ultimate, hyper\-personalized user experience.

* **Prerequisites**: You must integrate user **user event data** and configure a recommendation scenario (e.g., "Recommended for you"). To configure recommendations, see the [Configure personalized recommendations](https://www.volcengine.com/docs/85296/1856097?lang=zh) section.

* **Configuration example**: Enable "Initial item recommendations" and select the associated **homepage recommendation scenario**.

</columnsItem>
<columnsItem zoneid="B0t8BF9yPf">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0bb77f4b0d534ae8941971d96009b984) </span>



</columnsItem>
</columns>


<span id="b5091acb"></span>
#### Supplement knowledge base: Enhance shopping assistant capabilities

In addition to the product database, your company often has large amounts of unstructured documents, such as "After\-sales policy," "Return and exchange process," "Size chart," and "Membership benefits." With the knowledge base feature, you can upload these documents to give the shopping assistant the ability to answer these kinds of questions.


<columns>
<columnsItem zoneid="XV5RpfaGfs">

**Configuration process**:


1. Upload your knowledge documents (formats such as PDF, Word, and TXT are supported). For a detailed list of supported formats, see [document dataset--Global AI Search-Volcano Engine](https://www.volcengine.com/docs/85296/1894022?lang=zh).

2. The system automatically slices and vectorizes the documents.

3. When a user asks a non\-product query, such as "Do you support 7\-day no\-reason returns?", the AI assistant prioritizes retrieving relevant information from the uploaded documents to generate a precise answer.

</columnsItem>
<columnsItem zoneid="UHxy3OVvEK">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/076d42b8cd28460696269c8309221ed9) </span>



</columnsItem>
</columns>


<span id="f37ba4fc"></span>
#### Follow\-up recommendations

Enabling the follow\-up recommendation feature is strongly recommended to increase the multi\-turn conversation rate and avoid single\-exchange interactions.


<columns>
<columnsItem zoneid="smvimZT0Gx">

**API parameters**: when invoking the `ChatSearch` API, set `enable_suggestion=true`.

**Result**: after the AI assistant answers a question, it automatically generates 3 related follow\-up suggestion bubbles based on the context. As shown on the right.

This feature significantly reduces user input effort and effectively guides the conversation to a deeper level, uncovering more specific user needs.



</columnsItem>
<columnsItem zoneid="hpk2UNgjf3">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1bd43362674b483b8268447f06f0fe34) </span>



</columnsItem>
</columns>


**You can also refer to the following video guide for the overall configuration of the conversational search capability:** 

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c4c9f1799efe4cf2ab1ef088ad6e8044" controls></video>


&nbsp;

<span id="08709d33"></span>
### Upload full product data

After you configure the experience center in the console, if you want to **import more data** (e.g., import the full dataset or perform incremental updates), follow the steps below.


<columns>
<columnsItem zoneid="e2c6FduAqo">

1. Return to your **Datasets** list

2. Find the **target dataset** to which you want to add data.

3. Click **View** to open the details page for the dataset.

4. On this page, find and switch to the **Data import** tab.

</columnsItem>
<columnsItem zoneid="D7izxDNQYA">

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6aab1222cec542cfbe0204bc19715957) </span>



</columnsItem>
</columns>


Here, you will find two main data import methods (**Import via API** and **Upload JSONL file**) that you can use to add more data later.


1. **Upload JSONL file**

   1. You can upload files directly in the console by **clicking or dragging**.

2. **Real\-time import API**

   1. **API documentation**: [Real-time import and update of item data -- Viking AI Search - Volcano Engine](https://www.volcengine.com/docs/85296/1544970?lang=zh)

   2. **Use cases**:

      1. **Add items in real time**: Automatic processing and index building. Takes from a few to tens of seconds (processing takes longer for data with multiple images or videos).

      2. **Update items in real time**: Supports updating only some fields. If you only update filter fields (non\-retrieval fields), the changes take effect in seconds. If you update images, text, or videos, the processing time is longer.

3. **Batch import API**

   1. **API documentation link**: [Batch import item data - Global AI Search - Volcano Engine](https://www.volcengine.com/docs/85296/2123240?lang=zh)

   2. **Use cases**:

      1. **Initial full build**: one\-time import of complete product/content data for test or production environments.

      2. **Regular bulk updates**: update specific fields for more than 100,000 items (e.g., batch changing listing status).

      3. **Backfill new fields**: batch write newly added field values for the full data set.


<span id="cb5e7230"></span>
### Integrate the conversational search API

Viking AI Search provides standard APIs to integrate the capabilities you have built into your app, mini program, or webpage. The following is a summary of the API invocation.

<div style="text-align: center">
</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7f836ce853b54203b231b9ad97beb26f) </span>


&nbsp;

1. **Front\-end initiates a request**:

   * The user enters a question in the dialog box (e.g., "Recommend some breathable running shoes") or uploads an image.

   * The frontend application packages the user's input, the current session's `session_id` (generated and maintained by the frontend), and fixed parameters such as `user_id`, and sends them to your business backend.

2. **Backend invokes Viking AI Search**:

   * Upon receiving the request from the frontend, your business backend constructs a POST request to the Viking AI Search `/chat_search` endpoint.

   * The request body includes all the information from the frontend and your application's `API Key` for authentication.

   * **Key point**: The business backend needs to receive the response from the `/chat_search` endpoint as a stream.

3. **Process the streaming response and forward it to the frontend**:

   * The `/chat_search` endpoint sequentially returns a series of JSON data chunks. Each data chunk describes the AI assistant's current work step (`step`), which can be "intent recognition", "tool invocation" (along with the retrieved product data `payload`), or "response generation" (along with a text snippet `content`).

   * Your business backend needs to parse these data chunks in real time and **forward them to the frontend through the streaming connection without modification**.

4. **The frontend renders a rich interactive interface**:

   * The front end receives a data stream forwarded from the business back end.

   * When a **text stream** is received, the AI's response is rendered in real time with a "typewriter" effect.

   * When **E\-commerce** data is received, parse the product list in the `payload` and render it into visible, clickable **product cards** (including an Image, Title, Price, Purchase button, etc.).

   * When **follow\-up recommendation** data is received, it is rendered into clickable recommendation bubbles.

   * This dynamically presents a rich interactive interface to the user, including text, product cards, and recommendation bubbles.


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Why is a backend proxy needed?</div>


<div data-tips="true" data-tips-type="default">Although you can invoke the Viking AI Search API directly from the front end, we strongly recommend using your business backend to wrap and forward the requests. This approach has several key benefits:</div>


<div data-tips="true" data-tips-type="default"><strong>Security</strong>: Avoids exposing your <code>API Key</code> directly in front\-end code.</div>


<div data-tips="true" data-tips-type="default"><strong>Authentication and rate limiting</strong>: You can implement custom logic for user authentication, request frequency control, and more on your business backend.</div>


<div data-tips="true" data-tips-type="default"><strong>Logic aggregation</strong>: In the future, you can aggregate other internal services, such as querying orders and redeeming coupons, on the backend. This approach maintains a stable API for the front end.</div>


&nbsp;

**For detailed API integration instructions, see ** [ChatSearch - Conversational search--Global AI Search - Volcano Engine](https://www.volcengine.com/docs/85296/1873492?lang=zh) **.** 

&nbsp;

<span id="e06633cc"></span>
## Conclusion

**Industry differences and parameter tuning recommendations**

Finally, remember that best practices for Viking AI Search are not rigid rules. Different e\-commerce industries, and even different development stages within the same industry, prioritize search differently. A successful e\-commerce shopping assistant is the result of **high\-quality data, flexible strategies, and continuous optimization**.

&nbsp;


---



<span id="ebd3e79a"></span>
# FAQs

While implementing the AI shopping guide assistant, we have summarized some common configuration issues and pitfalls our customers face. Understanding and avoiding these issues in advance will make your integration process smoother.


|Frequently asked questions |Detailed description and impact |Recommendations |
|---|---|---|
|**Data source URL is inaccessible** |In the imported product data, the Image URL in the `images` field is an internal network address or is invalid. This will prevent AI Search from crawling the image. The item will lose all its visual information and cannot be retrieved by "search by image" or "text\-to\-image search". |Before data import, write a script to batch\-check the public accessibility of all image URLs and remove any invalid links. |
|**Inconsistent data schema** |In the same JSONL file, the data structure is inconsistent between different lines. For example, the `price` field is sometimes the number `199` and sometimes the string `"199.00"`. This will directly cause the data import task to fail. |Enforce consistent data types. The schema should be enforced at the data export stage. Use a data validation tool, such as `jsonschema`, to check your data before data import.<br><br> |
|**Image quality issues** |The provided images are too small (e.g., less than 100x100 pixels), have low resolution, or include many distracting watermarks unrelated to the product data. This seriously affects the quality of image feature extraction and reduces the accuracy of multimodal search. |Use clear, unobstructed main or scene images that are at least 300x300 pixels. If possible, provide multiple images from different angles. |
|**Testing before indexing is complete** |After importing a large amount of data, index construction takes some time. Testing search during this period may return incomplete or even empty results, which can lead to a misjudgment of system performance. |Closely monitor the index construction status in the console. Wait until the index status is "Configuration active" before you start comprehensive search experience testing. |
|**Field not marked as Filterable**<br><br> |You want to filter by brand, but during field configuration, you forget to check the `brand` field as "Filterable". This will cause API calls that `filter` by `brand` to fail or return an error. |During the data preparation stage, plan which fields might be used for filtering in the future, and then confirm during configuration that each of these fields is checked as "Filterable". |
|**Incomplete marking of Category/Type fields** |In this product, Category/Type is a broader concept that refers to important item fields with enumerable values. The model can automatically infer these fields as filter conditions that match user intent.<br><br> |Conventionally understood categories like `Beauty` and `Digital Products` can be marked as Category/Type. If you also want to parse other dimensional information from conversational search queries (for example, to identify that a user is interested in a specific brand), we also recommend marking the brand field as Category/Type. |
|**Large fields** |If you import data with very long fields, the amount of information input to the model increases significantly. This raises the overall API latency and can even cause the request to fail due to a timeout. |Analyze large fields to see if all the information they contain is valuable for search. Filter out information without value and only upload valuable information. |


&nbsp;


---



*To learn more about Viking AI Search capabilities, see * [Viking AI Search: The integrated intelligent engine for enterprise search, recommendation, and conversational search](https://www.volcengine.com/product/AI-Search-Rec) *.*
