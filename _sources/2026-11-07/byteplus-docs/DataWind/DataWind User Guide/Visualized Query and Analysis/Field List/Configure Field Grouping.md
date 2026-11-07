---
title: "Configure Field Grouping"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Configure_Field_Grouping"
---

Configuring field grouping enables information to be displayed in a collapsible format. This document describes how to create groups, including grouping by field values, by conditions, and by custom intervals.

<span id="_1-概述"></span>
# Feature overview

When there is a large amount of information and fields need to be displayed in groups, you can create groups to enable collapsible display. For dimension and metric fields, the supported field grouping methods currently differ. Details are as follows:


|Field type |Supported grouping methods |
|---|---|
|Dimension |Group by field value and group by condition |
|Metric |Group by field value, group by condition, and group by custom step size |


<span id="7ba16fe3"></span>
# **Application scenarios**


* Merging dimension items of text fields: Divide the field values in the "Country" field into "Europe", "Asia", and more, generate a new group field "Continent", and then use "Continent" as a dimension for analysis.

* Custom numeric metric data buckets: Divide the sales price into buckets such as 0\-100, 100\-300, and 300\-500 to analyze data performance within each range.


<span id="_2-快速入门"></span>
# Quick start


1. Select the field to be grouped and click [Create group].

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24762a7d3d5b4532a341efff04f1026e~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

2. Configure the field name, select the grouping method, set detailed grouping conditions and rules, and then click "OK" to confirm.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/810bc697b2f246da986ee4e2f4248540~tplv-goo7wpa0wc-image.image) </span>

   The following describes the relevant parameter configurations.

   
   |Parameter |Configuration description |
   |---|---|
   |Field name |The default format is "original field name (group)", and users can customize the field name after grouping. |
   |Grouping method |Includes two grouping methods: "by field value" and "by condition":<br><br><br>* Group by field value: Allows users to place field values into a specific group folder by fuzzy search or drag\-and\-drop.<br><br>* Group by condition: Allows users to set one or more AND/OR conditions for string or numeric fields to group them. |
   |Automatically merge ungrouped fields |All field values not assigned to a group are merged into a new group, with the default name "Ungrouped". Users can rename this group. |
   |Save to dataset |If "Save to dataset" is not selected, the added field will be a personal expression field.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Personal expression fields can be used for data analysis and exploration, but differ from other fields in the following ways:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When a field is a personal expression field, other users will not see this field when opening the dataset via "Switch Dataset".</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When a chart contains a personal expression, if the link is shared with others, they can query this field but cannot modify the field or view the field expression. At the same time, this field will appear grayed out in the dimension or metric bar for other users.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When a personal expression is referenced, it will be prefixed with "Personal".</div><br> |
   


<span id="_3-2-分组方式-字段值分组"></span>
# Grouping method \- group by field values


1. Click [Create group] to add a new group. Grouping by field values is supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed836c2298d4fef9c166931450316a3~tplv-goo7wpa0wc-image.image) </span>

2. When configuring groups, users can group by performing a fuzzy search or by directly dragging and dropping.

   * Users can use fuzzy search to filter field values, click [Add to], and select [Group];

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3949267dd5e44dca8efddee871c42131~tplv-goo7wpa0wc-image.image) </span>

   * Users can also drag and drop field values into a specific group folder.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c11c7d5a10564fb3956ff714f36544a4~tplv-goo7wpa0wc-image.image) </span>


<span id="93db3858"></span>
# Grouping method \- group by conditions


1. Click [Create group] to add a new group. Grouping by conditions is supported.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/666fbe1f65944f529c4cf6e47085bba7~tplv-goo7wpa0wc-image.image) </span>

2. When configuring groups, multiple grouping conditions can be added, and the logical relationships between grouping conditions can be set.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6783f882263c4f08810a7b3c322e4e26~tplv-goo7wpa0wc-image.image) </span>

   The parameter configuration instructions are as follows.

   
   |Parameter |Configuration description |
   |---|---|
   |Add condition |* For string fields, the following operators are supported: (not) contains, starts with (ends with), (not) like, (not) is null, (not) is empty string, and more.<br><br>* For numeric fields, the following operators are supported: =, ≠, \>, ≥, <, ≤, (not) is null, and more<br><br>* For boolean fields, the following operators are supported: =, ≠, (not) is null, and more. |
   |Set the logical relationship between conditions |Set whether the grouping method needs to meet "all conditions" or "any condition".<br><br><br>* If set to "all conditions", the conditions must have an AND relationship<br><br>* If set to "any condition", the conditions must have an OR relationship |
   

   For string types, the operator explanations are as follows:

   
   |Operator |Actual operation |
   |---|---|
   |Contains |like |
   |does not contain |not like |
   |starts with |like |
   |ends with |not like |
   |like |like |
   |not like |not like |
   |is empty |is null |
   |is not empty |is not null |
   |is an empty string |is empty |
   |is not an empty string |is not empty |
   


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">When grouping by conditions, ensure that the conditions for each group are mutually exclusive; otherwise, field values will be assigned to the first group, ensuring that each data entry belongs to only one group. For example, if the condition for group 1 is "contains Jiangsu" and the condition for group 2 is "contains Jiangsu" or "contains Hunan", then a field with the value "Jiangsu" will be assigned to group 1.</div>



<span id="c88b335a"></span>
# **Rename group**

Double\-click or click [Rename] to modify the group name.


* Group by field values interface:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5dba015df15b471da75ae8c6e313e664~tplv-goo7wpa0wc-image.image) </span>

* Group by conditions interface:

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/26e2b919eff941709c6d9f95aff05de8~tplv-goo7wpa0wc-image.image) </span>


<span id="c4727af6"></span>
# **Ungroup and delete group**

In the group by field value mode, all field values contained in the group are removed from the group, and the removed field values will be in an ungrouped state.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afeed2a3d1764dc18c5faad84b428eaa~tplv-goo7wpa0wc-image.image) </span>

In the group by condition mode, deleting existing groups is supported.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0b579814d904f4aac07d95f6d057e04~tplv-goo7wpa0wc-image.image) </span>

<span id="6153b08b"></span>
# Edit group

To modify the current grouping fields, click "Edit group" in the dimension field list area for the grouped field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a84ba23e69244ea79dee5bf08857afd1~tplv-goo7wpa0wc-image.image) </span>
