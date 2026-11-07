---
title: "Impact Analysis"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Impact_Analysis"
---

<span id="d0418190"></span>
# 1. Overview

Impact analysis is a feature designed to alert users to the relationships between data resources and to assess their impact. When users delete or modify datasets, dimensions, or metrics, the product displays a pop\-up window with an explanation of the impact, helping users understand the risks associated with deleting or modifying resources and reducing unnecessary losses caused by accidental deletion. Provides statistics on the total number of related downstream charts and dashboards for datasets, dimensions, or metrics, as well as the total number of accesses in the past 30 days.

<span id="270b0563"></span>
# 2. Feature overview

<span id="eb1be36c"></span>
## 2.1 Dataset impact analysis

On the details page of a dataset in Data Preparation, when a dataset is deleted, impact analysis is performed automatically and the results are displayed in a pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f79e1520889842a08dffc3b20867a9d3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c2d73344b9d42c38a82da0d187ea708~tplv-goo7wpa0wc-image.image) </span>

<span id="0cb1ccb5"></span>
## 2.2 Dimension/metric impact analysis

In the dataset module of Data Preparation, when fields are deleted or modified, explanations of the impact on dimensions or metrics are automatically generated and displayed in a pop\-up window.

The following diagram demonstrates the steps in the dataset module. The procedures in the visual query module are similar and will not be repeated here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8feab1719174754b3a2a971be7be19f~tplv-goo7wpa0wc-image.image) </span>

Supports selecting multiple fields for deletion. Impact analysis will provide statistics on both the overall and individual impact of each field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a25f30b1fe2e48b3a6c13e6b1a32ecd6~tplv-goo7wpa0wc-image.image) </span>

<span id="63941918"></span>
## 2.3 View lineage details

In the impact analysis pop\-up window, there are "View lineage details" and "Details" buttons. Clicking these will redirect to the lineage analysis page.

For more information about lineage analysis, see [lineage analysis](https://www.volcengine.com/docs/4726/1283232).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ffcc8f01f7d4372bee2afd2b03877e8~tplv-goo7wpa0wc-image.image) </span>
