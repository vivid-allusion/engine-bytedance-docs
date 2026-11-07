---
title: "Using recording rules to pre-aggregate and accelerate queries"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries"
---

When a dashboard frequently executes the same complex PromQL queries or queries data over a long time period, repeatedly scanning raw time series prolongs queries and consumes more compute resources. To address this issue, you can use recording rules to pre\-compute commonly used aggregation results and enable query acceleration. When the acceleration conditions are met, VMP automatically reuses the pre\-aggregated results, shortening query time and reducing workspace load without the need to modify the original PromQL. This topic describes how to use the recording rule pre\-aggregation feature.

<span id="L5K2LqGx"></span>
## Prerequisites


* A workspace is the basic environment for configuring recording rules and enabling query acceleration. Make sure you have [created a workspace](https://docs.byteplus.com/en/docs/vmp/Creating_a_workspace?lang=en).

* When you configure rules, we recommend first understanding which queries can automatically match acceleration rules and which changes prevent reuse. In this way, you can properly plan the calculation scope and label dimensions. For more details, see [Which queries can automatically match acceleration rules?](https://docs.byteplus.com/en/docs/vmp/Which-queries-can-automatically-match-acceleration-rules)


<span id="gnWKeoIh"></span>
## Procedure

<span id="AoyxcJaW"></span>
### Step 1: Select the query to accelerate


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target project and region.

3. Click **Workspace** in the left navigation pane. Then, click the name of the target workspace.

4. On the Overview page of the workspace, click **Slow query** in the left navigation pane. Select PromQLs with high duration and frequent execution. For more details, see [Slow queries](https://docs.byteplus.com/en/docs/vmp/Slow_queries).


<span id="91QodkYo"></span>
### Step 2: Design a pre\-aggregation rule

In this step, the Counter metric `http_requests_total` is used as an example to describe how to design a pre\-aggregation rule and enable query acceleration. This metric includes tags such as job, cluster, namespace, service, status_code, and instance\-related tags.

If you need to view the average request rate of each service in a specified cluster and namespace over the last 5 minutes, use the following PromQL:

```Plain Text
sum by (service) (
  rate(http_requests_total{
    job="gateway",
    cluster="prod-a",
    namespace="payments"
  }[5m])
)
```


When you design a pre\-aggregation rule, we recommend retaining the filter and grouping dimensions that dashboards use over the long term, such as `cluster`, `namespace`, `service`, and `status_code`. For instance\-level dimensions used only for temporary troubleshooting, such as `instance` and `pod`, you can decide whether to aggregate them as needed. Note that after a dimension is aggregated, you can no longer drill down by that dimension using the pre\-aggregated metric. Based on the preceding analysis, the following recording rule can be designed to achieve automatic query matching and acceleration.

```YAML
groups:
  - name: workload_http_requests_acceleration
    interval: 1m
    rules:
      - record: workload:http_requests:rate5m
        expr: |
          sum by (cluster, namespace, service, status_code) (
            rate(http_requests_total{job="gateway"}[5m])
          )
```



|**Parameter** |**Description** |
|---|---|
|interval |The rule execution interval, which is the generation frequency of pre\-aggregated data. A shorter interval results in more frequent data updates but higher resource overhead. A longer interval results in lower resource overhead but coarser data granularity.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The execution interval cannot be less than 5 seconds.</div><br> |
|record |The name of the pre\-aggregated metric. We recommend naming it in the format of "business scope + original metric + calculation scope" and keeping the name unique. This facilitates dashboard references, calculation scope identification, and troubleshooting. |
|expr |The pre\-aggregation expression, which determines the statistical scope of pre\-aggregated data. For Counter metrics, we recommend executing `rate` first and then aggregating the metrics. `5m` is the rate calculation window, which is different from the meaning of `interval`. |
|by (...) |The tag dimensions to retain after pre\-aggregation, which determine the range for subsequent filtering and grouping. Dimensions that are not retained will be aggregated, and you cannot drill down by the dimensions later. |
|labels |Used to add or overwrite tags for pre\-aggregated results. This configuration is not used in this example. If it is required, we recommend adding only management tags and avoiding overwriting existing business tags. This prevents the accuracy of dashboard grouping and rule matching from being affected. |


<span id="mrQv8JJz"></span>
### Step 3: Create a rule and enable query acceleration


1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target project and region.

3. Click **Workspace** in the left navigation pane. Then, click the name of the target workspace.

4. On the Overview page of the workspace, click **Recording rules management** in the left navigation pane.

5. Click **Create rule file** and specify the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Name |Specify the name of the recording rule file. Duplicate rule file names are not allowed within the same workspace. |
   |Write target |Select the workspace to which pre\-aggregated results are written. To ensure that the query can reuse pre\-aggregated results, we recommend selecting the workspace where the current query resides. |
   |YAML configuration |Specify the details of the recording rule file. Enter the rule designed in [Step 2](https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries?TagIDs=2,143&lang=en#91QodkYo). |
   |Allow for query acceleration |Whether to configure pre\-aggregation for queries. After it is enabled, the system automatically finds the part of the original PromQL that matches the rule expression and rewrites it into a query based on the pre\-aggregated metric. If matching conditions are not met, the system still executes the original PromQL. |
   

6. Click **Add** to complete the configuration.

7. Check the running status of the rule and confirm that the pre\-aggregated metric has generated data.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If the rule runs as expected, it does not guarantee that the query will hit the acceleration rule. Follow the instructions in <a href="https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries">Validate results</a> to verify it.   </div>
   

<span id="4BQAlL16"></span>
### Step 4: Query using the original PromQL

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Before verifying query acceleration for the first time, make sure the rule runs as expected, the preparation period has ended, and the query time range falls entirely after the end of the preparation period. Otherwise, the query may fail to hit the acceleration rule because the time range is not covered. If the query contains a subquery, you also need to cover the lookback window of the subquery (for example, <code>30m:1m</code> additionally reads data from the previous 30 minutes). After the time coverage conditions are met, check other hit conditions such as expression matching and query step.</div>



1. Log in to the [VMP console](https://console.byteplus.com/observe/prometheus). 

2. In the top navigation bar, select the target project and region.

3. Click **Explore** in the left navigation bar to go to the Explore page.

4. Specify the parameters in the upper\-right corner of the page.

   
   |Parameter |Description |
   |---|---|
   |workspace |Select the workspace where the rule resides. In this example, select the same workspace as in [Step 1](https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries?TagIDs=2,143&lang=en#AoyxcJaW).<br><br>If the query workspace differs from the workspace to which the pre\-aggregated results are written, the query cannot reuse the pre\-aggregated results. |
   |Min step |The minimum time interval between data points returned in a range query. The default setting is auto. In this example, it is set to 1m, which must not be less than the `interval` of the rule. |
   |Query time range |The default is the **last 30 minutes**.<br><br>After you click the drop\-down list, you can select the metric query time range. |
   |Data refresh method |**Manual refresh** and **automatic refresh** are supported. For the first verification, we recommend using manual refresh to prevent changes in the time range from affecting the result comparison. For continuous observation, you can enable auto\-refresh as needed. |
   

5. Execute the original PromQL selected in [Step 1](https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries?TagIDs=2,143&lang=en#AoyxcJaW).

6. After conditions such as rule matching, time coverage, and query step are met, the system automatically rewrites the query into an equivalent form based on the pre\-aggregated metric. You do not need to manually replace the PromQL in the dashboard. For example:

   ```Plain Text
   sum by (service) (
     workload:http_requests:rate5m{
       cluster="prod-a",
       namespace="payments"
     }
   )
   ```
   

7. If you use Grafana, make sure the panel ultimately issues a range query and that the actual `step` is not less than `1m`. If `$__rate_interval` or `$__interval` is used, also make sure the expanded calculation window matches the rule scope.


<span id="ELZl6RFO"></span>
## Validate results

<span id="z0foaE0F"></span>
### Confirm whether the automatic acceleration rule is hit

Check the range query response header `X-VMP-Query-Acceleration`. If the automatic acceleration rule is hit, this response header returns the rewritten PromQL. Querying only pre\-aggregated metric data does not prove that the original PromQL has hit the automatic acceleration rule. If the query goes through Grafana or another proxy, the response header may not be passed through to the browser. In this case, refer to the actual query response from VMP.

<span id="V6tTDCvn"></span>
### Compare the results of the same request with acceleration enabled and disabled

Use two sets of range query parameters for comparison. The workspace, PromQL, start, end, and step of the two requests must be exactly the same, and a fixed time range must be used to prevent changes in the comparison basis caused by auto\-refresh.


|**Parameters** |**Acceleration group** |**Original query control group** |
|---|---|---|
|Request path |/api/v1/query_range |/api/v1/query_range |
|query |The original PromQL selected in Step 1 |The same original PromQL |
|start、end |A fixed 2\-hour time range that is fully covered |The same start and end time |
|step |60s |60s |
|disable_query_acceleration |Not passed |true |


We recommend confirming the acceleration result in the following order:

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">We do not recommend judging acceleration benefits based on a single query duration. The actual improvement depends on factors such as the original series scale, aggregated series scale, query frequency, and service load.</div>



1. **Request availability**: Both groups of requests should return successful results. You cannot judge whether the query is available solely based on whether the acceleration response header exists.

2. **Business result consistency**: Compare the number of series, business tags, and values near the same time points, as well as whether null values or data gaps exist. Also confirm that the logic of dashboard legends and dependent metric names is not affected.

3. **Time granularity and alignment**: Recording rules generate results periodically. Therefore, the timestamps returned by a query may not exactly align with the evaluation timestamps. For rapidly changing metrics, judge the difference based on data arrival delay and the rule period. Not all data points are required to be exactly the same.

4. **Duration improvement**: Under similar load and cache conditions, alternately execute the two requests multiple times and compare the overall duration. When sufficient samples are available, further calculate P50 and P95. Hitting acceleration rules does not mean that query duration will decrease by a fixed multiple.

5. **Rule overhead**: Continuously observe the rule execution status, the number of pre\-aggregated series, and the workspace write volume and storage usage to ensure that query benefits exceed the additional pre\-computation cost.
