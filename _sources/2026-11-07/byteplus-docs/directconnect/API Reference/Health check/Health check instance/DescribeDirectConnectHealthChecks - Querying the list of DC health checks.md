---
title: "DescribeDirectConnectHealthChecks - Querying the list of DC health checks"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectHealthChecks"
---

Call the DescribeDirectConnectHealthChecks API to query details of health check instances that meet the conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectHealthChecks&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|pronal">必选</span> `Example: DescribeDirectConnectHealthChecks`

The interface name. The current API name is `DescribeDirectConnectHealthChecks`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Ub9Bvz">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectHealthCheckIds.N ** <span data-label="purple">String </span>`optional` `Example: dhc-2752hz4tek****`

The ID of the health check instance.


* N represents the sequence number of a health check instance. You can call a maximum of 100 instances in a single request.

* Separate multiple health check instances with ampersands (&).



**DirectConnectHealthCheckName ** <span data-label="purple">String </span>`optional` `Example: dchc-01`

Name of the health check instance.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If you omit it or set it to 0, the value defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

Total number of health check probes that meet the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**DirectConnectHealthChecks ** <span data-label="purple">Object[] </span>`Example: -`

Details of the health check instance


**VpcId** <span data-label="purple">String</span> `Example: vpc-01`

The Virtual Private Cloud (VPC) where the health check instance is located.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the health check instance.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**SubnetId ** <span data-label="purple">String </span>`Example: subnet-2752hyf603yf`

The subnet where the target monitoring source IP is located.



**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the account to which the resource belongs.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check instance is updated.



**Description ** <span data-label="purple">String </span>`Example: This is a healthcheck`

The description of the health check instance.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-12-07T15:57:22+08:00`

The time when the health check instance is created.



**DirectConnectHealthCheckId ** <span data-label="purple">String </span>`Example: dhc-274oahfm8gjy87fap8tpn6n1c`

The ID of the health check instance.



**DirectConnectHealthCheckName** <span data-label="purple">String</span> `Example: dchc-01`

Name of the health check instance.



**DirectConnectHealthCheckProbeIds** <span data-label="purple">String[]</span> `Example: dhp-2752hz4****`

List of probes included in the health check instance.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectHealthChecks&Version=2020-04-01&DirectConnectHealthCheckName=dchc-01 HTTP/1.1
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
        "Action": "DescribeDirectConnectHealthChecks",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectHealthChecks": [
            {
                "VpcId": "vpc-01",
                "Status": "Available",
                "SubnetId": "subnet-2752hyf603yf",
                "AccountId": "20******57",
                "UpdateTime": "2021-12-07T15:57:22+08:00",
                "Description": "This is a healthcheck",
                "CreationTime": "2021-12-07T15:57:22+08:00",
                "DirectConnectHealthCheckId": "dhc-274oahfm8gjy87fap8tpn6n1c",
                "DirectConnectHealthCheckName": "dchc-01",
                "DirectConnectHealthCheckProbeIds": [
                    "dhp-2752hz4****"
                ]
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
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.DirectConnectHealthCheckId |You've reached the limit on the number of direct connect health check IDs that you can describe. |You have reached the maximum number of health check IDs that can be queried. |
