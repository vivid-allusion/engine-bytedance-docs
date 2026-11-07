---
title: "Configure search strategy"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Configure_search_strategy"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Viking AI Search</strong> is an enterprise\-level AI search product based on generative AI. Leveraging large model multimodal semantic representation and understanding capabilities, combined with ByteDance’s years of best practices in information retrieval, it provides customers with an out\-of\-the\-box AI search platform service to help easily build and integrate end\-to\-end multimodal text and image search and recommendation capabilities.</div>



* <div data-tips="true" data-tips-type="default">To experience more Viking AI Search capabilities, click to visit: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search engine, integrated intelligent engine for enterprise search, push, and question answering</a></div>



<span id="7a2e0fd6"></span>
# AI search process overview

AI Search includes four stages: Item retrieval, Sorting, Rerank strategy, and refined operation intervention

**Recall:**  After preprocessing the user's query, the system performs cross\-modal matching recall calculation with multimodal content in the item dataset. You can adjust the recall strategy through the following configuration options:


* [Configure multimodal matching strategies](https://docs.byteplus.com/docs/393/Configure_search_strategy#e0d8eb20)

* [Configure the Maximum Number of Results](https://docs.byteplus.com/docs/393/Configure_search_strategy#68ef94b8)

* [Configure Prioritized Item Retrieval](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#388f9ec4)

* [Enable Personalized Retrieval](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#b1e67f28)


&nbsp;

**Sorting process:**  For the retrieved search results, you can configure whether to Rank by popularity


* [Configure item heat rank participation](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#294a09ed)


&nbsp;

**Rerank process:**  After sorting, you can further customize the intervention strategy based on actual needs for reranking you can adjust the sorting results again through the following configurations **If all the following strategies are enabled, sorting will first perform semantic rerank, then apply Boost, Demote, and custom sorting, and finally apply Diversity rules to diversify the results**:


* [Enable Multi-modal Re-ranking](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#0832ad50)

* [Configure Boost and Demotion](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#10e7aa50)

* [Configure customized Sorting rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#39776d7b)

* [Configure Diversity rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#9da94021)


&nbsp;

**Refined operation**: During actual use, you may find some special scenarios where general strategies may not suit. At this time, you can use the Refined operation feature provided on the console to configure a set of independent Item retrieval, Sorting, and Rerank strategies for specific search queries


* [Configure refined operation rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#ad28d011)


&nbsp;

In addition, you can also set features including Search term Synonyms, Typo tolerance, and Search term Autocomplete:


* [Customize Synonym groups](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#cf896f4f)

* [Search Typo Correction](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#3f11d811)

* [Search Query Completion](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#47bd3d38)


&nbsp;

If you want to explore a better search experience, you can use the following features provided on the platform:


* [Search result facet](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#c5e53777)


&nbsp;

After entering the app, you can configure recall, sorting, and search query strategies on the **Experience Center \> Search Experience** page and **create multiple configuration sets simultaneously**. Comparing different strategies helps identify the best practices for real business scenarios.

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/51a046bf91c1460699630cbeeb016d38) </span>

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div>


<div data-tips="true" data-tips-type="default">If multiple datasets are associated with the app simultaneously, you need to configure recall and ranking strategies separately for each dataset's index. You can select the dataset to configure from the datasets tab in the <strong>Configuration</strong> tab.</div>


&nbsp;

<span id="e0d8eb20"></span>
# Configure multimodal matching strategies

AI Search offers two methods: Text search and Image search.

<span id="29e5d6b2"></span>
## Text search

After receiving a search query, AI Search uses cross\-modal hybrid retrieval to search multiple data sources and returns results ranked by relevance. You can adjust the data modality matching weights to prioritize matching item text information or item image information. You can also adjust the semantic matching weight or keyword matching weight.

You can find configuration options in the sidebar:

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/662511fba28c48cea85907c326f5badd) </span>

You can choose from platform preset configurations or select custom mode.

&nbsp;

<span id="3cf355d6"></span>
### Preset configurations

To simplify setup, three preset modes are available to match common business requirements:

**Balanced mode**: uses preset balanced weights to leverage both vector search (understanding your natural language and image intent) and keyword search (precise matching of specific terms). This is the most general setting, recommended for first\-time use.

**Semantic search priority:**  this mode relies mainly on vector models to calculate semantic similarity. This mode works better when your search query is a natural question, descriptive long sentence, or when you want to perform "text\-to\-image" search.

**Keyword search priority:**  this mode relies mainly on keyword matching. This mode offers higher accuracy when you need to find content containing specific product models, proper nouns, codes, or other exact text.

<span id="7dd68c07"></span>
### Custom configuration

If the preset configuration does not meet your needs, try enabling custom configuration to adjust the matching weight for different feature types.


<columns>
<columnsItem zoneid="x2eRroiANm">

**Weight for matching image/text content:** 

This determines whether a text query matches more on the information in the text or features in the image within the candidate pool.

&nbsp;

**Weight for matching text semantics/keyword content:** 

This determines whether matching text content focuses more on semantic features or original keywords during retrieval. These two matching methods each have their focus. Understanding their differences helps you better adjust according to actual needs.


* **Semantic matching: understanding the "meaning" of content**

   Semantic matching is achieved through vector retrieval, encoding the "meaning" or "context" of text content into high\-dimensional vectors.

   It pays more attention to the **deep semantic relevance** between the query content and the stored texts in the database. Even if the query does not contain exactly the same keywords, semantic matching can find highly relevant results as long as their meanings are similar.

   **Applicable scenarios:** 

      * When you want search results matched by the **concept** or **topic** of the content.

      * When user queries are very colloquial, long sentences, or include synonyms.

      * When cross\-lingual search is needed or handling similar content expressed in various ways.

* **Keyword matching:**  exact matching of "literal" content

   Focus more on **exact matching** between query terms and document terms. If the queried keyword appears in the document, the document is considered relevant.

   **Applicable scenarios:** 

      * When you need to perform an exact search based on **specific terminology, product models, names, or codes**.

      * In scenarios demanding high vocabulary accuracy, such as legal, medical, or technical documents.

      * Users clearly know the specific keywords they are looking for.

</columnsItem>
<columnsItem zoneid="QvZeMSJaiw">

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c44ab781ed85441fa294e44ed6f861f4) </span>

</columnsItem>
</columns>


<span id="067bb3fc"></span>
## Image search

If the associated dataset in the application has created an image index, you can enable image search functionality. After uploading an image to initiate a search request, AI search will retrieve image information from items and return results sorted by similarity. Currently, there are two supported modes:

**Item Similarity Search**: Ignores the background and human subjects to focus specifically on **finding the similar item** shown in the image (e.g., finding the same pair of shoes from a street photo).

**Search by object similarity**: ignore the background and main subjects in the image to find pictures of the same product appearing in this image

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9b7dc605819046f5990226e5197ab52f) </span>

&nbsp;

<span id="68ef94b8"></span>
# Configure the Maximum Number of Results

This parameter controls the maximum number of result entries returned per search request for a **single associated dataset** when users search through this application. It directly determines the upper limit of information obtained from each data source. If your application associates multiple datasets, you can **set independent Maximum Number of Results** for each dataset. This allows you to control the number of results for each dataset based on its importance and content characteristics.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c197a88afed7453f8da0ee785ae36bc0) </span>

&nbsp;

**Default value**: `200`

**Configuration constraint:**  Allowed values range from `1` to `5000` as any integer

**Example:**  Suppose you set the **Maximum Number of Results** for dataset A associated with your application to `5`. Then, even if a user’s search query matches 100 results in dataset A, the system will return at most 5 of the most relevant results from dataset A.

<span id="66d097ab"></span>
# This feature adjusts the recalled results based on users’ personalized interest tags—derived from their behavioral data (typically covering dimensions such as categories and brands)—while ensuring relevance.

Prioritizing recall ensures that specific datasets or types of content appear first in search results, preventing high\-value or time\-sensitive items from being "buried" or filtered out during the initial retrieval phase.

If your candidate items are numerous but the final recall list is relatively short (for example, a base of 100,000 products with only 200 recalled results per search), you might encounter the following issues:


* Every search returns content from over a month ago. Although relevant to the user’s query, the timeliness is low.

* Promotional categories, brands, and other items might not be sufficiently exposed in search results.

* Even after boosting for timeliness and popularity, the first page of search results might still show old or less popular content.


This happens because the default search strategy matches the query against the entire pool of candidate items, selecting the final search results based on relevance scores, then applies strategy\-based re\-ranking. Newer or more popular content may have lower relevance scores, causing them to be excluded from recall and unable to participate in subsequent boosting and re\-ranking strategies.

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8f460590382a4c55b22375863dd91f86) </span>

&nbsp;

You can configure prioritized item retrieval to create separate recall channels for specific content for which you want to guarantee exposure or boost in the rankings, ensuring these items are recalled and included in later sorting and boosting. This prioritized content, based on your business strategy, can be:


* New content (for example, content published within the last month)

* Popular content (for example, content with likes or comments exceeding a certain threshold)

* Content requiring exposure support (such as promotional product categories, promoted content tags, etc.)

* ...


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/751053447d434838882750c1d50291f7) </span>

&nbsp;

<span id="b0cbfe94"></span>
## Create Prioritized Item Retrieval in the console

Configure Prioritized Item Retrieval in the console; after saving and activating the configuration, it applies to the corresponding search strategy API calls.

In the console, under Experience Center \- Search panel, find the search configuration tab you want to configure. Under the Item Retrieval section, you can configure Prioritized Item Retrieval strategies:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/473b987577ad4583bef04fe6be352528) </span>

&nbsp;

Click to add a Prioritized Item Retrieval recall channel:

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2f8bbd903a7f4c3f89d537dd27d53c3e" controls></video>


&nbsp;

Define which content this Prioritized Item Retrieval recall channel recalls by configuring item field conditions; recall conditions support complex condition combinations. Different field types support different types of filter conditions. See the table below:


|<div style="text-align: center"><br><strong>Field type</strong></div><br> |<div style="text-align: center"><br><strong>Supported operators</strong></div><br> |<div style="text-align: center"><br><strong>Input content</strong></div><br> |
|---|---|---|
|**String** |is in, is not in |string list |
|**integer**<br><br> |greater than, less than, greater than or equal to, less than or equal to, equal to, not equal to |numeric value |
||interval |(minimum value boundary, maximum value boundary) |
|**floating point number**<br><br> |greater than, less than |numeric value |
||interval |(minimum value boundary, maximum value boundary) |
|**string list** |contains, does not contain |string list |
|**integer list** |contains, does not contain |integer list |
|**boolean value** |equals, not equals |true / false |
|**date and time attribute fields**<br><br> |earlier than |fixed point in time |
||later than |fixed point in time |
||Dynamic time range |A dynamic time range relative to the search time, such as the last 30 days. |


**Configuration example:** 

Create a new recall channel to ensure exposure of new content. The recall conditions meet any of the following:


* Update time is within the past 60 days, and the status is published

* In\-stock tag is 1, and the status is published


&nbsp;

You can test the effect after clicking **Confirm**. Click **Sync Changes to API** in the upper right corner; Prioritized Item Retrieval takes effect when the API is called.

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3b3add4d826c4156854d7cde4046df19" controls></video>


&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div>


<div data-tips="true" data-tips-type="default">Prioritized Item Retrieval usage restrictions:</div>



* <div data-tips="true" data-tips-type="default">A maximum of three Prioritized Item Retrieval strategies can be active for each dataset</div>


* <div data-tips="true" data-tips-type="default">Each Prioritized Item Retrieval strategy can configure up to 5 conditional expressions</div>



&nbsp;

<span id="b1e67f28"></span>
# Enable Personalized Retrieval

The personalized retrieval capability adjusts the retrieval of results based on the user's personalized interest tags while ensuring the relevance of the search results. User interest tags are calculated based on their User event dataset, usually covering dimensions such as categories and brands.

Enable this feature after completing some prerequisite work

<span id="eb1d6b14"></span>
## Preparations for enabling Personalized Retrieval


* **Upload the User event dataset**: user interest tags depend on the User event dataset for inference and calculation. For importing event data, see [Create User Event Dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_User_Behavior_Dataset)

   After the User event dataset upload is complete, data initialization processing and interest tag generation are expected to take 1 day. During this period, Personalized Retrieval may not be enabled. Please be patient.

* **Configure interest tag fields as Filterable**: according to the console's prompts (Console \- Experience center \- Search result Strategy \- Retrieval \- Personalized Retrieval, hover over the option to see detailed hints), check the specified fields in the Item dataset as Filterable. For configuring the index, see [About datasets and indexes](https://docs.byteplus.com/docs/viking-aisearch/92184)


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9c4cd3923b204b77961f788e38b2322a) </span>

After completing the above configuration, you can enable the personalized retrieval feature in the console.

&nbsp;

<span id="ff713c00"></span>
## Enable and select the personalized retrieval intervention level

After enabling this feature, you can currently select from two levels: strong and weak, corresponding to different degrees of intervention.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/acf1eb0680574634a64be433daaa26ee) </span>


&nbsp;

* **Weak personalization intervention**: in this mode, the system recalls items related to the Search term and matching the current search user's user interest tags, but when calculating the item retrieval score, the weight of interest tag matching is relatively low, with more weight given to keyword matching and semantic matching.

* **Strong personalization intervention**: in this mode, the system also recalls items based on user interest tags, while assigning relatively higher weight to interest tag matching during retrieval score calculation, increasing the chance of interest\-related items ranking higher.


you can experience the search effect under different intervention levels in the console, and finally select the configuration that suits your business scenario. after verification, click the [sync changes to API] button to apply the personalized retrieval immediately to the search service.

&nbsp;

<span id="294a09ed"></span>
# Configure item heat rank participation

The item heat rank participation feature can **adjust the sorting based on item heat after considering search result relevance**.

The item heat score is calculated according to the user event data uploaded within the application: the more **positive feedback actions such as click, add to cart, purchase, comment, favorite, and share, the higher the item's heat and search ranking score**.

This feature helps your users discover more popular and trending items during Search

Enable this feature after completing some prerequisite work

<span id="3d7dd1b7"></span>
## Prerequisites for enabling rank by popularity


* **Upload user event dataset**: Because item popularity depends on user event dataset statistics, import user events referring to [Create User Event Dataset](https://docs.byteplus.com/docs/viking-aisearch/Create_User_Behavior_Dataset)

   After uploading the user event dataset, data initialization and popularity calculation begin immediately and typically take 1 day to take effect. Please be patient


Once uploading and calculation complete, enable the item popularity rank switch on the console

<span id="2c795ed7"></span>
## Enable rank by popularity

On the experience center page, find the [search result configuration \- rank by popularity] option and turn the switch on to experience search result sorting based on item popularity

After verifying on the experience page, click [sync changes to API] to immediately apply the rank by popularity strategy to the search service.

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/34d2315dc2194cf586f70a40cbb4274c) </span>

&nbsp;

<span id="0832ad50"></span>
# Enable Multi\-modal Re\-ranking

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/36e38f83b2594b1bbb465a7fbf830891) </span>

&nbsp;

This section is for enabling/disabling multi\-modal reranking and setting the number of items you want to rerank, optimizing the accuracy of your top N results. Enabling multi\-modal reranking reduces irrelevant content interference in search results and improves result accuracy.

The effectiveness of the semantic reordering feature mainly depends on the questions you ask and the related context. Enabling it will somewhat affect search results response latency. Therefore, we recommend **using Multi\-modal Re\-ranking primarily in Conversational Search**. For regular searches, since search terms are usually short and have limited text available for semantic understanding, the benefit of **Multi\-modal Re\-ranking** is often limited. Evaluate its suitability for your specific use case.

We will **disable Multi\-modal Re\-ranking by default** for you. If you want to enable it, you can find the setting in the search configuration on the left control panel, where you can choose whether to enable it. When Semantic Re\-ranking is enabled, the default setting is to re\-rank the top 20 results. You can also customize the number of results you want to re\-rank in the sidebar (configurable range is [2,100]).

When multiple datasets are configured, enabling Semantic Re\-ranking will re\-rank results separately for each dataset.


* **Note that multi\-modal re\-ranking only works for pure text searches.**  Searches containing non\-text content such as images or videos are not supported. If you add image content to a search query / question after enabling Multi\-modal Re\-ranking, the Multi\-modal Re\-ranking will automatically be disabled.

* If the number of results to re\-rank is greater than the number of records in your dataset or the configured maximum number of results, the system re\-ranks all available results.


You can find more information about the corresponding API fields involved in the semantic reordering feature by querying the [search API](https://arcosite.bytedance.net/sites/1740457395001/67bd5a617a7a0b0503e30be6/editor/6805b41e6ffc5805504abd99?docLang=zh&bv=6805b41e6ffc5805504abd75) in the **SearchResult** section.

&nbsp;

<span id="10e7aa50"></span>
# Configure Boost and Demotion

You can use Boost and Demotion strategies to select certain items based on their attributes for boosting and demotion.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6dfb79949cfd420b96c749d8f9fff603) </span>

&nbsp;

The configuration of Boost and Demotion strategies can be abstracted as: "For items meeting {condition}, increase the ranking score by {weight} when recalled in search." Details:


* {condition}: The selection criteria defining the scope of items where the strategy applies, expressed as {attribute field}:{condition operator}:{value}, for example, the "Product Name" field contains the keyword "promotion," the "Inventory" field is less than or equal to 10, or the "Price" field is greater than or equal to 1000.

* {weight}: The weight value, which can be chosen between \-100% and 100% (excluding 0).


You can configure boost and demotion strategies separately for each associated dataset in the application. In the search configuration interface, under the dataset tab in the configuration panel, click [Boost and Demotion] \> [Add Rule] to create a new boosting or demotion rule.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Explanation</div>


<div data-tips="true" data-tips-type="default">You can configure multiple boosting and demotion rules for a single field; the weight coefficients will be added together, for example:</div>



* <div data-tips="true" data-tips-type="default">Boost items priced over $500 by 50%</div>


* <div data-tips="true" data-tips-type="default">Boost items priced over $1,000 by 60%</div>



<div data-tips="true" data-tips-type="default">When an item meets both conditions of price over $500 and price over $1,000, its final uplift weight is 110% (= 50% + 60%).</div>


<span id="dbf82677"></span>
## Boost and Demotion configuration based on attributes

Currently, you can add one conditional selection for a single attribute at a time to apply promotion or demotion. The method to configure the effective scope based on item fields is shown in the table below:


|**Field type** |**Supported operators** |**Accepted target values** |**Condition meaning** |**Example** |
|---|---|---|---|---|
|String (`String`) |equals, not equals |String (`String`) |Adjust boosting or demotion when the string field value equals or does not equal a specific string | |
|List (`Array<String>`, `Array<Int64>`, `Array<Int32>`, `Array<Float>`) |contains |list in the corresponding format |If the list field contains all elements in the target list, adjust to boost or demote |Items containing "suspense" in the film genre are boosted |
|Integer types (`Int32`, `Int64`) |greater than, greater than or equal to, less than, less than or equal to, not equal to, equal to |numeric value |Apply boosting or demotion when the value of an integer field is greater than or less than a specific number |Boosting when the item's release time (UNIX timestamp) is greater than 1761661582 (2025\-10\-28 22:26:22) |
|floating point number (`Float`) |greater than, less than |numeric value |Apply boosting or demotion when the value of a floating\-point field is greater than or less than a specific number |Boosting for items priced above 500 yuan |


<span id="caf63e1a"></span>
## Boost and Demotion configuration based on geographic location

When your business scenario requires dynamic adjustment of search results based on the user's geographic distance, you can achieve this by configuring promotion and demotion strategies based on geographic location. The ranking engine calculates the distance between the user’s geographic location uploaded via the interface and the item's location, then applies the promotion and demotion rules based on the calculated distance.

Before setting the strategy, ensure your item data contains latitude and longitude information and is configured as longitude and latitude attributes. For details on configuring these attributes, refer to [Image & Text Item Dataset](https://docs.byteplus.com/docs/viking-aisearch/Introduction_Image_Text_Dataset)

&nbsp;

**Configure Boost and Demotion rules in the console**

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c863722893d34542958416e611c3096e" controls></video>



&nbsp;

1. Navigate to "Calculated Field" and select "Distance between User and Item".


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ed98f81f5bc04b22a05e727f345f3908) </span>


&nbsp;

2. In the scope condition settings, select "greater than" or "less than" from the dropdown, enter the distance value (e.g., 5000) in the input box, and choose the unit (e.g., meters).


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a04917dcb4514a6e875f6e9a7147a5cf) </span>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Geolocation list processing</div>


<div data-tips="true" data-tips-type="default">When the field storing geographic locations is a JSON object list, if an item has multiple sets of "longitude" and "latitude" coordinates, for example:</div>


<div data-tips="true" data-tips-type="default">"location":[{"long":121.228,"lat":32.112},{"long":124.029,"lat":33.072}]</div>


<div data-tips="true" data-tips-type="default">When calculating the distance to the user, the platform automatically selects the set of coordinates closest to the user.</div>


**Upload user location in the API request**

The API request's `context` object must include the `location` field to upload the user's current geographic location during the search call. For details, see [Context](https://docs.byteplus.com/docs/viking-aisearch/Search#7f9aa6e1).

**Experience location\-based boosting**

After configuring the Boost and Demotion strategy, the Experience Center page will guide you to simulate the user's geographic location on the left to test the effects.

&nbsp;

In the "Test User" area on the right, simulate and test scenarios of user location\-based boost and demotion by specifying user's location:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/95939f762c9e44a4ac941e82fc6a15c6) </span>

&nbsp;


|**Configuration plan** |**Description** |
|---|---|
|Get my location |Get your current location to simulate user testing. This requires you to grant the browser location permission.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Description</div><br><br><br><div data-tips="true" data-tips-type="default">If the platform does not automatically obtain latitude and longitude after clicking "Get My Location," check:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default">Whether the device's location feature is enabled</div><br><br><br>2. <div data-tips="true" data-tips-type="default">Whether the computer or browser restricts the browser’s access to location permissions</div><br><br><br><br><div data-tips="true" data-tips-type="default">If you previously denied location access for the browser, you may need to adjust your browser's site permission settings.</div><br> |
|Specify user location |Manually enter latitude and longitude coordinates (e.g., `longitude: 39.9°`, `latitude: 116.4°`) |


&nbsp;

<span id="39776d7b"></span>
# Configure customized Sorting rules

In real business scenarios, you may have sorting needs beyond query\-content relevance, such as "placing recently added content first" or "sorting products with higher recent sales first." You can use custom sorting strategies to adjust the final search result order.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Custom sorting vs. Post\-search sorting</div>


<div data-tips="true" data-tips-type="default">AI search supports configuring custom sorting adjustment rules in the console and also supports post\-search sorting of the search result list through the "Sort by" parameter in the Search API (see <a href="https://www.volcengine.com/docs/85296/1544974">Search \- Search</a> for details). Differences and applicable scenarios between the two:</div>



* <div data-tips="true" data-tips-type="default"><strong>Customized sorting:</strong> Before returning the search results, the system adjusts the ranking based on defined sorting fields. When multiple items have similar relevance scores, the system performs a local re\-ranking. The final search results comprehensively consider relevance and custom sorting rules, suitable for preset business rules like prioritizing recency or popularity.</div>


* <div data-tips="true" data-tips-type="default"><strong>Post\-search sorting:</strong> After returning the search list, globally rearrange items by the specified fields using sort by and sort order, suitable when users call the interface to reorder search results on the search list page.</div>



You can configure custom sorting strategies on the Console \- Search Experience page:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/98f4f7e0822d47fd8ca33eb8d2ca374d) </span>

&nbsp;

You can configure item sorting fields, sorting rules, and priority among different rules as needed:

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/78089fd699da4d00912df1c216878479" controls></video>


&nbsp;

**Select sorting fields:**  You can choose a String, Float, or Int type field attribute of an item as the sorting basis, such as sales volume (Int) or listing time (a "YYYY\-MM\-DD HH:MM:SS" string).

**Select ascending/descending order:**  Choose ascending or descending based on the field value. Strings sort lexicographically, while numeric fields sort by mathematical value.

Example: Freshness + Popularity

&nbsp;

<span id="9da94021"></span>
# Configure Diversity rules

AI Search recalls items highly relevant to the Search term you enter from the item pool. When items matched by the Search term in the item pool have high similarity, the returned search results may contain clustered similar items, causing user browsing fatigue.

Through the Diversity rules capability, you can customize rules to shuffle the result list before returning to users, improving item diversity in search results. This feature mainly targets operations teams and strategy product managers to help you enhance end\-user browsing experience and search efficiency. This chapter explains how to configure Diversity rules under the Search strategy.

Click [Search result configuration \- Diversity rules], then click [Add Rule] to start creating your Diversity rules:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fc9d1fac315e4afdb2978d2af81ed29d) </span>

&nbsp;

When configuring Diversity rules, you need to fill in the following Configuration items:


|**Configuration item** |**Description** |
|---|---|
|Rule name |enter the rule name to identify different Diversity rules configure a simple and easy\-to\-understand name |
|consecutive item window |define the scattering window, that is, the range within which you need to avoid the consecutive appearance of the same item<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">example</div><br><br><br><div data-tips="true" data-tips-type="default">when setting "continuous item window" = 10 and "display at most quantity" = 5, it means that among every 10 continuous search results , at most 5 similar items appear (whether items are similar is determined by the item conditions below).</div><br> |
|item condition |in the configuration of Diversity rules, the condition for item scattering currently supports two modes:<br><br><br>1. **specify the scattering field, scatter when item Field values are equal:**  you can select the Field that needs to be scattered. When two items have the same value in this Field, scatter these two items (for example, if you select the "ID" Field, after the rule takes effect, items with the same ID in the search results will be scattered). **warning, this Field must exist in the item dataset**<br><br>2. **Specify the Field to Break Apart: when an item’s field value meets a certain condition, break it apart:**  if you want to break apart a certain category of items, select the field and configure the field condition (for example, select the “Tags” field and configure the break condition: “Tags” includes “Clearance items”. After the rule takes effect, it will break apart the clearance items in the search results)<br><br><br>\*<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>1. <div data-tips="true" data-tips-type="warning">if the item field is an array type, only when the array <strong>content and sort order are exactly the same</strong>, will the items be considered identical and be dispersed.</div><br><br><br>2. <div data-tips="true" data-tips-type="warning">the platform does not allow saving new rules with the same "continuous item window" and "item conditions" as existing diversity rules.</div><br> |
|Display at most |Within a window, display at most several **items with the same item field value or that meet the item field condition** “Display at most” cannot be greater than “consecutive item window.”<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Example</div><br><br><br><div data-tips="true" data-tips-type="default">When setting “continuous item window” = 10 and “display at most number” = 5, it means that among every 10 consecutive search results, at most 5 similar items appear.</div><br> |


After configuration, click [Confirm] to save to the configuration panel. After verifying on the Experience center page, click the [Sync changes to API] button to Apply now the configured Diversity rules and apply them to the search service.

&nbsp;

<span id="ad28d011"></span>
# Configure refined operation rules

Viking AI Search supports setting differentiated search strategies for different Search terms (Query). You can define trigger conditions and corresponding execution actions so that the search service automatically executes the specified strategy when certain conditions are met, achieving refined operation intervention in search.

<span id="f0e8f1d3"></span>
## Feature introduction

By default, the search strategy applies uniformly to all search requests. However, in actual business scenarios, different types of Search terms may require different Search strategies to be triggered. For example:


* When users search for a brand, they want to recall and sort only the products of that brand and do not want Item from other brands to be recalled.

* When users enter pure numbers, they want to use only Keyword exact match for retrieval, recalling items that precisely match the product code.


The refined operation function meets these needs through the  **"Trigger conditions \-Specific rules"**  binary tuple pattern. You can create rules in the console, specify trigger conditions and corresponding strategy rules, and the system will automatically execute the corresponding strategy when the search request meets the conditions.

You can use this function in [Search result configuration \- refined operation].

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/a23799c89c524ad2af35b5f95e4de95a) </span>

