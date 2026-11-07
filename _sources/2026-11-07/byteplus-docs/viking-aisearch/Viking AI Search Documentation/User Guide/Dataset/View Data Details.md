---
title: "View Data Details"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/View_Data_Details"
---

After you complete configuring or creating a dataset, we provide the view data details feature to help you better understand and manage your data. This section explains in detail how to use this feature. This feature provides you with convenient data access and management entry points, allowing you to preview your data immediately after uploading, and easily search and view all historical uploaded data records, so you can clearly and promptly identify and address data with warnings or changes.

We provide specific display modes for **Image/Text** and **Video** data. Below are the detailed instructions for both:

<span id="ca0f4f68"></span>
# View Image & Text Data Details

<span id="b91733a2"></span>
## **Access the data details page**


1. After entering the application you want to view, go to the ** Item dataset** section in the **Configuration** page, and click your dataset name to enter the corresponding dataset page. 


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/61a082a91a8e4a46b167b83a8530f9f8) </span>


&nbsp;

2. On the dataset page, you can see ** Data preview** option; click it to view data details.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/c64c9eea9cb9422c9f28893179f2e853) </span>

&nbsp;

<span id="2d86ab25"></span>
## **Features**

<span id="ac5c954a"></span>
### **Data list**

On the data preview page, you can see four columns: **Content ID, Status, Updated at, Actions**. Below is an introduction to each column's function.


1. **Content ID:**  The list is sorted by import time in descending order. This unique identifier distinguishes each record. You can use the search box on top of it to find a specific ID.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1590826cfe5f403f834cc99f5eb8fc07) </span>


&nbsp;

2. **Status:**  Shows the validation status of your data.

   1. If it shows "Success", it indicates your data status is normal.

   2. If it shows "Failed", it means your data has data quality issues. 



|**Error** |**Description** |
|---|---|
|Custom field type error: field name, field name, ... |The uploaded data contains fields with types inconsistent with your initially defined schema. Please check and re\-upload. |
|Image URL inaccessible |The URLs in the uploaded posters, screenshots, or other film and TV image fields cannot be accessed by our service, or the links are invalid. This does not affect video understanding and retrieval and can be resolved by re\-uploading the links. |


If you have questions about **custom field format errors**, refer to [Data set introduction](https://www.volcengine.com/docs/85296/1544957#%E8%A7%86%E9%A2%91%E6%95%B0%E6%8D%AE%E9%9B%86) to see details about mandatory and optional fields.


&nbsp;

3. **Updated at:**  Displays the timestamp of each record (descending). Hover over the timestamp to see the **First Import Time** and **Last Update Time**.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/25e915b6a0274978af3f4a7d35662099) </span>


&nbsp;

4. **View details:**  Click to view the full Original JSON, the current status, detailed error reports (if any), and the complete update history.


<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/4cbb509a3304419cbf1dc56187646caf) </span>

&nbsp;

<span id="711ff219"></span>
# View Video Data Details

<span id="744ce6cf"></span>
## **Access the data details page**


1. After entering the application you want to check, go to ** Configuration** and then to the **Item dataset** page, click on your dataset name to access the corresponding dataset page.

2. On the dataset page, you can see the **Data preview** option; click it to enter the data details page.


&nbsp;

<span id="1879d68c"></span>
## Features

<span id="fc7dd404"></span>
### Data List


1. **Content ID:**  Displays the unique identifier of the data, sorted by import time in descending order, allowing you to distinguish each piece of your data. You can also use the **search box** on top of it to look up a specific data entry by content ID.

2. **Video download URL:**  Displays the URL of the video file.

