---
title: "Metrics Management"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Metrics_Management"
---

DataFinder provides you with metrics management capabilities, allowing you to create commonly used analytical metrics into solidified metrics in a unified page, making it easy for you to directly choose among multiple analytical tools, improving analysis efficiency and reducing data management costs. This article provides you with a guide to the use of metrics management.

<span id="_1-概述"></span>
# Feature Overview

As data access to growth analysis platforms becomes more abundant, and the metrics we create in analytical models such as event analysis become more and more complex, we may find that it takes longer and longer to configure metrics, and multiple reconfigurations are required for similar scenarios; or the metrics used in communication with the business are inconsistent, resulting in a gradual increase in communication costs.

Index management is used to solve the problems of index reuse and uniform caliber. In the unified management interface, you can view the existing metrics list and corresponding metrics definitions, and complete management operations such as creation, editing, and deletion in a unified manner, thus ensuring that the definition and consumption of the same metrics are consistent across all ends.

<span id="_2-功能介绍"></span>
# Operation steps

<span id="_2-1-指标创建"></span>
## Metric creation


1. Create the metrics entry. There are currently two operating entrances:

   * Data management \- Metadata management \- Metrics \- New metric.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50f8061da03047a2944aca2b630e2cf6~tplv-goo7wpa0wc-image.image) </span>

   * Each advanced analysis page, metrics selection drop\-down box \- save the metrics.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6857fa16d14e40869c311cccca0c1af5~tplv-goo7wpa0wc-image.image) </span>

2. Select the metrics type and configure the metrics parameters in the popup box.

   Currently supports new **event metrics** , **event combination metrics**, **retention metrics**, **Session metrics**, and **conversion metrics**. The calculation conditions of the index creation are consistent with each analysis module, which can be found in the instructions for each analysis module.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/146cf7d506e04639bbdb02300389c590~tplv-goo7wpa0wc-image.image) </span>


<span id="_2-2-指标管理"></span>
## Index management

For the created metrics, you can copy, edit, delete, add labels (classification) and other management operations.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Any user with project permissions has the viewing permission of metrics management, but only administrators can perform administrative operations such as editing and deleting.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dcf6dbb007e3449d8a55b31795b76db5~tplv-goo7wpa0wc-image.image) </span>


* Replication: Supports the quick creation of new metrics based on created metrics through replication operations. After clicking Copy, you only need to configure the metrics name, display name and other parameters in the pop\-up page. The metrics calculation conditions are consistent with the copied metrics by default, which can improve configuration efficiency.

* Edit: Support for modifying names, display names, meanings, permissions, and calculation conditions. After the metrics are edited, it will take effect globally, and all charts to which the metrics have been applied will be affected.

* Delete: All charts that have been applied to these metrics will not display properly, please delete with caution.

* Add labels (classification): When there are too many metrics, consider classifying the metrics through "labels".


<span id="_2-3-指标消费"></span>
## Usage metrics

The created metrics can be directly selected in the corresponding analysis model.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6173e30d5ae4f448e5c96270b7ebe8b~tplv-goo7wpa0wc-image.image) </span>

If you open Base analysis, you can more conveniently achieve cross\-analysis model analysis, that is, multiple analysis model metrics in the same chart, while grouping and filtering operations.

<span id="_3-常见问题"></span>
# Common problem

**Q1. Why are some of the saved metrics not used in the analytical model?** 

The metrics do not support nesting. Please check whether the currently invisible metrics contain the saved metrics, and then it can be used normally in the analysis model after removal.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9014f39c44e841ebae860aa670ca71f7~tplv-goo7wpa0wc-image.image) </span>
