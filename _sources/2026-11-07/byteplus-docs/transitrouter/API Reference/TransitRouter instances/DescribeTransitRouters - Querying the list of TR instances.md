---
title: "DescribeTransitRouters - Querying the list of TR instances"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters"
---

Call DescribeTransitRouters to query Transit Router (TR) instances that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouters&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|RKyMx2">必选</span> `Example: DescribeTransitRouters`

The interface name. The current API name is `DescribeTransitRouters`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|kF8j7u">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterName ** <span data-label="purple">String </span>`optional` `Example: transitrouter-01`

The name of the TR instance.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

The name of the project to which the TR instance belongs.



**TransitRouterIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.


* N represents the sequence number of a TR bandwidth package, ranging from 1 to 100.

* Separate multiple TR instance IDs with ampersands (&).



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key of the TR instance.


* N represents the sequence number of a tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the TR instances that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value of the TR instance.


* The first N represents the sequence number of a tag key, ranging from 1 to 10.

* The second N represents the sequence number of a tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).

* To provide this parameter, you must first provide TagFilters.N.Key.

* When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of qualified TR instances.



**TransitRouters ** <span data-label="purple">Object[] </span>`Example: --`

The details of qualified TR instances.


**AccountId ** <span data-label="purple">String </span>`Example: 200000****`

The ID of the account to which the TR instance belongs.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the TR instance is created.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-05-22 00:00:00`

The time when the TR instance is deleted.



**Description ** <span data-label="purple">String </span>`Example: This transit router is used for test.`

The description of the TR instance.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when the TR instance is suspended due to overdue payments.



**TransitRouterName ** <span data-label="purple">String </span>`Example: transitrouter-01`

The name of the TR instance.



**TransitRouterId ** <span data-label="purple">String </span>`Example: tr-3tehy13n2l4c6c0v****`

The ID of the TR instance.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the TR instance is last modified.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

The operational status of the TR instance.


* Normal

* FinancialLocked: Locked.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the TR instance.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**GrantStatus ** <span data-label="purple">String </span>`Example: Initial`

The status of the sharing rule.


* Accepted

* Initial: Pending acceptance.



**Asn ** <span data-label="purple">Integer </span>`Example: 64512`

The TR ASN.



**MulticastEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether to enable multicast.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the TR instance belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: --`

The tag information of the TR instance.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**GrantSourceType ** <span data-label="purple">String </span>`Example: rs`

The sharing method of the TR instance.


* rs: Shared via platform resource sharing​

* tr: Shared via TR instance sharing



**BillingOwnerType ** <span data-label="purple">String </span>`Example: ResourceOwner`

The payer account for the network instance attachment.


* `TransitRouterOwner`: The network instance attachment fee is charged to the account that owns the TR instance.

* `ResourceOwner`: The network instance attachment fee is charged to the account that owns the network instance.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouters&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033418Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouters",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 2,
        "TransitRouters": [
            {
                "Asn": 64512,
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Available",
                "AccountId": "200000****",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "DeletedTime": "2021-05-22 00:00:00",
                "Description": "This transit router is used for test.",
                "GrantStatus": "Initial",
                "OverdueTime": "2021-05-07 23:23:23",
                "ProjectName": "default",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "BusinessStatus": "Normal",
                "GrantSourceType": "rs",
                "TransitRouterId": "tr-3tehy13n2l4c6c0v****",
                "BillingOwnerType": "ResourceOwner",
                "MulticastEnabled": true,
                "TransitRouterName": "transitrouter-01"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
