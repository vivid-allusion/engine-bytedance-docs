---
title: "Set Field Value Aliases"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Set_Field_Value_Aliases"
---

Setting field value aliases can enhance data readability. Users can set aliases for dimension field values either manually or by binding to other fields. This article introduces how to set field value aliases.

<span id="_1-概述"></span>
# Feature overview

Users can assign aliases to specific data in dimension fields, either manually or by binding to other fields.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For example, if the "City" field in a dataset contains values such as 010, 020, 021, and more, you can use alias management to display the names as Beijing, Guangzhou, and Shanghai, making it easier for business personnel to understand the data. If the "country" field in a dataset is displayed in Chinese, such as 中国, 美国, 新加坡, and more, you can display them in English to help foreign members of the business team understand the data.</div>


<span id="e37eafef"></span>
# Prerequisites

Your account must have the necessary permissions to set field value aliases. For authorization operations, see [Role Management](https://docs.byteplus.com/docs/DataWind/Role_Management):


* To set aliases for dataset fields, you need edit permissions for the dataset.

* To set aliases for your own personal fields, no additional permissions are required.


<span id="293c31e6"></span>
# Manually set aliases


1. Click the settings icon to the right of the dimension field name and select "Field value alias".


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2dcd2ad8879f485d96bfa7bce317af8b~tplv-goo7wpa0wc-image.image) </span>


2. In the pop\-up field value alias configuration box, select the enumeration value to be aliased on the left, set the corresponding alias on the right, and click the plus sign below to add more alias values.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd4a99e74e204f6a8ca747ee2c48ca3e~tplv-goo7wpa0wc-image.image) </span>


3. Select the "Alias display mode" and confirm to save.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/244d2d552f2242209595d093f6e36613~tplv-goo7wpa0wc-image.image) </span>


|Alias display modes |Display result examples |
|---|---|
|Alias only |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53812c55ee6d4b53bf752430a66fa271~tplv-goo7wpa0wc-image.image) </span> |
|Original value only |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345117a353194de3afbbeba622d0b1de~tplv-goo7wpa0wc-image.image) </span> |
|Alias + original value |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/364d885892aa48f4ac706ee0cb9c093d~tplv-goo7wpa0wc-image.image) </span> |


<span id="e4065596"></span>
# Bind to other fields

In addition to manual input, field value aliases can also be set by binding to other fields in the same dataset field list. After selecting the corresponding binding field, aliases will be configured for the current field according to the mapping relationship. Multiple alias display modes can also be set.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89ed7fee3c9e461a8a310c5af8f0163d~tplv-goo7wpa0wc-image.image) </span>
