---
title: "Create an AI companion for a video platform using Viking AI Search"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_an_AI_companion_for_a_video_platform_using_Viking_AI_Search"
---

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">The new video retrieval feature from Viking AI Search completely breaks the traditional passive viewing model. It allows you to interact with the plot in real time, get answers to your questions, and receive precise content recommendations based on your preferences, making every viewing experience more engaging and personalized.</div>


* <div data-tips="true" data-tips-type="default">This guide shows you how to build a highly available and immersive AI video co\-watching assistant. By integrating this assistant, you can use natural language to easily converse with, precisely search, and deeply engage with an extensive video library, and even have fun Q&A sessions about the plot, fully unlocking the commercial and user value of your video content.</div>


* <div data-tips="true" data-tips-type="default">To learn more about the capabilities of Viking AI Search, see <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, the all\-in\-one intelligent engine for enterprise search, recommendation, and conversational search</a>.</div>



As the video viewing experience is upgraded, users now prefer real\-time intelligent companionship while watching. By introducing an "AI video viewing companion," users can discuss the plot with the AI in a natural, conversational way and have smoother, more engaging real\-time interactions. For example:


<columns>
<columnsItem zoneid="IkM2F4MFjx">

* Search for videos with natural language, and use multimodal intelligent retrieval to pinpoint the content you want to watch.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c618ccf41f624a73a6591d6d13ea5ff9" width="200px" /></div>




</columnsItem>
<columnsItem zoneid="dOHvXH9sQO">

* Get an in\-depth analysis of video content, ask follow\-up questions about plot details anytime, and grasp plot highlights with a single click.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0afa0873fc094811a0ca9776a7ac4295" width="200px" /></div>


</columnsItem>
</columns>


In the following sections, we provide a detailed analysis of the AI viewing companion's system architecture, integration process, and specific use case examples. This helps you quickly transform this cutting\-edge AI capability into a real driver for business growth.

<span id="d0928610"></span>
# Two. Data preparation

High\-quality, well\-structured data is the foundation for building an AI video viewing companion. Viking AI Search performs an in\-depth analysis of every field you provide. To ensure that video retrieval results better meet your needs, we recommend that you perform the following standardization and refinement tasks during the **data preparation phase**.

<span id="4c50b00a"></span>
### Fixed fields

To enable the system to accurately and efficiently process and index your video data, prepare the media data according to our specific requirements before uploading. You **must use our predefined field names** for storage.


|<div style="text-align: center"><br><strong>Field name</strong></div><br> |**Required for upload** |**Description** |
|---|---|---|
|<div style="text-align: center"><br><strong>content_id</strong></div><br> |Required<br><br> |String<br><br>Unique identifier of media content<br><br>Each record must have a unique identifier. |
|<div style="text-align: center"><br><strong>content_type</strong></div><br> |Required<br><br> |String<br><br>Content type. Supported enumerated values:<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><span id="07d42a33"></span><br>##### <div data-tips="true" data-tips-type="default">Video content type description</div><br><br><br><div data-tips="true" data-tips-type="default">Our video content is structurally divided into two main categories:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="default"><strong>"collection"</strong>: Collection\-type content (with a hierarchical structure)</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Represents a <strong>content collection</strong>, not a single video file</div><br><br><br>   * <div data-tips="true" data-tips-type="default">Example: The entire \*Empresses in the Palace\* series, the complete \*Hands\-on Python Introduction\* course, the \*Workplace Communication Skills\* series, the full season of the documentary \*Planet Earth\*, the full season collection of \*Rock & Roast\*</div><br><br><br>2. <div data-tips="true" data-tips-type="default"><strong>"video" </strong>Video content (supports hierarchical / standalone formats)</div><br><br><br>   * <div data-tips="true" data-tips-type="default">As collection sub\-content: A single video episode, which is an actual playable video file. Example: \*Empresses in the Palace\*, episode 1; \*Hands\-on Python Introduction\*, lesson 3; \*Planet Earth\* documentary, episode 2</div><br><br><br>   * <div data-tips="true" data-tips-type="default">As standalone content: A complete video with no hierarchical relationship. Example: The movie \*The Wandering Earth\*, a single public lecture, a single short video, a standalone variety show clip</div><br> |
|<div style="text-align: center"><br><strong>video_url</strong></div><br> |When the Dataset type is a series (such as a TV series), the `video_url` field **must be empty.** <br><br>When the Dataset type is Video (such as a single TV episode or a Movie), the `video_url` field must be uploaded.<br><br> |Array<String\><br><br>A list of video download URLs accessible to Volcengine, used for video understanding and processing.<br><br>If multiple `video_url`s are uploaded for the same `content_id`, the system will concatenate the videos into a single video in the order they are listed.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>Tip</strong></div><br><br><br><div data-tips="true" data-tips-type="default">This field supports uploading a list of <strong>publicly accessible</strong> video download URLs, but does not support crawling videos from webpages by uploading their URLs. Before uploading, ensure the total size of all video files in the list does not exceed 10GB, and the total duration does not exceed 3 Hours.</div><br><br><br><div data-tips="true" data-tips-type="default">Additionally, before importing video download URLs, ensure that the download URLs for these videos can be accessed by the VolcEngine official API domain (<a href="http://volcengine.com/">volcengine.com</a>).</div><br> |
|<div style="text-align: center"><br><strong>parent_content_id</strong></div><br> |Must be empty when the dataset type is a series (e.g., TV series). Parent\-child relationships of more than two levels are not currently supported. |This field identifies the parent content of the video content. For data with a type of `video`, you can identify its parent content by providing the `content_id` of the series it belongs to. In other words, the `parent_content_id` of the child content is the `content_id` of the parent content. |
|<div style="text-align: center"><br><strong>sequence_index</strong></div><br> |Optional for videos. If the video belongs to a parent series, it is highly recommended that you provide this value. |*Integer*<br><br>Used to link video content for cross\-video understanding within the same media series.<br><br>If omitted, cross\-video understanding is not performed. |


