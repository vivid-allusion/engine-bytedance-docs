---
title: "Create Item Dataset - Video Data"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Create_Item_Dataset_-_Video_Data"
---

To build a structured video dataset for intelligent search, recommendation, and conversational AI, you can use an Item Dataset. This guide provides detailed operational instructions for the video data workflow, covering essential steps like data preparation with mandatory fields, uploading sample data, and configuring field attributes to ensure your media is correctly indexed and processed.

The preparation and creation method for a dataset depends on the data type you are importing. This document focuses on the **Video Data** creation workflow, including data format requirements, field mapping rules, and solutions to common issues. 

If you wish to create an Image & Text dataset, please refer to ** ** [Create Item Dataset - Image & Text Data](https://docs.byteplus.com/docs/viking-aisearch/Create_item_dataset_image_text).

&nbsp;

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">This is a step\-by\-step guide for dataset creation and will require fundamental understanding of the different datasets found in Viking AI Search. </div>


<div data-tips="true" data-tips-type="default">To learn more about the different datasets and its features  — such as basic concepts of item datasets, supported data formats, specific definitions of field types, detailed parameter explanations, or search strategies — refer to the <a href="https://docs.byteplus.com/docs/viking-aisearch/Dataset_Introduction">Dataset Introduction</a> instead. </div>


&nbsp;


---



<span id="2772dc1a"></span>
# Video Dataset

<span id="acc32cd9"></span>
## Step 1: Data Preparation

Before you begin uploading a video dataset, it is essential to prepare your media data according to the following requirements. Unlike Image/Text datasets, video datasets include several **key fields that must be uploaded using fixed field names**. Therefore, it is critical to verify and adjust your data before the upload process.

Do note the following restrictions before uploading a video dataset:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>



1. <div data-tips="true" data-tips-type="default"><strong>Maximum </strong><strong>Two\-Layer Hierarchy: </strong>Video content only supports a 2\-layer hierarchy; a parent item cannot be a child of another item. If a media item already serves as a parent containing children, providing a parent_content_id for that parent will result in a processing error. </div>


2. <div data-tips="true" data-tips-type="default"><strong>Sequence Ordering:</strong> You can use <code>sequence_index</code>to define the order of child content within a parent. If the <code>sequence_index</code> values are not sequential (e.g., contain duplicates or gaps), the system will ignore this field, which may disrupt the chronological order and affect video understanding.</div>


3. <div data-tips="true" data-tips-type="default"><strong>4\-Hour Limit:</strong> Single videos exceeding <strong>4 hours</strong> are not supported.</div>



**Field name**: Must start with a letter and can only contain letters, numbers, and underscores.

**Field type**: Supports JSON schema types:


* String (Array)

* Integer (Array): Supports Int64 and Int32

* Float (Array)

* Boolean

* Object (Array): Supports nested objects up to three levels of hierarchy


**Field meaning**: During the automatic schema parsing phase, the LLM will interpret the meaning and content of each field based on the field name and uploaded sample data. These meanings, along with the field values, serve as semantic information within the vector representation. This enhances the accuracy of semantic searches by providing additional context for the field content. 

We recommend providing a concise description of the field's meaning in the language selected during dataset configuration (Currently supports English, Mandarin and Japanese).

<span id="795d5f35"></span>
### Reserved Fields

To ensure your video data is processed and indexed accurately and efficiently, please pay close attention to preparing your media data according to our specific requirements before uploading. You must use our predefined field names when uploading:


|**Field Name** |**Mandatory?**  |**Field Description** |
|---|---|---|
|content_id<br><br> |Mandatory |`*String*`<br><br>unique identifier of the media content<br><br>**Each data record must have a unique ID.**  |
|content_type |Mandatory |`*String*`<br><br>content type, supports uploading the following enumeration values:<br><br><br>*  **"collection"** : Media series object (e.g., a season of a TV drama). Do not upload a video file for "collection" data; it will be ignored if provided. Only metadata for the series is required.<br><br>* "**video**": Video object (e.g., an individual episode of a TV drama, or a movie). Upload video files and their corresponding metadata for "video" type data. |
|video_url |**Mandatory** for type  **"video"** ; <br><br>&nbsp;<br><br>Must be **empty** for type  **"collection"**  |`*Array<String>* `<br><br>A list of video download links accessible to the system, used for video understanding and processing. If multiple `video_url` links are uploaded under the same `content_id`, the system will concatenate them into a single video in the order provided.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">This field supports a list of publicly accessible video download links. Crawling videos from general web links is not supported.</div><br><br><br><div data-tips="true" data-tips-type="default">Before uploading, <strong>ensure the total size of all video files in the list does not exceed 10GB and the total duration does not exceed 3 hours.</strong></div><br><br><br><div data-tips="true" data-tips-type="default">Ensure these video URLs are accessible to Viking AI Search</div><br><br><br><div data-tips="true" data-tips-type="default"><strong>The following video file formats are supported for upload:</strong></div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Common playback formats: mp4, mkv, avi, mov, wmv, asf, rmvb</div><br><br><br>* <div data-tips="true" data-tips-type="default">Streaming formats: flv, f4v, ts, mpegts, m4s, webm, m3u8</div><br> |
|parent_content_id |Must be **empty** for type  **"collection"** ;<br><br>&nbsp;<br><br>Optional for type "video";  |`*String*`<br><br>If your media information has a hierarchical structure (e.g., TV dramas), use this field to identify the parent content of the video. For "video" type data, you can pass the `content_id` of the series to which the video belongs. The child's `parent_content_id` must be the parent's `content_id`.<br><br>**Note**: Hierarchical relationships beyond 2 levels are currently not supported. |
|sequence_index |Optional for type "video" |`*Integer*`<br><br>Indicates the sequence of multiple child content within the parent content (e.g., episode numbers of a TV drama), enabling cross\-video understanding within the same media series.<br><br>**Note**: Cross\-video understanding will not be performed if this is not provided. |


Please carefully review your data before uploading to ensure that your dataset includes all mandatory fields mentioned above and that these fields use the prescribed names. This ensures smooth data ingestion and the normal operation of subsequent features.

In addition to the fixed fields, you may use **custom fields** to upload other metadata (e.g., content title, video duration, video language, etc.). You can assign any name to these fields—such as the existing names in your database—to simplify the integration process.

&nbsp;

<span id="a98e3175"></span>
## Step 2: Start Creation

This initial step guides you to the dataset creation page to begin the workflow.


1. In the AI Search console, navigate to the **Datasets** page.

2. Click **Create Dataset**. In the pop\-up window, select **Item Dataset** and click **Create Now ** to start the creation process.


<span id="8829dee5"></span>
## Step 3: Upload Data

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3078eb7f2d24428588143550a0475b4c) </span>

