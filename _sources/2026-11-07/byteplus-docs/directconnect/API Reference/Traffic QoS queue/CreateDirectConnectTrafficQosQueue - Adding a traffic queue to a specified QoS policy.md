---
title: "CreateDirectConnectTrafficQosQueue - Adding a traffic queue to a specified QoS policy"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectTrafficQosQueue"
---

Call CreateDirectConnectTrafficQosQueue to add a traffic queue to a specified QoS policy.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

For more details and limits about traffic queues, see [QoS Policy overview](https://docs.byteplus.com/en/docs/directconnect/QoS_policy_overview).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectTrafficQosQueue&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|xSBFfh">必选</span> `Example: CreateDirectConnectTrafficQosQueue`

The interface name. The current API name is `CreateDirectConnectTrafficQosQueue`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|c5fStG">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span><span data-api-tag="require|gfIlw0">必选</span>`Example: dcq-jk17q7y1rk****`

The ID of the QoS policy with which the traffic queue is to be associated. You can call [DescribeDirectConnectTrafficQosPolicies](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies) to query the QoS policy ID.



**DirectConnectTrafficQosQueueName ** <span data-label="purple">String </span>`optional` `Example: dqq-name`

The name of the traffic queue.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If left empty, this parameter defaults to the traffic queue ID.



**Description ** <span data-label="purple">String </span>`optional` `Example: dqq-description`

The description of the traffic queue.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, this parameter defaults to an empty string.



**QueueType ** <span data-label="purple">String </span><span data-api-tag="require|RjMCdQ">必选</span> `Example: High`

The type of the traffic queue.


* **High**: high\-priority queue. High\-priority queues receive bandwidth allocation first. Each QoS policy can only have one high\-priority flow queue.

* **Medium**: Normal\-priority queues share the remaining bandwidth (after high\-priority allocation) based on their configured bandwidth percentage limits.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each QoS policy supports creating up to <strong>1</strong> <code>High</code> traffic queue (quota cannot be increased) and <strong>2</strong> <code>Medium</code> traffic queues (quota can be increased). For more usage limits on DC QoS policy configurations, see <a href="https://docs.byteplus.com/en/docs/directconnect/Limits">Limits</a>.</div>




**BandwidthPercent ** <span data-label="purple">Integer </span>`optional` `Example: 10`

The bandwidth percentage of the traffic queue.


* This field can be omitted when the traffic queue type is `High`.

* This field is required and must be an integer between 1 and 99 when the traffic queue type is `Medium`.

* The sum of the rate\-limiting bandwidth must not exceed 99 for all `Medium` traffic queues under the same QoS policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectTrafficQosQueueId ** <span data-label="purple">String </span>`Example: dqq-in0gopzrph4w8gbssykq****`

Traffic queue ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectTrafficQosQueue&Version=2020-04-01&DirectConnectTrafficQosPolicyId=dcq-12aso41dvse8017q7y2mq****&QueueType=Medium&BandwidthPercent=19 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241107160126BCE53F4F1F820D5C****",
        "Action": "CreateDirectConnectTrafficQosQueue",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20241107160126BCE53F4F1F820D5C****",
        "DirectConnectTrafficQosQueueId": "dqq-in0gopzrph4w8gbssykq****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectTrafficQosPolicy.InvalidStatus |The specified direct connect traffic qos policy is not in the correct status for the request. |The specified QoS policy cannot respond to this request due to its status. |
|400 |InvalidDirectConnectTrafficQosQueue.BandwidthPercentExceed |The specified bandwidth percentage of the traffic qos queue exceeds the available remaining bandwidth percentage. |The specified queue bandwidth percentage exceeds the remaining allocable bandwidth percentage. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidBandwidthPercent |The specified bandwidth percent of the direct connect traffic qos queue is invalid, Bandwidth percent only support 1~99. |The specified queue bandwidth percentage is invalid. Only integers from 1 to 99 are allowed. |
|400 |InvalidDirectConnectTrafficQosQueue.InvalidQueueType |The specified queue type of the direct connect traffic qos queue is invalid. |The specified QoS traffic queue type is invalid. |
|400 |InvalidDirectConnectTrafficQosQueue.RedundantBandwidthPercent |It is not supported to allocate bandwidth percent when direct connect traffic qos queue type is not medium. |Bandwidth percentage can be allocated only to normal\-priority QoS traffic queues. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |QuotaExceeded.DcTrafficQosQueue |You've reached the limit on the number of traffic qos queues that you can create. |You have reached the maximum number of QoS traffic queues that can be created. |
|404 |InvalidDirectConnectTrafficQosPolicy.NotFound |The specified direct connect traffic qos policy does not exist. |The specified QoS policy does not exist. |
|409 |InvalidDirectConnectTrafficQosQueue.HighTypeQueueConflict |A high type direct connect traffic qos queue already exists. You can have only one high type direct connect traffic qos queue per qos. |Only one high\-priority traffic queue can be created per QoS policy. A high queue already exists for this policy. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