<span id="58e0569b"></span>
### Custom metadata fields

In addition to the fixed fields, **you can also use custom fields to upload other metadata**, such as Content title, Video duration, video language, etc. You can assign any name to these fields. For example, using existing field names from your database simplifies the integration process. Custom fields have the following format requirements:


* String (Array)

* Integer (Array): Supports Int64 and Int32

* Float (Array)

* Boolean

* Object (Array): Supports fields that contain nested JSON objects, up to three levels of nesting.


<span id="8c31b852"></span>
### Sample data

Before a full data import, you should first run a validation test with 50\-100 representative items to verify that the entire process (Field configuration, Data import, index creation, and basic search) runs smoothly. The following is a sample video dataset:


<columns>
<columnsItem zoneid="qJlCDg43Ng">

```JSON
{
  "content_id": "tv_series_67890_episode_01",
  "video_url": ["https://example.com/tv_series/67890/episode_01.mp4"],
  "parent_content_id": "tv_series_67890",
  "sequence_index": 1,
  "title": "甄嬛传第一集",
  "director": "郑晓龙",
  "actors": ["孙俪", "陈建斌", "蔡少芬"],
  "first_air_date": "2011-11-17",
  "douban_rating": null,
  "genres": ["剧情", "古装"],
  "episode_summary": "时为满清雍正元年，结束了血腥的夺位之争，新的君主继位，国泰民安，政治清明，但在一片祥和的表象之下，一股暗流蠢蠢欲动。后宫选秀，少女甄嬛与自永安县来的好友眉庄、陵容参加选秀，因容貌酷似已故的纯元皇后，更兼聪慧机敏，立刻引起皇帝的注意……",
  "actor_list": [
    {"actor_name": "孙俪", "role_name": "甄嬛"},
    {"actor_name": "陈建斌", "role_name": "雍正"},
    {"actor_name": "蔡少芬", "role_name": "皇后"}
  ],
  "duration": 2700,
  "language": "zh-CN",
  "media_link": "https://example.com/tv_series/67890/episode_1/"
}
```




</columnsItem>
<columnsItem zoneid="MTaPRRCBsv">

```JSON
{
  "content_id": "movie_12345",
  "content_type": "video", // Must be `video`
  "video_url": ["https://您的服务器.com/12345.mp4"], // A link is required.
  "parent_content_id": null, // Must be empty
  "sequence_index": null,    // Must be empty
  "title": "流浪地球",
  "release_date": "2019-02-05",
  "plot_summary": "近未来，科学家们发现太阳急速衰老膨胀...",
  "actor_list": [
    {"actor_name": "吴京", "role_name": "刘培强"}
  ],
  "duration": 7740
}
```


</columnsItem>
</columns>


<span id="321f731a"></span>
### **Other data specifications and recommendations:** 

To make your AI viewing companion more flexible and adaptable to a wider range of user needs, we recommend enhancing and reviewing your datasets based on the following recommendations. Add **rich custom fields** to your datasets to help the AI better learn and understand the content.


