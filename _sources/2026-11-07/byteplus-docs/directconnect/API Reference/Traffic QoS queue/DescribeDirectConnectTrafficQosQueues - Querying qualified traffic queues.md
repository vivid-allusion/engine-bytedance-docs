---
title: "DescribeDirectConnectTrafficQosQueues - Querying qualified traffic queues"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosQueues"
---

Call DescribeDirectConnectTrafficQosQueues to query information about traffic queues that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectTrafficQosQueues&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|E0NyU4">必选</span> `Example: DescribeDirectConnectTrafficQosQueues`

The interface name. The current API name is `DescribeDirectConnectTrafficQosQueues`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Jytttz">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosQueueIds.N ** <span data-label="purple">String </span>`optional` `Example: dqq-93a1ee****`

The ID of the traffic queue.


* N represents the sequence number of a queue ID. You can call up to 100 IDs per request.

* Separate multiple IDs with ampersands (&).



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`optional` `Example: dcq-3bf8a0f4****`

The ID of the QoS policy associated with the traffic queue.



**DirectConnectTrafficQosQueueName ** <span data-label="purple">String </span>`optional` `Example: dqq-name`

The name of the traffic queue.



**QueueType ** <span data-label="purple">String </span>`optional` `Example: High`

The type of the traffic queue.


* **High**: High\-priority queue.

* **Medium**: Normal\-priority queue.

* **Default**: Default\-priority queue.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

The total number of qualified traffic queues.



**DirectConnectTrafficQosQueues ** <span data-label="purple">Object[] </span>`Example: -`

The list of traffic queues.


**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the traffic queue.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**QueueType ** <span data-label="purple">String </span>`Example: High`

The type of the traffic queue.


* **High**: High\-priority queue.

* **Medium**: Normal\-priority queue.

* **Default**: Default\-priority queue.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the traffic queue is updated.



**Description ** <span data-label="purple">String </span>`Example: test dqq`

The description of the traffic queue.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the traffic queue is created.



**BandwidthPercent ** <span data-label="purple">Integer </span>`Example: 10`

The bandwidth percentage of the traffic queue.


* Returns the corresponding percentage value when the traffic queue type is **Medium** or **Default**.

* Returns "0" when the traffic queue type is **High**.



**DirectConnectTrafficQosQueueId ** <span data-label="purple">String </span>`Example: dqq-5gta2c1cwd4c4gh0***`

The ID of the traffic queue.



**DirectConnectTrafficQosRuleIds ** <span data-label="purple">String[] </span>`Example: dqr-g8agtw13n58gcd89a****`

The ID of the traffic rule under the traffic queue.



**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-9atcc1cwd4c8g0a***`

The ID of the traffic queue.



**DirectConnectTrafficQosQueueName ** <span data-label="purple">String </span>`Example: dqq-name`

The name of the traffic queue.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectTrafficQosQueues&DirectConnectTrafficQosQueueIds.1=dqq-in0gqqzwvi808gbssyj5****&Version=2020-04-01 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectTrafficQosQueues",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectTrafficQosQueues": [
            {
                "Status": "Available",
                "QueueType": "High",
                "UpdateTime": "2021-04-09T08:36:47+08:00",
                "Description": "test dqq",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "BandwidthPercent": 10,
                "DirectConnectTrafficQosQueueId": "dqq-5gta2c1cwd4c4gh0***",
                "DirectConnectTrafficQosRuleIds": [
                    "dqr-g8agtw13n58gcd89a****"
                ],
                "DirectConnectTrafficQosPolicyId": "dcq-9atcc1cwd4c8g0a***",
                "DirectConnectTrafficQosQueueName": "dqq-name"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectTrafficQosQueueId |You've reached the limit on the number of direct connect traffic qos queue IDs that you can describe. |You have reached the maximum number of QoS traffic queues that can be queried. |
