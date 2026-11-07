---
title: "Enabling Multimodal Search for a Stock Media Platform with Viking AI Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Enabling_Multimodal_Search_for_a_Stock_Media_Platform_with_Viking_AI_Search"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">This document is a detailed implementation guide to <strong>Multimodal Search configuration</strong> in Viking AI Search, intended for the business, product, operations, and technical teams of <strong>stock media platforms (such as general photo libraries, icon and UI assets, creative background assets, etc.)</strong>. Based on the specific needs of asset retrieval scenarios, we will systematically introduce the best practices for the entire process, from data preparation and search mode configuration to sorting strategy optimization.</div>


* <div data-tips="true" data-tips-type="default">To learn more about Viking AI Search product capabilities, see: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the integrated intelligent engine for enterprise search, recommendation, and Q&A</a>.</div>



An excellent stock media platform must not only have abundant stock images but also the capability to accurately match them to user search intent. By completing the configuration in this guide, you can achieve the following business results and improve the item retrieval rate for stock images:


<columns>
<columnsItem zoneid="WF69kQgIgJ">

**Keyword image search**


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dd9d95c8aa6a42438858e3ea120185ba) </span>



</columnsItem>
<columnsItem zoneid="IGJI9z7mDs">

**Natural language image search**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9961563aaf8c49ec83ee43fea2c66f0d" width="236px" /></div>




</columnsItem>
<columnsItem zoneid="yZ1oQozJOV">

**Search by image**


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5582dd075ffd46e5898cf0b0ac5c8646" width="234px" /></div>




</columnsItem>
</columns>


<span id="f0034129"></span>
# One: Data preparation

Before you configure the search system for your stock media platform, **filter your fields first** instead of uploading all of them. **Invalid fields increase your token costs and interfere with the large model's reasoning**.

You can remove large, low\-value fields (such as large blocks of HTML source code and Base64\-encoded images) and retain the data fields that help the search model understand content semantics and perform a multimodal search.

<span id="54c1588e"></span>
## 1. Item dataset

The item dataset contains **data for stock images, such as their title, tags, publication date, and author**, and is the foundation for building a multimodal search engine.

The following is a list of **recommended core fields for item data on a stock media platform**. Including the key information below is recommended to improve overall performance.

If some fields are missing, filter by your existing fields before uploading.


|<div style="text-align: center"><br><strong>Example field name (Your actual field names do not need to match these exactly)</strong></div><br> |<div style="text-align: center"><br><strong>Purpose and recommended scenarios</strong></div><br> |
|---|---|
|**post_id** |The unique identifier for the stock image. Prevents duplicates and allows the system to update content and record user click events. |
|**images** |Stock image. The system analyzes image content to support text\-to\-image and image\-to\-image search.<br><br>Note: **Image URLs must be publicly accessible**, otherwise the image will not be displayed. It is recommended that **images are clear, feature a prominent subject, are at least 300x300 pixels, and are 5MB or less**, as this can affect processing efficiency and quality. |
|**post_time** |The release time of the stock images. Use to prioritize new stock images or filter out expired content. |
|**user_id** |The unique identifier of the publisher. Use for author\-based search strategies (such as boosting official or editor\-recommended stock images) or content diversification (to avoid too much content from the same author in search results). |
|**username** |The publisher's username. Use for searching by creator or providing an autocomplete feature in the search box. |
|**title** |The title of the stock images. Used for precise item retrieval based on keyword matching and semantic analysis. |
|**content** |Description of the stock images. The system analyzes the core meaning of the description to find semantically matching stock images. |
|**comments** |Number of comments. Reflects the engagement level of the stock images and can be used to filter for popular content or help gauge community sentiment. |
|**likes** |Number of likes. A key popularity metric that measures the popularity of stock images and often serves as an important weighted feature for search and sorting models. |
|**shares**<br><br> |Number of shares. Represents the distribution value of the stock image. Stock images with a high number of shares usually have greater viral potential and can be used for weighted search. |
|**tags** |List of tags associated with the stock image. Used for content retrieval by category, matching user interest tags, and item retrieval for specific audience segments. |
|**score_final** |Overall score of the stock image. Reflects the overall quality of the stock image. It can be used to filter for high\-quality stock images or as a key factor in sorting. |
|**downloads** |Download count. A core popularity metric used to measure the practical value and popularity of stock images. It is often used as an important weighted feature in search sorting models. |
|**price_type** |The price type of the stock image (e.g., free, paid). Used to distinguish between paid and free content. Supports configuring priority item retrieval or boost strategies for paid stock images. |
|**file_type** |The file format of the stock image (e.g., JPG, PNG, SVG, EPS). Used to distinguish between stock images of different formats. Supports configuring boost strategies for specific formats (e.g., for vector stock media platforms). |
|**keywords_count** |Keyword count. Detects suspected keyword stuffing and supports configuring anti\-spam strategies (e.g., demote when the keyword count is greater than 50). |


