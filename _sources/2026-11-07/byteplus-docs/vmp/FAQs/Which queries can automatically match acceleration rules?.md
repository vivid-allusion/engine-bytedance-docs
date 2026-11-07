---
title: "Which queries can automatically match acceleration rules?"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Which-queries-can-automatically-match-acceleration-rules"
---

VMP supports automatically reusing pre\-aggregated results without manually modifying PromQL in dashboards. This topic describes which queries can reuse existing rules and which changes prevent reuse.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">An expression meeting the matching conditions does not guarantee that the query will actually be accelerated. The actual result is determined by the <code>X-VMP-Query-Acceleration</code> response header. For more details, see <a href="https://docs.byteplus.com/en/docs/vmp/Using-recording-rules-to-pre-aggregate-and-accelerate-queries?TagIDs=2,143&lang=en#ELZl6RFO">Best practices for using recording rules to pre\-aggregate and accelerate queries</a>.</div>



|**Matching method** |**Which queries can match** |**Typical purpose** |
|---|---|---|
|Full expression match |The query has the same calculation semantics as the rule expression. |Directly reuse the complete pre\-aggregated result. |
|Partial expression match |A certain part of a complex query matches the rule, while the outer calculation remains unchanged. |Continuing to perform comparisons, statistics, or judgments based on the original query |
|Continue filtering or aggregating |The query uses only the tags retained in the rule and continues to perform less fine\-grained aggregation. |Reuse the same rule to support different filter conditions and display granularities. |


The examples in this topic are based on the following recording rule expression:

```Plain Text
sum by (cluster, namespace, service, status_code) (
  rate(http_requests_total{job="gateway"}[5m])
)
```


The generated pre\-aggregated metric is:

```Plain Text
workload:http_requests:rate5m
```


<span id="FdPKaIO0"></span>
## Queries that can reuse the rule in this example

<span id="rWV5Kvkl"></span>
### Example 1: Match the complete expression

This query can directly hit the acceleration rule. Even with minor syntactic differences, the rule can still be reused as long as the calculation semantics remain unchanged.

**Original query:** 

```Plain Text
sum by (cluster, namespace, service, status_code) (
  rate(http_requests_total{job="gateway"}[5m])
)
```


**Rewritten after match:** 

```Plain Text
workload:http_requests:rate5m
```


<span id="iHpknjRu"></span>
### Example 2: Match only part of a complex query

This query can hit the acceleration rule. The system first replaces the reusable part and then keeps the outer\-level condition. The presence of the response header only indicates that some expression in the query has been replaced.

**Original query:** 

```Plain Text
sum by (cluster, namespace, service, status_code) (
  rate(http_requests_total{job="gateway"}[5m])
) > 100
```


**Rewritten after match:** 

```Plain Text
workload:http_requests:rate5m > 100
```


<span id="KQUgZmYd"></span>
### Example 3: Add filtering by tags and narrow grouping dimensions

If the tags used by the newly added filter conditions are already retained in the rule, the query can reuse the pre\-aggregated results. If the tags that are not retained are used, such as `pod` and `instance`, the pre\-aggregated results cannot be reused.

**Original query:** 

```Plain Text
sum by (service) (
  rate(
    http_requests_total{
      job="gateway",
      cluster="prod-a",
      namespace="payments",
      status_code=~"5.."
    }[5m]
  )
)
```


**Rewritten after match:** 

```Plain Text
sum by (service) (
  workload:http_requests:rate5m{
    cluster="prod-a",
    namespace="payments",
    status_code=~"5.."
  }
)
```


<span id="kOvhipYS"></span>
### Example 4: Aggregate into a total value

Pre\-aggregated results can be further aggregated into less fine\-grained results, such as a total.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Aggregated tags cannot be recovered and cannot be used for grouping in subsequent queries.</div>


**Original query:** 

```Plain Text
sum(
  rate(
    http_requests_total{
      job="gateway",
      cluster="prod-a"
    }[5m]
  )
)
```


**Rewritten after match:** 

```Plain Text
sum(
  workload:http_requests:rate5m{
    cluster="prod-a"
  }
)
```


<span id="BqbhccGk"></span>
### Example 5: Match inside a subquery

