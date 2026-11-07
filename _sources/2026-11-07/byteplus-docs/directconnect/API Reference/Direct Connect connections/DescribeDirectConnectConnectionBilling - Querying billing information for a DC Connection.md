---
title: "DescribeDirectConnectConnectionBilling - Querying billing information for a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnectionBilling"
---

Call DescribeDirectConnectConnectionBilling to query the billing information of a Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectConnectionBilling&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|5GhwoA">必选</span> `Example: DescribeDirectConnectConnectionBilling`

The interface name. The current API name is `DescribeDirectConnectConnectionBilling`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Ct3PFc">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Value range: 1–100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number for pagination query.


* Set this parameter to a non\-negative integer.

* If left blank or set to 0, it defaults to 1.



**DirectConnectConnectionIds.N ** <span data-label="purple">String </span>`optional` `Example: dcc-8ha23ndut0jd93****`

The ID of the DC Connection.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.


* N represents the sequence number of the DC Connection ID.

* Separate multiple IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount** <span data-label="purple">Integer</span> `Example: 1`

The number of DC Connections that meet the query conditions.



**DirectConnectConnections ** <span data-label="purple">Object[] </span>`Example: -`

The detailed billing information of the DC Connection.


**RenewType ** <span data-label="purple">String </span>`Example: Auto`

The renewal method.


* Auto: Automatic renewal.

* Manual: Manual renewal.

* NoRenew: Non\-renewal upon expiration.



**BillingType ** <span data-label="purple">Integer </span>`Example: 1`

The billing method. Currently, only "**1**" (Subscription) is supported.



**ExpiredTime ** <span data-label="purple">String </span>`Example: 2022-10-11 23:59:59`

The time when the DC Connection resource expires.



**BillingStatus ** <span data-label="purple">Integer </span>`Example: 1`

The billing status.


* 1: Billing running

* 2: Instance creation failed

* 3: Unsubscribed

* 4: Expired and suspended

* 5: Expired and reclaimed



**ReclaimedTime** <span data-label="purple">String</span> `Example: 2022-10-12: 23:33:59`

The time when the DC Connection resource is reclaimed.



**RemainRenewTimes ** <span data-label="purple">Integer </span>`Example: 1`

The number of remaining automatic renewals available.



**DirectConnectConnectionId** <span data-label="purple">String</span> `Example: dcc-2j8b0283****`

The ID of the DC Connection.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectConnectionBilling&Version=2020-04-01&PageSize=20&PageNumber=1&DirectConnectConnectionIds.1=dcc-8ha23ndut0jd93**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectConnectionBilling",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectConnections": [
            {
                "RenewType": "Auto",
                "BillingType": 1,
                "ExpiredTime": "2022-10-11 23:59:59",
                "BillingStatus": 1,
                "ReclaimedTime": "2022-10-12: 23:33:59",
                "RemainRenewTimes": 1,
                "DirectConnectConnectionId": "dcc-2j8b0283****"
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
|400 |LimitExceeded.DirectConnectConnectionId |You've reached the limit on the number of direct connect connection IDs that you can describe. |You have reached the maximum number of DC Connection IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
