---
title: "Lineage Analysis"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Lineage_Analysis"
---

<span id="6b0bd0f1"></span>
# 1. Overview of data lineage analysis

<span id="02e68ec3"></span>
## 1.1 Overview

Data lineage analysis is a method used to trace and understand the origin, flow, and evolution of data throughout an entire system or process, helping users manage data more efficiently.

Through data lineage analysis, users can query the full\-chain upstream and downstream dependencies of resources such as dashboards, charts, datasets, visual modeling, digital large screens, and data sources/data connections, clearly understanding how data is generated, what processing steps and transformations it undergoes, and which resources ultimately use it. When troubleshooting, data lineage analysis can also help users quickly locate the source of issues, such as tracing upward to identify key nodes that introduce metric calculation problems, or evaluating downstream the impact scope of metric changes on the calculation standard. The data lineage analysis feature is crucial for ensuring data reliability, availability, and value realization, as well as for improving an enterprise's data management and business decision\-making capabilities.

<span id="7ffc311b"></span>
## **1.2 Application scenarios**


* **Master the data analysis chain**: By viewing resource lineage, users can see the relationships among each data source, dataset, visual modeling task, chart, dashboard, digital large screen, and more, making it easy to understand the data analysis process.

* **Assess resource deletion and modification risks**: Understanding upstream and downstream dependencies of resources enables a more comprehensive assessment of the risks associated with deleting or modifying resources. When troubleshooting, users can also quickly locate the source of issues, such as tracing upward to identify key nodes that introduce metric calculation problems, or evaluating downstream the impact scope of metric changes on the calculation standard.


<span id="8cd6bda9"></span>
# 2. Feature introduction

<span id="9d09f7cf"></span>
## 2.1 Access data lineage analysis

(1) Click Project Center.

(2) Click Data Lineage Analysis on the left to enter the data lineage analysis interface. Select resource type, object, analysis granularity, and so on to view the full\-chain relationships among resources.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbd98cec6bed4284abca6117f951ad3a~tplv-goo7wpa0wc-image.image) </span>

<span id="b279c2ab"></span>
## 2.2 Query resource lineage

As shown in the figure, users can sequentially query by resource type, resource object, and analysis granularity to view the end\-to\-end lineage analysis of a specific resource.

(1) Select the resource type. Users can query resources of the following types: dashboard, chart, dataset, visual modeling, display board, and data source/data connection:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06b6884e89414788a663b8b2a2900486~tplv-goo7wpa0wc-image.image) </span>

(2) Under the selected resource type, select the resource object for which you want to view the end\-to\-end lineage analysis.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a0ed9205d4fb44d2b86e6184c7cd20e1~tplv-goo7wpa0wc-image.image) </span>

(3) Select the analysis granularity. If the resource type is chart, dataset, or data source/data connection, you can select the analysis granularity to view lineage analysis at different levels of granularity:


|Type |Analysis granularity |
|---|---|
|Chart |Chart |
||Dimension/metric |
|Dataset |Dataset |
||Dimension/metric |
|Data source/data connection |Table/sheet name |
||Field |
|Dashboard |Dashboard |
|Visual modeling |Visual modeling |
|Large screen |Large screen |


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1626582c39954d5c92368ffa0a161e35~tplv-goo7wpa0wc-image.image) </span>

For example, for the dataset resource type, if dimension/metric is selected as the analysis granularity, you can select a field in the upper right corner to perform end\-to\-end lineage analysis for a single field.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2879038989af4b358d5775b182c31671~tplv-goo7wpa0wc-image.image) </span>

<span id="2103ce6c"></span>
## 2.3 View lineage details

(1) After selecting the resource for which you want to view the lineage, the system will automatically count the number of associated resources, as well as the types and numbers of upstream and downstream resources, to provide an overview for the user.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/358f03b594a9439689d7c2fc54724378~tplv-goo7wpa0wc-image.image) </span>

(2) The lineage analysis view displays detailed information about other resources related to this resource in a list format:


* Resource name: Click to navigate to the resource details editing page

* Resource type

* Upstream and downstream: Indicates the direction of data flow and dependency relationships. Divided into upstream, baseline, and downstream. The currently selected resource is the baseline. Upstream refers to the source of the data or the starting point where data is generated, while downstream refers to the stages that depend on upstream data for further processing, transformation, storage, or usage.

> Upstream: data source, visual modeling, dataset

> Downstream: dashboard, chart, display board, visual modeling, dataset


* Hierarchy: Displays the hierarchical relationship. The currently selected resource is at hierarchy level 0

* Resource ID

* Path

* Owner


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ddc2d5d7590f42d695eeeb5b0b683e1d~tplv-goo7wpa0wc-image.image) </span>

(2) Click [Access Statistics] to navigate to the access details of this resource:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57e2f7de2f7d43ad9e0828fce1819215~tplv-goo7wpa0wc-image.image) </span>

(3) If the granularity selected is field or dimension/metric, the field information of the related resources will be displayed:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a6f4ba2755493cb6aef4c23969d967~tplv-goo7wpa0wc-image.image) </span>

(4) To check whether a resource is related to the selected resource, or to view a single resource when there are many lineage\-related resources, enter the **Resource ID** in the search bar at the upper right. As shown in the figure below, the data source with Resource ID 354 has a lineage relationship with the currently selected dataset

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/781719c1a9e340948a487c0f92432fef~tplv-goo7wpa0wc-image.image) </span>

<span id="a7405d67"></span>
## 2.4 Download lineage analysis

Click the download button in the upper right corner to download the current lineage analysis result in xlsx/csv format to your local device for archiving, further analysis, or presentation.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2475747bb1842d5bdffb0f80a563d5b~tplv-goo7wpa0wc-image.image) </span>

\***Explanation of lineage link completeness and accuracy:** 


* Dataset: Custom SQL type supports only table\-level lineage, with 90% accuracy.

* Dimension/metric: Only the completeness and accuracy of expressions that use data source fields can be guaranteed.


For example, if there are metrics A1/A2 in the dataset and a field A3=A1+A2 is added, the lineage of A3 cannot currently be identified.