&nbsp;

In this step, we will guide you through naming your new video dataset and uploading a sample file to parse data fields and generate configurations.


1. Enter the **Dataset Name** on the creation page.

2. Select **Video Data** as the Dataset Type.

3. **Upload Data:**  Upload a sample of your data here. This helps the system automatically identify fields and generate initial configurations. This is for configuration preview only; you can decide later whether to formally add this data to the dataset. The system supports two upload methods; toggle below the upload control to choose your preferred method.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">\*Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Mandatory Fields:</strong> Each data record must include the following information using strictly prescribed field names:   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Unique Identifier (<code>content_id)</code>: A unique ID (`String`) that serves as the basis for retrieval.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Content Type (<code>content_type</code>): Supports enumerated values: <code>"collection"</code> (media collection) and <code>"video"</code> (video content).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Conditional Mandatory Fields:</strong> These are not required in all cases, but if your data contains this information, you <strong>must</strong> use our prescribed field names: Video URL (<code>video_url</code>), Parent Unique ID (<code>parent_content_id</code>), and Child Content Sequence (<code>sequence_index</code>).   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Schema Consistency:</strong> Conflicting formats for fields with the same name across multiple records will cause an error.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Multi\-level Structure:</strong> Supports nested objects up to 3 levels for effective indexing.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1"><strong>Image Resource Handling:</strong> Supports passing images via URL references. You can provide an image link via a field named <code>cover_image_url</code>. We recommend keeping image sizes under <strong>5MB</strong>.   </div>
   

&nbsp;



