---
title: "DescribeSessionLogs - Querying session logs"
product: "NAT Gateway"
product_code: "natgateway"
source: "https://docs.byteplus.com/en/docs/natgateway/DescribeSessionLogs"
---

Call the DescribeSessionLogs API to query the session log list for a NAT instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSessionLogs&groupName=NAT%E4%BC%9A%E8%AF%9D%E6%97%A5%E5%BF%97&serviceCode=natgateway&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|hTfrUM">必选</span> `Example: DescribeSessionLogs`

The action that you want to perform. Value: DescribeSessionLogs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|WjhHko">必选</span> `Example: 2020-04-01`

The API version. Value: 2020\-04\-01.



**PageNumber ** <span data-label="purple">integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example: 1`

The number of entries on each page in a pagination query. Valid range: 1–100. Default: 20.



**NatGatewayId ** <span data-label="purple">string </span>`optional` `Example: ngw-123456****`

The NAT instance ID in the session log for retrieving log information

You can call the [DescribeNatGateways](https://docs.byteplus.com/en/docs/natgateway/DescribeNatGateways) API to query the ID of the NAT gateway.



**SessionLogName ** <span data-label="purple">string </span>`optional` `Example: ngw-SessionLog`

The name of the session log.



**TlsProjectName ** <span data-label="purple">string </span>`optional` `Example: TLS-project`

The name of the log project.



**TlsTopicName ** <span data-label="purple">string </span>`optional` `Example: TLS-topic`

The name of the log topic.



**Status ** <span data-label="purple">string </span>`optional` `Example: Active`

The status of the session log. Values:


* Active: Enabled.

* Inactive: Not enabled.

* Pending: Action in progress​.

* Creating

* Deleting



**SessionLogIds.N ** <span data-label="purple">string[] </span>`optional` `Example: nsl-273w1s2v5xnuo7fap8t8****`

The ID of the session log.


* N represents the sequence number of a session log ID. You can specify a maximum of 20 IDs per call.

* Separate multiple IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">integer </span>`Example: 1`

Total number of query results that meet the conditions.



**RequestId ** <span data-label="purple">string </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28****`

Request ID.



**SessionLogs ** <span data-label="purple">object[] </span>`Example: 1`

Details of the NAT session log.


**NatGatewayId ** <span data-label="purple">string </span>`Example: ngw-SessionLog`

The NAT instance ID in the session log for retrieving log information



**SessionLogId ** <span data-label="purple">string </span>`Example: nsl-273w1s2v5xnuo7fap8t8****`

The ID of the session log.



**SessionLogName ** <span data-label="purple">string </span>`Example: ngw-SessionLog`

The name of the session log.



**Description ** <span data-label="purple">string </span>`Example: -`

The description of the session log.



**TlsProjectName ** <span data-label="purple">string </span>`Example: TLS-project`

The project name of the session log.



**TlsProjectId ** <span data-label="purple">string </span>`Example: 98143db1-0078-400d-bfcf-6925f28****`

The project ID of the session log.



**TlsTopicName ** <span data-label="purple">string </span>`Example: TLS-topic`

The topic name of the session log.



**TlsTopicId ** <span data-label="purple">string </span>`Example: 98143db1-0078-400d-bfcf-6925f28****`

ID of the Torch Log Service (TLS) topic.



**AggregationInterval ** <span data-label="purple">integer </span>`Example: -`

The collection interval of the NAT session log.



**Status ** <span data-label="purple">string </span>`Example: Active`

The status of the session log.


* Active: Enabled.

* Inactive: Not enabled.

* Pending: Action in progress​.

* Creating

* Deleting




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```text
GET /?Action=DescribeSessionLogs&Version=2020-04-01&TlsProjectName=TLS-project HTTP/1.1
Host: natgateway.cn-beijing.byteplusapi.com.cn
ServiceName: natgateway
Region: cn-beijing
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```text
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "DescribeSessionLogs",
        "Version": "2020-04-01",
        "Service": "natgateway",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 1,
        "PageNumber": 1,
        "PageSize": 20,
        "SnatEntries": [
            {
                "NatGatewayId": "ngw-123456****",
                "Description": " ",
                "SessionLogId": "nsl-273w1s2v5xnuo7fap8t8****",
                "SessionLogName": "ngw-SessionLog",
                "TlsProjectId":"98143db1-0078-400d-bfcf-6925f28****",
                "TlsProjectName": "TLS-project",
                "TlsTopicId": "98143db1-0078-400d-bfcf-6925f28****",
                "TlsTopicName": "TLS-topic",
                "Status": "Active"

            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/natgateway/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |A parameter specified in the request is not valid, is unsupported or cannot be used. |The request contains invalid or unsupported parameters. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.SessionLogId |You've reached the limit on the number of session log instance IDs that you can describe. |You have reached the maximum number of NAT session log IDs that can be queried. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. |
