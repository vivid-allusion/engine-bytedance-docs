---
title: "Query ByteHouse monitoring data using SDK"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/cdw-query-bytehouse-monitoring-data-using-sdk"
---

<span id="f03dd084"></span>
# Prerequisites

Obtain the Access Key for your ByteHouse account. For detailed steps, refer to [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey).

<span id="f82f1acf"></span>
# Parameter description

Refer to the related cloud monitoring document for specific request Body parameters: [GetMetricData](https://docs.byteplus.com/en/docs/cloudmonitor/GetMetricData).

Here are some required parameters:


|**Parameter name** |**Required** |**Remark** |
|---|---|---|
|Region |Yes |Example: ap\-southeast\-1 |
|AccessKey/SecretKey |Yes |The current account's AccessKey/SecretKey. For detailed steps, see [Creating an access key](https://docs.byteplus.com/en/docs/byteplus-platform/docs-creating-an-accesskey). |
|MetricName |Yes |The name of the monitoring metric to query. |
|StartTime |Yes |Start time of the query period, in seconds timestamp, e.g. 1632904500. |
|EndTime |Yes |The end time of the queried time range, represented as a second\-level timestamp, for example 1632904801.<br><br>EndTime \> StartTime.<br><br>End Time cannot be set to a future time.<br><br>End Time < Products allowed query Total Days + Start Time. |
|Period |Yes |The interval at which data is queried.<br><br><br>* **m**: minute<br><br>* **s**: second<br><br>* **h**: hour<br><br>* **d**: day<br><br>* **w**: week |
|Namespace |Yes |Fixed as: **VCM_ByteHouse** |
|Instances |Yes |Metric dimension information to query. For example, when querying the Connection_Gateway_Connection_Count metric, set the dimension to ResourceID.<br><br>If multiple instances exist, the logical relation between instances is or.<br><br>If the instance parameter is not provided, monitoring data for all instances in that region will be returned. **Large data volume may cause max\-select\-point limit exceedance, affecting business. Handle with caution**. |
|SubNamespace |No |The dimension to which the metric being queried belongs. |


For the full list of metrics currently available in Bytehouse cloud monitoring, see [Monitoring metric description](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm#c2ada7cb).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Each metric must include a ResourceID. In the current version, ResourceID equals envID, so provide envID.</div>


<span id="95452d9b"></span>
# Example

Using the GO SDK as an example, query the VirtualWarehouse_CPU_Usage_Percentage metric with the dimension filter set to ResourceID, VWID.

Replace ResourceID and VWID with actual values. You can obtain the ResourceID and VWID following the instructions below:


* **ResourceID**: Env ID. Log in to the ByteHouse console, click **Tenant management** at the top, and then click the **Basic information** tab. You can view and copy the environment name in the **Current environment** module.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fe784c9af5d4847a92890a1dd757858~tplv-goo7wpa0wc-image.image) </span>

* **VWID**: Virtual warehouse ID. Log in to the ByteHouse console and click the Virtual warehouse on the top bar. View and copy the virtual warehouse ID in the list.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbaafc4a768749f8a6bbaf961ad846ed~tplv-goo7wpa0wc-image.image) </span>


```Go
POST https://volc-observe.ap-southeast-1.byteplusapi.com.cn?Action=GetMetricData&Version=2018-01-01
ServiceName=Volc_Observe
Region=ap-southeast-1
AccessKey=xxx 
SecretKey=xxx 

{
    "MetricName":"VirtualWarehouse_CPU_Usage_Percentage",
    "StartTime":1648048800,
    "EndTime":1648049400,
    "Period":"1m",
    "Namespace":"VCM_ByteHouse",
    "Instances":[
        {
            "Dimensions":[
                {
                    "Name":"ResourceID",
                    "Value":"xxxxxxxxx"
                }
            ]
        },
        {
            "Dimensions":[
                {
                    "Name":"VWID",
                    "Value":"vw-{vwID}-{vw_name}"
                }
            ]
        }
    ],
    "SubNamespace":""
}
```
