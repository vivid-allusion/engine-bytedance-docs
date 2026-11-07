---
title: "DescribeTransitRouterTrafficQosQueuePolicies - Querying traffic queue policies list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueuePolicies"
---

Call the DescribeTransitRouterTrafficQosQueuePolicies API to query traffic queue policies that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterTrafficQosQueuePolicies&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String ` example value: `DescribeTransitRouterTrafficQosQueuePolicies`

Interface name. The current API name is `DescribeTransitRouterTrafficQosQueuePolicies`.



**Version ** `String ` Example: `2020-04-01`

API version. The current API version is `2020-04-01`.



**PageSize ** `Integer optional` example value: `20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** `Integer optional` Example: `1`

Page number of the list. Default: 1.



**TransitRouterTrafficQosQueuePolicyIds.N ** `String optional` example value: `tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy.


* N: indicates the index of the traffic queue policy, ranging from 1 to 100.

* Use "&" to separate multiple traffic queue policy IDs.



**TransitRouterTrafficQosQueuePolicyName** `String optional` example value: `tmp-02`

Name of the traffic queue policy.



**TransitRouterId ** `String ` example value: `tr-7qthudw0ll6jmc****`

The ID of the TR instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the TR instance ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameter

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterTrafficQosQueuePolicies** `Object[] optional` example value: `--`

Details of matching traffic queue policies.


**TransitRouterTrafficQosQueuePolicyName ** `String optional` example value: `trafficqosqueuepolicy-1`

Name of the traffic queue policy.



**TransitRouterTrafficQosQueuePolicyId ** `String optional` example value: `tr-tqp-hy13n2l4c6c0v****`

ID of the traffic queue policy.



**Status ** `String optional` Example value: `Available`

Status of the traffic queue policy.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**UpdateTime** `String optional` example value: `2021-04-10T09:18:28+08:00`

Last update time of the traffic queue policy.



**Description ** `String optional` Example: `description`

Description of the traffic queue policy.



**CreationTime ** `String optional` example value: `2021-04-09T08:36:47+08:00`

Created on time of the traffic queue policy.




**PageSize ** `Integer optional` Example: `20`

Number of entries per page in the current pagination.



**PageNumber ** `Integer optional` example value: `1`

The current page number.



**TotalCount ** `Integer optional` example value: `2`

Total number of matching traffic queue policies.



<span id="xUu6StqZ"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterTrafficQosQueuePolicies&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T040442Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="uFPG756s"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815120446229012112150BF907C",
    "Action": "DescribeTransitRouterTrafficQosQueuePolicies",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterTrafficQosQueuePolicies": [
      {
        "TransitRouterTrafficQosQueuePolicyName": "trafficqosqueuepolicy-1",
        "TransitRouterTrafficQosQueuePolicyId": "tr-tqp-hy13n2l4c6c0v****",
        "Status": "Available",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "Description": "description",
        "CreationTime": "2021-04-09T08:36:47+08:00"
      }
    ],
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 2
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
