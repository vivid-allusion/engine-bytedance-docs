---
title: "DescribeDirectConnectGateways - Querying DC Gateways"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways"
---

Call DescribeDirectConnectGateways to query the details of Direct Connect (DC) Gateways that meet specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If the DirectConnectGatewayIds request parameter is not specified, the system queries based on the other parameters provided and returns the qualified DC Gateways.

* If you do not provide any optional request parameters, the system queries based on the currently logged\-in account and returns all DC Gateways under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectGateways&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|BkibOP">必选</span> `Example: DescribeDirectConnectGateways`

The interface name. The current API name is `DescribeDirectConnectGateways`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|bpleAD">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayIds.N ** <span data-label="purple">String </span>`optional` `Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway.


* N represents the sequence number of a DC Gateway ID. You can call a maximum of 100 IDs per request.

* Separate multiple DC Gateway IDs with ampersands ( & ).



**DirectConnectGatewayName ** <span data-label="purple">String </span>`optional` `Example: dcwg-name`

Name of the DC Gateway.



**CenId ** <span data-label="purple">String </span>`optional` `Example: cen-257gqcdfvx6n****`

ID of the Cloud Enterprise Network (CEN) to which the DC Gateway belongs.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* If you specify this parameter, it must be a non\-negative integer.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the cloud resource instance.


* N represents the sequence number of a tag key. Valid values: 1\-10.

* Separate multiple tag keys with ampersands `(&)`.

* If you set multiple `TagFilters.N.Key` values, these `TagFilters.N.Key` values must be unique and are combined with a logical AND​​.



**TagFilters.N.Values.M ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the cloud resource instance.


* N represents the sequence number of a tag key. Valid values: 1\-10.

* M represents the sequence number of a tag value. Valid range: 1–3. That is, you can query up to 3 tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide `TagFilters.N.Key`.

* If you only provide `TagFilters.N.Key` without this parameter, the system will query all tag values of the same tag key.

* If you provide an empty string, the system will query tags with an empty tag value.

* If you set multiple `TagFilters.N.Values.M` values for the same `TagFilters.N.Key`, these `TagFilters.N.Values.M` values are combined with a logical OR.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 10`

The total number of DC Gateways that meet the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**DirectConnectGateways ** <span data-label="purple">Object[] </span>`Example: -`

Details of the DC Gateway.


**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

ID of the account to which the DC Gateway belongs.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-7qthudw0ll6jmc****`

ID of the DC Gateway.



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

The time when the resource is frozen. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-04-30 01:37:38`

The time when the resource is scheduled to be forcibly reclaimed. This parameter returns a value only if the resource is frozen due to arrears. Otherwise, it returns an empty string.



**AssociateCens ** <span data-label="purple">Object[] </span>`Example: -`

Information about the associated CEN.


**CenId ** <span data-label="purple">String </span>`Example: cen-23987fdc****`

CEN ID.



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

Project to which the DC Gateway belongs.



**BgpAsn ** <span data-label="purple">Integer </span>`Example: 137718`

ASN of the DC Gateway.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectGateways&Version=2020-04-01&DirectConnectGatewayIds.1=dcg-7qthudw0ll6jmc****&DirectConnectGatewayName=dcwg-name&CenId=cen-257gqcdfvx6n****&PageNumber=1&PageSize=20&TagFilters.1.Key=key1&TagFilters.1.Values.M=value1 HTTP/1.1
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
        "Action": "DescribeDirectConnectGateways",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "DirectConnectGateways": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "BgpAsn": 137718,
                "Status": "Available",
                "AccountId": "21000*****",
                "EnableIpv6": false,
                "LockReason": "Financial",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "DeletedTime": "2021-04-30 01:37:38",
                "Description": "This is a sample description",
                "OverdueTime": "2021-04-29 01:37:38",
                "ProjectName": "project-01",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "AssociateCens": [
                    {
                        "CenId": "cen-23987fdc****",
                        "CenStatus": "Attached",
                        "CenOwnerId": "122***023"
                    }
                ],
                "BusinessStatus": "FinancialLocked",
                "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****",
                "DirectConnectGatewayName": "dcwg-name"
            }
        ],
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 10
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.DirectConnectGatewayId |You've reached the limit on the number of direct connect gateway IDs that you can describe. |You have reached the maximum number of DC Gateway IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
