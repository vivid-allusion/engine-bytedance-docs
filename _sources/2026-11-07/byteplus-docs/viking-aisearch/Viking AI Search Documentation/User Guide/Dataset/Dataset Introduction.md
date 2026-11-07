---
title: "Dataset Introduction"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Dataset_Introduction"
---

On our platform, **datasets** serve as the data foundation for all search\-related features. The platform primarily supports two types of dataset:


1. **Item dataset:**  The basis for application search and recommendation. Item datasets contain specific product or content information, categorized into **Image & Text Data** and **Video Data**. To initialize basic application configurations (such as index building), an application must be linked to at least one (and up to three of the same type) item dataset.

2. **User event dataset:**  These datasets record historical user actions and are used for personalized recommendations.


Additionally, both Item and User Event datasets can be **reused across multiple applications**, enabling efficient data sharing and management. This article details the definitions, data structures, configurations, and application methods for these datasets to help you build a high\-quality data foundation for AI search and recommendation features.


---



<span id="f429834e"></span>
# Item Dataset

Item datasets are the core foundation for enabling precise search and intelligent recommendations for structured content such as products, creative assets, news, and videos.

Item datasets consist of two primary types:


* **Image & Text Data:**  Items containing images and related textual descriptions, such as product details, articles, or user\-shared posts.

* **Video Data:**  Content containing video files and their associated metadata, such as short videos, tutorials, movie clips, or news reports.


Item data is **structured** and defined/uploaded using standard JSON format. You can create item datasets to store any structured searchable objects. Standard search and conversational AI queries essentially involve finding and matching information within these datasets.

To achieve higher recall and more accurate results, item datasets support **multimodal content understanding**. The platform performs deep analysis by combining different data types. For example, it synthesizes visual and textual info for Image & Text data, and analyzes video content alongside metadata (titles, descriptions, tags, duration) for Video data. This multimodal approach significantly enhances the platform's deep understanding of content.

<span id="2d7826ca"></span>
## Image & Text Dataset

If you wish to integrate image & text content (such as product info, news, design assets) into a search and recommendation system, or enable content\-based Q&A and information extraction — Image & Text Datasets are a suitable solution.

The system utilizes multimodal preprocessing to parse visual information and textual semantics. This content is then indexed, allowing users to perform searches or ask questions about the image & text content during AI dialogues.

**Applicable Scenarios:** 


* **E\-commerce:**  Helps users find products quickly via image and/or text understanding, personalized recommendations, and intelligent Q&A.

* **Design Assets:**  Enables creators to retrieve images, templates, and illustrations based on style and content.

* **Other Scenarios:**  Internal corporate knowledge bases, academic literature matching, etc.


&nbsp;

<span id="d0cd3ad4"></span>
### **Dataset Description**

The dataset description allows you to provide a summary of the data content, source, and key features (e.g.,  *"Laptop Product Table containing basic info, images, and specifications"* ).

**Viking AI Search Conversational Search Agent** uses this description to understand the scope and theme of the dataset, leading to better judgment during queries and improved accuracy. We recommend providing clear and precise descriptions.

<span id="173726cd"></span>
### **Data Schema**

Image & Text datasets support **flexible schema definitions**. We do not restrict field names; you may customize the JSON structure (field names and types) to describe your data. When creating a dataset in the console, you can upload one or more JSON objects for schema parsing. The built\-in LLM will automatically identify field structures, names, special attributes, and content summaries.

**Field name**: Must start with a letter and contain only letters, numbers, and underscores.

**Field type**: Supports JSON schema types. 


|**Data Type** |**Note** |
|---|---|
|String, Array<String\> |\- |
|Integer, Array<Int\> |Supports both Int64 and Int32 |
|Float, Array<Float\> |\- |
|Boolean | |
|Object, Array<Object\> |Supports up to 3 layers (2 nested objects) |


**Field definition**: During automatic schema parsing, the Large Language Model (LLM) interprets what each field represents based on its name and sample data. These meanings, along with field values, are converted into *vector representations* to provide better context during semantic searches. We recommend using concise descriptions for field meanings.

&nbsp;

**Field attributes**: Configure special attributes for subsequent data processing. Currently supported attributes include:


