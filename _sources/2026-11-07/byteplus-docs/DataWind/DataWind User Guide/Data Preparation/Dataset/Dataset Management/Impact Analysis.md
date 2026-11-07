---
title: "Impact Analysis"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Impact_Analysis"
---

<span id="d0418190"></span>
# 1. Overview

Impact analysis is a feature used to remind users of the relationships between data resources and to assess the potential impact of changes. When users delete or modify datasets, dimensions, or measures, the product displays a pop\-up window with an impact explanation to help users understand the risks of modifying or deleting resources and reduce unnecessary losses caused by accidental deletions. Supports counting the total number of related downstream charts and dashboards for datasets, dimensions, or measures, as well as the total number of accesses in the past 30 days.

(This feature is currently only available for self\-hosted deployments of version V2.72.0 and above. To use this feature, please contact your company's sales representative or customer success manager for purchase information.)

<span id="270b0563"></span>
# 2. Feature introduction

<span id="eb1be36c"></span>
## 2.1 Dataset impact analysis

On the details page of a dataset in Data Preparation, when deleting a dataset, impact analysis is automatically performed and the results are displayed in a pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb53ecd75fc54902a11a5af5d37b600e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c712d1d3ba946ae9e43657a80e75c04~tplv-goo7wpa0wc-image.image) </span>

<span id="0cb1ccb5"></span>
## 2.2 Dimension/measure impact analysis

In the Data Preparation dataset module and the Visual Query module, when deleting or modifying fields, the dimension/measure impact explanation is automatically performed and the results are displayed in a pop\-up window.

The following figure demonstrates the operation steps in the dataset module. The operation in the Visual Query module is similar and will not be repeated here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2fd56b21c174670a5e617966b4f4c47~tplv-goo7wpa0wc-image.image) </span>

Supports selecting multiple fields to delete. Impact analysis will count the overall and individual impact of each field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4ff2e0f8c054451cafec75d3f60dffe3~tplv-goo7wpa0wc-image.image) </span>

<span id="63941918"></span>
## 2.3 View lineage details

In the impact analysis pop\-up window, there are "View lineage details" and "Details" buttons. Clicking these buttons will redirect to the lineage analysis page.

For more information about lineage analysis, see [Lineage Analysis](https://docs.byteplus.com/docs/DataWind/Lineage_Analysis).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1105a5dd85a747bab7ebd459a51d8f24~tplv-goo7wpa0wc-image.image) </span>
