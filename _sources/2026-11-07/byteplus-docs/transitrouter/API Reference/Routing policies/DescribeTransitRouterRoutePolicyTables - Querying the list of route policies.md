---
title: "DescribeTransitRouterRoutePolicyTables - Querying the list of route policies"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables"
---

Call the DescribeTransitRouterRoutePolicyTables API to query route policies that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRoutePolicyTables&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|7ezsSr">必选</span> `Example: DescribeTransitRouterRoutePolicyTables`

The interface name. The current API name is `DescribeTransitRouterRoutePolicyTables`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|L4ubfJ">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** <span data-label="purple"> Integer </span>`Optional` `Example: 1`

The page number of the list. Default: 1.



**TransitRouterId ** <span data-label="purple"> String </span><span data-api-tag="require|z-bFBO">必选</span> `Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**TransitRouterRoutePolicyTableName ** <span data-label="purple"> String </span>`Optional` `Example: tr-routepolicy-for-rtb1`

The name of the route policy.



**TransitRouterRoutePolicyTableIds.N ** <span data-label="purple"> String </span>`Optional` `Example value: tr-rpt-hy13n2l4c6c0v****`

The ID of the route policy.


* N represents the serial number of the route policy, ranging from 1 to 100.

* Separate multiple TR route policy IDs with ampersands (&).



**Direction ** <span data-label="purple"> String </span>`optional` `example value: In`

The direction of the route policy. Values:


* In: Inbound. The direction that TR receives routes from a network instance only if they meet the route policy.

* Out: Outbound. The direction that TR synchronizes routes to a network instance only if they meet the route policy.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple"> Integer  </span>`Example value: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple"> Integer </span>`Example value: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer </span>`Example value: 1`

The total number of qualified route policies.



**TransitRouterRoutePolicyTables ** <span data-label="purple"> Object[]  </span>`Example value: --`

The details of qualified route policies.


**TransitRouterRoutePolicyTableId ** <span data-label="purple"> String  </span>`Example value: tr-fpt-hy13n2l4c6c0v****`

The ID of the route policy.



**TransitRouterRoutePolicyTableName ** <span data-label="purple"> String </span>`Example value: tr-routepolicy-for-rtb1`

The name of the route policy.



**TransitRouterId ** <span data-label="purple"> String </span>`Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance to which the route policy belongs.



**Description ** <span data-label="purple"> String </span>`Example: This route table is used for tests.`

The description of the route policy.



**Status ** <span data-label="purple"> String  </span>`Example value: Available`

The status of the route policy.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Direction ** <span data-label="purple"> String  </span>`Example: In`

The direction of the route policy.



**CreationTime ** <span data-label="purple"> String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the route policy is created.



**UpdateTime ** <span data-label="purple"> String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the route policy is last modified.



**TransitRouterRouteTableIds ** <span data-label="purple"> String[] </span>`example value: tr-rtb-hy13n2l4c6c0v****`

The ID of the TR route table to which the route policy is attached.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterRoutePolicyTables&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T033520Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202508151135240071130872368610BA",
    "Action": "DescribeTransitRouterRoutePolicyTables",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 1,
    "TransitRouterRoutePolicyTables": [
      {
        "TransitRouterRoutePolicyTableId": "tr-fpt-hy13n2l4c6c0v****",
        "TransitRouterRoutePolicyTableName": "tr-routepolicy-for-rtb1",
        "TransitRouterId": "tr-7qthudw0ll6jmc****",
        "Description": "This route table is used for tests.",
        "Status": "Available",
        "Direction": "In",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "TransitRouterRouteTableIds": [
          "tr-rtb-hy13n2l4c6c0v****"
        ]
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
