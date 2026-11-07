---
title: "Project Information"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Project_Information"
---

<span id="_1-概述"></span>
# 1. Overview

As a project administrator, the first screen you see upon entering the project center is the project information interface. Here, project administrators can view basic project information and configure project\-level settings, including project type, project control level, dashboard display rules, dataset display rules, rules for downloading or copying data, whether to allow embedding project resources, default units for data formats, and a resource overview.

<span id="_2-功能介绍"></span>
# 2. Feature overview

<span id="_2-1-常用使用场景"></span>
## 2.1 Common use cases

**View and edit project information**: Project administrators can view and edit basic project information (such as project name and logo), and view the growth trends of dashboards, datasets, and disk space usage within the project.

**Configure project\-related settings**: Project administrators can configure project\-related settings (such as setting the project as confidential, or configuring the public dashboard or dataset list page to display all items or only those with full permissions).

<span id="_2-2-功能具体介绍"></span>
## 2.2 Detailed feature description

As a project administrator, clicking Project Center brings you to the project information interface as the first screen.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f796f577c89402bb7a0c95e71ad2c1d~tplv-goo7wpa0wc-image.image) </span>

(1) Basic information: You can view basic project information (such as logo, project name, and project administrator), and modify the project logo and project name.

(2) Project settings (only administrators can change settings):


* Project type: This sets whether the project is confidential. Confidential projects are only visible and searchable to authorized users in the project list.

* Project control level settings are divided into "General", "Moderate", and "Strict". The differences are as follows:


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f8dce534810430bb1f5e800c76a2885~tplv-goo7wpa0wc-image.image) </span>

The project control level can be switched between modes. New resources are handled according to the current level, while historical data remains unchanged. Frequent switching is not recommended.


* Public dashboard/dataset list display rules: Supports switching between [All dashboards] and [Dashboards with permissions only] modes. If configured as [Dashboards with permissions only], users in the project can only see dashboards or datasets for which they have permissions.

* Download/copy data: Whether to allow project members to download or copy data, including results from visualized queries on datasets and dashboard data. You can configure the following options: allow all resources, disallow all resources, allow only some resources, or disallow only some resources. If you select to allow or disallow only some resources, you need to click the "Resource list" next to specify which resources can or cannot be downloaded and copied.


(3) Resource overview: You can view the number of dashboards, number of datasets, storage size, trends over the past 30 days, as well as growth compared to yesterday and week\-over\-week data within the project.

<span id="_2-3-特殊场景"></span>
## 2.3 Special scenarios

On\-premises deployment supports encrypting embedded links into short links, which requires the project administrator to perform relevant operations in the project information interface. Details are as follows:

First, the system administrator needs to check "Encrypted embed" in System Management \> Security Settings \> Network Zone Access Control.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ce83f2b4956e4039aa2bfcc7bc6d60bc~tplv-goo7wpa0wc-image.image) </span>

Second, the project administrator needs to check "Include encrypted embed" in the embedded project resources section in Project Center \> Project Information.

Finally, when users in the project embed charts or dashboards, the embedded links will be encrypted.
