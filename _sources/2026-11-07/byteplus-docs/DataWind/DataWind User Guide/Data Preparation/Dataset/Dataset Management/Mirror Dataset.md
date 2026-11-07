---
title: "Mirror Dataset"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Mirror_Dataset"
---

<span id="_1-概述"></span>
# 1. Overview

Dataset producers can use the mirror dataset feature to allow multiple projects to use the same dataset (identical data source, data model, dimensions, and metrics) for creating charts and dashboards through simple configuration, saving storage resources and reducing operational costs.

**Common application scenarios**


* The same dataset needs to be reused across multiple business lines, but unified data management and operations standards are required.


<span id="_2-快速入门"></span>
# 2. Quick start

**Step 1:**  Click the dataset to be configured, go to the dataset overview page, and click the top right corner to configure cross\-project settings.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9892f1af1182434b84e3489931f699f0~tplv-goo7wpa0wc-image.image) </span>

**Step 2:**  Select the projects that need to use this dataset, and enable or disable usage notifications as needed.

If notifications are enabled, when a member of the target project uses this dataset to create a chart or dashboard, the designated administrator will receive a notification.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36404c9171ef408aa7c8d83baf414dbe~tplv-goo7wpa0wc-image.image) </span>

**Step 3:**  Users can independently enter the corresponding project to view the mirror dataset and perform subsequent operations such as building charts or dashboards. The mirror dataset supports adding fields, batch editing fields, and viewing the dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/208529b279ba4677bdf25a7cb21b800d~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能介绍"></span>
# 3. Feature introduction

To facilitate understanding of the following feature introduction section, we have standardized the descriptions as follows:

The user configures a cross\-project mirror for the **referenced dataset** in the **original project**, specifies the creation of a **mirror dataset** in the **new project**, and creates a **new chart or new dashboard** based on this dataset.

<span id="_3-1-被引用数据集的管理"></span>
## 3.1 Management of referenced datasets

<span id="_3-1-1-授权管理"></span>
### 3.1.1 Authorization management


* Copy dimension and metric configurations, and synchronization task settings for extract\-type datasets

* Do not copy dataset permission configurations or the physical data of extract\-type datasets


<span id="_3-1-2-开启-关闭镜像连接"></span>
### 3.1.2 Enable/disable mirror connection


* Add or remove projects in the cross\-project configuration pop\-up on the dataset page as needed

* If the mirror connection is enabled, the mirror dataset can be searched and viewed in the dataset list of the new project

* If the mirror connection is disabled, this mirror dataset will not appear in the dataset list of the new project


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b7f3a20ef14436da25905641561ce90~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-3-配置变更"></span>
### 3.1.3 Configuration changes

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a3b74aa3b7a4427a005aa30f62b9d5b~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-1-4-管理运维"></span>
### 3.1.4 Operations and maintenance


* All dataset editing, access/log management, and lineage management operations must be performed on the referenced dataset.


<span id="_3-2-镜像数据集的管理"></span>
## 3.2 Management of mirrored datasets

<span id="_3-2-1-使用权限"></span>
### 3.2.1 Usage permissions


* To use mirrored datasets (for querying, charting, or creating dashboards) in a new project, authorization from the administrator of the referenced dataset in the original project is required.


<span id="_3-2-2-管理运维"></span>
### 3.2.2 Operations and maintenance


* Editing, operations and maintenance, and governance actions are not supported for mirrored datasets within new projects.

* To modify configurations, changes must be made based on the referenced dataset.

* Accesses in the original project and multiple new projects are all counted in the access statistics of the referenced dataset, facilitating governance.