<Tabs>
<Tab zoneid="GWziD9c1Xw" title="Upload JSONL file">
<TabTitle>Upload JSONL file</TabTitle>

**Upload JSONL file**

Click or drag a **JSONL file**. The format must follow standard JSONL specifications, with each data entry on a new line. The file size should not exceed **10 MB.** 

The following example demonstrates our required standard JSONL format:

```JSON
{"content_id":"tv_stranger_things_s01_e01","content_type":"video","video_url":["https://example.com/tv_series/67890/episode_01.mp4"],"parent_content_id":"tv_stranger_things_s01","sequence_index":1,"title":"Chapter One: The Vanishing of Will Byers","director":"The Duffer Brothers","actors":["Winona Ryder","David Harbour","Finn Wolfhard"],"actor_names":["Winona Ryder","David Harbour","Finn Wolfhard"],"role_names":["Joyce Byers","Jim Hopper","Mike Wheeler"],"first_air_date":"2016-07-15","douban_rating":null,"genres":["Sci-Fi","Horror","Drama"],"episode_summary":"On his way home from a friend's house, young Will sees something terrifying. Nearby, a sinister secret lurks in the depths of a government lab.","duration":2940,"language":"en-GB","media_link":"https://example.com/tv_series/67890/episode_1/"}
```



</Tab>
<Tab zoneid="rcrVqSruTW" title="Paste JSON data">
<TabTitle>Paste JSON data</TabTitle>

**Paste JSON data**

Paste one or more data entries using the **JSON Object** (or Array<Object\>) format. It is recommended to paste fewer than **100 records ** at a time. You must follow standard JSON formatting when entering the data.

The following example demonstrates our required standard JSON format:

