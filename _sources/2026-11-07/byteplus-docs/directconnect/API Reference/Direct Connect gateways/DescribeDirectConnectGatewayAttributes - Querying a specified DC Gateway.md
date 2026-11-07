---
title: "DescribeDirectConnectGatewayAttributes - Querying a specified DC Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayAttributes"
---

Call DescribeDirectConnectGatewayAttributes to query the details of a specified Direct Connect (DC) Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectGatewayAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|e20sX7">必选</span> `Example: DescribeDirectConnectGatewayAttributes`

The interface name. The current API name is `DescribeDirectConnectGatewayAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|JSLaWW">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|uZ4zAv">必选</span>`Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway to be queried.

You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the DC Gateway ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the account to which the DC Gateway belongs.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway.



**DirectConnectGatewayName ** <span data-label="purple">String </span>`Example: test`

Name of the DC Gateway.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

Description of the DC Gateway.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the DC Gateway is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the DC Gateway is updated.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the DC Gateway.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**BusinessStatus ** <span data-label="purple">String </span>`Example: FinancialLocked`

Specify whether the DC Gateway is locked.


* Normal

* FinancialLocked: Being locked.



**LockReason ** <span data-label="purple">String </span>`Example: Financial`

The reason why the DC Gateway is locked.


* unlock

* financial: Being locked due to arrears.

* security: Being locked due to security.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-04-29 01:37:38`

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to overdue payments. Otherwise, it returns an empty string.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-04-30 01:37:38`

The scheduled time when the resource is reclaimed forcibly. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.



**AssociateCens ** <span data-label="purple">Object[] </span>`Example: -`

Information about the associated Cloud Enterprise Network (CEN).


**CenId ** <span data-label="purple">String </span>`Example: cen-23987fdc****`

The ID of the CEN.



**CenOwnerId ** <span data-label="purple">String </span>`Example: 122***023`

User ID of the CEN.



**CenStatus ** <span data-label="purple">String </span>`Example: Attached`

The instance status in the CEN.


* Attaching

* Attached




**Tags ** <span data-label="purple">Object[] </span>`Example: -`

All tags added to the DC Gateway.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**EnableIpv6 ** <span data-label="purple">Boolean </span>`Example: false`

Specify whether IPv6 is supported.


* true: Supported

* false: Not supported



**ProjectName ** <span data-label="purple">String </span>`Example: project-01`

The project to which the DC Gateway belongs.



**BgpAsn ** <span data-label="purple">Integer </span>`Example: 137718`

ASN of the DC Gateway.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectGatewayAttributes&Version=2020-04-01&DirectConnectGatewayId=dcg-7qthudw0ll6jmc**** HTTP/1.1
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
        "Action": "DescribeDirectConnectGatewayAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "21000*****",
        "AssociateCens": [
            {
                "CenId": "cen-23987fdc****",
                "CenStatus": "Attached",
                "CenOwnerId": "122***023"
            }
        ],
        "BgpAsn": 137718,
        "BusinessStatus": "FinancialLocked",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "DeletedTime": "2021-04-30 01:37:38",
        "Description": "This is a sample description",
        "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****",
        "DirectConnectGatewayName": "test",
        "EnableIpv6": true,
        "LockReason": "Financial",
        "OverdueTime": "2021-04-29 01:37:38",
        "ProjectName": "project-01",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-04-10T09:18:28+08:00"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
