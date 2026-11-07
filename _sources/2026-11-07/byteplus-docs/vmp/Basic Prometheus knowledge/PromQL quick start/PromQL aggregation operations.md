---
title: "PromQL aggregation operations"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/PromQL-aggregation-operations"
---

PromQL provides aggregation operators that act on instant vectors. The aggregation operators can be used to aggregate the sample data returned by an instant\-vector\-typed expression and form the data into a new time series. Common aggregation operators are shown in the following table.


|**Operation Function** |Description |Explanation |
|---|---|---|
|sum |Sum |Sums the values of records. For example, `sum(http_requests_total)` counts the total number of HTTP requests. |
|min |Minimum |Returns the minimum value of all records. |
|max |Maximum |Returns the maximum value of all records. |
|avg |Average |Returns the average of all records. |
|stddev |Standard deviation |Returns the standard deviation of all records. |
|count |Count |Returns the number of all records. |
|bottomk |The last n time series |Sorts sample values and returns the time series with the last n sample values. |
|topk |The first n time series |Sorts sample values and returns the time series with the top n sample values. |