|**Field name (Code name)**  |**Description** |<div style="text-align: center"><br><strong>Example</strong></div><br> |
|---|---|---|
|<div style="text-align: center"><br><strong>Content title (</strong><strong><code>title</code></strong><strong>)</strong></div><br> |Highly recommended |```JSON```<br>```"title": "甄嬛传第一集"```<br> |
|<div style="text-align: center"><br><strong>Release time</strong></div><br> |Used for conversational searches such as "Find the latest sci\-fi movies for me."<br><br>Supports String format (e.g., `"2019-02-05"` or standard ISO time) and also supports UNIX Timestamp (seconds or milliseconds). |```JSON```<br>```"publish_time": "2024-11-20" #字符串格式```<br>```"publish_time": 1732060800 # UNIX 时间戳:(秒) "publish_time": 1732060800000 # UNIX 时间戳:(毫秒)```<br> |
|<div style="text-align: center"><br><strong>Video duration (</strong><strong><code>duration</code></strong><strong>)</strong></div><br> |In seconds (Int64) |```JSON```<br>```"duration": 7200```<br> |
|<div style="text-align: center"><br><strong>Video language (</strong><strong><code>language</code></strong><strong>)</strong></div><br> |For example, `"zh-CN"` (Chinese) or `"en"` (English). |```JSON```<br>```"language": "en-US"```<br> |
|<div style="text-align: center"><br><strong>Return and redirection</strong></div><br> |Media cover image URL (poster) and a media page URL that users can click to play the content. |```JSON```<br>```"poster_url": "https://img.link/p1.jpg" #封面图```<br>```"playback_url": "https://v.link/watch/54321" #跳转链接```<br> |
|**Actor\-to\-character mapping (** **`actor_list`** **)**  |Enables the AI to accurately answer questions about character attribution. |```JSON```<br>```{"actor_name": "陈建斌", "role_name": "雍正"}```<br> |
|**Plot summary (** **`episode_summary`** **/** **`plot_summary`** **)**  |The text basis for the AI model to summarize plots and answer questions about video content.<br><br> |```JSON```<br>```"summary": "2007 年，地球基础科学出现异常扰动，科学界人心惶惶，多名科学家离奇自杀。纳米科学家汪淼被警官史强带到联合作战中心，潜入 “科学边界” 组织协助调查。汪淼接触到名为 ETO 的组织，发现其幕后统帅是自杀身亡的科学家杨冬的母亲叶文洁。随着 ETO 与作战中心的不断博弈，汪淼和史强逐渐确定《三体》游戏中的世界真实存在。一切事件源于两个文明为生存空间展开的生死相逐。在联合作战中心及科学家们的共同努力下，汪淼、史强等人坚定信念，准备与即将入侵的三体人展开殊死斗争。"```<br> |
|**Category tags (** **`genres`** **)**  |Allows users to ask the assistant to recommend specific types of movies. |```JSON```<br>```["剧情", "古装"]```<br> |
|**Others (e.g., ** **`director`** **, ** **`douban_rating`** **)**  |Add movie\-related personnel and rating information. |```JSON```<br>```"director": ["杨磊"],                 # 导演列表```<br>```"screenwriter": ["田良良", "陈晨"],    # 编剧列表（其他人员扩充）```<br>```"douban_rating": 8.7,                 # 豆瓣评分（建议使用浮点数）```<br>```"rating_count": 412500                # 参与评分人数（可选，用于辅助推荐权重） ```<br> |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details on video datasets, refer to this document: <a href="https://www.volcengine.com/docs/85296/1873473?lang=en">Video dataset introduction</a></div>


<span id="fae7ce56"></span>
# Build an AI video viewing companion in four easy steps

Based on the [Volcano Engine Quickstart](https://www.volcengine.com/docs/85296/2222393?lang=zh) process, we have simplified building a complex AI video viewing companion into four core steps.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e5e4bfba56a5415c903f6b15c56afdfb" width="2432px" /></div>


<span id="53214e5b"></span>
## Step One: New application


<columns>
<columnsItem zoneid="gUmVMV8Y9w">

Log in to the [Viking AI Search console](https://console.volcengine.com/aisearch/platform/region:aisearch-platform+cn-beijing/home/app-list) and click "New application". The system provides preset industry templates (e.g., e\-commerce, content communities). For the video companion assistant use case, you must select the **Video platform** industry. This preloads strategy configurations suitable for video scenarios. After entering the application name, proceed to the next step: "Dataset creation and import".

</columnsItem>
<columnsItem zoneid="kWSIBDfseQ">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ef8f888081d34d96afc7e080d195772f" width="1814px" /></div>


</columnsItem>
</columns>


<span id="ead5ac2e"></span>
## Step Two: Import data samples and configure in the console


<columns>
<columnsItem zoneid="Ih1lK0Df0k">

1. Create a new dataset. For dataset type, select **Item dataset**. For data type, select **Video data**.


After selecting the data type to upload, you can import your prepared JSONL files or paste into the JSON editor.



</columnsItem>
<columnsItem zoneid="mAqJMA69Yo">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2e4ae356e9b344289f6498a6dd178971" controls></video>




</columnsItem>
</columns>


&nbsp;


<columns>
<columnsItem zoneid="G5pzkodnde">

2. For Attributes and index configuration, the large model automatically scans sample data to infer the data type, meaning, and configuration method. You can also **manually calibrate** the data after AI analysis (e.g., correcting a year field misidentified by the AI as "float" to the "String" type, or configuring a more suitable indexing method for specific fields).




</columnsItem>
<columnsItem zoneid="qDMQkVWCVZ">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/0e105f871eea4427b8474c3b2cc7bdc7" controls></video>




</columnsItem>
</columns>


&nbsp;


<columns>
<columnsItem zoneid="LCmGJy8ZFT">

3. After the Data import, the system performs video understanding and index building using a large model (this may take some time). When complete, the dataset status will show  **"Configuration active"** .


After confirming the data is valid, you can click **Experience center** to use the **Video search** and **Conversational search** features on the experience page.

</columnsItem>
<columnsItem zoneid="ofQBwyc26M">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/051055df1b934922ad8ba632e5a68aec" width="3840px" /></div>


</columnsItem>
</columns>



<columns>
<columnsItem zoneid="hED4yYpGH6">

4. User event Data upload (Optional)


To enable the **personalized series recommendation** feature, you must first upload and integrate user viewing event data to provide the model with a basis for preference learning and precise recommendations.

</columnsItem>
<columnsItem zoneid="zG1PCySHdg">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/9c11f48614a143cdbf718cf5c327a019" controls></video>




</columnsItem>
</columns>


<span id="0e67b670"></span>
## Step Three: Experience tuning and strategy configuration

After completing the steps above, you have set up the basic search and conversational search capabilities for your **AI video viewing companion**. Next, you will proceed to the **experience tuning** phase. The companion's intelligence highly depends on the content returned by search. To achieve a more natural and seamless viewing experience, you need to optimize both the **search strategy** and the **conversational search strategy**.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Key suggestion:</strong> Do not use fixed template configurations. Different Movies and TV content (such as series, movies, variety shows, and anime) and different content volumes require different optimal strategies. For example, movies and TV series place more importance on <strong>plot, actors, and characters</strong>, while variety shows focus more on <strong>guests, themes, and episodes</strong>.</div>


<span id="f998b7da"></span>
### **Search strategy**

<span id="920e4c7c"></span>
#### Search mode

We recommend enabling **Balanced mode** by default to meet most Search and Conversational search needs:


|<div style="text-align: center"><br><strong>Mode name</strong></div><br> |<div style="text-align: center"><br><strong>Detailed description</strong></div><br> |<div style="text-align: center"><br><strong>Console guide</strong></div><br> |
|---|---|---|
|<div style="text-align: center"><br><strong>Balanced mode (Recommended for daily use)</strong></div><br><br><br><div style="text-align: center"><br></div><br> |User questions during co\-watching are often flexible and varied. They might directly state **lines, character names, or actor names;** <br><br>or ask using vague descriptions, such as:<br><br>"Where did that red\-haired character just go?"<br><br>"Play that awesome fight scene at the end"<br><br>&nbsp;<br><br>Balanced mode balances **precise keyword matching** with **cross\-modal semantic understanding**, allowing the AI to understand both explicit references and natural, conversational descriptions for a highly stable daily experience.<br><br> |<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b0670b1a77444a16a05f43b2125afb4e) </span> |


Only configure these settings for your specific use case when the AI demonstrates **inaccurate understanding or returns mismatched search results**:


<columns>
<columnsItem zoneid="m2c42xFVvz">

* **Semantic dominant**


Semantic search understands the **real intent** of a user's query, rather than relying solely on literal matches. When you enable Semantic dominant mode, **semantically related content** has a higher item retrieval priority than content that only matches keywords.

**Query characteristics**: longer, more subjective sentences or conditional descriptions

**Example**: Find me a high\-rated, fast\-paced suspense crime drama from the last year, preferably a domestic production with one case per episode.

</columnsItem>
<columnsItem zoneid="s6y3hfvDmh">

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f96fdb52826c46348edab4616f1da0a1) </span>

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="OrZT2eCy4Y">

* **Keyword dominant**


Keyword search requires keywords to **exactly match** the content. When Keyword dominant mode is enabled, **item retrieval** prioritizes content with exact matches over content that is only semantically related.

**Query characteristics**: use this when you need to perform high\-precision searches for items like technical terms, show titles, and actor names.

**Example**: Ye Wenjie, Empresses in the Palace Episode 12, Xinwen Lianbo 20260226, Oppenheimer full movie

</columnsItem>
<columnsItem zoneid="uU4vbsmN06">

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/040c0545898140cb846402cb9a341aa0) </span>

</columnsItem>
</columns>



<columns>
<columnsItem zoneid="WZpbNQdDjQ">

* **Define custom weighting**


If the modes above do not meet your actual application scenarios, you can use **Define custom weighting.** 

Supports flexible configuration of retrieval strategies based on business scenarios and search requirements, allowing you to freely adjust the weights of semantic search and keyword search to meet personalized and fine\-grained search requirements.

</columnsItem>
<columnsItem zoneid="Nw8tKMW3lH">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e2ad700c6f2a4a5faebd8c22529b7548" width="1804px" /></div>


</columnsItem>
</columns>


<span id="a1919e98"></span>
#### Result limits


<columns>
<columnsItem zoneid="pI9RdyvW0s">

Result limits control the number of video results returned for a single search request. This parameter has **no absolute standard**, and you can configure it flexibly based on your video library size, business scenarios, and performance requirements.

Set a reasonable value for the result limits **in conjunction with your front\-end interactive design**. **Do not set the value too high**, as this can increase API response times and slow down loading.

</columnsItem>
<columnsItem zoneid="RLFvqvmg0x">

<div style="text-align: center">
<h4 id="36e9c183"><img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/5d43e35664fe4ca29ee0c4dbd3b70ed9" width="2738px" /></h4></div>


</columnsItem>
</columns>


<span id="aca9b0c6"></span>
#### Multi\-modal reranking


<columns>
<columnsItem zoneid="VvWFFiaeRE">

When you enable this feature, the AI selects snippets based on user instructions and then performs a **deep understanding and secondary rerank** of the top\-ranked snippets. You can **customize** the number of items to rerank (default is 20). Lowering this value can improve response speed.

This step ensures that the top snippets or answers returned to the user **accurately match the query intent**, effectively improving the AI's understanding accuracy and overall intelligent experience.

</columnsItem>
<columnsItem zoneid="X6O4PmRa5B">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/514f1e9ce19c4c6abc7ff7d4f69686eb" width="2972px" /></div>


</columnsItem>
</columns>


<span id="b3e159d3"></span>
#### Boost

<span id="c1fe192c"></span>
##### **New show boost**

**Background:**  When users search for actors or genres, **newly released shows might be buried due to limited data or low ratings**, wasting the platform's copyright and promotional window. Configuring a time\-based boost for new shows significantly raises their ranking, prioritizing the display of the latest content. This enhances the user experience with fresh content and maximizes the value of the platform's copyrights.

**Example scenario**


* User query: "I want to watch a crime drama starring actor XX."

* Standard item retrieval (Problem): Older dramas rank higher due to more historical data, while newly released dramas are pushed down in the results.

* Boost new dramas (Enhanced experience): Dramas released within the last 30 days receive a significant score bonus, allowing them to surpass older dramas and rank at the top. This maximizes exposure for major new releases.



<columns>
<columnsItem zoneid="HHvZMaeIvU">

* **Rule name: ** `New show boost`

* **Scope:** 

   * Field: `first_air_date` (The date the video first aired)

   * Logic selection: `Relative to today` \-\> enter `30` \-\> select unit `days` \-\> select `Within` (i.e., content first aired within the last 30 days is in the new show protection period).

* **Boost / demotion configuration:** 


Drag the slider to the right to `+80%` or even `+100%`. This applies a very strong positive weight, ensuring new shows can overcome the score gap from historical view counts and immediately rank at the top.

</columnsItem>
<columnsItem zoneid="gdjB8qKu3i">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c1944c04ed234e72925895927f5cef45" controls></video>




</columnsItem>
</columns>


<span id="a86cf9f8"></span>
##### Boost high\-quality dramas

**Background:**  To prevent high\-quality content from being underrated, a weighting strategy is applied to highly\-rated dramas. This prioritizes well\-regarded, highly\-rated content in search results, improving the reliability of AI recommendations and the viewing experience.


* **User query**: When looking for something to watch over the weekend, a user might ask the AI, "Find me some good suspense dramas."

* **Standard item retrieval (Problem)** : The volume of suspense content is vast. When relying solely on text matching, some low\-rated dramas may rank higher than highly\-rated works due to a high density of keywords like "suspense" or "plot twist" in their synopses. This leads users to perceive the AI recommendations as low quality.

* **Enhanced experience (Quality gatekeeping)** : By setting a boost rule for the `rating` score field, well\-regarded dramas with a score of 8.5 or higher receive an extra bonus. Even with a slightly lower text relevance score, high\-quality works like "The Long Season" and "The Bad Kids" can be prioritized in the top 3 results. This improves the quality of AI recommendations and reduces the risk of users selecting subpar content.



<columns>
<columnsItem zoneid="b4bRNiwbm8">

* **Rule name: ** `Boost high-rated shows`

* **Scope:** 

   * Field selection: Select `rating` from the dropdown (video rating, numeric field)

   * Logic selection: Select `Greater than` from the dropdown, then enter `8.5` in the input box (assuming a maximum score of 10, 8.5 is the recognized threshold for high quality).

* **Boost configuration:** 

   * Drag the slider to the right to `+40%` or even `+80%`. This applies a significant positive weight to ensure that high\-quality content is prioritized for display among items of the same genre.

</columnsItem>
<columnsItem zoneid="j5aLn2iX7X">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/44797f14e7224be785dbe99f39a73b34" controls></video>


&nbsp;

&nbsp;



</columnsItem>
</columns>


<span id="b8118eee"></span>
#### Demote

<span id="5f5d20ac"></span>
##### Demote non\-feature content

**Background:**  When users search for a specific movie or TV show, they typically want to watch the full feature. If relying solely on text matching, supplementary content like trailers and behind\-the\-scenes footage can easily rank higher, which significantly deviates from the user's viewing intent. You can demote this type of non\-feature content to a lower rank to ensure the full feature is displayed first.

**Use case**


* **User command:**  The user says, "Play The Wandering Earth 2."

* **Problem:**  The system prioritizes returning trailers and behind\-the\-scenes footage instead of the full feature film, which significantly degrades the viewing experience.

* **Experience enhancement:**  By automatically demoting non\-feature content, the system places the full feature film at the top of the results, meeting the user's actual needs.



<columns>
<columnsItem zoneid="WcXPaZG4GT">

* **Condition field: ** `content_type` (Media content type)

* **Trigger condition: ** `content_type IN ["Trailer", "Behind-the-scenes", "Special feature", "Clip"]`

* **Demotion configuration:**  **`-60%`**  (Heavy demotion)


**Note:**  If a user explicitly says "I want to watch the trailer for The Wandering Earth," the text match score will be very high, which can offset a demotion and ensure it is returned. However, if they only search for the movie title, the trailer will be ranked lower.

</columnsItem>
<columnsItem zoneid="SPPDThv8DC">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/abbf585c84ba47e0b7cf3ed382c5eada" controls></video>




</columnsItem>
</columns>


<span id="d4538aee"></span>
#### Sort by field

**Background:**  Overrides sorting by relevance score from the large model and enforces sorting in ascending or descending order by the video clip's native timestamp or episode number.

**User scenario:**  When co\-watching esports events, live sports, or press conferences, users might ask questions like, "How has this player performed recently?" or "What are the latest developments on this news story?"

**Actions:** 


* **Field: ** `Updated at (update_time)` OR `Release time (publish_time)`

* **Sort order: ** `Descending`


**Business value:**  Ensures the knowledge base prioritizes retrieving the **latest** information, preventing the assistant from generating outdated or incorrect responses based on historical data.

<span id="6ddce32a"></span>
### Conversational search configuration

Viking AI Search, powered by a Conversational Search Agent, deeply integrates multimodal retrieval, personalized recommendation, and the conversational capabilities of large language models (LLMs) to help you quickly build an intelligent AI video co\-watching assistant that is **interactive, content\-aware, and can provide guidance**.

<span id="f9c2b4c0"></span>
#### Agent persona


<columns>
<columnsItem zoneid="e5J4E5HRwb">

You can set a unique "identity and persona" for your video companion assistant. Although this does not directly change the series retrieved by the search, it greatly affects the user experience.

</columnsItem>
<columnsItem zoneid="k6v1X7ztMf">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/75a695086a534087a7b817272f6d7795" width="2358px" /></div>


</columnsItem>
</columns>


**Prompt example:** 


<columns>
<columnsItem zoneid="J3Mten3qxv">

Professional video companion assistant (Default example)

```Plain Text
你是一个专业的视频内容智能推荐助手，拥有丰富的影视知识和精准的用户需求洞察力，专注于为用户提供个性化的电影、电视剧、纪录片等视频内容推荐服务。
```


</columnsItem>
<columnsItem zoneid="deYBfd0rMk">

Personalized video companion assistant

```Plain Text
你是 {品牌名} 视频平台的智能陪看助手 {助手名称}，是用户的观影搭子与内容推荐官。
你对影视剧、综艺、动漫、短剧、纪录片、短视频、名场面、高光片段、剧情解读有极强的理解与鉴赏能力，擅长快速定位用户想看的内容，帮用户找得准、看得爽、不踩雷。
你性格亲切、耐心、有判断力、善于共情，能精准理解用户的口语化指令、模糊需求和场景偏好，既懂热门内容，也懂小众喜好。
你不只做简单检索，更能理解意图、梳理剧情、推荐片段、过滤干扰、提升观看体验。
你的目标：让用户快速找到想看的内容，体验更流畅、更智能、更贴心，每一次观看都轻松、愉悦、有被懂的感觉。
```


</columnsItem>
</columns>


<span id="5a5bfbde"></span>
#### Response style settings

Configure the structure, tone, and language of the video assistant's responses. We recommend optimizing settings such as the style, quantity, and delivery of video recommendations to align with your business needs.

**Prompt example:** 


<columns>
<columnsItem zoneid="i5Km9BHwPy">

Professional video companion assistant (Default example)

```Plain Text
- 你热情友好、耐心细致，总能用亲切的语言与用户沟通，让用户感受到贴心的服务；
- 积极主动，善于发现用户在"用户当前问题"和"用户上文对话"表达的潜在需求，同时具备同理心，能敏锐察觉用户情绪，及时给予安抚和帮助。
- 你的表达要在字数和视频信息允许的范围内，尽可能详尽具体，回答风格俏皮可爱但又不失专业性
```


</columnsItem>
<columnsItem zoneid="TLumuXPCoL">

Personalized video companion assistant

```Plain Text
一、视频推荐原则
每次推荐 最多精选 4 个视频/片段，优先选择最符合用户核心需求的内容（如正片、高光、名场面）
推荐的内容可能来自 同一影视剧/综艺的不同片段（如名场面、关键剧情、高光合集）
对同一影视剧/综艺的不同片段 进行合并介绍与总结说明（如区分正片、花絮、片段类型）
避免对同款内容、重复片段的冗余描述
推荐时需说明：
适合的观看场景（如休闲放松、全家共看、碎片时间、深度追剧）
内容特点与观看建议（如高能下饭、烧脑悬疑、治愈解压，适合睡前/通勤观看）
内容优势（如实拍质感、剧情紧凑、名场面密集、无多余干扰）
二、对话与表达风格
语气要求：
热情、生动、自然，有陪看感
富有同理心与理解力，精准共情用户观影心情（如剧荒、想看高能、想找治愈内容）
不评判、不标签化用户的观影喜好、审美或选择（如不否定用户喜欢的题材、片段）
表达方式：
善用 加粗、列表、分段 突出重点（如重点标注内容类型、观看亮点）
长回复必须具备 清晰的结构层次（如先总述推荐方向，再分点介绍内容）
当信息较复杂时（如多部同题材内容对比），提供 简要、准确的总结，帮助用户快速决策
三、需求理解与延展
在推荐内容前：
仔细分析用户的提问或需求描述
判断其核心诉求与真实观影场景（如通勤碎片看、周末深度追、全家共看、解压放松）
在每次推荐后：
合理猜测用户的后续需求
如：是否需要同题材的更多内容
是否在意内容时长（如短视频、完整正片、高光片段）、无广告干扰
是否需要不同风格或题材的备选（如从悬疑转向治愈、从综艺转向短剧）
通过自然引导，帮助用户继续探索更适合自己的观影选择
四、无法完全满足需求时的处理方式
当当前平台内容无法完全满足用户需求时：
以 委婉、诚恳 的方式说明限制（如“目前平台暂未收录该片段，为你推荐同类型优质内容哦”）
优先推荐：
同题材的替代方案（如不同影视剧的同类型片段、同主演的其他作品）
相近风格或相近场景的内容（如用户找某类悬疑片段，推荐其他高能悬疑名场面）
始终以「尽量接近用户需求」为目标，避免简单拒绝或生硬转向
五、核心目标
帮助用户：
更清楚自己适合看什么、想看什么
更少踩雷、更快找到心仪内容，节省找剧时间
看到真正“好看、对味、适配场景”的视频内容
```


</columnsItem>
</columns>


<span id="5e0f4cce"></span>
#### Follow\-up suggestions


<columns>
<columnsItem zoneid="rOJbiSDsYw">

To improve multi\-turn conversation rates and avoid awkward single\-turn Q&A, enable the follow\-up question suggestion feature.

**Effect**: After the AI assistant completes a conversational turn, it automatically generates three relevant follow\-up suggestion bubbles based on the context. As shown in the image on the right.

This feature significantly reduces user input cost, effectively guiding the conversation to a deeper level to uncover more precise user needs.

</columnsItem>
<columnsItem zoneid="zq01WExOtt">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/ac8740c51cbd47b487069b0e50b90411" width="2222px" /></div>


</columnsItem>
</columns>


<span id="4518dacb"></span>
#### Web search

Web search is primarily used to help understand user queries and retrieve up\-to\-date information. For example, if a user searches for "this year's Oscar for Best Picture," the latest results cannot be retrieved using only the private video library and the model's inherent knowledge. Web search is required to supplement this with real\-time information.

Web search supports two modes: **Always on** (automatically performs a web search in every conversation) and **Auto\-detect** (only performs a search when it determines that the conversation requires time\-sensitive information).


<columns>
<columnsItem zoneid="CdykrBcGqA">

* **User command**: While the family was watching "The Three\-Body Problem," Dad asked, "Who played the young Ye Wenjie? What other popular shows has she been in?"

* **Local search only**: The AI can only find the actor's name and cannot provide other major works, causing the conversational search to end abruptly.

* **Web search**: The AI automatically completes the "character → actor → all works online" mapping, provides a complete answer, and proactively guides the user to view related content.

</columnsItem>
<columnsItem zoneid="dKJ7D8frLZ">

&nbsp;

<video src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/06328d44d355448fb9318c7b393f70f4" controls></video>




</columnsItem>
</columns>


<span id="dd8a1191"></span>
## Step Four: Integrate the API

<span id="19f15416"></span>
### Upload all video data

After you complete the Experience center configuration, if you want to **import more data** (e.g., a full dataset or incremental updates), follow the steps below.


1. Return to your **Datasets** list

2. Find the **target dataset** you want to add data to.

3. Click **View** to go to the dataset's details page.

4. On this page, find and switch to the **Data import** tab.



<columns>
<columnsItem zoneid="FDQ8YtKiZA">

Here, you can see the two main data import methods (**Import via API** and **Upload JSONL file**), which can be used to add data later.


1. **Upload JSONL file**

   1. You can upload files directly in the console by **clicking/dragging**.

2. **Real\-time import API**

   1. **API documentation link**: [Real-time import and update Item data - Viking AI Search - Volcano Engine](https://www.volcengine.com/docs/85296/1544970?lang=zh)

   2. **Use cases**:

      1. **Add items in real time**: Automatic processing and index building. Takes from a few to dozens of seconds (processing time is longer for multi\-image or video data).

      2. **Update items in real time**: Supports partial field updates. Updates to filter fields (non\-retrieval fields) take effect within seconds; updates to images, text, or videos take longer to process.

3. **Batch import via API**

   1. **API documentation link**: [Batch import item data--Viking AI Search-Volcano Engine](https://www.volcengine.com/docs/85296/2123240?lang=zh)

   2. **Use cases**:

      1. **Initial full build**: One\-time import of complete product or content data for test or production environments.

      2. **Regular large\-batch updates**: For updating specific fields across more than 100,000 data records (e.g., batch changes to listing status).

      3. **Backfill new fields**: Batch\-write values for newly added fields to your entire dataset.

</columnsItem>
<columnsItem zoneid="hLUQeSYjkC">

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/75d17881859846f0b432fba4f0d5d501" width="3840px" /></div>


</columnsItem>
</columns>


<span id="ff722557"></span>
### Integrate the conversational search API

Viking AI Search provides standard APIs to integrate the capabilities you build into your app, mini program, or webpage. The following is an invocation summary for this API.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/6bcc4f4c13994dfd8c17c6138f31d8ca" width="586px" /></div>



1. **Frontend initiates request**:

   * The user enters a question in the dialog box (e.g., "Recommend some feel\-good movies").

   * The frontend application packages the user's input, the current session's `session_id` (generated and maintained by the frontend), and fixed parameters like `user_id`, and sends them to your business backend.

2. **Business backend invokes AI search**:

   * After receiving the request from the frontend, your business backend constructs a POST request to the Viking AI Search `/chat_search` endpoint.

   * The request body contains all information from the frontend and includes your application's `API Key` for authentication.

   * **Key point**: The business backend must receive the response from the `/chat_search` endpoint in a **streaming** manner.

3. **Processing the streaming response and forwarding it to the frontend**:

   * The `/chat_search` endpoint returns a series of JSON data chunks in sequence. Each data chunk describes the AI assistant's current work step (`step`), which can be "intent recognition", "tool invocation" (with the retrieved video `payload`), or "response generation" (with a short text `content`).

   * Your business backend must parse these data chunks in real time and **forward them to the frontend as is via the streaming connection**.

4. **Front end renders a rich interactive interface**:

   * The front end receives the data stream forwarded from the business back end.

   * When it receives a **text stream**, it renders the AI's text response in real time with a "typewriter" effect.

   * When it receives **follow\-up suggestion** data, it renders them as clickable suggestion bubbles.

   * A rich interactive interface with text, item cards, and suggestion bubbles is then dynamically displayed to the user.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><strong>Why use a business backend proxy?</strong></div>


<div data-tips="true" data-tips-type="default">Although you can invoke the AI Search API directly from the frontend, we strongly recommend encapsulating and forwarding requests through your business backend. This approach has several key benefits:</div>



1. <div data-tips="true" data-tips-type="default"><strong>Security</strong>: Avoid exposing your <code>API Key</code> directly in your frontend code.</div>


2. <div data-tips="true" data-tips-type="default"><strong>Authentication and rate limiting</strong>: You can implement your own logic for user authentication and request rate limiting in your business backend.</div>


3. <div data-tips="true" data-tips-type="default"><strong>Logic aggregation</strong>: In the future, if you need to aggregate other internal services (such as querying orders or redeeming coupons), you can handle them in the backend to maintain a stable API for the frontend.</div>



**For detailed API integration instructions, see ** [ChatSearch - Conversational search--Viking AI Search-Volcengine](https://www.volcengine.com/docs/85296/1873492?lang=zh) **.** 

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">To learn more about Viking AI Search product capabilities, see: <a href="https://www.volcengine.com/product/AI-Search-Rec">Viking AI Search, an integrated intelligent engine for enterprise search, recommendation, and Q&A</a></div>