3. **Parent content ID:**  if your media information has a hierarchical structure (such as a TV series), this field marks the parent content of the video. The `parent_content_id` of a child content corresponds to the `content_id` of its parent. For more details, please refer to the [dataset introduction](https://www.volcengine.com/docs/85296/1544957#%E8%A7%86%E9%A2%91%E6%95%B0%E6%8D%AE%E9%9B%86).

4. **Content index:**  Shows the sequence number of the content (e.g., Episode number).

5. **Status:**  this shows the status of your data, divided into three states: **Success, Processing, Failed**

   1. If a data's status shows **Success** with no "!" icon on the right, it means your data status is normal and no issue.

      If the data status of an entry shows **Success** but has an "!" icon on the right, it means your data has been successfully stored but may contain some data quality issues. You can hover over the "!" icon to see specific data quality problems.

   2. If the data status of an entry shows **Failed** and has an "!" icon on the right, it indicates that your data status is abnormal. You can hover over the "!" icon to view the specific data error details.


For cases of **Success** ** with an "!" icon on the right**, the included data quality issue types are as follows:


|**Data status** |**Included data validation status** |**Exception impact and solution** |
|---|---|---|
|Data is normal, but there is a "!" icon on the right indicating a warning |Missing unique identifier for parent content |This issue indicates that the data you uploaded is a "single episode" (video) and includes a parent content ID to indicate a hierarchical relationship. However, the collection corresponding to the parent content ID has not been uploaded. This affects the model's ability to link multiple child videos under the parent content for full comprehension.<br><br>Uploading the collection corresponding to the parent content is recommended. |
||Custom field type error: field name, field name, ... |The data you uploaded contains fields inconsistent with the originally defined schema field types. Please check and re\-upload. |
||Image link cannot be accessed**** |The URLs in the uploaded poster, screenshot, and other media image fields cannot be accessed by our service or are invalid. This does not affect video understanding or retrieval and can be resolved by re\-uploading the link. |


For cases of **Failed**, the included data error types are as follows:


|**Data status** |**Included data validation results** |**Anomaly impact and solutions** |
|---|---|---|
|<div style="text-align: center"><br>Data anomaly</div><br> |Abnormal value in the content_type field |content_type contains enum values other than "video" and "collection" |
||For video type data, the video URL cannot be empty |Data of type "video" must upload a video URL for video parsing |
||Parent content can only be a series |For uploaded video data, the "parent_content_id" must refer to a series type ("collection") content |
||Video link is inaccessible |Video link is inaccessible. Check whether the link is valid, if the corresponding video has been deleted, whether it is private, or if it is a video link |
||Duplicate media sequence number |The uploaded video data contains content sequence numbers that duplicate others in the same series, causing confusion in cross\-video content understanding. Recommend re\-uploading. |
||Preset field type error: `field name`, `field name`, ... |The preset fields for video data ("content_id", "parent_content_id", "content_type" or "sequence_index", "video_url") have data types that do not conform to definitions |
||Video size exceeds processing limit |The total video size uploaded in "video_url" must be kept under 10GB |
||Video length exceeds processing limit |The total length of the uploaded video in "video_url" must be under 3.5 hours |
||Video processing error |An error occurred during video processing; if this happens, you may contact us for assistance |


For data with both of the above validation issues, the data status will display as **Failed**. You can hover over the "!" icon to view all validation errors.

If processing fails during data updates, then:


   1. If the data **already exists**, the original data is retained. The list information remains consistent with the original data, and the new data is discarded.

   2. If the data **did not exist** before, the new data is not discarded but saved in the dataset. The list information remains consistent with the new data.

6. **Updated at:**  shows the first import time and update status of the data.

   1. You can view the description of the update time by hovering over the header of the **Updated** ** at** column: data with failed updates will retain the most recent successful update content.

   2. For data with the status **Processing**, you can view the ** first import time** by hovering over the update time.

   3. For data with the status **Success**, you can view the **first import time, last effective update time, and most recent update time** by hovering over the update time.

   4. For data with status **Failed**, you can view the **first import time, last effective update time, most recent update time, and reason for the anomaly** by hovering over the update time.

7. **View details:**  comprehensively view the **specific content of a data entry** along with its **data status** and **data records**. The full content of the original data JSON is displayed, along with the data status and detailed issues if the status is abnormal, and at the bottom, the first import time and most recent update records of the data are shown.