<span id="12ec075b"></span>
## Configure trigger conditions

Trigger conditions define the effective scene of the rule. You can **configure up to 5** trigger conditions, supporting logical **AND,**  **OR** between multiple conditions:


* Conditions with an "and" relationship must all be met to trigger the rule

* Conditions with an "or" relationship require only one to be met to trigger the rule


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/bb0ffaaac63442b1bfc314abff2fda32) </span>

&nbsp;

The system supports the following 3 types of conditions:


|**Condition type** |**Supported operators** |**Supported condition values and requirements to meet** |
|---|---|---|
|**Search term** |* contains<br><br>* Equals |For example, when the condition is set to "Search term Equals Apple":<br><br><br>* If the request query is 'Apple', the condition triggers.<br><br>* If the request query is 'Apple 17', the condition does not trigger. |
|**Search term type** |* contains<br><br>* Equals |Supports 2 types of judgments:<br><br><br>* Number<br><br>* Numbers + English<br><br><br>&nbsp;<br><br>When the search term includes or equals a Selected type, this condition is considered met.<br><br>For example, when the condition is configured as "Search term type \- Includes \- Numbers + English":<br><br><br>* The condition triggered when the request query is 'iPhone17'<br><br>* The condition does not trigger when the request query is 'iPhone' |
|**Search term length** |* greater than or equal<br><br>* Greater than or equal to<br><br>* less than or equal<br><br>* Less than or equal to<br><br>* interval |The value must be an integer, and the minimum cannot be less than 0.<br><br>The condition is met when the search term length satisfies the requirement set by the condition. |