|**Attribute** |**Required?**  |**Attribute Description** |
|---|---|---|
|Unique identifier |<span data-api-tag="require\|aVtlVAu6k">必选</span> |The unique identifier for a single piece of data, which is the primary key. In search and recommendation scenarios, a different item ID represents a different "candidate".<br><br>A **data schema must contain exactly one unique identifier.** <br><br><br>* Supports upload as a **String** type.<br><br>* Only an outermost, non\-nested field can be used as the unique identifier. |
|Image URL<br><br> |\- |For fields configured as image URLs, the system automatically fetches images and extracts visual features for multimodal understanding after uploading data. To use URLs for uploading images in multimodal search, mark the field storing the image URLs as the image URL attribute.<br><br>This attribute can be configured when the field is **String or Array<String\>** . Please ensure the URL is publicly accessible.<br><br>Multiple fields can be configured as image URL attributes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To ensure successful processing, uploaded images must meet the following criteria:</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Formats:</strong> jpeg, png, webp, bmp, tiff, ico, dib, icns, sgi, jpeg2000</div><br><br><br><div data-tips="true" data-tips-type="default">For tiff, sgi, icns, jpeg2000 formats, ensure metadata alignment by correctly setting file metadata in object storage; otherwise, parsing will fail.</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Aspect Ratio (Width/Height):</strong> Must be within the range [1/100, 100]</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Dimensions:</strong> Must be within [10, 6000] px, i.e., the shorter side must be greater than 10 px and the longer side must be less than 6000 px.</div><br> |


<span id="6a61c6a7"></span>
### **Sample Data**

Here is an example of Image & Text data:

