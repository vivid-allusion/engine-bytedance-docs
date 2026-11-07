---
title: "Impact Analysis"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Impact_Analysis_"
---

<span id="d0418190"></span>
# 1. Overview

Impact analysis is a feature used to remind users of the relationships between data resources and to assess their impact. When users delete or modify datasets, dimensions, or metrics, the product will display a popup window showing an impact explanation to help users understand the risks of resource deletion or modification and reduce unnecessary losses caused by accidental deletion. Supports statistics on the total number of related downstream charts and dashboards for datasets, dimensions, or metrics, as well as the total number of accesses in the past 30 days.

<span id="270b0563"></span>
# 2. Feature introduction

<span id="eb1be36c"></span>
## 2.1 Dataset impact analysis

On the details page of a dataset in Data Preparation, when deleting a dataset, impact analysis is automatically performed and the results are displayed in a popup window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f79e1520889842a08dffc3b20867a9d3~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9c2d73344b9d42c38a82da0d187ea708~tplv-goo7wpa0wc-image.image) </span>

<span id="0cb1ccb5"></span>
## 2.2 Dimension/metric impact analysis

In the dataset module of Data Preparation, when deleting or modifying fields, dimension/metric impact explanations are automatically generated and displayed in a popup window.

The diagram below demonstrates the operation steps in the dataset module. The operations in the Visual Query module are similar and are therefore not described here.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8feab1719174754b3a2a971be7be19f~tplv-goo7wpa0wc-image.image) </span>

Supports selecting multiple fields to delete. Impact analysis will provide statistics on both the overall and individual impact for each field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a25f30b1fe2e48b3a6c13e6b1a32ecd6~tplv-goo7wpa0wc-image.image) </span>

<span id="63941918"></span>
## 2.3 View lineage details

In the impact analysis popup window, there are "View lineage details" and "Details" buttons. Clicking these will redirect to the lineage analysis page.

For more information about lineage analysis, see [Lineage analysis](https://docs.volcengine.com/docs/4726/1283232?lang=en).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ffcc8f01f7d4372bee2afd2b03877e8~tplv-goo7wpa0wc-image.image) </span>
