---
title: "DescribeTransitRouterRoutePolicyEntries - Querying the list of route policy entries"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyEntries"
---

Call the DescribeTransitRouterRoutePolicyEntries API to query route policy entries that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRoutePolicyEntries&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|8b8LMu">必选</span> `Example: DescribeTransitRouterRoutePolicyEntries`

The interface name. The current API name is `DescribeTransitRouterRoutePolicyEntries`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|GpBMN5">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**TransitRouterRoutePolicyTableId ** <span data-label="purple">String </span><span data-api-tag="require|z85FFb">必选</span> `Example: tr-rpt-hy13n2l4c6c0v****`

ID of the route policy. You can call the [DescribeTransitRouterRoutePolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRoutePolicyTables) API to obtain the ID of the route policy.



**TransitRouterRoutePolicyEntryIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-rpe-13f1fdx5l****`

The ID of the policy entry.



**Direction ** <span data-label="purple">String </span>`optional` `Example: In`

The direction of the route policy. Values:


* In: Inbound. The direction that the TR learns routes from network instances. It only accepts routes that match the route policies.

* Out: Outbound. The direction that the TR synchronizes routes to network instances. It only sends routes that match the route policies.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 1`

Total number of qualified route policy entries.



**TransitRouterRoutePolicyEntries ** <span data-label="purple">Object[] </span>`Example: --`

The details of qualified route policy entries.


**IpPrefixMatchMode ** <span data-label="purple">String </span>`Example: Complete`

The match mode of the route prefix.


* Include: Inclusion match. When the route prefix in the match condition contains the route prefix of the matched route, it is considered a successful match. For example: A policy entry with a route prefix of 10.10.0.0/16 can fuzzily match a route with a destination CIDR of 10.10.1.0/24.

* Complete: Exact match. A match is only considered successful if the route prefix specified in the condition is identical to the prefix of the target route.​ For Example: A policy entry with a route prefix of 10.10.0.0/16 can only exactly match a route with a destination CIDR of 10.10.0.0/16.



**TransitRouterRoutePolicyTableId ** <span data-label="purple">String </span>`Example: tr-rpt-hy13n2l4c6c0v****`

The ID of the route policy.



**TransitRouterRoutePolicyEntryId ** <span data-label="purple">String </span>`Example: tr-rpe-13f1fdx5l****`

The ID of the policy entry.



**Description ** <span data-label="purple">String </span>`Example: for test`

The description of the route policy entry.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the route policy entry.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Priority ** <span data-label="purple">Integer </span>`Example: 100`

The priority of the route policy. A lower value indicates a higher precedence.



**IpPrefixes ** <span data-label="purple">String[] </span>`Example: 192.168.XX.XX/24`

The route prefix of the route policy entry.



**SourceResourceTypes ** <span data-label="purple">String[] </span>`Example: VPC`

The source instance type of the route policy entry.


* VPC: Virtual Private Cloud.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Inter\-region Transit Router.



**SourceResourceIds ** <span data-label="purple">String[] </span>`Example: vpc-bp1aevy8sofi8mh1****`

The source instance ID of the route policy entry.



**DestinationResourceTypes ** <span data-label="purple">String[] </span>`Example: VPC`

The destination instance type of the route policy entry.


* VPC: Virtual Private Cloud.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Inter\-region Transit Router.



**DestinationResourceIds ** <span data-label="purple">String[] </span>`Example: vpc-bp1aevy8sofi8mh1****`

The destination instance ID of the route policy entry.



**ActionResult ** <span data-label="purple">String </span>`Example: Permit`

The policy action of the route policy entry.


* Permit. It means allowing the routes that match the route policy to pass.

* Deny. It means rejecting the routes that match the route policy entry from passing.



**AsPathOperateMode ** <span data-label="purple">String </span>`Example: Additive`

The AsPath setting method for the route policy entry.


* Additive: Append As Path. This means adding the specified AsPath to the front of the AsPath of routes allowed to pass.

* Replace: Replace As Path. This means replacing the AsPath of routes allowed to pass with the specified AsPath.



**ApplyAsPathValues ** <span data-label="purple">Integer[] </span>`Example: 65001`

The AsPath of the route policy entry.



**CreationTime ** <span data-label="purple">String </span>`Example: 2023-08-14T18:05:17+08:00`

The time when the route policy entry is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2023-08-14T18:05:17+08:00`

The time when the route policy entry is updated.



**PrefixListId ** <span data-label="purple">String </span>`Example: pl-1234567890abcdef0`

The prefix list ID associated with the route policy entry.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterRoutePolicyEntries&Version=2020-04-01&TransitRouterRoutePolicyTableId=tr-rpt-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250815T033712Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250815/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterRoutePolicyEntries",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "TransitRouterRoutePolicyEntries": [
            {
                "IpPrefixMatchMode": "Complete",
                "TransitRouterRoutePolicyTableId": "tr-rpt-hy13n2l4c6c0v****",
                "TransitRouterRoutePolicyEntryId": "tr-rpe-13f1fdx5l****",
                "Description": "for test",
                "Status": "Available",
                "Priority": 100,
                "IpPrefixes": [
                    "192.168.XX.XX/24"
                ],
                "SourceResourceTypes": [
                    "VPC"
                ],
                "SourceResourceIds": [
                    "vpc-bp1aevy8sofi8mh1****"
                ],
                "DestinationResourceTypes": [
                    "VPC"
                ],
                "DestinationResourceIds": [
                    "vpc-bp1aevy8sofi8mh1****"
                ],
                "ActionResult": "Permit",
                "AsPathOperateMode": "Additive",
                "ApplyAsPathValues": [
                    65001
                ],
                "CreationTime": "2023-08-14T18:05:17+08:00",
                "UpdateTime": "2023-08-14T18:05:17+08:00"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |This request contains an invalid or unsupported parameter. The maximum number of resource query results is 100. |
