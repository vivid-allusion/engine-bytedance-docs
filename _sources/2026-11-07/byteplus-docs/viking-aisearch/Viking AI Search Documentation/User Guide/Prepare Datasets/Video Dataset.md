---
title: "Video Dataset"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Introduction_to_Video_Dataset"
---

A Video Dataset is a feature for uploading video files along with their metadata, such as titles and custom fields. The system automatically analyzes this content to power advanced video search engines and Q&A assistants. This guide details the specific data preparation requirements, including the mandatory JSON format, fixed and custom fields, and how to structure hierarchical data for content like TV series.

A video dataset allows you to upload video files along with their metadata (such as titles, authors, release dates, and other custom fields). The system automatically invokes video pre\-processing and understanding capabilities to analyse the metadata and extract, understand, and summarise the audio, visual, and textual components of the video files. This enables the construction of a video search engine and allows intelligent assistants to provide Q&A services based on the video content.

Video datasets are suitable for the following types of content:


* **Film and TV Content:**  Film and TV content on video platforms includes metadata (title, summary, genre, cast, etc.) and video files. The video dataset uses JSON objects to store the metadata and associated video files for a film or TV show, supporting a hierarchical series\-episode structure to represent the seasons and episodes with parent\-child relationships.

* **Video Courses:**  JSON objects are used to store metadata and video files for educational content. The Series\-Episode hierarchical structure can be used to represent the parent\-child relationship between a course and its sequence of individual videos.

* **Short Videos:**  JSON objects are used to store short video metadata (authors, dates, keywords, etc.) and the corresponding video files. The system automatically understands the short video content and supplements it with additional metadata.


<span id="3ab88547"></span>
# Video Dataset Format

Unlike Image & Text Datasets, before uploading a Video Dataset, you must prepare your media data in accordance with specific upload requirements. The unique identifier for media content, content type, video download link, unique identifier for parent content, and sequence number **must** **use** **fixed field names**. Other metadata can be uploaded using flexible, custom fields.

<span id="3d3737ed"></span>
#### Fixed Fields

To ensure your video data is processed and indexed accurately and efficiently by the system, please pay particular attention to preparing your media data according to our specific requirements before uploading. You **must** **use our pre\-defined field names ** for storage. Fields marked as "Mandatory" must be included in each data record, including `content_id` (representing the unique ID of the media data) and `content_type` (indicating whether the media data is a series object or an individual video object).


|**Field Name** |**Mandatory?**  |**Field Description** |
|---|---|---|
|content_id<br><br> |Mandatory |`*String*`<br><br>Unique identifier of the media content<br><br>**Each data record must have a unique ID.**  |
|content_type |Mandatory |`*String*`<br><br>Content type, supports uploading the following enumeration values:<br><br><br>* "**collection**": Media series object (e.g., a season of a TV drama). No video file to be uploaded for "collection" data (it will be ignored if uploaded). Only metadata for the series is required.<br><br>* "**video**": Video object (e.g., an individual episode of a TV drama, or a movie). Video files and their corresponding metadata to be uploaded for "video" type data. |
|video_url |**Mandatory** for type  **"video"** ; <br><br>&nbsp;<br><br>Must be **empty** for type  **"collection"**  |`*Array<String>* `<br><br>A list of video download links accessible to the system, used for video understanding and processing. If multiple `video_url` links are uploaded under the same `content_id`, the system will splice them into a single video according to the list order.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This field supports a list of publicly accessible video download links. Crawling videos from general web links is not supported.</div><br><br><br><div data-tips="true" data-tips-type="default">Before uploading, <strong>ensure the total size of all video files in the list does not exceed 10GB and the total duration does not exceed 3 hours.</strong></div><br><br><br><div data-tips="true" data-tips-type="default">Ensure these video URLs are accessible to Volcengine’s official interface domain (volcengine.com).</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>The following video file formats are supported for upload:</strong></div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Common playback formats: mp4, mkv, avi, mov, wmv, asf, rmvb</div><br><br><br>* <div data-tips="true" data-tips-type="default">Streaming formats: flv, f4v, ts, mpegts, m4s, webm, m3u8</div><br> |
|parent_content_id |Must be **empty** for type  **"collection"** ;<br><br>&nbsp;<br><br>Optional for type "video";  |`*String*`<br><br>If your media information has a hierarchical structure (e.g., TV dramas), use this field to identify the parent content of the video. For "video" type data, you can pass the `content_id` of the series that the video belongs to. *The * `*parent_content_id*` * of the child content is the * `*content_id*` * of the parent.* <br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Hierarchical relationships beyond 2 levels are currently not supported.</div><br> |
|sequence_index |Optional for type "video" |`*Integer*`<br><br>Indicates the sequence of multiple child content within the parent content (e.g., episode numbers of a TV drama), enabling cross\-video understanding within the same media series.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Cross\-video understanding will not be performed if this is not provided.</div><br> |


