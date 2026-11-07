---
title: "Synthesize New Fields using Large Language Models"
product: "Viking AI Search"
product_code: "viking-aisearch"
source: "https://docs.byteplus.com/en/docs/viking-aisearch/Synthesize_New_Fields_using_Large_Language_Models"
---

During dataset configuration, we offer an advanced feature powered by AI Large Language Models (LLMs) designed to help you unlock the potential of your existing data. This chapter details how to enable and configure this feature, which analyzes the images and text already in your dataset to automatically generate new text fields. These new fields (such as item descriptions, keywords, and related queries) are integrated directly into your dataset to enhance search, filtering, and autocomplete performance, effectively improving data discoverability and overall value.

<span id="fccac8ad"></span>
# Access the configuration page for synthesizing new fields with LLMs

**During Initial Dataset Configuration**

If you are creating a new dataset, you can enable this feature directly during the data configuration phase by clicking **Create new fields using large model synthesis**.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7e4f81ea971042ef80e335b2de0c96f9) </span>


&nbsp;

1. Follow the dataset creation process till **Configure Data** step.


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1ccd07c8eba24fe4a330f36c0442f497" width="649px" /></div>



&nbsp;

2. On this step's interface, click **OK** to create new fields using large model synthesis.


&nbsp;

<span id="3c6468c4"></span>
# Item Description

Generate a descriptive text (*String type*) using the item's existing text or image fields. This aggregates various pieces of information to enrich searchable data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/1ccd07c8eba24fe4a330f36c0442f497" width="649px" /></div>


To simplify your configuration, the system analyzes your uploaded sample data and automatically fills in the parameters required to create new fields accordingly. We recommend that you refer to the parameter descriptions below,  carefully review these preset values, and adjust them according to your specific needs.


|**Parameter name** |**required** |**parameter description** |
|---|---|---|
|field name |yes |assign a field name to the generated item description field for identification<br><br><br>* supports English letters, numbers, and underscores |
|field source |yes |specify the source for the values in the generated item description field<br><br><br>* example: as shown above, selecting `detail`, `description`, and `features` tells AI to generate the new item description field `generated_description` based on data from these three fields.<br><br>* Supports multiple selectable multimodal sources: images, text, etc. |
|field description |no |a custom description for this field<br><br><br>* length requirement: [1, 500] |


&nbsp;

<span id="17000f4c"></span>
# Keywords

Generates multiple keywords (*Array*) using the item's text or image fields to enrich searchable data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/403446b1df174d55894b8aeb78e427f8" width="667px" /></div>


&nbsp;

To simplify your configuration, the system analyzes the sample data you upload and automatically fills in the parameters needed to create new fields accordingly. We recommend that you refer to the parameter descriptions below, carefully review these preset values, and adjust them according to your specific needs.


|**parameter name** |**is it required** |**parameter description** |
|---|---|---|
|field name |yes |Set a field name to identify the generated keyword field<br><br><br>* Supports English characters, numbers, and underscores |
|Field source |Yes |Specify the source of values in the generated keyword field<br><br><br>* Supports multiple selectable multimodal sources: images, text, etc.<br><br>* Example: as shown in the above image, when you select `title`, `main_category`, and `features`, it instructs AI to generate keywords for the new field `generated_keywords` based on data from these three fields. |
|Number of generated keywords |Yes |Specify the number of keywords to generate<br><br><br>* Default value: 3<br><br>* The user can configure an integer between 1 and 10 |
|Field description |No |Custom description for this field<br><br><br>* Length requirement: [1, 500] |


&nbsp;

<span id="6d5cee64"></span>
# Query List

Generates multiple search queries (*Array*) using the item's text or image fields to enrich search suggestion and autocomplete data.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/eedff8133f2c492d8e9339f3116688fa" width="633px" /></div>


&nbsp;

To simplify your configuration, the system analyzes the sample data you upload and automatically fills in the parameters needed to create new fields accordingly. We recommend that you refer to the parameter descriptions below, carefully review these preset values, and adjust them according to your specific needs.


|**Parameter name** |**Required or not** |**Parameter description** |
|---|---|---|
|Field name |yes |Configure a field name to identify the generated keyword field<br><br><br>* Supports English characters, numbers, and underscores |
|Field source |yes |Specify the source of values in the generated keyword field<br><br><br>* Supports multiple selections and multimodal enhanced sources: images, text, etc.<br><br>* Example: as shown in the above image, when you select `feature` and `details`, it indicates that AI needs to generate the Query list in the new field `generated_search_queries` based on the data from these two fields |
|Number of generated queries |yes |Used to specify the number of Queries generated<br><br><br>* Default value: 3<br><br>* The user can configure an integer between 1 and 10 |
|Field description |No |Custom description of this field<br><br><br>* Length requirement: [1, 500]. |


&nbsp;
