---
title: "DescribeDirectConnectTrafficQosPolicies - Querying qualified QoS policies"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectTrafficQosPolicies"
---

Call DescribeDirectConnectTrafficQosPolicies to query QoS policies that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectTrafficQosPolicies&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|rifkAn">必选</span> `Example: DescribeDirectConnectTrafficQosPolicies`

The interface name. The current API name is `DescribeDirectConnectTrafficQosPolicies`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|tcIpO0">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectTrafficQosPolicyIds.N ** <span data-label="purple">String </span>`optional` `Example: dcq-4bwbhc****`

The ID of the QoS policy.


* N represents the sequence number of a QoS policy ID. You can call a maximum of 100 IDs in a single request.

* Separate multiple IDs with ampersands (&).



**DirectConnectTrafficQosPolicyName ** <span data-label="purple">String </span>`optional` `Example: Qos-policy002`

The name of the QoS policy.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

Page size of the query results. Maximum: 100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of query results


* Set this parameter to a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 33`

The total number of QoS policies matching the query conditions.



**DirectConnectTrafficQosPolicies ** <span data-label="purple">Object[] </span>`Example: -`

The list of QoS policies.


**DirectConnectTrafficQosPolicyId ** <span data-label="purple">String </span>`Example: dcq-my4e8i4****`

The ID of the QoS policy.



**DirectConnectTrafficQosPolicyName ** <span data-label="purple">String </span>`Example: dcq-name`

The name of the QoS policy.



**Description ** <span data-label="purple">String </span>`Example: dcq-describe`

The description of the QoS policy.



**Status ** <span data-label="purple">String </span>`Example: Pending`

The status of the QoS policy.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**DirectConnectConnectionIds ** <span data-label="purple">String[] </span>`Example: dcc-2l4c6c0v****`

The ID of the DC Connection with which the QoS policy is associated.



**DirectConnectTrafficQosQueueIds ** <span data-label="purple">String[] </span>`Example: dqq-1234****`

The ID of the traffic queue associated with the QoS policy.



**CreationTime ** <span data-label="purple">String </span>`Example: 2024-10-09T08:36:47+08:00`

The time when the QoS policy is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2024-10-10T08:36:47+08:00`

The time when the QoS policy is updated.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectTrafficQosPolicies&Version=2020-04-01&DirectConnectTrafficQosPolicyIds.1=dcq-12aso41dvse8017q7y2m****&PageNumber=1&PageSize=20 HTTP/1.1
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
        "Action": "DescribeDirectConnectTrafficQosPolicies",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectTrafficQosPolicies": [
            {
                "Status": "Pending",
                "UpdateTime": "2024-10-10T08:36:47+08:00",
                "Description": "dcq-describe",
                "CreationTime": "2024-10-09T08:36:47+08:00",
                "DirectConnectConnectionIds": [
                    "dcc-2l4c6c0v****"
                ],
                "DirectConnectTrafficQosPolicyId": "dcq-my4e8i4****",
                "DirectConnectTrafficQosQueueIds": [
                    "dqq-1234****"
                ],
                "DirectConnectTrafficQosPolicyName": "dcq-name"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 33
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
|400 |LimitExceeded.DirectConnectTrafficQosPolicyId |You've reached the limit on the number of direct connect traffic qos policy IDs that you can describe. |You have reached the maximum number of QoS policies that can be queried |