Expressions inside the subquery can hit the acceleration rule, and the outer subquery syntax does not need to be modified. When you use such queries, make sure the time range covers the lookback window of the subquery.

**Original query:** 

```Plain Text
max_over_time(
  (
    sum by (service) (
      rate(
        http_requests_total{
          job="gateway",
          cluster="prod-a"
        }[5m]
      )
    )
  )[30m:1m]
)
```


**Rewritten after match:** 

```Plain Text
max_over_time(
  (
    sum by (service) (
      workload:http_requests:rate5m{
        cluster="prod-a"
      }
    )
  )[30m:1m]
)
```


<span id="SgruOqxF"></span>
### Example 6: Derived matches for min, max, and count

The following examples each use three separate rules, and each rule retains the `cluster` and `service` tags.

<span id="xeqAI6Ao"></span>
#### min derived match

When the rule has retained the required tags, `min` can continue to be calculated on the pre\-aggregated results. This approach is suitable for pre\-computing at a finer granularity first and then viewing the minimum value over a larger scope.

**Rule expression:** 

```Plain Text
min by (cluster, service) (
  worker_queue_depth
)
```


**The generated pre\-aggregated metric is:** 

```Plain Text
workload:worker_queue_depth:min
```


**Original query:** 

```Plain Text
min(
  worker_queue_depth{
    cluster="prod-a"
  }
)
```


**Rewritten after match**

```Plain Text
min(
  workload:worker_queue_depth:min{
    cluster="prod-a"
  }
)
```


<span id="ZmDsSCiT"></span>
#### max derived match

`max` is handled similarly to `min` and can continue to be aggregated on the pre\-aggregated results. The rule can be reused as long as the filter conditions and retained dimensions are consistent.

**Rule expression:** 

```Plain Text
max by (cluster, service) (
  worker_queue_depth
)
```


**The generated pre\-aggregated metric is:** 

```Plain Text
workload:worker_queue_depth:max
```


**Original query:** 

```Plain Text
max(
  worker_queue_depth{
    cluster="prod-a"
  }
)
```


**Rewritten after match:** 

```Plain Text
max(
  workload:worker_queue_depth:max{
    cluster="prod-a"
  }
)
```


<span id="la0515Gj"></span>
#### count derived match

Unlike `min` and `max`, `count` usually requires `sum` to accumulate results during continued aggregation. If `count` is used directly for further aggregation, the result typically does not represent the total count of the original series.

**Rule expression:** 

```Plain Text
count by (cluster, service) (
  up
)
```


**The generated pre\-aggregated metric is:** 

```Plain Text
workload:up:count
```


**Original query:** 

```Plain Text
count(
  up{
    cluster="prod-a"
  }
)
```


**Rewritten after match:** 

```Plain Text
sum(
  workload:up:count{
    cluster="prod-a"
  }
)
```


<span id="MHhw84CF"></span>
## Changes that cannot reuse the rule in this example

The following table uses the request rate rule at the beginning of this section as an example. "Cannot reuse" means the rule cannot replace the corresponding expression, and the query is still executed based on the original PromQL.


|**Query change** |**Reasons for non\-reusability** |
|---|---|
|Adding a `pod="pod-a"` filter |The rule does not retain the pod. Therefore, filtering by this tag is not possible. |
|Grouping using `sum by (pod)` |The pod dimension has been aggregated and cannot be recovered. |
|Removing `job="gateway"` |The query scope is expanded beyond the original coverage of the rule. |
|Changing `5m` to `1m` |The calculation window changes, resulting in different statistical semantics. |
|Changing `rate(...)` to `irate(...)` |The calculation function and metric meaning change. Therefore, the result means something different. |
|Changing `sum` to `avg` |The rule stores the sum result, which cannot be used to recover the average. |
|Changing `by (...)` to `without (...)` |The output tag set changes and cannot be reused directly. |
|Adding `offset` |The query time semantics change and become inconsistent with the rule expression. |


When determining whether a query can reuse a rule, check the following items in order:


1. Whether the original metric is consistent.

2. Whether the function and calculation window are consistent.

3. Whether the basic filter conditions remain unchanged.

4. Whether the tags used by the newly added filter are already retained by the rule.

5. Whether the output grouping is a subset of the dimensions retained by the rule.
