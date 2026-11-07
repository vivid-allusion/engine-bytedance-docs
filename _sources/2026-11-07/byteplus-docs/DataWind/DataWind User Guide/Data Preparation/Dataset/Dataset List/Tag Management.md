---
title: "Tag Management"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Tag_Management"
---

<span id="_1-概述"></span>
# 1. Overview

Datasets in a project are often in different business states and need to be identified when used. **For example: deprecated, pending transformation, completed data warehouse construction, and more.**  Through tag management, datasets in a project can be categorized by tags, and the corresponding tags can be displayed in downstream charts and dashboards, helping readers quickly understand the data status. Tag management consists of three parts: project tag configuration, dataset tagging, and tag display, among which **only project administrators can configure tags**.

> [Mirror Dataset](https://docs.byteplus.com/docs/DataWind/Mirror_Dataset)：The tags are consistent with the original dataset


<span id="_2-快速入门"></span>
# 2. Quick start

> Note: Only project administrators can manage tags


<span id="_2-1-设置标签"></span>
## 2.1 Configure tags

On the dataset overview page, click "Tag management" in the upper right corner to configure the tag list. Dataset tags will be assigned based on this list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d315586ffcb745a5a0286fc75e60798e~tplv-goo7wpa0wc-image.image) </span>

Click "Create tag" to create a tag and set the tag color. Click Confirm to complete the creation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24143569f43343439a9d0e12bbb4ac02~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-数据集打标"></span>
## 2.2 Dataset tagging

Select a dataset, click the ⋮ to the right of the dataset name in the dataset list, and select "Configure tags".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f63f75d35e14117bba14efb7ae8a7c7~tplv-goo7wpa0wc-image.image) </span>

After selecting the required tags, click Confirm. Supports multiple selection and tag search.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86180a5c5fbc48668418f46b434ac355~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-3-标签显示"></span>
## 2.3 Tag display

On the dataset information page and in the dataset information pop\-up in visualizations, you can see the tags associated with the dataset and quickly distinguish the dataset status.

> To display tags in chart titles on dashboards, select "Inherit this tag to chart title" when editing tags in Step 1.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e49a89d7bf24e17924c7ea3e2d38bc4~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

> Note: Only project administrators can manage tags


<span id="_3-1-标签编辑及标签显示位置"></span>
## 3.1 Tag editing and tag display locations

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/347cd9571b8547938f37edcdb9f0f8f0~tplv-goo7wpa0wc-image.image" width="610px" /></div>



* Tag name: The display name of the tag

* Tag style: The color of the tag, supports seven preset combinations, and you can preview the effect after selection

* Inherit this tag to chart title: Can be selected, not selected by default.

   * If not selected: For datasets using this tag, the tag will be displayed next to the dataset name on the dataset information page and in the dataset information toolbar in visual query.

* If selected: For datasets using this tag, in addition to the above locations, the tag will also be displayed next to the chart name where the dataset is used, next to the chart name on the dashboard, and in the chart toolbar information on the dashboard.


<span id="_3-2-标签增删"></span>
## 3.2 Add or remove tags

When administrators manage tags, they can add or delete tags.

<span id="_3-3-新建标签"></span>
## 3.3 Create a new tag

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05fd9125d0734d71a5a3cee8f535c7d9~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-4-删除标签"></span>
## 3.4 Delete a tag

After deletion, the corresponding tag for datasets using this tag will also disappear.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91a3d1f7c4264e35bd214776139d5dc7~tplv-goo7wpa0wc-image.image" width="610px" /></div>


<span id="_3-5-数据集标签编辑"></span>
## 3.5 Edit dataset tags

In the dataset list, find the dataset to be tagged, click the ⋮ to the right of the dataset name, and select "Set tags".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d415645bb8b48939a511d75cf173a8a~tplv-goo7wpa0wc-image.image) </span>

In the pop\-up window, you can select or deselect the required tags. To remove a tag, either deselect it or click the × next to the selected tag.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/443e1e8311a343169e526dd52eed86b2~tplv-goo7wpa0wc-image.image) </span>

If there are no tags in the project, the message "No tags available" will be displayed. For project administrators, the message "Click here to create a new tag" will also be displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/05648b4dafad4e11b2186e30c405d5b0~tplv-goo7wpa0wc-image.image) </span>
