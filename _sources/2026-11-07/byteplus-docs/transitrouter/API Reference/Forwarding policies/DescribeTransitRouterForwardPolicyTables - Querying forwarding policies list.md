---
title: "DescribeTransitRouterForwardPolicyTables - Querying forwarding policies list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables"
---

Call the DescribeTransitRouterForwardPolicyTables interface to query forwarding policies that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterForwardPolicyTables&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String ` example value: `DescribeTransitRouterForwardPolicyTables`

Interface name. The current API name is `DescribeTransitRouterForwardPolicyTables`.



**Version ** `String ` example value: `2020-04-01`

API version. The current API version is `2020-04-01`.



**PageSize ** `Integer optional` example value: `20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** `Integer optional` example: `1`

Pagination page number.



**TransitRouterForwardPolicyTableIds.N ** `String optional` example value: `tr-fpt-hy13n2l4c6c0v****`

ID of the forwarding policy.


* N: represents the serial number of the forwarding policy, ranging from 1 to 100.

* Multiple forwarding policy IDs are separated by “&”.



**TransitRouterForwardPolicyTableName ** `String optional` example value: `fpt-02`

Name of the forwarding policy.



**TransitRouterId ** `String ` example value: `tr-1i5i8khf9m58gae5kcx6****`

The ID of the TR instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the TR instance ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** `Integer optional` example value: `1`

The current page number.



**PageSize ** `Integer optional` example value: `20`

Number of entries per page in the current pagination.



**TotalCount ** `Integer optional` example value: `2`

The total number of matching TR route tables.



**TransitRouterForwardPolicyTables** `Object[] optional` example value: `--`

Detailed information of forwarding policies that meet the conditions.


**CreationTime ** `String optional` example value: `2021-04-09T08:36:47+08:00`

Date created for the forwarding policy.



**Status ** `String optional` example: `Available`

Status of the forwarding policy.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**TransitRouterForwardPolicyTableId ** `String optional` example value: `tr-fpt-hy13n2l4c6c0v****`

Forwarding policy ID.



**TransitRouterForwardPolicyTableName ** `String optional` example value: `forwardpolicy-1`

Name of the forwarding policy.



**UpdateTime** `String optional` example value: `2021-04-10T09:18:28+08:00`

The latest operation time of the forwarding policy.



**Description ** `String optional` example value: `This route table is used for test.`

Description of the forwarding policy.




<span id="jfwhMTXk"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterForwardPolicyTables&Version=2020-04-01&TransitRouterId=tr-1i5i8khf9m58gae5kcx6**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034225Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="tDNSOrEP"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202508151142290301990370033D7C98",
    "Action": "DescribeTransitRouterForwardPolicyTables",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 20,
    "TotalCount": 2,
    "TransitRouterForwardPolicyTables": [
      {
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "Status": "Available",
        "TransitRouterForwardPolicyTableId": "tr-fpt-hy13n2l4c6c0v****",
        "TransitRouterForwardPolicyTableName": "forwardpolicy-1",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "Description": "This route table is used for test."
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
