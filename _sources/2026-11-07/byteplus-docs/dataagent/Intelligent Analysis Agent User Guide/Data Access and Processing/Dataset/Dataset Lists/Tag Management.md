---
title: "Tag Management"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Tag_Management"
---

<span id="_1-概述"></span>
# 1. Overview

Datasets in a project are often in different business states and need to be identified during use. **For example: deprecated, pending transformation, completed data warehouse construction, and more.**  By using tag management, datasets in a project can be categorized by tags, and the corresponding tags can be displayed in downstream charts and dashboards, helping readers quickly understand the data status. Tag management consists of three parts: project tag settings, dataset tagging, and tag display, among which **only project administrators can set tags**.

<span id="_2-快速入门"></span>
# 2. Quick start

> Note: Only project administrators can manage tags


<span id="_2-1-设置标签"></span>
## 2.1 Set tags

In the dataset overview interface, click "Tag management" in the upper right corner to set the tag list. Dataset tags will be applied based on this list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/929544e2819e49d6b826c151454bca8c~tplv-goo7wpa0wc-image.image) </span>

Click "Create tag" to create a tag and set the tag color. Click Confirm to complete the creation. Be cautious when selecting "Inherit this tag in chart titles"; recommended scenarios include "about to be decommissioned", "data missing", and many other cases.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1310dc337c5945f583bb23ed318bed61~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-数据集打标"></span>
## 2.2 Tag datasets

Select a dataset, click the ⋮ to the right of the dataset name in the dataset list, and select "Set tags".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/75f6149f0d514c059f909f3a4435aa5f~tplv-goo7wpa0wc-image.image) </span>

After selecting the required tags, click Confirm. Supports selecting multiple tags and searching tags.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/74897e84f37c47aa89131305f294eb4a~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-标签显示"></span>
## 2.3 Tag display

On the dataset information page, you can see the tags associated with the dataset and quickly distinguish the dataset status.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e842972ddf814aca8da0371ac34669df~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

> Note: Only project administrators can manage tags


<span id="_3-1-标签编辑及标签显示位置"></span>
## 3.1 Tag editing and tag display location

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4b3c0f22abda4ccdad20b98f7f192ef8~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Tag name: The display name of the tag

* Tag style: The color of the tag, supports seven preset color combinations, and you can preview the effect after selection

* Inherit this tag in chart titles: Can be selected, not selected by default.

   * If not selected: Datasets using this tag will display the tag next to the dataset name on the dataset information page

   * When checked: For datasets using this tag, in addition to the locations mentioned above, this tag will also be displayed next to the chart name in charts using the dataset, next to the chart name in dashboards, and in the chart tooltip information in dashboards.


<span id="_3-2-标签增删"></span>
## 3.2 Add or remove tags

Administrators can add or remove tags when managing tags.

<span id="_3-3-新建标签"></span>
## 3.3 Create a new tag

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/68e29dd2158844458b88a87ad05b9d1f~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-4-删除标签"></span>
## 3.4 Delete a tag

After deletion, the tags associated with datasets using this tag will also disappear.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0b78ea9da2374322be919b14ee9fe47c~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-5-数据集标签编辑"></span>
## 3.5 Edit dataset tags

Find the dataset to be tagged in the dataset list, click the ⋮ to the right of the dataset name, and select "Set tags".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/66556d9a7c0c4978bdf88e67a1b27169~tplv-goo7wpa0wc-image.image) </span>

In the pop\-up window, you can check or uncheck the required tags. To remove a tag, either uncheck it or click the × next to the selected tag.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38e53aecbdc74faaa84cbce62eccf495~tplv-goo7wpa0wc-image.image) </span>

If there are no tags in the project, the prompt "No tags available" will be displayed. For project administrators, the prompt "Click here to create a new tag" will also be displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ead541bdae549749f52521a828f8784~tplv-goo7wpa0wc-image.image) </span>
