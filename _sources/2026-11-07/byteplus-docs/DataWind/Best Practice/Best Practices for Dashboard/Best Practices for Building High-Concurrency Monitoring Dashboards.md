---
title: "Best Practices for Building High-Concurrency Monitoring Dashboards"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/Best_Practices_for_Building_High-Concurrency_Monitoring_Dashboards"
---

<span id="_1-使用场景"></span>
# 1. Usage scenarios


* In the retail industry, monitoring daily reports for each store may be accessed by thousands of users, with different row\-level permissions. There is a possibility of high concurrency around 8 a.m.

* In e\-commerce event scenarios, a large number of users may access the same dashboard simultaneously within a specified period, and each user may have different data permissions.


<span id="_2-搭建建议"></span>
# 2. Recommendations for building

<span id="_2-1-数据准备"></span>
## 2.1 Data preparation

(1) Because this is a relatively fixed monitoring scenario and requires high concurrency, it is recommended to aggregate metrics in advance. You can preprocess the ads layer tables in the data warehouse and then extract them to the BI platform, or use the product's Visual Modeling to build the result data. The dashboard/visual query function should directly query the result data. Try to avoid aggregating directly from detailed data through visual queries, as performance may be significantly affected under high concurrency.

(2) Configure primary keys for the fields used in filter conditions to improve query performance.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d1b6d2a77ae0451084e801b8af8718ee~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(3) The business may require viewing a large amount of data, and problem analysis based on metric anomalies may also be necessary. Because human attention is limited, a summary\-detail structure is a better approach. The core is a monitoring daily report that presents the most critical data. When data in certain business domains appears abnormal, users can navigate to a detail page to view more dimensions and more detailed data. Instead of presenting all data to users at once.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fd11f92353d5412ab7e29e07e51dfbff~tplv-goo7wpa0wc-image.image" width="610px" /></div>


(4) It is recommended to control the number of charts in the core report. More data is not always better; it should be highly refined to what users need to see.

(5) If there are tables, please add pagination, as users cannot view many rows of data at a glance.

(6) It is recommended to limit the number of items displayed in each chart to ensure data readability.

(7) Try to keep the query time for charts in the core report within 1 second.
