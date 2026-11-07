---
title: "Subfilters"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Subfilters"
---

<span id="_1-概述"></span>
# 1. Overview

The filter field supports configuring cascading relationships between chart filters. A cascading relationship means that the value of one filter can affect the available options for precise filtering in other filters.

For example, if one filter field is "Province" and another is "City", after setting the "Province" filter condition, the "City" list will only display cities within the selected province. Note that the two filter fields used for cascading filtering must have a hierarchical structure.

<span id="_2-使用示例"></span>
# 2. Usage examples

<span id="_2-1-使用过程示例"></span>
## 2.1 Usage example

In the visual query interface, click the drop\-down icon on the left side of the filter field capsule to configure the subfilters affected by the current filter condition.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15b0d728f4e54999a459b947bfab2ec0~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e068297d1ac245be9cedc29f8ac10cbc~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8aff1d54454d46b19edb1f552b811eae~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0d7780e126604caa9f0dba5f81be6861~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/77d0a1f0bba9469c950e1dc13db3177e~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-功能限制"></span>
# 3. Functional limitations


* The cascading relationship between filters is an inclusion relationship.

   * For example, if the subfilter of the "Region" field is set to "Province", after the user filters by "Region", the "Province" display is limited to the selected "Region". If the "Province" filter condition is set, the corresponding "Region" will be automatically matched.

* You can set multiple subfilters for a single field at the same time.

   * For example, "Region" can be configured to affect both "Province" and "City".

* When there is a conflict between a public filter and a chart filter, the public filter overrides the chart filter logic.
