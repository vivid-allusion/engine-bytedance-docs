---
title: "ModifyDirectConnectTrafficQosQueueAttributes - Modifying a specified traffic queue"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectTrafficQosQueueAttributes"
---

Call ModifyDirectConnectTrafficQosQueueAttributes to modify a specified traffic queue.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Default traffic queues do not support modification. You can call [DescribeDirectConnectTrafficQosQueues](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues) to query the traffic queue information. The queue with DirectConnectTrafficQosQueueName set to **Default** and Description set to **Default Queue** is a default traffic queue.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectTrafficQosQueueAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|uH1YGv">必选</span> `Example: ModifyDirectConnectTrafficQosQueueAttributes`

The interface name. The current API name is `ModifyDirectConnectTrafficQosQueueAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|rjWsiB">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosQueueId ** <span data-label="purple">String </span><span data-api-tag="require|9sTuj6">必选</span> `Example: dqq-123456`

Traffic queue ID.



**DirectConnectTrafficQosQueueName** <span data-label="purple">String</span> `optional` `Example: dqq-name`

The name of the traffic queue.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left blank, the original configuration remains.



**Description ** <span data-label="purple">String </span>`optional` `Example: dqq-description`

The description of the traffic queue.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



**BandwidthPercent ** <span data-label="purple">Integer </span>`optional` `Example: 78`

The bandwidth percentage of the traffic queue. You can call [DescribeDirectConnectTrafficQosQueues](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues) to query the type of traffic queue.


* This parameter is configurable only for `Medium` traffic queues, with a value range of 1 to 99.

* The sum of the rate\-limiting bandwidth must not exceed 99 for all `Medium` traffic queues under the same QoS policy.

* If left blank, the current configuration remains.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectTrafficQosQueueAttributes&Version=2020-04-01&DirectConnectTrafficQosQueueId=dqq-in0gqqzwvi808gbssyj5****&DirectConnectTrafficQosQueueName=test&Description=test HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107160240BCE53F4F1F820D5****",
        "Action": "ModifyDirectConnectTrafficQosQueueAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107160240BCE53F4F1F820D5****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.BandwidthPercentExceed |The specified bandwidth percentage of the traffic qos queue exceeds the available remaining bandwidth percentage. |The specified queue bandwidth percentage exceeds the remaining allocable bandwidth percentage. |
|400 |InvalidDirectConnectTrafficQosQueue.DefaultQueueTypeUnsupported |It is not supported to operate the direct connect traffic qos queue with default queue type. |Actions on the default\-type traffic queues are not supported. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidBandwidthPercent |The specified bandwidth percent of the direct connect traffic qos queue is invalid, Bandwidth percent only support 1~99. |The specified queue bandwidth percentage is invalid. Only integers from 1 to 99 are allowed. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidStatus |The specified direct connect traffic qos queue is not in the correct status for the request. |The specified QoS traffic queue cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.RedundantBandwidthPercent |It is not supported to allocate bandwidth percent when direct connect traffic qos queue type is not medium. |Bandwidth percentage can be allocated only to normal\-priority QoS traffic queues. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|404 |InvalidDirectConnectTrafficQosQueue.NotFound |The specified direct connect traffic qos queue does not exist. |The specified QoS traffic queue does not exist. |
