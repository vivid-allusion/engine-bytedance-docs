---
title: "Time series clustering functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Time-series-clustering-functions"
---

This topic introduces the syntax of the time series clustering functions supported by Torch Log Service(TLS) and examples of usage in common scenarios.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the machine learning functions are in public beta.</div>


<span id="1536be1a"></span>
## Function list


|Function |Description |
|---|---|
|ts_density_cluster |Uses the density clustering method to cluster multiple time series curves. |
|ts_hierarchical_cluster |Uses a hierarchical clustering method to cluster multiple time series curves. |
|ts_similar_instance |Searches for time series curves that are similar to the specified time series curve. |


<span id="2c8462cc"></span>
## **ts_density_cluster**

ts_density_cluster function uses the density clustering method to cluster multiple time series curves.

<span id="dd28128e"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_density_cluster(x, y, z) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |x |String |The name of the time column. The format is unixtime timestamp in seconds. |
   |y |String |The name of the numeric column corresponding to the data at a certain time. |
   |z |String |The name of the curve corresponding to the data at a certain moment. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="1b520b80"></span>
### Function example


* Query and analysis statement

   ```SQL
   * | select ts_density_cluster(stamp, value,CAST( (stamp-stamp % 7200)  as varchar) ) from (select stamp, value limit 1000)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/54e08f0d4c634411beb1999c8d5ba2b6~tplv-goo7wpa0wc-image.image) </span>


<span id="3e2775b1"></span>
## ts_hierarchical_cluster

The ts_hierarchical_cluster function uses a hierarchical clustering method to cluster multiple time series curves.

<span id="5eb44295"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_hierarchical_cluster(x, y, z) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |x |String |The name of the time column. The format is unixtime timestamp in seconds. |
   |y |String |The name of the numeric column corresponding to the data at a certain time. |
   |z |String |The name of the curve corresponding to the data at a certain moment. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="c92886c6"></span>
### Function example


* Query and analysis statement

   ```SQL
   * | select ts_hierarchical_cluster(stamp, value,CAST( (stamp-stamp % 6000)  as varchar) )  from (select stamp, value limit 1000)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c3ffeb7f05a42d8969137aa98ba742a~tplv-goo7wpa0wc-image.image) </span>


<span id="4873c444"></span>
## **ts_similar_instance**

ts_similar_instance function is used to search for time series curves that are similar to the specified time series curve.

<span id="f40b0b1d"></span>
### Function syntax


* Syntax format

   ```SQL
   ts_similar_instance(x, y, z，instance_name，topK，metricType) 
   ```
   

* Parameter description

   
   |Parameter |Data type |Description |
   |---|---|---|
   |*x* |String |The name of the time column. The format is unixtime timestamp in seconds. |
   |*y* |String |The name of the numeric column corresponding to the data at a certain time. |
   |z |String |The name of the curve corresponds to the data at a certain moment. |
   |instance_name |String |Specify the name of a curve to be searched. It must be a curve that has already been created. |
   |topK |Long |Return at most K curves that are similar to the given curve. |
   |metricType |String |An indicator for measuring the similarity between time series curves. |
   

* Return value description

   If the input value is null, null will be returned.


<span id="6f685e1c"></span>
### Function example


* Query and analysis statement

   ```SQL
   * | select  ts_similar_instance(stamp, value,CAST( (stamp-stamp % 6000)  as varchar),CAST( (stamp-stamp % 6000)  as varchar) ) from (select stamp, value limit 1000)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7423e81178b84c63a6388f058d8ff698~tplv-goo7wpa0wc-image.image) </span>
