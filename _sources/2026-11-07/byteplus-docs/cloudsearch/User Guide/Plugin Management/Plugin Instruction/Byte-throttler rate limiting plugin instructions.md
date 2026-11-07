---
title: "Byte-throttler rate limiting plugin instructions"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/limiting_rate_with_the_byte_throttler_plugin"
---

Cloud Search instances may experience sudden spikes in QPS or write throughput during business traffic growth. If instance resources remain unchanged, sudden traffic spikes may cause increased request latency, cluster pending, or even node exceptions. To reduce the impact of burst traffic on instance stability, Cloud Search provides a rate limiting plugin to restrict business QPS and write throughput, helping instances maintain stable operation under traffic spikes.

<span id="d126f32a"></span>
## Prerequisites

The Byte\-throttler plugin is not installed by default. Install it in advance if needed. For installation instructions, see [Installing built-in plugins](https://docs.byteplus.com/docs/cloudsearch/manage-built-in-plugins).

<span id="GZzp0dcq"></span>
## Precautions


* This limits access by QPS/throughput dimension for specific indexes to prevent sudden QPS spikes from crashing the cluster or increased QPS on certain indexes affecting latency or other performance metrics of existing business.

* This does not apply to scenarios where large queries crash the cluster, such as extremely large Agg queries. The rate\-limiting plugin cannot protect the Cloud Search instance in this scenario.

* Only Elasticsearch 7.10.2 instances support the Byte\-throttler plugin.


<span id="1f60080b"></span>
## Step 1: Enable the rate\-limiting plugin

It is off by default and requires updating the configuration to enable before use.

```HTTP
# 查看集群所有默认配置
# GET _cluster/settings?include_defaults&flat_settings
PUT _cluster/settings
{ 
  "transient" : {
      "index.ratelimit.enabled" : "true"
  }
}
```


<span id="9676b77a"></span>
## Step 2: Add rate\-limiting rules

The rate limiter mainly consists of two parts: limiter definitions and tag definitions. Tags define resource limits, while limiters specify the rate\-limiting types and thresholds.


* The index name in tags supports the `*` wildcard.

* Multiple rate\-limiting types can be configured under each rate\-limiting rule. A single limiter name supports setting rate limits for one or more of `search.qps/writer.qps/write.throughput`.

* If multiple rate limiting rules apply to a single read\-write request, the request is rejected as soon as any one rule triggers the limit.


Once the request exceeds the rate limit, the instance rejects any subsequent requests. The returned HTTP code is 429, with content showing the triggered rule and its name.


|**Query operations** |RESTful request example |
|---|---|
|Set query QPS rate limiting for a single index |```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "search.qps": "1000"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index"```<br>```  }```<br>```}```<br>``````<br>```{"limiters": {"search.qps": "1"}, "tags": {"index": "test_index"}}```<br> |
|Set query QPS rate limit for indexes with a specified name prefix |```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "search.qps": "1000"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index-*"```<br>```  }```<br>```}```<br> |
|Set total query QPS rate limit for all indexes |```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "search.qps": "1000"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index-*"```<br>```  }```<br>```}```<br> |
|**write operation** |RESTful request example |
|Set write QPS rate limit for a single index |```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "write.qps": "1000"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index"```<br>```  }```<br>```}```<br> |
|Set write throughput rate limiting for a single index |```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "write.throughput": "1048576"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index"```<br>```  }```<br>```}```<br> |
|**Set configurations for multiple rate limiters** ||
|```HTTP```<br>```PUT _ratelimit/<limiterName>```<br>```{```<br>```  "limiters": {```<br>```    "search.qps": "1000",```<br>```    "write.qps": "1000",```<br>```    "write.throughput": "1048576"```<br>```  },```<br>```  "tags": {```<br>```    "index": "test_index"```<br>```  }```<br>```}```<br> ||


<span id="122d8358"></span>
## Step 3: View rate limiting rules


|**Actions** |RESTful request example |
|---|---|
|Get all rate limit configurations |```HTTP```<br>```GET _ratelimit/```<br> |
|Get a single specified rate limit configuration |```HTTP```<br>```GET _ratelimit/<limiterName>```<br> |


<span id="aaee953c"></span>
## Step 4: Delete rate limiting rules


|**Actions** |RESTful request example |
|---|---|
|Delete a single specified rate limit configuration |```HTTP```<br>```DELET _ratelimit/<limiterName>```<br> |


<span id="76755d34"></span>
## Step 5: Get monitoring information


|**Actions** |RESTful request example |
|---|---|
|Get metrics for all rate limiters |```HTTP```<br>```GET _ratelimit/metric```<br> |
|Get metrics for the specified rate limiter |```HTTP```<br>```GET _ratelimit/metric/{limitName}```<br> |
|Obtain metric data for all rate limiters on the specified node |```HTTP```<br>```GET _ratelimit/nodes/{nodeId}/metric```<br> |
|Obtain metric data for the specified rate limiter on the specified node |```HTTP```<br>```GET _ratelimit/nodes/{nodeId}/metric/{limitName}```<br> |