<span id="603a066c"></span>
## **2. Sample data preparation**

Before importing all your data, run a connectivity test with 50\-100 representative data entries to verify that the item ingestion and user event association process runs smoothly.

<Attachment link="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d8426b06169b4e3ea102de95989ef6e5" name="素材平台样例物品数据集.jsonl">素材平台样例物品数据集.jsonl</Attachment>


<span id="eb1fc44d"></span>
# Two: Build a multimodal search engine for a stock media platform in 4 steps

Following the [Volcano Engine quick start process](https://www.volcengine.com/docs/85296/2222393?lang=zh), we simplify building a complex recommendation system into four core steps.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5c9926f1c6dd4242968709b20b6dbfad) </span>

&nbsp;

<span id="4e00a1a6"></span>
## Step one: New application


<columns>
<columnsItem zoneid="tO6jcJJ4zW">

1. Log in to the [AI Search console](https://console.volcengine.com/aisearch/platform/region:aisearch-platform+cn-beijing/home/app-list) and click New application.

2. Enter the application name.

3. Select the **Stock media platform** template. This will preload the policy configuration for this scenario.

</columnsItem>
<columnsItem zoneid="lnK1AplQCO">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5c353c9cdf8b4b958c4292d6c0c3dad4" width="2940px" /></div>


</columnsItem>
</columns>


<span id="508486ea"></span>
## Step two: Import data

<span id="3d946354"></span>
### 1. Create dataset


<columns>
<columnsItem zoneid="baYNYUHIZ3">

* Enter the dataset name.

* Select the dataset type. Item dataset can be used to upload structured data, and Documents can be used to upload unstructured data. **To build a multimodal search engine, select Item dataset.** 

* Select the data type. If your dataset includes multimodal content, **you must upload image/text content and video content to their respective item datasets separately.** 

* Directly upload a **sample JSONL file**, or upload data via JSON code.

</columnsItem>
<columnsItem zoneid="QPzcLSA731">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/32743de3cfbf4a339cc789f11b26db2e" width="2935px" /></div>


</columnsItem>
</columns>


<span id="ee437643"></span>
### 2. Configure fields


<columns>
<columnsItem zoneid="cUTnNSJkFW">

* After the data import, the large model scans the sample data to infer data types, attributes, meanings, and index configurations. This takes about two minutes.

* You can use the table below to **manually calibrate or delete fields.** 




</columnsItem>
<columnsItem zoneid="kxezaVBug0">

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2f694a2d1ad64ec2b12b9206e5498560" controls></video>


</columnsItem>
</columns>



|<div style="text-align: center"><br><strong>Example field name (Your actual field names do not need to match this exactly)</strong></div><br> |<div style="text-align: center"><br><strong>Attribute recommendation</strong></div><br> |<div style="text-align: center"><br><strong>Recommended application configuration</strong></div><br> |
|---|---|---|
|**post_id** |Unique identifier (**You must specify one**. It is the primary identifier for the entire system. All data updates and associations rely on this ID.) |Filterable |
|**images** |Image URL (**The stock image link is displayed as an image in the console only when it is set as the Image URL.** ) |Searchable (Text), Searchable (Image)<br><br> |
|**post_time** |Release time |Filterable |
|**user_id** | |\- |
|**username** | |Searchable (Text), Autocomplete |
|**title** | |Searchable (Text), Autocomplete |
|**content** | |Searchable (Text) |
|**comments** | |Filterable |
|**likes** | |Filterable |
|**shares**<br><br> | |Filterable |
|**tags** | |Searchable (Text), Filterable, Autocomplete |
|**score_final** | |Filterable |
|**downloads** | |Filterable |
|**price_type** | |Filterable |
|**file_type** | |Filterable |
|**keywords_count** | |Filterable |



<columns>
<columnsItem zoneid="VCt8Mq5eVd">

When you click Next, an error handling prompt appears, **but this does not mean there is a problem with your data**. To avoid unnecessary token consumption, you can choose between two billing methods:


*  **"Not processed, marked as invalid data": Recommended for stock media platforms.**  If image assets are your core assets, select this option. After selecting this option, if an image in a data record has an issue, the entire data record is not processed.

* "Continue processing and skip only problem images": Select this option if you allow users to upload only image content or if text content is more important. After selecting this option, the image field in the resulting data might be empty, but other fields (such as content, comments, etc.) are complete.

</columnsItem>
<columnsItem zoneid="gyNjmC2vxS">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/339bcb2735c14577b44abc4c02401d58" width="1280px" /></div>




</columnsItem>
</columns>


<span id="a5413b75"></span>
### 3. Configure display settings


* Populate the fields you want to return as follows. This is just a diagram of the console; you can configure the actual page yourself.



<columns>
<columnsItem zoneid="dMpCds52rg">

&nbsp;

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/dd7b99b6c62c45f6b7a0cccdf27c0c40) </span>



</columnsItem>
<columnsItem zoneid="G84mEArT1F">

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1272ea706f334927afafb6ab4c39e982" controls></video>


</columnsItem>
</columns>



<columns>
<columnsItem zoneid="Y5gtIUBSVu">

* Click Done and the system will start the data upload, which may take about 10 minutes per 1,000 data records.

* When complete, **the dataset Status changes to "Configuration active," a "Configuration updated" notification appears in the top\-right corner, and the Valid items count shows the total number of items**.




</columnsItem>
<columnsItem zoneid="zb95QDb1yO">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/85b3380b7ec141938b8c7dd20853dfe0" width="398px" /></div>


</columnsItem>
</columns>


<span id="ef035bcd"></span>
## Step three: configure multimodal search

The following are some of the most common experience configuration capabilities for a stock media platform, which you can configure based on your business requirements:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Avoid a one\-size\-fits\-all "template" configuration</strong>. The optimal search strategy may differ significantly for a stock media platform's various sub\-scenarios (such as general photography libraries, UI icon stock images, creative background stock images, etc.), different stock image types (real photos / vector icons / creative backgrounds), and different user groups (designers / social media creators / corporate buyers).</div>


<div data-tips="true" data-tips-type="default">For example, a general photography library might prioritize "visual consistency" and "high resolution", whereas UI icon stock images might prioritize "format standardization (e.g., SVG/EPS)" and "precise keyword matching", and creative background stock images might focus more on "style matching" and "copyright compliance".</div>


<div data-tips="true" data-tips-type="default">Therefore, we strongly recommend that you <strong>treat search strategy configuration as a continuous iterative process and use online search user event data and user download conversion feedback to scientifically evaluate and select the optimal strategy</strong>.</div>


<span id="133914e0"></span>
### **1. Search mode configuration: precisely match your stock media retrieval needs**

The search mode determines how the system understands and matches user search intent and is the foundation for effective search results. Based on the characteristics of a stock media platform (e.g., images, videos, design assets), the following are the configuration options for each mode:


|Scenario name |Search type |Mode selection |Rationale |
|---|---|---|---|
|**General photography / real photo library** stock media platform |Text Search configuration<br><br> |Define custom weighting<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/fec3ff20b4624df59c69e5d35ab14f78" width="188px" /></div><br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6f16f6ca6f40436a8091619c9476f37d" width="190px" /></div><br><br><br> |**Data type weighting (Text 0.4 / Image 0.6)** : photographs emphasize **visual composition**. **Increase the "Image" weight** to let the model understand the "visuals behind the words" instead of strictly matching the image description.<br><br>**Text search weighting: (Semantic 0.6 / Keyword 0.4)** : when a user searches for "sadness," the image tags may not include the word "sadness," but the image shows a person crying. **Semantic matching resolves these types of conceptual searches.**  |
||Image search configuration |Visual similarity search<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/641578724a564a5f8c2fb8f108197cc4" width="220px" /></div><br><br><br> |Prioritizes matching the **overall visual features** of the image to accurately reproduce the visual style of a reference image, meeting the visual consistency requirements for photographic stock images.<br><br> |
|**Icon / UI asset / vector illustration** stock media platform |Text Search configuration<br><br> |Define custom weighting<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/8f724ddb9a354e10af2bb90e2b354265" width="208px" /></div><br><br><br> |**Data type weighting (Text 0.8 / Image 0.2):**  Icon libraries usually have a standardized naming system (e.g., `icon_home_fill`). Strong reliance on text metadata matching is most accurate, while generalized associations from images can lead to less relevant results.<br><br>**Text search weighting: (Semantic 0.2 / Keyword 0.8)** : "Precise targeting" is required. When users search for "Home," they do not need semantic associations to "Family" or "House," only the icon named "Home." |
||Image search configuration |Item similarity search<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/cea6026d7c0141c1ab01c01c81d9b9e1" width="198px" /></div><br> |Ignore background colors and focus on **line shapes and contour structures**. For icons, strictly match **geometric features**.<br><br> |
|**Creative/Background** stock media platform |Text search configuration<br><br> |Semantic dominant (or define custom weighting)<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2038572b44c3465ea354429ff708e601" width="206px" /></div><br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/afba0d44f94945269faf80b354b3af5f" width="190px" /></div><br><br><br> |**Data type weighting: Text 0.2 / Image 0.8**: in this scenario, text descriptions are scarce (e.g., "cyberpunk," "minimalist and cold"). It must heavily rely on the model's understanding of **image visual features**.<br><br>**Text search weighting (Semantic 0.9 / Keyword 0.1):**  keywords are almost ineffective. It relies entirely on semantic vectors to capture the connection between the "abstract adjectives" from the user's input and the "visual style" of the image.<br><br> |
||Image search configuration |Define custom instructions<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/d1d013c49abf401db5460e49da852660" width="180px" /></div><br><br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/35ce61fff46c410f831e38bbbc30a9f0" width="186px" /></div><br><br><br> |Define custom instructions recommendation: ignore specific objects and focus on **color distribution, texture and Material, and artistic style** (e.g., oil painting, 3D rendering, watercolor), as well as **the mood of the image**. |


<span id="47fcffaf"></span>
### **2. Returned item quantity configuration: optimize the user browsing experience**


<columns>
<columnsItem zoneid="Ud2lmeGRRr">

Appropriately setting the number of returned results balances system response speed (performance) with the user's need for in\-depth browsing.


* Recommendation: **Set the initial value to 200\-400 for a cold start**. This is an "industry standard value" that best balances performance response speed and content richness. Subsequently, observe the user's "pagination depth" (or scroll depth). If users frequently scroll to the bottom and run out of images, gradually increase the value to 600 or 800. Otherwise, decrease it.

* **When increasing the value, monitor the performance overhead.**  If setting the value to 1000 causes the search API response time to exceed 500ms (users on image sites have zero tolerance for lag), reduce it to 400 or 200. Smoothness is more important than the number of Items returned.

</columnsItem>
<columnsItem zoneid="Zs5Izs6yyJ">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ffeec068adfa41e88904e3d0cf7eeaf7" width="768px" /></div>


</columnsItem>
</columns>


<span id="99707c34"></span>
### **3. Item retrieval strategy configuration: build a multi\-dimensional stock media retrieval system**

The item retrieval strategy determines how the system quickly filters a relevant candidate set from a massive stock media library, which is the quality guarantee for search results.

The core logic of  **"Prioritized item retrieval"**  is: **add privileged images to the candidate pool regardless of their relevance scores**. Below are some common Prioritized item retrieval configurations for stock media platforms:


|**Configuration name** |**Recommended conditions** |**Purpose** |
|---|---|---|
|**Holiday trends** |`tag` found in `Halloween`<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/045815a8cebf4566b8c7dba9c55cfefc" width="268px" /></div><br><br><br> |Two weeks before a holiday (e.g., Halloween), enforce item retrieval for images where the `tag` includes `Halloween`. |
|**High\-quality priority retrieval**<br><br> |`download` **Greater than** `2000`<br><br> **OR**<br><br>`score_final` **Greater than** `4`<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/15ae42f163f643c994e86453283086b6" width="266px" /></div><br><br><br> |Prevent search results from being overwhelmed by low\-quality UGC content and ensure strong visual impact above the fold. Display high\-quality content even when there are no search results.<br><br> |
|**Paid priority retrieval** |`price_type` found in `Paid`<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0df5e92cc4db4adba96ff1ce834ce54d" width="266px" /></div><br> |Ensure paid content is not displaced by free content to increase revenue.<br><br> |


<span id="f6607016"></span>
### **4. Rerank strategy configuration: Making high\-quality stock images stand out**

The rerank strategy determines the final display order of item retrieval results and serves as a further optimization of the search results.

<span id="cc65ced3"></span>
#### 4.1 Multi\-modal reranking


<columns>
<columnsItem zoneid="a2hxuDUj7d">

* Using ByteDance's proprietary **Rerank model**, **this feature reranks some results to display stock images that are more relevant to the user's search terms**. This optimizes the user's search experience, and we recommend enabling it.

* We recommend **setting the number of items to rerank to 1\-2 times the number of items displayed on the first screen, typically 20**. This improves the quality of the first\-screen stock images while keeping loading times within an acceptable range. Do not indiscriminately increase the number of reranked results, as this leads to increased loading times and token consumption.

</columnsItem>
<columnsItem zoneid="yPfy4h88r7">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3d25608923d742ae8247e19482543f75" width="294px" /></div>


</columnsItem>
</columns>


<span id="935ae9e6"></span>
#### 4.2 Boost and demotion

In addition to matching search results with user queries, you can dynamically adjust the sorting weight of stock images based on attributes like subscription type or download count. These weight scores are cumulative. Below are some common weight adjustment configurations for stock media platforms:


|Strategy category |Configuration diagram |Effective scope |Configuration |Effect description |
|---|---|---|---|---|
|Boost high\-download stock images |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3deca7587cca4a40bb8c350b0a22426d" width="1274px" /></div><br> |`download` **Greater than ** `2000`<br><br> |Boost 5%\-10% |Ensure the top search results are high\-quality stock images.<br><br> |
|Boost high\-quality stock images |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b087e84544234d0eaf44ff2084d2264f" width="1276px" /></div><br> |`score_final` **Greater than ** `4`<br><br> |Boost 5%\-10% ||
|Boost paid stock images |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4339701d1d2e40fbaa480bcaf9be0a3c" width="1272px" /></div><br> |`price_type` **found in ** `Paid`<br><br> |Boost 20% |Intersperse paid stock images in the first few rows of search results to attract users to subscribe or make single purchases. |
|Boost official/editor\-recommended stock images<br><br> |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/382a024fe88043548e1fc637507977d6" width="1270px" /></div><br> |`username` **Equals ** `official` |Boost 20% |Images handpicked by the operations team represent the platform's highest standards and are boosted to the top. |
|Boost specific stock image formats |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3e1a13deceee451e8db530ec73ff7b7c" width="1024px" /></div><br> |`file_type` **Equals ** `svg` |Boost 50%<br><br> |**Applicable for vector stock media platforms**. When users search for icons, editable vector formats are much more valuable than bitmaps (JPG/PNG). |
||<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/63d6a065a70347928d01da8ae3014691" width="1024px" /></div><br> |`file_type` **Equals ** `eps` |||
|Demote low\-quality stock images<br><br> |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9fd81677527b4903b80a76cf9ce5c012" width="1274px" /></div><br> |`score_final` less than `2`<br><br> |Demote 20%<br><br> |Moves low\-quality content to the bottom.<br><br> |
|Demote stock images with low downloads |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/23e8ff2855c540f391f521525b2163a1" width="1270px" /></div><br> |`download` **less than ** `10` |||
|Demote stock images suspected of keyword stuffing |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5d6b0e9acc654187bf6fe9ee9384d903" width="1024px" /></div><br><br><br> |`keywords_count` **greater than**`50` |Demote 50% |Anti\-spam. Some uploaders add 50 irrelevant tags to an image to get more traffic. Heavily demote items to prevent irrelevant results. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>If a stock image has low relevance to a user's search query, it may be filtered out during item retrieval, and the boost will not take effect</strong>. Therefore, for items that need to be prioritized, such as new and seasonal stock images, configure both "Boost" and "Prioritized item retrieval". This creates a dedicated item retrieval channel for these items, ensuring that the boost strategy is effective.</div>


<span id="ac540ce2"></span>
#### 4.3 Sort by field

This is the last step in the search pipeline and determines the final sort order when the relevance scores calculated by the algorithm are identical. You can set the priority of multiple sorting rules.


|Priority |Field |Sort order |Configuration diagram |
|---|---|---|---|
|1 |`score_final` |Descending |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c6f6dcf669994cb1be4c441996b48b0d" width="362px" /></div><br> |
|2 |`downloads` |Descending |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/eae77df647ae47198850feee09f22548" width="372px" /></div><br><br><br> |
|3<br><br> |`post_time` |Descending |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/37802063108f455bb9786c165ba8e134" width="382px" /></div><br><br><br> |


<span id="78e54cb1"></span>
### 5. Search guide configuration

&nbsp;


<columns>
<columnsItem zoneid="Q4g8MCZHny">

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f8902037fcf04fa18f3bf42267b97b2d) </span>



