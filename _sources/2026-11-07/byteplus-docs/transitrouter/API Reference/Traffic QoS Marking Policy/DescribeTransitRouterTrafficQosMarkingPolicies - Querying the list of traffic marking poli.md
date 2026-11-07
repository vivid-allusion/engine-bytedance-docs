---
title: "DescribeTransitRouterTrafficQosMarkingPolicies - Querying the list of traffic marking policies"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies"
---

Call the DescribeTransitRouterTrafficQosMarkingPolicies API to query traffic marking policies that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterTrafficQosMarkingPolicies&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|r399Bu">必选</span> `Example: DescribeTransitRouterTrafficQosMarkingPolicies`

The interface name. The current API name is `DescribeTransitRouterTrafficQosMarkingPolicies`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|yl_FJm">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageSize ** <span data-label="purple"> Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** <span data-label="purple"> Integer </span>`Optional` `Example value: 1`

The page number of the list. Default: 1.



**TransitRouterTrafficQosMarkingPolicyIds.N ** <span data-label="purple"> String  </span>`Optional` `Example value: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy.


* N represents the serial number of the traffic marking policy, ranging from 1 to 100.

* Separate multiple traffic marking policy IDs with ampersands (&).



**TransitRouterTrafficQosMarkingPolicyName ** <span data-label="purple"> String </span>`Optional` `Example: tmp-02`

The name of the traffic marking policy.



**TransitRouterId ** <span data-label="purple"> String </span><span data-api-tag="require|SRLwsA">必选</span> `Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterTrafficQosMarkingPolicies ** <span data-label="purple"> Object[]  </span>`Example value: --`

The details of the qualified traffic marking policies.


**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple"> String </span>`Example value: tr-tmp-hy13n2l4c6c0v****`

ID of the traffic marking policy.



**TransitRouterTrafficQosMarkingPolicyName ** <span data-label="purple"> String </span>`Example value: trafficqosmarkingpolicy-1`

The name of the traffic marking policy.



**UpdateTime ** <span data-label="purple"> String </span>`Example value: 2021-04-10T09:18:28+08:00`

The time when the traffic marking policy is recently updated.



**Description ** <span data-label="purple"> String </span>`Example value: description`

The description of the traffic marking policy.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the traffic marking policy is created.



**Status** <span data-label="purple">String</span> `Example: Available`

The status of the traffic marking policy.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available




**PageSize ** <span data-label="purple"> Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple"> Integer </span>`Example value: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer </span>`Example value: 2`

The total number of qualified traffic marking policies.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterTrafficQosMarkingPolicies&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T034705Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250815114708005219151145EA9D7B",
    "Action": "DescribeTransitRouterTrafficQosMarkingPolicies",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterTrafficQosMarkingPolicies": [
      {
        "TransitRouterTrafficQosMarkingPolicyId": "tr-tmp-hy13n2l4c6c0v****",
        "TransitRouterTrafficQosMarkingPolicyName": "trafficqosmarkingpolicy-1",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "Description": "description",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "Status": "Available"
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