```Plain Text
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
  "douban_rating": null,
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



</Tab>
</Tabs>



4. You can choose whether to enable the ***Automatically delete video files after 7 days*** feature. If enabled, the system will automatically delete the original video files 7 days after processing and intelligent understanding is complete. This is designed to enhance data security and reduce potential leakage risks.

5. Click **`Next: Configure Fields`** to proceed to the data configuration section.


&nbsp;

<span id="2f494731"></span>
## Step 4: Add Fields (Optional)

The platform will automatically identify most data fields based on your uploaded sample data. However, in certain cases, you may wish to add fields manually. The platform provides two methods for manual field addition:

&nbsp;

**Method 1**: Click the blue  **`+ Add Field`** button at the bottom of the field list to add a new field.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/775102ed30064296a4cb345355ca0a31) </span>

&nbsp;

**Method 2**: For fields with a data type of **Object** or **Object Array**, you can click the  **`+`**  ** button** next to the field name. This allows you to add individual nested fields within that object (or within the objects in the array) and specify their names, types, and other information.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">The platform currently supports a maximum nested object depth of <strong>3 levels</strong>.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/85c14f1765c8443d8a0480055d8b386f) </span>

&nbsp;

<span id="6dbf15b8"></span>
## Step 5: Delete Field (Optional)

During the dataset structure configuration, if you find that certain fields are redundant, no longer needed, or were incorrectly identified, you can remove them from the data structure definition. Please note that deleting a field will remove all its associated configuration information.


1. In the field list, locate the field you wish to delete. Click the **`Delete`** button on the far right of the corresponding row to remove it.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Mandatory fields cannot be deleted.</div>


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/3ebbfca9eb49454294027713fec12f02) </span>

&nbsp;

<span id="d63252a9"></span>
## Step 6: Configure Data Attributes

The system has automatically identified and pre\-filled the dataset description, field names, field types, and field attributes based on the uploaded sample data. Please review these auto\-generated configurations. Ensure that your field list correctly identifies and includes the two core fields: `content_id` (Unique Identifier) and `content_type` (Content Type).

&nbsp;

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="warning">Field attributes are used by downstream tasks and <strong>cannot be changed</strong> once configured. Please ensure the accuracy of the attribute settings before saving.</div>


&nbsp;

Compared to Image & Text datasets, video datasets support a richer set of field attributes to meet the requirements of more complex business scenarios.


|**Attribute** |**Mandatory?**  |**attribute description** |
|---|---|---|
|content identifier |**Required & Fixed** |`*String*`<br><br>corresponds to the `*content_id*` field |
|video download URL |**Conditional & Fixed** |`*Array<String>* `<br><br>Corresponding to the `*video_url*` field |
|parent content identifier |**Conditional & Fixed** |`*String*`<br><br>Corresponding to the `*parent_content_id*` field |
|content index |**Conditional & Fixed** |`*Integer*`<br><br>Corresponding to the `*sequence_index*` field |
|content title<br><br> |Optional  |`*String*`<br><br>Title of the media content, uploading this field is strongly recommended |
|media cover image url |Optional |`*String*`<br><br>Download link for the media cover image |
|media page link |Optional |`*String*`<br><br>A link to the media content page, used for previews in search results |
|video duration (seconds) |Optional |`*Int64*`<br><br>Video duration (in seconds) |
|video language (BCP 47)<br><br> |Optional |`*Array<String>* `<br><br>Language tags that comply with the BCP 47 standard<br><br>For example, Chinese: zh; English: en |
|release time  |Optional |`*String*`<br><br>The release or premiere time of media content, formatted in ISO 8601 (YYYY\-MM\-DD T HH:MM:SS), supporting precision to day or second |


You can refer to [Field Attributes](https://docs.byteplus.com/docs/viking-aisearch/Dataset_Introduction#8d68ff39) for detailed explanations of these attributes.

&nbsp;

<span id="411dd2ab"></span>
## Step 6: Synthesize New Fields with LLM (Optional)

After completing the basic field configuration, we offer an advanced feature powered by AI Large Language Models:  **"Synthesize New Fields with LLM."**  This is designed to help you further tap into the potential of your existing data for data enrichment.

This feature can generate entirely new, high\-value text fields based on your existing data. Examples include generating image/text descriptions, extracting core keywords, or creating relevant user query lists. These AI\-generated fields are integrated directly into the dataset, effectively enhancing search and autocomplete performance, thereby improving the overall discoverability and utility of your data.

This is **not a required step** for creating a dataset, but rather an optional advanced optimization. If you are interested in using AI to automatically enrich your content, please refer to [Synthesize New Fields using LLM](https://docs.byteplus.com/docs/viking-aisearch/Dataset_Introduction#2b52d903) for more detailed instructions and explanations.

&nbsp;

<span id="d62ba96d"></span>
## Step 7: Complete Creation


1. Click **Complete configuration ** to create the dataset.


Once the configuration is finalized and activated, the system will automatically perform semantic analysis and indexing of the data.

&nbsp;


---



<span id="d12f9f9b"></span>
# View Dataset

Once the video dataset is created, you can find it in the Dataset List. On the Dataset Details page, you can view basic information, field configurations, and operation history.


1. After successfully creating the video dataset, return to the **Datasets** page to see the newly created item dataset.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/e00a96a93f854bc3a68aab4efd1aba2d) </span>


&nbsp;

2. In the Dataset List, locate the dataset you wish to view and click the **`View`** button in the "Action" column.



&nbsp;

3. **Dataset Details Page**: Once you enter the details page, you will see several key tabs:


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/2a3c31d29a854a31b44b1b1aed9edea1" width="581px" /></div>



   * **Configuration:**  This tab allows you to view and adjust various configuration parameters for the current dataset.

      <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="2">Note      </div>
      

      <div data-tips="true" data-tips-type="warning" data-wrapper-indent="2">Changes made here must be manually confirmed and activated before they are synced to the item dataset and applied to the index configuration.      </div>
      

   * **Data preview: ** This tab allows you to check the status of image/text data validation and processing. You can also view the timestamps for data imports and recent updates, as well as preview the data. 

   * **Activity history: ** You can view all key operations performed on the dataset, such as configuration changes and data import tasks. This allows you to track the modification history of the dataset. 

      * In addition to the Dataset Details page, you can also view the history by clicking the **`Activity history`** button in the "Action" column for the corresponding dataset on the Dataset List page.

   * **Import Data:**  In top right corner, you can add more data.

      * For detailed data import procedures and format requirements, please refer to the [Import and Update Item Data in Real Time](https://docs.byteplus.com/docs/viking-aisearch/Import_and_Update_Item_Data_in_Real_Time)


&nbsp;