```JSON
{
    "product_id": "P10092385",
    "title": "ultra-thin laptop",
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



|**Sample Field** |**Field Type** |**Field Attribute** |**Field Meaning** |
|---|---|---|---|
|product_id |*String* |unique identifier |Product's unique ID |
|title |*String* | |Product title |
|images |*Object* | |Image information included in the product |
|   * images.primary |*String* |image URL |Product main image |
|   * images.gallery |*Array<String\>*  |image URL |Product detail carousel, containing images of the product's main information |
|price |*Object* | |Product price information |
|   * price.current |*Float* | |Product current displayed price |
|   * price.original |*Float* | |Product original price |
|   * price.discount_percentage |*Float* | |Product discount in percentage |
|specs |*Object* | |Product specifications |
|processor |*String* | |Processor |
|memory |*String* | |Memory |
|storage |*String* | |Computer storage space and type |


<span id="0f5287ce"></span>
### **Fields Data Configuration**


|**Configuration** |**Description** |
|---|---|
|Text Search |Semantic information within these fields will be included in the item's semantic representation for retrieval. It is recommended to select fields containing key searchable information such as **product names, core features, and categories**.<br><br>If you would like to utilise **image search**, you must select the `images` field as both a text search and image search field.  |
|Image Search |Check this option to enable "Search by Image" for the images in this field. You can selectively enable this feature to precisely control which types of images respond to user image search requests based on your specific application scenario (e.g., "Product Main Image," "User Avatar," "Scene Photo," etc.).<br><br>**Note:**  This field must already be marked as a **Searchable Field** and its attribute must be set to **Image URL**. |
|Filterable Fields |These fields can be used to filter search results when calling search and conversational APIs. Supports numeric types (`Float`, `Int`), `Boolean`, `String`, and `String Array`. It is recommended to select fields like **Category** or **Price**. |
|Autocomplete Fields |The values of selected fields in each data entry will be indexed as suggested terms for use in the Search Autocomplete API. Supports `String` and `String Array` formats. |


Using the previous example data, you could configure:


* **`title`**: For basic text matching and autocomplete.

* **`images.primary`**: For **Image\-to\-Image Search**.

* **`images.gallery`**: To allow the system to understand product briefs or feature highlights within the images.

* **`price.current`**: Enables users to ask about product prices during a conversation.

* **`specs`**: All technical specifications can be used for search; for example, searching "Laptop 1TB SSD" will retrieve products matching those specific parameters.


&nbsp;


---



<span id="e3ee5802"></span>
## Video Dataset

To integrate video content (such as movies, TV shows, and short videos) into your search and recommendation system and enable content\-based Q&A you should utilise **Video Datasets instead of Image & Text Dataset.** 

Video datasets allow you to upload data containing video files. The system automatically invokes video preprocessing and understanding capabilities to analyze audio\-visual content. This content is then indexed, enabling users to perform searches, receive recommendations, and ask questions about video content during AI conversations.

**Applicable Scenarios:** 


* **Film & TV Search and Q&A:**  Matches video metadata and content based on user needs, recommending media that fits their preferences during dialogues.

* **Plot\-Based Queries:**  Deeply understands videos across the platform to generate responses and media recommendations when users ask about specific plot points or storylines.

* **Short Video Scenarios:**  Performs content tagging based on video segments, supporting natural language searches that match audio, visual, and text elements.

* **Other Scenarios:**  Searching for courses or specific knowledge points on educational platforms, retrieving video design assets, etc.


&nbsp;

<span id="68077606"></span>
### Dataset Description

The dataset description allows you to provide a summary of the data content, source, applicable fields, or key characteristics (e.g.,  *"Domestic TV Series Information Table, including basic info for series and episodes, cover images, etc."* ).

**Viking AI Search Conversational Search Agent** utilizes this description to understand the theme and scope of the dataset. This helps the assistant make better judgments when executing searches, thereby improving result accuracy. We recommend providing a clear and precise description.

<span id="ad9b000f"></span>
### Data Format

Unlike Image & Text datasets, preparing video datasets requires following specific structural requirements. 

The **Unique Content ID, Content Type, Video Download URL, Parent Content ID,**  and **Sequence Index** must be uploaded using fixed field names. Other metadata can be uploaded using flexible, custom fields.

Before uploading a video dataset, please note the following restrictions:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="warning"><strong>Hierarchical Limits:</strong> The system only supports a <strong>two\-layer hierarchy</strong>. A "parent" content item cannot simultaneously be a "child" of another item. If a media item already serves as a parent containing children, assigning it a <code>parent_content_id</code> will result in a processing error.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Sequential Order:</strong> You should use the <code>sequence_index</code> field to specify the order of child content within a parent item. If the <code>sequence_index</code> is <strong>disordered</strong> (e.g., two items share the same index or the index is missing), the system will ignore the ordering data during processing. This may disrupt the chronological flow of the video content and negatively affect video understanding.</div>


* <div data-tips="true" data-tips-type="warning"><strong>Video Duration Limit:</strong> The system does not support individual videos exceeding <strong>4 hours</strong> in length.</div>



&nbsp;

**Field name**: Must start with a letter and can only contain letters, numbers, and underscores.

**Field type**: Supports JSON schema types.


|**Data Type** |**Note** |
|---|---|
|String, Array<String\> |\- |
|Integer, Array<Int\> |Supports both Int64 and Int32 |
|Float, Array<Float\> |\- |
|Boolean | |
|Object, Array<Object\> |Supports up to 3 layers (2 nested objects) |


**Field meaning**: During the automatic schema parsing phase, the LLM will interpret the meaning and content of each field based on the field name and uploaded sample data. These meanings, along with the field values, serve as semantic information within the *vector representation*. This enhances the accuracy of supplementary context for field content during semantic searches. We recommend providing a concise description of the field's meaning in Chinese or English.

<span id="90075116"></span>
#### Reserved Fields

To ensure your video data is processed and indexed accurately and efficiently, please pay close attention to preparing your media data according to our specific requirements before uploading. **You must use our predefined field names when uploading data:** 


|**Field Name** |**Required?**  |**Field Description** |
|---|---|---|
|content_id<br><br> |<span data-api-tag="require\|a9DM9FQqx">必选</span> |`*String*`<br><br>unique identifier of the media content<br><br>**Each data record must have a unique ID.**  |
|content_type |<span data-api-tag="require\|a2XUtTleA">必选</span> |`*String*`<br><br>content type, supports uploading the following enumeration values:<br><br><br>* "**collection**": Media series object (e.g., a season of a TV drama). No video file to be uploaded for "collection" data (it will be ignored if you uploaded). Only metadata for the series is required.<br><br>* "**video**": Video object (e.g., an individual episode of a TV drama, or a movie). Video files and their corresponding metadata to be uploaded for "video" type data. |
|video_url |<span data-api-tag="require\|acNnTW8nB">必选</span>for type  **"video"** ; <br><br>&nbsp;<br><br>Must be **empty** for type  **"collection"**  |`*Array<String>* `<br><br>A list of publicly accessible video download links, used for video understanding and processing. If multiple `video_url` links are uploaded under the same `content_id`, the system will splice them into a single video according to the list order.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This field supports a list of publicly accessible video download links. Crawling videos from general web links is not supported.</div><br><br><br><div data-tips="true" data-tips-type="default">Before uploading, <strong>ensure the total size of all video files in the list does not exceed 10GB and the total duration does not exceed 4 hours.</strong></div><br><br><br><div data-tips="true" data-tips-type="default">Ensure these video URLs are accessible to Volcengine’s official interface domain (volcengine.com).</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>The following video file formats are supported for upload:</strong></div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Common playback formats: mp4, mkv, avi, mov, wmv, asf, rmvb</div><br><br><br>* <div data-tips="true" data-tips-type="default">Streaming formats: flv, f4v, ts, mpegts, m4s, webm, m3u8</div><br> |
|parent_content_id |Must be **empty** for type  **"collection"** ;<br><br>&nbsp;<br><br>Optional for type "video";  |`*String*`<br><br>If your media information has a hierarchical structure (e.g., TV dramas), use this field to identify the parent content of the video. For "video" type data, you can pass the `content_id` of the series which the video belongs to. *The * `*parent_content_id*` * of the child content is the * `*content_id*` * of the parent.* <br><br>**Note**: Hierarchical relationships beyond 2 levels are currently not supported. |
|sequence_index |Optional for type "video" |`*Integer*`<br><br>Indicates the sequence of multiple child content within the parent content (e.g., episode numbers of a TV drama), enabling cross\-video understanding within the same media series.<br><br>**Note**: Cross\-video understanding will not be performed if this is not provided. |


In addition to the fixed fields mentioned above, you may also use **custom fields** to upload other metadata (e.g., content title, video duration, video language, etc.). You can assign these fields any name — for instance, by using the existing field names from your database — to simplify the integration process.

&nbsp;

<span id="8d68ff39"></span>
#### Field Attributes

Configure special attributes for your fields to facilitate subsequent data processing. Currently, these specialized fields with predefined attributes cover **all fixed fields** as well as **certain optional fields**. We strongly recommend uploading these optional fields that have fixed, pre\-set attributes.


|**Attribute** |**Required?**  |**Attribute Description** |
|---|---|---|
|content identifier |**Required & Fixed** |`*String*`<br><br>Corresponds to the `*content_id*` field |
|video download URL |**Conditional & Fixed** |`*Array<String>* `<br><br>Corresponding to the `*video_url*` field |
|parent content identifier |**Conditional & Fixed** |`*String*`<br><br>Corresponding to the `*parent_content_id*` field |
|content index |**Conditional & Fixed** |`*Integer*`<br><br>Corresponding to the `*sequence_index*` field |
|content title<br><br> |Optional  |`*String*`<br><br>Title of the media content, **uploading is strongly recommended** |
|media cover image url |Optional |`*String*`<br><br>Download link for the media cover image |
|media page link |Optional |`*String*`<br><br>URL for the media content page, for search list previews only |
|video duration (seconds) |Optional |`*Int64*`<br><br>Video duration (in seconds) |
|video language (BCP 47)<br><br> |Optional |`*Array<String>* `<br><br>Language tags that comply with BCP 47 standard<br><br>For example, Chinese: zh; English: en |
|release time  |Optional |`*String*`<br><br>The release or premiere time of media content, formatted in ISO 8601 (YYYY\-MM\-DD T HH:MM:SS), supporting precision to day or second |


The following is an example of a video data entry (a TV episode):

```JSON
{
  "content_id": "tv_stranger_things_s01_e01",
  "content_type":"video",
  "video_url": ["https://example.com/tv_series/67890/episode_01.mp4"],
  "parent_content_id": "tv_stranger_things_s01",
  "sequence_index": 1,
  "title": "Chapter One: The Vanishing of Will Byers",
  "director": "The Duffer Brothers",
  "actors": ["Winona Ryder", "David Harbour", "Finn Wolfhard"],
  "first_air_date": "2016-07-15",
  "rating": null,
  "genres": ["Sci-Fi", "Horror", "Drama"],
  "episode_summary": "On his way home from a friend's house, young Will sees something terrifying. Nearby, a sinister secret lurks in the depths of a government lab.", 
  "actor_list": [
      {"actor_name": "Winona Ryder", "role_name": "Joyce Byers"}, 
      {"actor_name": "David Harbour", "role_name": "Jim Hopper"}, 
      {"actor_name": "Finn Wolfhard", "role_name": "Mike Wheeler"}
  ],
  "duration": 2940,
  "language": "en-GB",
  "media_link": "https://example.com/tv_series/67890/episode_1/"
}
```



|**Sample Field** |**Field Type** |**Field Attribute** |**Field Meaning** |
|---|---|---|---|
|content_id (fixed field) |`*String*` |content identifier |unique identifier of media content |
|video_url (fixed field) |*Array<String\>*  |video download URL |download link of the video under media content |
|parent_content_id (fixed field) |*String* |parent content identifier |unique identifier of the parent content to which the media content belongs |
|sequence_index (fixed field) |*Integer* |content sequence number |order information of media content within the parent content |
|title |*String* |content title |display title of media content |
|director |*String* | |director of the media content |
|actors |*Array<String\>*  | |cast list of media content |
|first_air_date |*String* |release date (date\-time format) |release date of media content |
|rating |*Float* | |rating of media content |
|genres |*Array<String\>*  | |type of media content |
|episode_summary |*String* | |summary of media content |
|actor_list |Array<Object\> | |cast and character list of media content |
|* actor_list.actor_name |*String* | |actor name |
|* actors_list.role_name |*String* | |role played by the actor |
|duration |*Int64* |video duration (seconds) |length of media content |
|language |*String* |video language (BCP 47) |media content language |
|media_link |*String* |media page link |media content redirect link |


&nbsp;

<span id="e5817a8e"></span>
### Video Data Hierarchy

To help you manage and distinguish between serial works and standalone pieces more clearly, Viking AI Search supports hierarchical media data uploads. 

It supports a **two\-layer media relationship** defined by the `content_id` and `parent_content_id` fields. Media content at each level can have its own independent metadata.

**Using hierarchical relationships enables the following business objectives:** 


* **Integrated Video Understanding:**  Video content under the same parent can be analyzed with cross\-video understanding. By specifying the sequence of child content (using the integer field `sequence_index`), the system will analyze all child videos under a parent as a whole, enabling serial continuity and contextual understanding.

* **Focused Primary Content Display:**  In film and TV scenarios, you may prefer that search results only display parent\-level content (e.g., returning the TV series itself rather than individual episodes). You can configure the video search result return strategy in the console to ensure only parent\-level content is displayed during recall.


Below is a detailed explanation of content hierarchies:


|**Content Type** |**Type Description** |**Sample** |
|---|---|---|
|Parent content |The top level of the hierarchy; this content usually refers to a series of works, the most typical example being a TV series.<br><br>&nbsp;<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique content identifier, used as the `*parent_content_id*` of its child content.<br><br>`*content_type*`："collection"<br><br>`*video_url*`: must be empty<br><br>`*parent_content_id*`: must be empty<br><br>`*sequence_index*`: must be empty |```JSON```<br>```{```<br>```  "content_id": "tv_stranger_things_s01",```<br>```  "content_type":"collection",```<br>```  "video_url": null,```<br>```  "parent_content_id": null,```<br>```  "sequence_index": null,```<br>```  "title": "Stranger Things (Season 1)",```<br>```  "director": "The Duffer Brothers",```<br>```  "actors": ["Winona Ryder", "David Harbour", "Finn Wolfhard"],```<br>```  "first_air_date": "2016-07-15",```<br>```  "douban_rating": 9.3,```<br>```  "genres": ["Sci-Fi", "Horror", "Drama"],```<br>```  "plot_summary": "When a young boy vanishes, a small town uncovers a mystery involving secret experiments, terrifying supernatural forces, and one strange little girl.", ```<br>```  "actor_list": [```<br>```    {"actor_name": "Winona Ryder", "role_name": "Joyce Byers"}, ```<br>```    {"actor_name": "David Harbour", "role_name": "Jim Hopper"}, ```<br>```    {"actor_name": "Finn Wolfhard", "role_name": "Mike Wheeler"}```<br>```  ],```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/tv_series/67890/"```<br>```}```<br> |
|Child content |The second level in the hierarchy, representing a part of the series, such as an episode of a TV show. <br><br>Each child's content must belong to one parent content.<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique identifier for the content<br><br>`*content_type*`："video"<br><br>`*video_url*`: required, video file URL<br><br>`*parent_content_id*` *: * the `*content_id*` of the parent content<br><br>`*sequence_index*`: indicates the order of multiple sub\-contents within the parent content |```JSON```<br>```{```<br>```  "content_id": "tv_stranger_things_s01_e01",```<br>```  "content_type":"video",```<br>```  "video_url": ["https://example.com/tv_series/67890/episode_01.mp4"],```<br>```  "parent_content_id": "tv_stranger_things_s01",```<br>```  "sequence_index": 1,```<br>```  "title": "Chapter One: The Vanishing of Will Byers",```<br>```  "director": "The Duffer Brothers",```<br>```  "actors": ["Winona Ryder", "David Harbour", "Finn Wolfhard"],```<br>```  "first_air_date": "2016-07-15",```<br>```  "douban_rating": null,```<br>```  "genres": ["Sci-Fi", "Horror", "Drama"],```<br>```  "episode_summary": "On his way home from a friend's house, young Will sees something terrifying. Nearby, a sinister secret lurks in the depths of a government lab.", ```<br>```  "actor_list": [```<br>```      {"actor_name": "Winona Ryder", "role_name": "Joyce Byers"}, ```<br>```      {"actor_name": "David Harbour", "role_name": "Jim Hopper"}, ```<br>```      {"actor_name": "Finn Wolfhard", "role_name": "Mike Wheeler"}```<br>```  ],```<br>```  "duration": 2940,```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/tv_series/67890/episode_1/"```<br>```}```<br> |
|Independent video content |Content without hierarchical relationships, such as a movie.<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique content identifier<br><br>`*content_type*`："video"<br><br>`*video_url*`: required, video file URL<br><br>`*parent_content_id*`: must be empty<br><br>`*sequence_index*`: must be empty |```JSON```<br>```{```<br>```  "content_id": "movie_12345",```<br>```  "content_type":"video",```<br>```  "video_url": ["https://example.com/movies/12345.mp4"],```<br>```  "parent_content_id": null,```<br>```  "sequence_index": null,```<br>```  "title": "Interstellar",```<br>```  "director": "Christopher Nolan",```<br>```  "actors": ["Matthew McConaughey", "Anne Hathaway", "Jessica Chastain"],```<br>```  "release_date": "2014-11-07",```<br>```  "douban_rating": 8.7,```<br>```  "genres": ["Sci-Fi", "Drama", "Adventure"],```<br>```  "plot_summary": "In a future where Earth is becoming uninhabitable, a team of ex-pilots and scientists travel through a wormhole in search of a new home for mankind, exploring the relationship between time, gravity, and love across the cosmos.",```<br>```  "actor_list": [```<br>```  {"actor_name": "Matthew McConaughey", "role_name": "Cooper"}, ```<br>```  {"actor_name": "Anne Hathaway", "role_name": "Brand"}, ```<br>```  {"actor_name": "Jessica Chastain", "role_name": "Murph"}```<br>```  ],```<br>```  "duration": 10140,```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/movies/12345/details"```<br>```}```<br> |


Using the TV series "*Stranger Things (Season 1)* ", episode 1 of "*Stranger Things (Season 1)* ", and the movie "Interstellar" as examples:


| ** **  |**`video_url`** |**parent_content_id** |**content_type** |
|---|---|---|---|
|TV series "*Stranger Things (Season 1)* " |must be empty |must be empty |"collection" |
|"*Stranger Things (Season 1)* " episode 1 |required |required |"video" |
|Movie "Interstellar" |required |must be empty |"video" |


&nbsp;

<span id="9b198402"></span>
### Fields Data Configuration


|**Parameter** |**Description** |
|---|---|
|Searchable fields |Audio\-visual or semantic information within the field will be included in the semantic representation for retrieval.<br><br>**Video Download URL field (** **`video_url`** **) is checked by default and cannot be unchecked.**  The platform processes videos by default. If you do not need video understanding and only want to search metadata, we recommend using an Image & Text dataset.<br><br>Recommended fields: content title, video summary, cast list, etc. <br><br>**Note: Image\-to\-video search is currently not supported.**  |
|Filterable fields |When calling search and dialogue interfaces, the selected fields can filter the search results<br><br>Supports numeric fields (Float, Int), boolean (Bool), string (String), and string list (Array<String\>)<br><br>The `content_id`, `content_type`, `parent_content_id`, and `sequence_index` fields are mandatory to be configured for filtering.<br><br>It is recommended to select video type, rating, etc. |
|Fields used for search autocomplete |The values of selected fields from each data entry will be indexed as suggested terms, serving as the data source for the Search Autocomplete API.<br><br>Supports data in `String` and `String Array` formats. |


Taking the single episode data from the previous example as an instance, you can configure:


* **`video_url`**: Used for video plot search.

* **`episode_summary`**: Allows users to find the corresponding TV series via plot summaries in dialogues.

* **`director`**: Enables searching for all film and television works by a specific director.

* **`actors`**: Allows users to inquire about a specific actor's works during a dialogue.


&nbsp;


---



<span id="2b52d903"></span>
## Synthesize New Fields using LLM

When configuring a dataset, this feature allows you to leverage Large Language Models (LLMs) to automatically generate new, high\-value text fields based on existing image and text information. 

These newly generated fields can then be added to the dataset and directly utilized in **searching, filtering, and search completion**, effectively enhancing data discoverability and application value. Currently, this feature primarily supports three enhancement types: **Item Descriptions, Keywords, and Query Lists**.


|**Enhancement Type** |**Type Description** |
|---|---|
|**Item Description** |Uses text or image fields of the item to generate a descriptive text (*String*), integrating multi\-source information to enrich searchable data. |
|**Keywords** |Uses text or image fields to generate multiple keywords (*Array*) to enrich searchable data. |
|**Query List** |Uses text or image fields to generate multiple queries (*Array*) to enrich search autocomplete data. |


&nbsp;


---



<span id="34fca5e6"></span>
# User Event Dataset

A **User Event Dataset** is a structured collection of data used to record and analyze various interactions users have within an application or platform. To improve long\-term recommendation performance and provide users with personalized capabilities for next\-generation generative recommendations, we provide the User Behavior Dataset feature.

By leveraging rich, fine\-grained user behavior data combined with user intent, behavioral sequencing, and contextual dialogue history, the platform delivers superior end\-to\-end recommendation results. We recommend using the behavior data upload feature to enhance long\-term content recommendations in specific scenarios, such as:


* **E\-commerce Platforms:**  Combines short\-term actions (e.g., favorites, adding to cart, placing orders) with long\-term habits (e.g., preferred categories, spending ranges) to infer a user's true interests, thereby achieving personalized recommendations and increasing sales conversion.

* **Information/Content Platforms:**  Where user behavior is often unstructured and topics are diverse, the system combines interaction data (e.g., browsing, liking, commenting, sharing, dwell time) with a generative recommendation system. This extracts behavioral trajectories across different time periods and content domains, providing the LLM with more semantic behavioral context for highly refined and personalized content recommendations.


&nbsp;

<span id="e3fda811"></span>
## Mandatory Fields

This dataset consists of **five mandatory field types** and several custom optional fields used to represent user action trajectories and interaction methods. This data supports product optimization, personalized recommendations, and user experience improvements. In a user behavior dataset, each record corresponds to a behavioral event (e.g., "User A clicked a product on the homepage"), and the table exists in the form of an **event log**.

When uploading a user event dataset, you must configure the following five mandatory fields attributes along with any number of custom fields:


1. **User ID**

2. **Item ID**

3. **Event Type** (e.g., exposure, click, favorite, share, purchase, rating, search, etc.)

4. **Event Timestamp** (in milliseconds)

5. **Event Scene** (e.g., homepage, detail page, search results page, etc.)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Field names can be user\-defined. </div>


For detailed instructions on creating and editing these datasets, please refer to [Create User Event Dataset](https://docs.byteplus.com/docs/393/Create_User_Behavior_Dataset).


---



If you wish to use recommendation features within your application, the application must be linked to at least one **Item Dataset** and one **User Event Dataset**. While a single application supports the configuration of multiple item datasets of the same type, each application can be configured with **only one** User Event Dataset.

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Before linking a user event dataset for a specific application, you must first complete the configuration of the <strong>Item Dataset</strong> within that application.</div>
