---
title: "Prometheus time series data format"
product: "Vital Managed Service for Prometheus"
product_code: "vmp"
source: "https://docs.byteplus.com/en/docs/vmp/Format-of-Prometheus-time-series-data"
---

This topic describes the format of Prometheus time series data.

<span id=".5pe26Ze05bqP5YiX"></span>
## Time series

**Time series** data is the basic component of Prometheus data. Prometheus stores all collected sample data as time series in an in\-memory database and periodically saves the data to disks.

Every time series is uniquely identified by a metric name and a labelset, and is arranged by timestamp.


* Each time series has a name. For example:

   * `node_cpu_seconds_total` \- The usage duration of the node CPU.

   * `node_filesystem_free_bytes` \- The available space on the file system mount point.

   * `kube_pod_status_ready` \- All pods in the Ready status in the cluster.

* Each time series can have multiple `label="value"` labels. For example:

   * `node_cpu_seconds_total{cluster="ccdxxx",host_ip="10.10.128.2"}`

   * `kube_pod_status_ready{namespace="default"}`

* If the name or any label key\-value pair differs between two time series, they are defined as different time series. The following example demonstrates three time series.

   * `kube_pod_status_ready`

   * `kube_pod_status_ready{namespace="default"}`

   * `kube_pod_status_ready{namespace="volcano-metrics"}`


Time series are stored in sequential order of timestamps and values, which are referred to as vectors. The following figure shows an example.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2531821924f099c61f0931005dc72e98.png) </span>

<span id=".5rS76LeD5pe25bqP"></span>
## Active time series

An active time series is a time series that receives new data within the specified time (1 hour).

The number of active time series is directly related to the write performance of the workspace. If your maximum number of active time series exceeds the workspace quota, the collected data will be discarded. Therefore, you need to estimate the maximum number of active time series based on your business requirements.

<span id=".5qC35pys"></span>
## Sample

In a time series, each point is called a sample, which consists of the following three parts:


* Metric: a metric that consists of a metric name and a set of labelsets that describe the characteristics of the sample

* Timestamp: a timestamp that is accurate to milliseconds

* Value: a float64 value that indicates the value of the current sample


The following sample code shows a sample.

```Plain Text
<--------------- metric ---------------------><---timestamp--><-value->
http_request_total{status="200", method="GET"}@1434417560938 => 94355
```


<span id=".5oyH5qCH"></span>
## Metric

A metric consists of **a metric name and labels**. A metric can contain multiple labels.

```Plain Text
<--metric name -->{<label name>=<label value>, ...}
prometheus_http_requests_total{status="200", method="GET"}
```



| | | | | |
|---|---|---|---|---|
| | | | | |
| | | | | |
| | | | | |
