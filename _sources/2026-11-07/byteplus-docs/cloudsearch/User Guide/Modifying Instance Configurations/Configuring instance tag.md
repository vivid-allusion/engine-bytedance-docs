---
title: "Configuring instance tag"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/configure-instance-tag"
---

Tags are used to identify and categorize cloud resources. You can classify instances by tag for simplified instance search and resource aggregation.

<span id="9af8b56f"></span>
## Background information

With the continuous increase of cloud resources, managing them becomes increasingly complex. With the tag management feature offered by BytePlus, you can identify and classify cloud service resources in various dimensions. Once tags are associated with an instance, you can filter a list of instances by tag when retrieving instances. Meanwhile, bill\-split can be applied across various dimensions, which make clear the costs among departments and products.

Cloud Search allows you to add tags to instances, namely manage tag at instance level. A tag is a key\-value pair, consisting of a tag key and a tag value. You can add multiple tags of different categories to each instance, such as `module:https` and `city: beijing`.

<span id="f719a181"></span>
## Limits


* You can add multiple tags of different categories to each instance, but each tag key can only have one tag value. For example, when there is already an existing tag `module:https`, then tag key `module` cannot be added to the same instance.

* Tag information is isolated among different regions. For example, tags created in the China (Beijing) Region are invisible in the China (Shanghai) Region.

* Each instance can be associated with a maximum of 50 tags.


<span id="eddd6b4f"></span>
## Tag configuration rules

Before adding tags to an instance, please understand the rules for setting tags as listed below.


|**Item** |**Description** |
|---|---|
|Tag key |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces, and special characters including `_.:/=+-@`.<br><br>* `volc:` is a default tag key. Your custom tag key cannot start with any case variation of `volc:`.<br><br>* A tag key must be 1 and 128 characters in length. |
|Tag value |* It can contain letters or characters in any language (such as Chinese and English), digits, spaces, and special characters including `_.:/=+-@`.<br><br>* A tag value must be 0 and 256 characters in length, allowing for an empty tag value. |
|Number of tags |* Each instance can be associated with a maximum of 50 tags.<br><br>* You can set up to 20 tags at a time. |


<span id="e2b23930"></span>
## Configure tags


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the name of the instance.

4. On the **Basic information** page, click the edit icon for Tag in basic information pane.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21dd2c9e8eec4d3288c02795e2e79ca1~tplv-goo7wpa0wc-image.image) </span>

5. In the displayed dialog box, you can add, modify and delete tags, and then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7158373b03d74dba8cd0b389fec1e088~tplv-goo7wpa0wc-image.image) </span>


<span id="67ee6341"></span>
## Filter instances by tags


1. Log into the [BytePlus Cloud Search console](https://console.byteplus.com/es).

2. In the top menu bar, select the Project and Region where the desired instance resides.

3. On the **Instances** page, click the filter icon behind **Tag** in the instance list.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d38094cdeed74c38b0305957aae994d9~tplv-goo7wpa0wc-image.image) </span>


4. In the displayed dialog box, choose tag key and tag value as needed.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09260b51131a4cf5b816073c42857c98~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">A maximum of 10 tag filters can be set when filtering instances, with different tags having an OR relationship, meaning a match with any one of the filtering conditions counts as a successful match.</div>



* <div data-tips="true" data-tips-type="tip">Filter by tag key: during the search, only a tag key must be specified, not a tag value. This method is suitable for fuzzy search scenarios.</div>


* <div data-tips="true" data-tips-type="tip">Filter by tag key and tag value: both tag keys and tag values must be specified. This method is suitable for exact search scenarios.</div>
