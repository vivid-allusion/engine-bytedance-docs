---
title: "Abnormal comparison function"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Abnormal-comparison-function"
---

This topic describes the syntax of the abnormal comparison function supported by Torch Log Service(TLS) and examples of usage in common scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="cb7b66c2"></span>
## anomaly_compare

<span id="586c9994"></span>
#### Function syntax


* Syntax format

   ```SQL
   anomaly_compare(stamp, array[ feature_1, feature_2 ], array[ feature1_name, feature2_name ], timepoint, interval)
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |stamp |String |The name of the time column in the format unixtime timestamp in seconds. |
   |array[features] |Array |The characteristic data of the observed object at a certain moment. |
   |array[featureNames] |Array |The description information of the feature data. |
   |timepoint |Bigint |The point in time when the observed object changed, in the format unixtime timestamp. |
   |interval |Bigint |The interval at which data is collected, for example: every 10 seconds, the interval is 10. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="e8f9cc6b"></span>
#### Function example


* Query and analysis statement

   ```SQL
   *| SELECT anomaly_compare(stamp,array[ReqSize,RespSize],array['ReqSize','RespSize'],1702236290,1) FROM (SELECT stamp,ReqSize,RespSize FROM (SELECT CAST(stamp as BIGINT) AS stamp,ReqSize, RespSize order by stamp limit 1000))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/747ba5ab4e934ba19f68689951c79409~tplv-goo7wpa0wc-image.image) </span>


&nbsp;
