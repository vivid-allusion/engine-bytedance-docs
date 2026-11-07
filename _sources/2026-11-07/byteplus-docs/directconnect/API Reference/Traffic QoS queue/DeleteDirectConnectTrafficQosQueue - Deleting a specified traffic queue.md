---
title: "DeleteDirectConnectTrafficQosQueue - Deleting a specified traffic queue"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosQueue"
---

Call DeleteDirectConnectTrafficQosQueue to delete a specified traffic queue.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* Deleting a traffic queue may affect traffic marking. Ensure the queue bandwidth meets actual business needs.

* To delete a traffic queue, first call [DeleteDirectConnectTrafficQosRule](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectTrafficQosRule) to delete all manually added traffic rules in the queue.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectTrafficQosQueue&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|qWEWGx">必选</span> `Example: DeleteDirectConnectTrafficQosQueue`

The interface name. The current API name is `DeleteDirectConnectTrafficQosQueue`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|SyRy8j">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosQueueId** <span data-label="purple">String</span> <span data-api-tag="require|ArZUZa">必选</span>`Example: dqq-bf8a0f45ce****`

The ID of the traffic Queue to be deleted.

You can call the [DescribeDirectConnectTrafficQosQueues](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues) API to query the traffic queue ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectTrafficQosQueue&Version=2020-04-01&DirectConnectTrafficQosQueueId=dqq-in0gopzrph4w8gbssykq**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107160158BCE53F4F1F820D5****",
        "Action": "DeleteDirectConnectTrafficQosQueue",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107160158BCE53F4F1F820D5****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.DefaultQueueTypeUnsupported |It is not supported to operate the direct connect traffic qos queue with default queue type. |Actions on the default\-type traffic queues are not supported. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidStatus |The specified direct connect traffic qos queue is not in the correct status for the request. |The specified QoS traffic queue cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.WithTrafficQosRule |The specified traffic qos queue is in use. If you are trying to delete the traffic qos queue, ensure that its traffic qos rules have been deleted. |The specified QoS traffic queue is in use. Before attempting to delete a traffic queue, ensure all associated traffic rules have been deleted. |
|400 |QuotaExceeded.DcTrafficQosQueue |You've reached the limit on the number of traffic qos queues that you can create. |You have reached the maximum number of QoS traffic queues that can be created. |
|404 |InvalidDirectConnectTrafficQosQueue.NotFound |The specified direct connect traffic qos queue does not exist. |The specified QoS traffic queue does not exist. |
