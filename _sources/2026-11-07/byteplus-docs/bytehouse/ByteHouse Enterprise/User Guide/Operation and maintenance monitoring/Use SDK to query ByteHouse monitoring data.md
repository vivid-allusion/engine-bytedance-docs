---
title: "Use SDK to query ByteHouse monitoring data"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/ce-use-sdk-to-query-bytehouse-monitoring-data"
---

<span id="67896701"></span>
# Prerequisites

Obtain the ByteHouse account Access Key. For detailed steps, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

<span id="cc7963b5"></span>
# Parameter description

Refer to the cloud monitoring documentation for the specific request Body parameters: [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData).

Here are some required parameters:


|**Parameter name** |**Required** |**Remark** |
|---|---|---|
|Region |Yes |For example: ap\-southeast\-1 |
|AccessKey/SecretKey |Yes |The current account's AccessKey/SecretKey. Refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey) for specific steps. |
|MetricName |Yes |Name of the monitoring metric to query. |
|StartTime |Yes |The start time of the query period, a second\-level timestamp, for example 1632904500. |
|EndTime |Yes |The end time of the query time segment, a second\-level timestamp, such as 1632904801.<br><br>EndTime \> StartTime。<br><br>End Time cannot be set to a future time.<br><br>End Time < Products allowed query days + Start Time. |
|Period |Yes |The interval at which data is queried.<br><br><br>* **m**: minute<br><br>* **s**: second<br><br>* **h**: hour<br><br>* **d**: day<br><br>* **w**: week |
|Namespace |Yes |Fixed as: **VCM_ByteHouse_Ce** |
|Instances |Yes |Metric dimension information to query. For example, when querying the Connection_Gateway_Connection_Count metric, configure the dimension as ResourceID.<br><br>When multiple instances exist, the logical relationship between instances is `or`.<br><br>If the instance parameter is not passed, monitoring data for all instances under the region will be returned. **Large amounts of data may cause max\-select\-point to exceed limits, affecting business operations. proceed with caution**. |
|SubNamespace |No |Dimension to which the metric belongs. |


For the full list of metrics currently viewable in Bytehouse Cloud Monitoring, see [Monitoring alerts](https://docs.byteplus.com/docs/bytehouse/ce-monitoring-alerts).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">ResourceID must be passed for each metric. In the current version, ResourceID equals instance ID.</div>


<span id="ae8fe4b0"></span>
# Code example

Using the GO SDK as an example, query the cluster_cpu_usage_percentage metric with ResourceID as the dimension filter.

Replace ResourceID with actual values. You can obtain the ResourceID following the instructions below:

**ResourceID**: Instance ID. You can log in to BytePlus, click **Cluster management** at the top, go to the **Cluster list** page, click the target cluster, and view the Instance ID on the **Basic information** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fbfcd959afd41a88728dddea50db062~tplv-goo7wpa0wc-image.image) </span>

```Go
POST https://volc-observe.ap-southeast-1.byteplusapi.com.cn?Action=GetMetricData&Version=2018-01-01
ServiceName=Volc_Observe
Region=ap-southeast-1
AccessKey=xxx 
SecretKey=xxx 

{
    "MetricName":"cluster_cpu_usage_percentage",
    "StartTime":1648048800,
    "EndTime":1648049400,
    "Period":"1m",
    "Namespace":"VCM_ByteHouse_Ce",
    "Instances":[
        {
            "Dimensions":[
                {
                    "Name":"ResourceID",
                    "Value":"Bytehouse_enterprisexxxxxxxxxxxxxx"
                }
            ]
        },
    ],
    "SubNamespace":""
}
```
