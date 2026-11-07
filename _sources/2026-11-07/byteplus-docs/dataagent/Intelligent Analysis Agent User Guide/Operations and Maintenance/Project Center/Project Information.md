---
title: "Project Information"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Project_Information"
---

<span id="_1-概述"></span>
# 1. Overview

As a project administrator, when you enter the project center, the first interface you see is the project information interface. Here, project administrators can view the basic information of the project and configure project\-level settings, including project type, project control level, dataset display rules, field display rules, multilingual display configuration, default units for data formats, rules for using extracted datasets, and so on.

<span id="_2-功能介绍"></span>
# 2. Feature introduction

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

**View and edit project information**: Project administrators can view and edit the basic information of the project (such as project administrator, project name, and so on).

**Configure project\-related settings**: Project administrators can configure project\-related settings (such as whether the project is confidential, project control level, and so on).

<span id="_2-2-功能具体介绍"></span>
## 2.2 Detailed feature description

As a project administrator, when you click Project Center, the first screen is the project information screen.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/326ed1bef863447dbd9ad5dcd9ec43d9~tplv-goo7wpa0wc-image.image) </span>

(1) Basic information: You can view the basic information of the project (such as project name, project administrator), and you can modify the project name.

(2) Project settings (only administrators can change settings):


* Project type: This sets whether the project is confidential. Confidential projects are only visible and searchable to authorized users in the project list.

* Project control level settings are divided into "General", "Moderate", and "Strict". The differences are as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/feb0026c2a9846f392c823f21c705082~tplv-goo7wpa0wc-image.image) </span>

The project control level can be switched between options. New resources are handled according to the selected level, while historical data is not affected. Frequent switching is not recommended.


* Dataset display rules: Supports switching between [All datasets] and [Authorized datasets only] modes. If configured as [Authorized datasets only], users in the project can only see datasets for which they have permission.

* Field display rules: Supports switching between [All fields] and [Authorized fields only] modes. If "All fields" is selected, all fields will be displayed when users access Visual Query/Metric Query, and fields without column permissions will be grayed out. If "Only authorized fields" is selected, only fields with column permissions will be displayed when users access Visual Query/Metric Query. In addition, when accessing the details page of a dataset/business subject without permissions, the field information (such as field names and field descriptions) of that dataset/business subject will not be displayed on the page.

* Configure multilingual display: After enabling this option, resources such as dataset names and dataset field names can be configured for multiple languages.

* Default unit for data format: Supports switching among three modes—[Auto], [Chinese unit], and [English unit]. When data format is automatically inferred for display, the set Chinese or English unit will be used for display. For example, if a project is set to use English as the default data format unit, all data formats set to [Auto] within that project will be automatically inferred and displayed using English units (K, M, B, and so on) by default.

* Extraction dataset usage rules: This sets the available scope for extraction datasets. [Available to all] applies no special restrictions. [Available only to project administrators] means extraction datasets can only be used within the configured scope of usage rules; in all other cases, they are disabled.
