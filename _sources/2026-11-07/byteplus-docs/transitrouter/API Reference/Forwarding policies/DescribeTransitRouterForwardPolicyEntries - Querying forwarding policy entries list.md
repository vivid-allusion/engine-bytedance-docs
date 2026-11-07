---
title: "DescribeTransitRouterForwardPolicyEntries - Querying forwarding policy entries list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyEntries"
---

Call the DescribeTransitRouterForwardPolicyEntries interface to query forwarding policy entries that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterForwardPolicyEntries&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String ` example value: `DescribeTransitRouterForwardPolicyEntries`

Name of the interface. The current API name is `DescribeTransitRouterForwardPolicyEntries`.



**Version ** `String ` Example value: `2020-04-01`

Interface version. The current API version is `2020-04-01`.



**PageNumber ** `Integer optional` example: `1`

Page number of the list. Default: 1.



**PageSize ** `Integer optional` Example: `20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**SourceCidrBlock ** `String optional` example value: `192.168.XX.XX/24`

The source address segment of the forwarding policy entry.



**DestinationCidrBlock ** `String optional` Example: `192.168.XX.XX/24`

The destination address segment of the forwarding policy entry.



**TransitRouterForwardPolicyEntryIds.N ** `String optional` example value: `tr-fpe-1i5i8khf9m58gae5kcx6****`

Forwarding policy entry ID.



**TransitRouterForwardPolicyTableId ** `String ` Example value: `tr-fpt-hy13n2l4c6c0v****`

ID of the forwarding policy. You can call the [DescribeTransitRouterForwardPolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables) interface to get the forwarding policy ID.



**TransitRouterRouteTableId ** `String optional` example: `tr-rtb-hy13n2l4c6c0v****`

Forward route table ID of the forwarding policy entry. You can call [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) to obtain the TR route table ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** `Integer optional` Example: `1`

Pagination page number.



**PageSize ** `Integer optional` example value: `20`

Number of entries per page in the current pagination.



**TotalCount ** `Integer optional` example value: `2`

Total number of forwarding policy entries that meet the conditions.



**TransitRouterForwardPolicyEntries ** `Object[] optional` example: `--`

Details of the forwarding policy entries that meet the conditions.


**Description** `String optional` Example value: `This is a sample description.`

The description of the forwarding policy entry.



**SourceCidrBlock ** `String optional` example value: `192.168.XX.XX/24`

Source address segment of the forwarding policy entry.



**DestinationCidrBlock** `String optional` Example value: `192.168.XX.XX/24`

The destination address segment of the forwarding policy entry.



**Status ** `String optional` example value: `Available`

Status of the forwarding policy entry.


* Available

* Creating

* Pending: ​​Configuration in progress.

* Deleting

* Conflicted: Not effective.



**Priority ** `Integer optional` example: `100`

Priority of the forwarding policy entry.



**TransitRouterRouteTableId ** `String optional` Example value: `tr-rtb-35r03ksl3qpds1vfuib55****`

ID of the forwarding route table.



**CreationTime** `String optional` Example value: `2021-04-09T08:36:47+08:00`

The creation time of the forwarding policy entry.



**UpdateTime ** `String optional` example value: `2021-04-09T08:36:47+08:00`

Recent operating time of the forwarding policy entry.



**TransitRouterForwardPolicyTableId ** `String optional` example: `tr-fpt-hrgyyj6jmty****`

Forwarding policy ID.



**TransitRouterForwardPolicyEntryId ** `String optional` example value: `tr-fpe-12ghy8jkmg****`

Forwarding policy entry ID.




<span id="oKWBOFdI"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterForwardPolicyEntries&Version=2020-04-01&TransitRouterForwardPolicyTableId=tr-fpt-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034430Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="EoLTJWUr"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815114433134063066072934B6C",
    "Action": "DescribeTransitRouterForwardPolicyEntries",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 20,
    "TotalCount": 2,
    "TransitRouterForwardPolicyEntries": [
      {
        "Description": "This is a sample description.\t",
        "SourceCidrBlock": "192.168.XX.XX/24",
        "DestinationCidrBlock": "192.168.XX.XX/24",
        "Status": "Available",
        "Priority": 100,
        "TransitRouterRouteTableId": "tr-rtb-35r03ksl3qpds1vfuib55****",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-09T08:36:47+08:00",
        "TransitRouterForwardPolicyTableId": "tr-fpt-hrgyyj6jmty****",
        "TransitRouterForwardPolicyEntryId": "tr-fpe-12ghy8jkmg****"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Explanation** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
