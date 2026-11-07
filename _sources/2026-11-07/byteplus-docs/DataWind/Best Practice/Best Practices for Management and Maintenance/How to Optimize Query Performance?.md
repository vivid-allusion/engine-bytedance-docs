---
title: "How to Optimize Query Performance?"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/How_to_Optimize_Query_Performance"
---

Thank you for using our product. Ensuring a high\-performance experience is our responsibility.

So, as a user, why do you also need to understand how to optimize it?

<span id="_1-原因"></span>
# 1. Reasons

<span id="_1-1-机器资源"></span>
## 1.1 Machine resources

The product relies on ClickHouse as the query engine to provide data retrieval and analysis capabilities. From a technical perspective, ClickHouse is likely the fastest large\-scale OLAP engine currently in use, and it is difficult to replace it with more advanced technology in the short term. Therefore, for the same ClickHouse cluster, the machine configuration directly affects the query speed.

<span id="_1-2-数据生产"></span>
## 1.2 Data production

For many data products, the platform is responsible for data production, and users simply act as consumers.

This product, as a self\-service insight and analysis tool, not only provides dashboards, visualization, and other query tools, but also offers dataset functionality, allowing users to flexibly choose the imported data and storage structure. These two aspects greatly affect query performance, yet are often overlooked. The performance of many queries is often determined when the dataset is created. To achieve fast dashboard queries, the dataset must be well designed.

<span id="_1-3-查询方式"></span>
## 1.3 Query methods

Returning to the query itself, factors such as the volume of data queried, the operators used, whether the cache is hit, and whether the dataset settings are matched all affect query speed. By applying appropriate query methods, it is often possible to obtain query results more quickly.

<span id="_2-具体做法"></span>
# 2. Specific approaches

The company can optimize across three dimensions: machine resources, data production, and query methods. This article focuses on methods for optimizing query performance through query methods.

If query performance is still unsatisfactory, please contact us for more targeted solutions.

<span id="_2-1-查询方式"></span>
## 2.1 Query methods

Improvements to query methods mainly depend on dashboard and chart owners or users of visual ad hoc queries.


|Optimization methods |Criteria and reasons for judgment |Specific steps |
|---|---|---|
|Maximize the chances for queries to **hit the cache** |Whether for real\-time or offline data, as long as queries do not always require the latest data, there is an opportunity to hit the cache.<br><br>Reason: The vast majority of cache\-hit queries can return within 1 second.<br><br><br>* Offline data is generally updated on a daily basis. If there are repeated queries within a day, all subsequent queries after the first one can hit the cache.<br><br>* Real\-time data is updated more frequently. However, if it is not necessary to see the latest data with every query, you can still set a cache validity period, such as 15 or 30 minutes. This helps improve query efficiency and reduce cluster load. |Before July 1, check whether random sampling is enabled for the chart. Random sampling does not attempt to use the cache and has poor performance. If sampling is needed, select the default sampling option.<br><br>After July 1, you can explicitly set whether to enable caching in the chart settings on the visualization page.<br><br><br>* Caching can be enabled for all offline data. DataWind will intelligently determine whether the data has changed and decide whether to update the cache, ensuring that expired data is not cached.<br><br>* Real\-time data has a default cache duration of 5 minutes. Since this policy was launched in May, no users have reported experiencing data latency. Normally, there is no need to disable it.<br><br>   If higher latency is acceptable, it is recommended to increase the cache duration setting to optimize query performance.<br><br>   Additionally, minimize the use of functions such as now() and today(). If these functions are included in the query, caching cannot be enabled on the backend to ensure data accuracy. The today() function can later be replaced by a parameter. For now, consider whether it is equivalent to p_date and try to replace it. |
|Reduce the number of days in **query partitions** |Query as few days as possible; reduce the number of partition days to decrease the amount of data queried. |In visual queries, reduce the number of days for the p_date filter condition, and reduce the number of days in the dashboard filter. |
|Minimize or replace **time\-consuming operators** |Time\-consuming operators such as countd, uniqExact, quantileExact, arrayhas, like, match, jsonExtract, and lengthy case when statements may all result in slow queries, and the query efficiency of certain operators cannot be improved by upgrading cluster configurations. |1. If it is not necessary to ensure completely accurate results, functions such as countd, uniqExact, and quantileExact can be replaced with corresponding approximate calculation functions like uniq and quantile, sacrificing some precision to improve query efficiency.<br><br>2. For functions such as json, case when, and like, consider materializing columns at the data warehouse level instead of calculating them during queries.<br><br>3. For functions such as arrayhas and arrayset, consider creating indexes in advance.<br><br>   Overall, minimize the use of the above functions, or place metrics that use these functions in a separate chart to avoid slowing down the query speed of the entire chart. |
|Use **time\-consuming analytical functions** less frequently |Some analytical functions provided by DataWind may have high latency in large data volume scenarios, such as LOD, period\-over\-period, comparison, detail aggregation, pivot table subtotal, and aggregation.<br><br>Reason: The implementation of these functions either involves complex joins, requires processing all data, or needs multiple calculations to assemble results. |1. For comparison and period\-over\-period analysis, try to limit the number of groups and consider setting commonly used dimension items as shard keys to make the join process local.<br><br>2. For Fixed, if filter conditions can be added, set dimension filters. Currently, there are no particularly effective optimization methods for other LOD queries.<br><br>3. For functions such as aggregation and percentages, it is best to use data currently displayed rather than all data.<br><br>   Overall, use the listed analytical functions with caution when dealing with large data volumes (single partition \> 100 million rows). |
|Set **sampling** |For scenarios such as analyzing proportions, trends, avg, and quantiles, consider using the sampling feature.<br><br>Reason: Sampling can reduce the amount of data queried, improve query speed, and lower resource consumption. In scenarios where high precision is not required, such as trend and proportion analysis, sampled data does not affect the analysis of results. |Set the sampling ratio on the visualization page (prefer stable sampling before 6/25). Sampling reduces the amount of data read and affects sum and count results, but does not impact pie chart proportions, line chart trend analysis, or operators such as avg and quantile.<br><br>Sampled data loses precision and is only suitable for approximate analysis in specific scenarios. |
|Reduce **dimensions** |Most queries use no more than five dimensions. Too many dimension items will result in reading too many columns and increase computational cost. |Remove unnecessary dimensions |
