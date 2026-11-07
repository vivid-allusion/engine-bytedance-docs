---
title: "Effeciency: Dimensional Dictionary"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Effeciency_Dimensional_Dictionary"
---

Dimension dictionary is used to translate property values, converting poorly readable values into readable text, and is a function of processing data during query. This is very useful in some scenarios where the readability value cannot be reported during event tracking reports. Other common scenarios also have inconsistent reported values, such as case inconsistencies, such as: "xiaomi", "Xiaomi", expect to correspond to the same "Xiaomi", so it should also be treated as "Xiaomi" when filtering and grouping. This article provides you with the functionality details of the DataFinder Dimension Dictionary.

<span id="_2-使用说明"></span>
# Upload Dimension Dictionary

<span id="_2-1-属性管理"></span>
## Operation entrance

On the Event Properties and User Properties feature page in Data Management, you can see that the "Dictionary" column has been added to each row. Click **Upload** under the Dictionary column to upload a dimension dictionary.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff5e7ed038de43858cd870b457c085de~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Upload</strong> as gray means that the corresponding property is a system preset property, and the upload dimension dictionary is not supported.</div>


<span id="_2-2-准备字典文件"></span>
## Prepare dictionary file

Click the "Upload" link in a property dictionary column to configure a dictionary file for that property.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62abd7d2ccf14ac89ba68b4e1102b491~tplv-goo7wpa0wc-image.image) </span>

The format requirements for a dictionary file are as follows:


* UTF\-8 encoding format

* Suffix csv or txt

* 1 correspondence per line, separated by English commas, for example: `original value, translation value`

* File content should be less than 100,000 lines, the whole should be less than 10Mb

* The content length of the original and translated values should not exceed the maximum allowed by the system, currently both 1024 characters


<span id="_2-3-完成上传"></span>
## Complete upload

The properties of uploaded dictionary files will change from "Uploaded" to "Uploaded", and previously uploaded dictionary files can be downloaded or deleted.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51c734be0ee840a29bb2c37ced11286c~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After the dictionary file is successfully uploaded, the system needs about 20 to 30 minutes to update the data. Please check again in 30 minutes.</div>


<span id="_2-4-进行查询"></span>
# Application example


1. Take the property "Owned Platform" as an example. When the property does not configure the dimension dictionary, the property grouping display results are as follows:

   <span>![图片](https://lf3-volc-editor.volccdn.com/obj/tos-cn-v-697126/1c8f1f15a07d4b2e84ac7024c19a3f47) </span>

2. Created a dictionary file with the following content for the owning platform properties:

   ```Plain
   *, cross terminal
   app, Mobile terminal
   mp, Mini Program
   web, Website
   ```
   

3. After the upload is successful, about 20 minutes later, the query is initiated again, and you can see that the property value has been translated. The grouped display results are as follows:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a6b05cbba3743d0ba014272f559986a~tplv-goo7wpa0wc-image.image) </span>


<span id="_3-功能限制"></span>
# Usage restrictions

<span id="_3-1-支持维度字典的数据类型"></span>
## Data types that support dimension dictionaries


|Property data type |Whether to support uploading dictionaries |Logical description |
|---|---|---|
|string |support |The dictionary does not take effect when calculating maximum/minimum/average/SUM/PCT, filter conditions greater than or equal to, less than or equal to, deduplicate, and still uses the original value calculation |
|int |support ||
|float |support ||
|version |support ||
|list |SaaS\-cloud\-native is not supported, privatization is supported ||
|dataime |Not supported |Does not involve |


<span id="_3-2-部分预置属性不支持配置维度字典"></span>
## Some preset properties do not support the configuration dimension dictionary

Event properties


|**Property name** |**Property description** |
|---|---|
|first_utm_source |ad monitoring |
|first_utm_medium |ad monitoring |
|first_utm_campaign |ad monitoring |
|first_utm_term |ad monitoring |
|first_utm_content |ad monitoring |
|utm_campaign |ad monitoring |
|utm_source |ad monitoring |
|utm_term |ad monitoring |
|utm_medium |ad monitoring |
|utm_content |ad monitoring |
|utm_source |ad monitoring |
|is_login |Whether to log in |
|user_is_new | |
|tracking_id | |
|custom_mp_platform | |
|mp_platform | |
|gender |Gender |
|first_utm_campaign |ad monitoring |
|utm_campaign |ad monitoring |
|$inactive |Is it a passive event? |
|campaign_group_id |ad monitoring |
|first_utm_source |ad monitoring |
|promotion_channel_id |ad monitoring |
|$campaign_group_id |ad monitoring |
|$is_first_time |Whether to visit for the first time |
|$is_first_day |Whether to visit on the first day |
|scene |Scene Value (Mini Program) |
|$utm_from_url |ad monitoring |
|first_visit_source | |
|tr_admaster |ad monitoring |
|tr_param1 |ad monitoring |
|tr_param2 |ad monitoring |
|tr_param3 |ad monitoring |
|tr_param4 |ad monitoring |
|tr_shareuser |ad monitoring |
|is_from_tracer |ad monitoring |
|activation_channel |ad monitoring |
|activation_type |ad monitoring |
|tr_install_type |ad monitoring |
|install_type |ad monitoring |
|ab_version |A/B test experimental version |


<span id="_3-3-部分属性配置限制"></span>
## Partial property configuration restrictions

loc_city_id, loc_country_id, loc_province_id these three properties rely on numbers 5, 6, 7 and < = 0, so it is forbidden to configure such data as the original value.