</columnsItem>
<columnsItem zoneid="tGOlypTMKB">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0c2c6da58fc84fad81edd57d96146eaa" width="340px" /></div>




</columnsItem>
</columns>


<span id="a1dd4879"></span>
### 6. Search dictionary configuration


<columns>
<columnsItem zoneid="yGJ0bT7ydr">

When a user's search query returns no results, you can use the synonym dictionary to associate the query with existing terms. In addition, special industry terms that need to be associated (such as frosted glass, matte, blur, and Glassmorphism) can also be configured using this feature.

With the help of large models (semantic search), the Synonyms feature of Viking AI Search does not need to include all basic industry vocabulary. It is mainly used to "fill gaps" and "correct biases."

We recommend that you **periodically associate search terms that return unexpected results with existing terms via Synonyms** to enhance the user search experience.

</columnsItem>
<columnsItem zoneid="LhXHm9vLFL">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/70941a6632e145799f8077b3f01bfdc1" width="2096px" /></div>


</columnsItem>
</columns>


<span id="5aa66b08"></span>
## **Step Four: Upload full data and integrate the Search API**

<span id="060312df"></span>
### **1. Upload full data**


<columns>
<columnsItem zoneid="jL9BjepIYU">

* Click the list of Datasets and find the dataset to which you need to upload the full data.

