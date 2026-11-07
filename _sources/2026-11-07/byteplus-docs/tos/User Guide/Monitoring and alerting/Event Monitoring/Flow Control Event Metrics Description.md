---
title: "Flow Control Event Metrics Description"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Flow-control-event-metrics-description"
---

This article introduces the flow control event indicators supported by TOS and provides examples of flow control event alarm notifications.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Event indicators are divided into the limit threshold and the reporting threshold, and the specific descriptions are as follows:</div>



* <div data-tips="true" data-tips-type="tip">Limit threshold: The maximum value of TOS resources that can be used by the current account. For detailed information about the default maximum value of available resources, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-restrictions">Restrictions</a>.</div>


* <div data-tips="true" data-tips-type="tip">Reporting threshold: The reporting threshold = the limit threshold × 0.8</div>



<span id="57b15b8b"></span>
## Flow control event metrics


|Event |Event description |Impact |Solution method |
|---|---|---|---|
|tos:Maintenance:AccountUploadBandwidthThresholdExceeded |User uplink bandwidth exceeds limit threshold |The latency of upstream requests will increase. |Reasonably reduce the number of concurrent upstream requests. |
|tos:Maintenance:AccountDownloadBandwidthThresholdExceeded |User downlink bandwidth exceeds limit threshold |The latency of downstream requests will increase. |Reasonably reduce the number of concurrent downstream requests. |
|tos:Maintenance:AccountGetQPSThresholdExceeded |User download QPS exceeds limit threshold |Reject and respond to some downstream requests and return a 429 status code. |Reasonably reduce the number of downstream requests per second. |
|tos:Maintenance:AccountListQPSThresholdExceeded |The user enumerates QPS exceeding the limit threshold |Reject and respond to some of the listed requests and return a 429 status code. |Reasonably reduce the number of listing requests per second. |
|tos:Maintenance:AccountPutQPSThresholdExceeded |User upload QPS exceeds limit threshold |Reject and respond to some of the upstream requests and return a 429 status code. |Reasonably reduce the number of upstream requests per second. |
|tos:Maintenance:AccountQosPolicyUploadBandwidthThresholdExceeded |User flow control policy uplink bandwidth exceeds limit threshold |The latency of upstream requests will increase. |Reasonably reduce the number of concurrent upstream requests. |
|tos:Maintenance:AccountQosPolicyDownloadBandwidthThresholdExceeded |The downlink bandwidth of the user flow control strategy exceeds the limit threshold |The latency of downstream requests will increase. |Reasonably reduce the number of concurrent downstream requests. |
|tos:Maintenance:AccountQosPolicyGetQPSThresholdExceeded |User flow control policy download QPS exceeds limit threshold |Reject and respond to some downstream requests and return a 429 status code. |Reasonably reduce the number of downstream requests per second. |
|tos:Maintenance:AccountQosPolicyListQPSThresholdExceeded |User flow control policy enumeration QPS exceeds limit threshold |Reject and respond to some of the listed requests and return a 429 status code. |Reasonably reduce the number of listing requests per second. |
|tos:Maintenance:AccountQosPolicyPutQPSThresholdExceeded |User flow control policy upload QPS exceeds limit threshold |Reject and respond to some of the upstream requests and return a 429 status code. |Reasonably reduce the number of upstream requests per second. |
|tos:Maintenance:BucketUploadBandwidthThresholdExceeded |Bucket upstream bandwidth exceeds limit threshold |The latency of upstream requests will increase. |Reasonably reduce the number of concurrent upstream requests. |
|tos:Maintenance:BucketDownloadBandwidthThresholdExceeded |Bucket downlink bandwidth exceeds limit threshold |The latency of downstream requests will increase. |Reasonably reduce the number of concurrent downstream requests. |
|tos:Maintenance:BucketGetQPSThresholdExceeded |Bucket download QPS exceeds limit threshold |Reject and respond to some downstream requests and return a 429 status code. |Reasonably reduce the number of downstream requests per second. |
|tos:Maintenance:BucketListQPSThresholdExceeded |Bucket enumeration QPS exceeds limit threshold |Reject and respond to some of the listed requests and return a 429 status code. |Reasonably reduce the number of listing requests per second. |
|tos:Maintenance:BucketPutQPSThresholdExceeded |Bucket upload QPS exceeds limit threshold |Reject and respond to some of the upstream requests and return a 429 status code. |Reasonably reduce the number of upstream requests per second. |
|tos:Maintenance:AccountDownloadBandwidth |User downlink bandwidth exceeds reporting threshold |None |None |
|tos:Maintenance:AccountGetQPS |User downloads QPS exceed reporting threshold |None |None |
|tos:Maintenance:AccountListQPS |Users cite QPS exceeding reporting thresholds |None |None |
|tos:Maintenance:AccountPutQPS |User upload QPS exceeds reporting threshold |None |None |
|tos:Maintenance:AccountQosPolicyDownloadBandwidth |The downlink bandwidth of the user flow control strategy exceeds the reporting threshold |None |None |
|tos:Maintenance:AccountQosPolicyGetQPS |User flow control strategy download QPS exceeds reporting threshold |None |None |
|tos:Maintenance:AccountQosPolicyListQPS |User flow control policy enumeration QPS exceeds reporting threshold |None |None |
|tos:Maintenance:AccountQosPolicyPutQPS |User flow control policy upload QPS exceeds reporting threshold |None |None |
|tos:Maintenance:AccountQosPolicyUploadBandwidth |Uplink bandwidth of user flow control strategy exceeds reporting threshold |None |None |
|tos:Maintenance:AccountUploadBandwidth |User uplink bandwidth exceeds reporting threshold |None |None |
|tos:Maintenance:BucketDownloadBandwidth |Bucket downlink bandwidth exceeds reporting threshold |None |None |
|tos:Maintenance:BucketGetQPS |Bucket download QPS exceeds reporting threshold |None |None |
|tos:Maintenance:BucketListQPS |Barrel enumeration QPS exceeds reporting threshold |None |None |
|tos:Maintenance:BucketPutQPS |Bucket upload QPS exceeds reporting threshold |None |None |
|tos:Maintenance:BucketUploadBandwidth |Bucket uplink bandwidth exceeds reporting threshold |None |None |


<span id="957203b6"></span>
## Event alarm notification example

After setting up event alarms according to the flow control settings, when the corresponding event occurs or the reporting threshold is reached, the system will push alarm notifications in the manner you specified. Specific examples of alarm notifications are as follows:

```JSON
{
  "data": {
    "AccountId": "214748****",
    "BucketName":"bucketname",
    "PercentThresholdLevel": 100,
    "QosPolicySid": "qospolicy-c862",
    "TrafficSource": "net_all"
  }
}
```


The parameter descriptions are as follows:


|**Parameter** |**Description** |
|---|---|
|AccountId |account ID. |
|BucketName |Bucket name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Alert notifications only return <code>BucketName</code> when the bucket flow control event is triggered.</div><br> |
|PercentThresholdLevel |The percentage of the traffic volume that triggers an event alarm relative to the flow control limit threshold. |
|QosPolicySid |Flow control policy name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Alert notifications only return <code>QosPolicySid</code> when the flow control policy event is triggered.</div><br> |
|TrafficSource |The type of network bandwidth that triggers the flow control alarm, with the following descriptions:<br><br><br>* `Extranet`: External network bandwidth.<br><br>* `net_all`: Total bandwidth, including both external and internal network bandwidths. |