You can delete unused conditions at any time:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f7c68c7267624e708ec11df0f2ff9a2d) </span>

&nbsp;

<span id="2d97f866"></span>
## Configure specific rules

After configuring trigger conditions, the next step is to continue configuring the differentiated rules to execute under this set of conditions. You can configure multiple rules, and the rules have an **AND** relationship, all of which will simultaneously apply within the specified condition scope.

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/263ca189332f450f96afe04f7c1302c4) </span>

&nbsp;

&nbsp;

The currently supported search rules are as follows. Please note that the configuration of each type of rule is the same as when configuring global effective rules:


|**Rule item** |**Description** |
|---|---|
|**Text search mode**<br><br>(Usage reference: [Text search](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#29e5d6b2)) |Configure the Search mode (Semantic dominant / Keyword dominant / Balanced mode / Custom) and related retrieval parameters |
|**Prioritized item retrieval**<br><br>(Usage reference: [Configure Prioritized Item Retrieval](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#388f9ec4)) |Configure prioritized item retrieval that meets specific conditions |
|**Filter items** |Configure filtering conditions for search results |
|**Boosting and demotion**<br><br>(Usage reference: [Configure Boost and Demotion](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#10e7aa50)) |Configure Boost or Demote policies for item attributes |
|**Sort by field**<br><br>(Process reference: [Configure customized Sorting rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#39776d7b)) |Configure custom sort fields and sort order |
|**Diversity rules**<br><br>(Process reference: [Configure Diversity rules](https://docs.byteplus.com/docs/viking-aisearch/Configure_search_strategy#9da94021)) |Configure diversity rules for search result dispersion |


You can delete useless rules at any time, but at least one rule must be retained, otherwise, saving will fail:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/417576a406a5448bb5b21134b03f32b5) </span>

&nbsp;

<span id="cf896f4f"></span>
# Customize Synonym groups

AI search uses semantic vector matching. The model has already learned features of consensual phrases with similar semantics, which can solve general synonym matching needs to some extent (for example: "Apple Inc." and "apple"). However, for synonym matching of technical terms or domain\-specific vocabulary, it is recommended to supplement the configuration with a custom synonyms list to ensure retrieval accuracy and completeness.

The platform supports **synonym group** configuration. Multiple words within the same synonym group are treated as "mutual synonyms." When a user inputs any word from a synonym group, items containing other words from that group are considered relevant and will be recalled.

Click [Query configuration \- Synonym settings] to start building your industry or brand\-specific vertical synonyms list:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ab0c7b7337c14558bbc1b3769b82d47c) </span>

&nbsp;

Note that **a word can only exist in one unique synonym group**. Duplicate configurations confuse the system in determining the correct synonym mapping. The system will prompt a warning for duplicates upon saving:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c805d16fa5b94dca9b2c910604179435) </span>

&nbsp;

After configuration, click [OK] to save to the configuration panel. After verifying on the experience page, click the [Sync Changes to API] button to activate the synonym rules immediately and apply them to the Search service.

&nbsp;

<span id="3f11d811"></span>
# Search Typo Correction

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8c75dea9abcc4ba19dfc0f9073800106) </span>

Viking AI Search provides automatic keyword correction in the search box experience. When users input spelling or common errors, the system automatically identifies and suggests corrections to improve search result accuracy and user experience.

Two configuration options are available under Query Configuration \> Typo Tolerance when the switch is turned on:


* **Autocorrect:**  When the system detects spelling or common errors in search terms, it automatically corrects them to the right words and returns corrected search results directly without user confirmation.

* **Suggestion: ** When the system detects errors in search terms, it searches using the user’s original terms while returning correction suggestions through the Search API. You can display a prompt at the top of the page such as \*"Did you mean to search: {corrected term}?"\*, allowing users to decide whether to accept the correction.


Regardless of the mode selected, the Search API will always return the corrected suggestion in the response body for flexible UI integration. You can integrate this feature according to your search interface design and user experience. See details: [Search](https://docs.byteplus.com/docs/viking-aisearch/Search).

&nbsp;

<span id="47bd3d38"></span>
# Search Query Completion

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/48b8826a081140c9965d5aa777d1d541) </span>

&nbsp;

Viking AI Search supports automatic character\-based suggestion and recommendation of related search terms in the search box experience. This boosts user input efficiency, helps users quickly find desired content, and amplifies the effectiveness and value of your search scenarios.

Two configuration options are available under Query Configuration \> Autocompletion:


* **Max Completion Terms:**  The maximum number of suggested terms returned per request. Default is **10**.

* **Minimum characters to activate auto\-complete:**  This defines how many characters the user must enter before triggering a search completion request. The default is 2, meaning autocompletion and related search recommendations are not triggered when the input is less than 2 characters, but are triggered when the input is 2 or more characters.


**Item Dataset fields:**  Values from item fields you have designated as "Autocomplete" in your dataset configuration.

You can also call this service through the search term completion API and integrate it freely according to your search interface design. See details: [Query Autocomplete](https://docs.byteplus.com/docs/viking-aisearch/Query_Autocomplete).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To experience more Viking AI Search capabilities, click to go to: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search engine, integrated intelligent engine for enterprise search and recommendation</a></div>


&nbsp;

<span id="c5e53777"></span>
# Search result facet

Viking AI Search supports **Facets ** of search results by specified fields. After enabling this feature, each search request returns the matching count numbers for each enumerated value under the specified field along with the search results, making it easier for you to build interactive components such as classification tags and sidebar filters on the search results page. This helps users quickly narrow down the search scope and improve search efficiency.

<span id="cf8dd1a6"></span>
## Feature introduction

In search scenarios, users typically need to further filter results using classification tags or filter panels besides browsing the search result list. For example:


* In e\-commerce scenarios, after searching for "mobile phones," the sidebar displays classification tags such as brand (Apple: 120, Huawei: 70) and price range (0\-2000: 50, 2000\-5000: 80) for users to filter results.

* In document search scenarios, after searching for keywords, classification tags for document types (Knowledge: 30, Video: 15, API: 8) appear at the top of the page to help users quickly locate the target content.


The facet function supports such scenarios. You can specify one or more fields in the item dataset as aggregation dimensions. The system automatically counts the number of matches for each enumerated value under each dimension during search and returns them along with the search results.

<span id="d820041a"></span>
## Supported data types for facet

The facet function supports the following data types:


|**Field type** |**Aggregation method** |**Description** |
|---|---|---|
|**String** |aggregate by original value of field |group and count directly by string value, such as brand name, category name, etc. |
|**Boolean** |aggregate by original value of field |group and count by true/false value. |
|**Array<String\>**  |aggregate by original value of field |each element in the list independently participates in aggregation and counting. for example, for the tags field `["AI", "Search"]`, "AI" and "Search" are counted separately. |
|**Int** |Aggregate by field original value / aggregate by value range |Supports grouping directly by numeric value and also supports setting a value range for bucket statistics. |
|**Float** |Aggregate by field original value / aggregate by value range |Same as above. |
|**Array<Int\>**  |Aggregate by field original value / aggregate by value range |Each element in the list participates independently in the aggregation, supporting both original value and range methods. |
|**Array<Float\>**  |Aggregate by field original value / aggregate by value range |Same as above. |


> **The Object type field** is temporarily unsupported for faceting.


<span id="b51374d1"></span>
## Prerequisites

Complete the following configurations before using this function:


1. **New application** has been created and associated with an item dataset.

2. ***Filterable/Faceting*** ** must be enabled in the dataset field configuration**: go to the dataset field configuration page of the application and check the fields needed for aggregation as Filterable/Faceting. Only fields with this option enabled can be selected as aggregation fields in the experience center.

3. **Index construction done**: after selecting the field, the system will build an index for it, making it available for use once completed.


&nbsp;

<span id="5582e801"></span>
## Configure facet rules


1. Enter the target new application, click **Experience center \> Search experience**.

2. In the strategy area, find **Facet** and click **Add Rule**.


&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/562de4ed86b84b71b5a40589def16b1b) </span>

Select the item field to aggregate and count in the rule. The optional fields list includes fields marked as <Filterable/Faceting\> in the dataset field configuration.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0470ead8e46d45f097733560042353d6) </span>

The parameters to configure vary according to the selected field’s data type:

**String type fields (String, Boolean, Array<String\>)** 

For this type, only classification and counting by field enumerated values are supported. Configure the maximum number of enumerated values returned by the API:


|**Configuration item** |**Description** |**Default value** |**Value range** |
|---|---|---|---|
|Maximum number of returned enumerated values |Set the maximum number of enumerated value aggregation results returned per field. |10 |1 ~ 50, integer |


**Numeric type fields (Int, Float, Array<Int\>, Array<Float\>)** 

Numeric type field supports two aggregation methods. You need to select the aggregation method first, then configure the corresponding parameters:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5e47ee6d57174878b0ceb45cdd6cd8fe) </span>


|**Aggregation method** |**Description** |
|---|---|
|**Value range** |Preset numeric bucket ranges; the system counts matching quantities within each bucket by range. Use this when you need to price, rating, and other continuous numeric values. |
|**Enum value** |Directly group and count based on the original numeric values of the field. Use this when you need to enumerated values with fewer discrete values. |


When selecting **Value range**:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fda832768431474e9e583829637b92f6) </span>


|**Configuration item** |**Description** |**Default value** |**Range quantity** |
|---|---|---|---|
|Numeric bucket range |Configure the numeric value range for aggregation statistics, each range consists of a start value and an end value.<br><br>The range is a **left\-closed right\-open** range. |One group of range must be filled in by default |at least 1 group, up to 50 groups |


When selecting **Enum value**:

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fc36206e06ae446f96025aeef6b8002b) </span>


|Configuration item |Description |Default value |Range |
|---|---|---|---|
|maximum number of returned enum values |Set the maximum number of enumerated value aggregation statistics returned per field. |10 |1 ~ 50, integer |


<span id="049f9056"></span>
#### Save and apply

After configuration is complete, click **Confirm** to save the rule. After verifying the search effect on the experience center page, click the **Sync changes to API** button to apply the aggregation statistics rule to the search service.