* Click View to go to the dataset details page.

* Click Data import.

* Item data supports two import methods: local JsonL file import and API import. API import supports Batch import and Real\-time import. For detailed steps, see:

   * [Batch import item data - Global AI search - Volcano Engine](https://www.volcengine.com/docs/85296/2123240?lang=zh)

   * [Real-time import and update of item data - Global AI search - Volcano Engine](https://www.volcengine.com/docs/85296/1544970?lang=zh)

</columnsItem>
<columnsItem zoneid="Y3t5pXovvp">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/beab60c5ca454778bc5591d304bba8eb" width="2126px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ce59064ce0734ac1949172b2bf3ec9b2" width="2936px" /></div>


</columnsItem>
</columns>


<span id="20db20a5"></span>
### **2. Search feature launch**


<columns>
<columnsItem zoneid="o4av5jAfOI">

After the full data has been imported and applied, you can integrate the configured search strategy into your business system to enable the AI search feature for your users.


* **Sync configuration to the API**: In the upper\-right corner of the Recommendation scenario configuration page, click the  **"Sync changes to API"**  button and select the configuration to publish.

</columnsItem>
<columnsItem zoneid="oHsallyuTU">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c5d970f3bd114bdbbc27fde8be7fb59b" width="2938px" /></div>


</columnsItem>
</columns>



<columns>
<columnsItem zoneid="pWBwyjP9PM">

* **Create and integrate an API Key**:

   * Create a new API Key and associate it with the search strategy you want to launch.

   * Select "Search", copy the provided **API call sample code**, and give it to your technical team.

   * The technical team needs to integrate the Search API into your application's front\-end page to get search results and display them to users.

</columnsItem>
<columnsItem zoneid="c7pK2AaUCd">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9fc67efb86c145da9e899cd00d740287" width="3578px" /></div>


</columnsItem>
</columns>


<span id="ee794152"></span>
### **3. Search feature integration logic**

Viking AI provides a standard API to integrate the built capabilities into your app, mini program, or webpage. Below is a summary of the API invocation.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you are a technical user, view <a href="https://www.volcengine.com/docs/85296/1544974?lang=zh">Search \- Search</a></div>


<div data-tips="true" data-tips-type="default">If you are a business user, see the following content.</div>


To create a fast, secure search experience that is highly tailored to your business on the stock media platform, we strongly recommend adopting the three\-tier architecture of **Front\-end interaction \-\> Business back\-end forwarding \-\> AI search service**.

<span id="5cac0383"></span>
#### 3.1 Complete data flow path


* **Frontend initiates smart search**: A user enters search terms on the web or app, or uploads a reference image to perform an image search.  **(Suggestion: The frontend should pre\-compress images before uploading to ensure that each request is strictly within the 10 MB system limit.)** 

* **Backend encapsulation and authentication**: After receiving the frontend request, the backend constructs a POST request to the AI Search API. In this stage, the backend must attach an API key for security authentication and inject required system\-level parameters, such as the `dataset_id` to search and the current user's `user_id`.

* **Engine performs multi\-channel item retrieval**: The AI Search service receives the request, extracts features from the text query or the Base64\-encoded image, performs millisecond\-level matching and retrieval in your image and text dataset, and returns JSON data containing a list of results.

* **Backend data processing and frontend rendering**: After receiving the raw response from the AI engine, the backend can trim or format the data as needed (for example, by extracting only the `display_fields` required by the frontend or assembling pagination information) and then return it to the frontend. After parsing the data, the frontend renders it as a rich media interactive interface (such as a waterfall flow of stock image cards or a video preview list) and dynamically provides the user with spelling correction suggestions based on the `spell_correction` field.


<span id="e4bf9362"></span>
#### 3.2 Why is it required to route requests through the backend?

Although the frontend can technically make requests directly to the AI Search API, in a real production environment, it is essential to route them through your backend as a gateway. This is based on the following key considerations:


*  **🔒 Maintain a baseline for asset security**: Hardcoding API Keys or Access Keys in front\-end code creates an extremely high risk of exposure, which can easily lead to malicious use of your API. Proxying requests through your back\-end is the most basic line of defense for hiding secret keys and protecting system security.

*  **🛡️ Unified control of business rules and permissions (Filter mechanism)** : The front\-end should focus on expressing user intent, while the back\-end controls business filtering rules. For example, when sending a request to the AI engine, the back\-end can enforce `filter` conditions, such as retrieving only `Stock images` with a "published" status, or filtering copyrighted image\-text libraries based on the user's VIP level. This decoupling ensures the simplicity of the front\-end code and the security of system data.

*  **👤 Accurate user behavior collection and context injection**: The back\-end injects the current logged\-in user's `user_id`  into the request body. This helps you accumulate reliable system operation logs and user search paths, providing a data foundation for future personalized content delivery.

*  **🚦 Bandwidth optimization and traffic anti\-abuse**: Image base64 encoding is typically large in size. The back\-end can rate\-limit user image searches and intercept abnormally large concurrent requests, thereby protecting the overall availability of the system.


<span id="ac5409f8"></span>
# **Three, Common issues and optimization recommendations**

<span id="d143a12d"></span>
### 1. Document search returns empty results


* Check if the `Searchable (Text)` and `Searchable (Image)` fields are adequate

* Check if the filter condition parameters are correct, see [Search - Search](https://www.volcengine.com/docs/85296/1544974?lang=zh#aead416b) for details


<span id="da2f822b"></span>
### 2. Image search returns empty results


|Troubleshooting item |Troubleshooting logic and Recommendation |
|---|---|
|Confirm the image search feature is enabled |Check the "Searchable (Image)" option in the configuration interface. If unchecked, the Image's embedding will not be stored, and only the Text derived from image analysis will be indexed for search. No data re\-upload is required. On the configuration page, click "Edit schema" and then submit.<br><br> |
|Whether the image index was created successfully |Check if the linked item dataset has the expected number of valid items. Primarily, check if the image index was built successfully. For items that failed to index, go to Dataset details to view if the item has error messages, such as Image fetch failed or incorrect image format. Common reasons for image indexing failure include:<br><br><br>* Validation failed: The image does not meet preprocessing rules. An error code beginning with "Image" is recorded in the Mongo status table.<br><br>* Image inaccessible: The Image URL has issues such as access timeouts or CDN blocks. These are uniformly recorded as error code 10010.<br><br>* Fangzhou TPM/RPM limit exceeded: This can cause indexing failure (low probability; a retry mechanism is in place). |


<span id="0a735f6b"></span>
### 3. Long search time

Long search times are likely caused by excessive input information.

In particular, check if any `Searchable (Text)` fields are large. Like the following fields


|**Checklist** |**Troubleshooting logic and recommendations** |
|---|---|
|Multi\-modal reranking<br><br> |Whether the multi\-modal reranking count is too high. Recommendation: Configure to 20.<br><br><div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f8506ba8579b4108a6116ff3610e1ee2" width="224px" /></div><br><br><br> |
|Whether there are large fields used for document search |<div style="text-align: center"><br><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/86dbd6397dec4c57a8d558728f0fb71f" width="374px" /></div><br> |


&nbsp;

<span id="7718e159"></span>
### 4. Document search: Returns items with low relevance


|**Check items** |**Troubleshooting logic and recommendations** |
|---|---|
|Whether the fields for document search are appropriate |* Select fields with core information, such as Title, category, etc.<br><br>* Do not select non\-core information to prevent too much generic information from diluting core information and returning irrelevant Items. |
|Whether the search matching strategy is appropriate |* If your business focuses more on direct keyword matching, increase the keyword weight in \*\*Text search weighting\*\*.<br><br><br><span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/aefac9042ae8425da39a8c769f2e6547) </span> |


<span id="0d2d7c65"></span>
### 5. Image search: Returns items with low relevance

The current image search logic embeds the query image and then uses it to search the candidate image pool.

You can optimize search performance by adjusting search directives.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b787b197f276453fa86693f2e8eb6620" width="670px" /></div>


<span id="23eff79f"></span>
### 6. Search\-filter not taking effect

If the search filter isn't working, it is likely due to an invalid parameter format. Check your format against the [Search filter parameter specifications](https://www.volcengine.com/docs/85296/1873488?lang=zh#%E8%BF%87%E6%BB%A4%E7%AE%97%E5%AD%90%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To learn more about Viking AI Search capabilities, see: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the all\-in\-one intelligent engine for enterprise search, recommendation, and Q&A</a></div>