<span id="da2c9cb9"></span>
#### Custom Metadata Fields

In addition to the fixed fields listed above, **you may also use custom fields to upload other metadata** such as content title, video duration, video language, etc. You can assign any names to these fields, for example, by directly using existing field names from your database to simplify integration. Custom fields must follow the format requirements below:


* **Field name**: must start with a letter and can only contain letters, numbers, and underscores

* **Field type**: supports the following data types defined in the JSON schema

   * String (and Array<String\>)

   * Integer (Array<Integer\>): supports both Int64 and Int32

   * Float (and Array<Float\>)

   * Boolean

   * Object (and Array<Object\>): supports fields containing nested JSON objects, with a maximum of three levels of object nesting.


<span id="20246742"></span>
## About Data Hierarchy

To assist you in managing and distinguishing between series and individual content more clearly, we support the uploading of media data in hierarchies. It supports two layers of media relationships, defined using the `content_id` and `parent_content_id` fields. Media content at each level can have its own metadata.

&nbsp;

**Using hierarchical relationships can meet the following business requirements:** 


* **Sequential Video Understanding**: Video content under the same parent can undergo **cross\-video understanding**. You must specify the sequential order of the child content under the parent (using the integer field `sequence_index`). During video understanding, all child videos under the parent will be analysed to achieve content linking and contextual understanding.

* **Focusing on Core Content Display**: In film and television scenarios, you may prefer that **only parent\-level content is displayed** in search and recommendation result lists (for example, finding a TV series rather than individual episodes). You can configure the search result display strategy in the console to ensure that only parent\-level content is displayed during retrieval.


&nbsp;

The following provides detailed explanations on content hierarchy:


|**Content Type** |**Type Description** |**Sample** |
|---|---|---|
|Series |The top level of the hierarchy; this content usually refers to a series of works, the most typical example being a TV series.<br><br>&nbsp;<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique content identifier, used as the `*parent_content_id*` of its child content.<br><br>`*content_type*`："collection"<br><br>`*video_url*`: must be empty<br><br>`*parent_content_id*`: must be empty<br><br>`*sequence_index*`: must be empty |```JSON```<br>```{```<br>```  "content_id": "tv_stranger_things_s01",```<br>```  "content_type":"collection",```<br>```  "video_url": null,```<br>```  "parent_content_id": null,```<br>```  "sequence_index": null,```<br>```  "title": "Stranger Things (Season 1)",```<br>```  "director": "The Duffer Brothers",```<br>```  "actors": ["Winona Ryder", "David Harbour", "Finn Wolfhard"],```<br>```  "first_air_date": "2016-07-15",```<br>```  "douban_rating": 9.3,```<br>```  "genres": ["Sci-Fi", "Horror", "Drama"],```<br>```  "plot_summary": "When a young boy vanishes, a small town uncovers a mystery involving secret experiments, terrifying supernatural forces, and one strange little girl.", ```<br>```  "actor_list": [```<br>```    {"actor_name": "Winona Ryder", "role_name": "Joyce Byers"}, ```<br>```    {"actor_name": "David Harbour", "role_name": "Jim Hopper"}, ```<br>```    {"actor_name": "Finn Wolfhard", "role_name": "Mike Wheeler"}```<br>```  ],```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/tv_series/67890/"```<br>```}```<br> |
|Video in the series |The second level in the hierarchy, represents a part of the series, such as an episode of a TV show. <br><br>Each sub\-content must belong to one parent's content.<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique identifier for the content<br><br>`*content_type*`："video"<br><br>`*video_url*`: required, video file URL<br><br>`*parent_content_id*` *: * the `*content_id*` of the parent content<br><br>`*sequence_index*`: indicates the order of multiple sub\-contents within the parent content |```JSON```<br>```{```<br>```  "content_id": "tv_stranger_things_s01_e01",```<br>```  "content_type":"video",```<br>```  "video_url": ["https://example.com/tv_series/67890/episode_01.mp4"],```<br>```  "parent_content_id": "tv_stranger_things_s01",```<br>```  "sequence_index": 1,```<br>```  "title": "Chapter One: The Vanishing of Will Byers",```<br>```  "director": "The Duffer Brothers",```<br>```  "actors": ["Winona Ryder", "David Harbour", "Finn Wolfhard"],```<br>```  "first_air_date": "2016-07-15",```<br>```  "douban_rating": null,```<br>```  "genres": ["Sci-Fi", "Horror", "Drama"],```<br>```  "episode_summary": "On his way home from a friend's house, young Will sees something terrifying. Nearby, a sinister secret lurks in the depths of a government lab.", ```<br>```  "actor_list": [```<br>```      {"actor_name": "Winona Ryder", "role_name": "Joyce Byers"}, ```<br>```      {"actor_name": "David Harbour", "role_name": "Jim Hopper"}, ```<br>```      {"actor_name": "Finn Wolfhard", "role_name": "Mike Wheeler"}```<br>```  ],```<br>```  "duration": 2940,```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/tv_series/67890/episode_1/"```<br>```}```<br> |
|Independent video content |Content without hierarchical relationships, such as a movie.<br><br>Its structural features are as follows:<br><br>`*content_id*`: unique content identifier<br><br>`*content_type*`："video"<br><br>`*video_url*`: required, video file URL<br><br>`*parent_content_id*`: must be empty<br><br>`*sequence_index*`: must be empty |```JSON```<br>```{```<br>```  "content_id": "movie_12345",```<br>```  "content_type":"video",```<br>```  "video_url": ["https://example.com/movies/12345.mp4"],```<br>```  "parent_content_id": null,```<br>```  "sequence_index": null,```<br>```  "title": "Interstellar",```<br>```  "director": "Christopher Nolan",```<br>```  "actors": ["Matthew McConaughey", "Anne Hathaway", "Jessica Chastain"],```<br>```  "release_date": "2014-11-07",```<br>```  "douban_rating": 8.7,```<br>```  "genres": ["Sci-Fi", "Drama", "Adventure"],```<br>```  "plot_summary": "In a future where Earth is becoming uninhabitable, a team of ex-pilots and scientists travel through a wormhole in search of a new home for mankind, exploring the relationship between time, gravity, and love across the cosmos.",```<br>```  "actor_list": [```<br>```  {"actor_name": "Matthew McConaughey", "role_name": "Cooper"}, ```<br>```  {"actor_name": "Anne Hathaway", "role_name": "Brand"}, ```<br>```  {"actor_name": "Jessica Chastain", "role_name": "Murph"}```<br>```  ],```<br>```  "duration": 10140,```<br>```  "language": "en-GB",```<br>```  "media_link": "https://example.com/movies/12345/details"```<br>```}```<br> |


Using the TV series "*Stranger Things (Season 1)* ", episode 1 of "*Stranger Things (Season 1)* ", and the movie "Interstellar" as examples:


|**Content Sample** |**Expected ** **`content_type`** |**Expected ** **`video_url`** |**Expected`parent_content_id`** |
|---|---|---|---|
|TV series "*Stranger Things (Season 1)* " |"collection" |must be empty |must be empty |
|"*Stranger Things (Season 1)* " episode 1 |"video" |required, upload the video file link of episode 1 of "*Stranger Things (Season 1)* " in the form of ["{video_download_url}"] |required, upload the content_id of "*Stranger Things (Season 1)* " |
|Movie "Interstellar" |"video" |Upload the video file link of "Interstellar" in the form of ["{video_download_url}"] if required |Must be empty |


<span id="d5a0d7ba"></span>
# Reserved Field Attributes

The "attributes" of a field are a set of reserved field configurations which you will be guided to set up during dataset creation. Fields configured with specific attributes will undergo specific processing and will be used in content understanding and ranking strategies during search, recommendation and conversation. When preparing your data, you can pre\-determine whether your database contains the following information. We recommend passing these attributes in the specified format to maximise utility of Viking AI Search's  intelligent data processing and online strategies.

&nbsp;

The video dataset has the following reserved attributes:


|**Attribute** |**Mandatory?**  |**Supported Field Type(s)**  |**Attribute Description** |
|---|---|---|---|
|content identifier |**Required & Fixed** |`*String*` |Corresponding to the `*content_id*` field |
|video download URL |**Conditional & Fixed** |`*Array<String>* ` |Corresponding to the `*video_url*` field |
|parent content identifier |**Conditional & Fixed** |`*String*` |Corresponding to the `*parent_content_id*` field |
|content index |**Conditional & Fixed** |`*Integer*` |Corresponding to the `*sequence_index*` field |
|content title<br><br> |Optional<br><br>**Recommended** |`*String*` |Media content title  **(Strongly recommended)** <br><br>Only one field per data record can be used to store the title attribute. |
|media cover image url |Optional |`*String*` |Media content cover image download link |
|media page link |Optional |`*String*` |Media content redirect link, for search results list preview only |
|video duration (seconds) |Optional |`*Int64*` |Video length (in seconds) |
|video language (BCP 47)<br><br> |Optional |`*Array<String>* ` |Language tags compliant with BCP 47<br><br>(E.g. Chinese: zh; English: en) |
|publish time (Date/Time Format) |Optional |`*String*` |Stores the publish or listing time of the item in date\-time format, used for sorting by newness in search and recommendation. <br><br>supports the following formats:<br><br><br>* Standard ISO date\-time strings (`YYYY-MM-DDThh:mm:ss+08:00`).<br><br>* Non\-standard date\-time strings (`YYYY-MM-DD hh:mm:ss` or date\-only strings). The system will automatically convert these to standard format. |
|publish time (UNIX Timestamp, Seconds) |Optional |`*Int64*` |Item publish time represented by a standard 10\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |
|publish time (UNIX Timestamp, Milliseconds) |Optional |`*Int64*` |Item listing time represented by a standard 13\-digit UNIX timestamp, used for freshness ranking in search and recommendation. |


<span id="f70f98b5"></span>
# Sample Data

The following is an example of a video data entry (a TV episode):

&nbsp;

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
|content_id (fixed field) |`*String*` |content identifier |Unique identifier of media content |
|video_url (fixed field) |*Array<String\>*  |video download URL |Download link for the video associated with the media content |
|parent_content_id (fixed field) |*String* |parent content identifier |Unique identifier of the parent content to which the media content belongs |
|sequence_index (fixed field) |*Integer* |content sequence number |Sequence number of the media content within the parent content |
|title |*String* |content title |Display title of media content |
|director |*String* | |Director of the media content |
|actors |*Array<String\>*  | |Cast list of media content |
|first_air_date |*String* |release date (date\-time format) |Release date of media content |
|rating |*Float* | |Rating of media content |
|genres |*Array<String\>*  | |Type of media content |
|episode_summary |*String* | |Summary of media content |
|actor_list |Array<Object\> | |Cast and character list of media content |
|* actor_list.actor_name |*String* | |Actor's name |
|* actors_list.role_name |*String* | |Role played by the actor |
|duration |*Int64* |video duration (seconds) |Length of media content |
|language |*String* |video language (BCP 47) |Media content language |
|media_link |*String* |media page link |Media content redirect link |
