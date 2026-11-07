---
title: "DescribeTransitRouterBandwidthPackages - Querying the list of TR bandwidth packages"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterBandwidthPackages"
---

Call DescribeTransitRouterBandwidthPackages to query Transit Router (TR) bandwidth packages that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterBandwidthPackages&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|a7KwRn">必选</span> `Example: DescribeTransitRouterBandwidthPackages`

The interface name. The current API name is `DescribeTransitRouterBandwidthPackages`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|WQR1Vf">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterBandwidthPackageIds.N** <span data-label="purple">String</span> <span data-api-tag="require|8CLcPD">必选</span> `Example: tr-bp-qw2u6ur8lhe2t****`

The ID of the Transit Router (TR) bandwidth package.


* N represents the sequence number of a TR bandwidth package, ranging from 1 to 100.

* Separate TR bandwidth package IDs with ampersands (&).



**LocalGeographicRegionSetId** <span data-label="purple">String</span> <span data-api-tag="require|L4Rg7u">必选</span> `Example: China`

Local Geographic Region ID for TR bandwidth package interconnection. Values:


* China: Mainland China.

* Asia: Asia Pacific.



**PeerGeographicRegionSetId** <span data-label="purple">String</span> <span data-api-tag="require|YCFlVN">必选</span> `Example: China`

Peer Geographic Region ID for TR bandwidth package interconnection. Values:


* China: Mainland China.

* Asia: Asia Pacific.



**TransitRouterPeerAttachmentId** <span data-label="purple">String</span> <span data-api-tag="require|aOmVeN">必选</span> `Example: tr-attach-12w7hruhlhlrd****`

The ID of the inter\-region attachment.



**TransitRouterBandwidthPackageName** <span data-label="purple">String</span> <span data-api-tag="require|l6dGzt">必选</span> `Example: trbp-test`

The name of the TR bandwidth package.



**PageNumber** <span data-label="purple">Integer</span> <span data-api-tag="require|LCn7EX">必选</span> `Example: 1`

The page number of the list. Default: 1.



**PageSize** <span data-label="purple">Integer</span> <span data-api-tag="require|77Y874">必选</span> `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**ProjectName** <span data-label="purple">String</span> <span data-api-tag="require|yxDCWF">必选</span> `Example: default`

The name of the project to which the TR bandwidth package belongs.



**TagFilters.N.Key** <span data-label="purple">String</span> <span data-api-tag="require|naHhBL">必选</span> `Example: k1`

The tag key of the tag for the TR bandwidth package.


* N represents the sequence number of a tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the inter\-region attachments that contain all specified tag keys.



**TagFilters.N.Values.N** <span data-label="purple">String</span> <span data-api-tag="require|coGsp7">必选</span> `Example: v1`

The tag value of the tag for the TR bandwidth package.


* The first N represents the sequence number of a tag key, ranging from 1 to 10.

* The second N represents the sequence number of a tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).

* To provide this parameter, you must first provide TagFilters.N.Key.

* When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple"> Integer  </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple"> Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 2`

The total number of qualified TR bandwidth packages.



**TransitRouterBandwidthPackages ** <span data-label="purple"> Object[]  </span>`Example: -`

The details of qualified TR bandwidth packages.


**Line Operator ** <span data-label="purple"> String </span>`Example: ChinaUnicom`

The provider of the cross\-border bandwidth package.



**Tags ** <span data-label="purple"> Object[]  </span>`Example: -`

The information of the tag for the TR bandwidth package.


**Key ** <span data-label="purple"> String  </span>`Example: k1`

The tag key of the tag.



**Value ** <span data-label="purple"> String  </span>`Example: v1`

The tag value.




**ProjectName ** <span data-label="purple"> String  </span>`Example: default`

The name of the project to which the TR bandwidth package belongs.



**TransitRouterBandwidthPackageId ** <span data-label="purple"> String  </span>`Example: tr-bp-qw2u6ur8lhe2t****`

The ID of the TR bandwidth package.



**TransitRouterBandwidthPackageName ** <span data-label="purple"> String  </span>`Example: trbp-01`

The name of the TR bandwidth package.



**Description ** <span data-label="purple"> String  </span>`Example: This package is used for test.`

The description of the TR bandwidth package.



**LocalGeographicRegionSetId ** <span data-label="purple"> String </span>`Example: China`

Local Geographic Region ID for TR bandwidth package interconnection.


* China: Mainland China.

* Asia: Asia Pacific.



**PeerGeographicRegionSetId ** <span data-label="purple"> String  </span>`Example: China`

Peer Geographic Region ID for TR bandwidth package interconnection.


* China: Mainland China.

* Asia: Asia Pacific.



**Bandwidth ** <span data-label="purple"> Integer </span>`Example: 2`

The peak bandwidth of the TR bandwidth package, measured in Mbps.



**RemainingBandwidth ** <span data-label="purple"> Integer  </span>`Example: 2`

The remaining unallocated bandwidth of the TR bandwidth package, measured in Mbps.



**Status ** <span data-label="purple"> String </span>`Example: Available`

The status of the TR bandwidth package.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**CreationTime ** <span data-label="purple"> String  </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the TR bandwidth package is created.



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the TR bandwidth package is last operated.



**BusinessStatus ** <span data-label="purple"> String  </span>`Example: Normal`

The service status of the TR bandwidth package.


* Normal

* FinancialLocked: Locked.



**BillingType ** <span data-label="purple"> Integer  </span>`Example: 1`

The metering method for the TR bandwidth package. 1: Subscription.



**DeletedTime ** <span data-label="purple"> String </span>`Example: 2021-05-07 23:23:23`

The time when the TR bandwidth package is deleted.



**ExpiredTime ** <span data-label="purple"> String </span>`Example: 2021-05-07 23:23:23`

The time when the TR bandwidth package expires.



**Allocations ** <span data-label="purple"> Object[]  </span>`Example: -`

The details of the inter\-region attachment associated with the bandwidth package.


**TransitRouterPeerAttachmentId ** <span data-label="purple"> String </span>`Example: tr-attach-12w7hruhlhlrd****`

The ID of the inter\-region attachment.



**AllocateTime ** <span data-label="purple"> String  </span>`Example: 2021-05-07 23:23:23`

The time when the bandwidth package is attached to the inter\-region attachment.



**LocalRegionId ** <span data-label="purple"> String  </span>`Example: cn-beijing`

The ID of the region where the local TR instance associated with the inter\-region attachment resides.



**PeerRegionId ** <span data-label="purple"> String  </span>`Example: cn-guangzhou`

The ID of the region where the peer TR instance associated with the inter\-region attachment resides.



**Bandwidth ** <span data-label="purple"> Integer </span>`Example: 2`

The peak bandwidth of the inter\-region attachment, measured in Mbps.




**AccountId ** <span data-label="purple"> String </span>`Example: 200000****`

The ID of the account that owns the TR bandwidth package.



**ExpectedExpireShutdownTime ** <span data-label="purple"> String </span>`Example: 2024-06-05T23:59:59+08:00`

The time when the TR bandwidth package is suspended due to expiration.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterBandwidthPackages&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T035011Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250804115016027122160094F26862",
    "Action": "DescribeTransitRouterBandwidthPackages",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 20,
    "TotalCount": 2,
    "TransitRouterBandwidthPackages": [
      {
        "LineOperator": "ChinaUnicom",
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          }
        ],
        "ProjectName": "default",
        "TransitRouterBandwidthPackageId": "tr-bp-qw2u6ur8lhe2t****",
        "TransitRouterBandwidthPackageName": "trbp-01",
        "Description": "This package is used for test.",
        "LocalGeographicRegionSetId": "China",
        "PeerGeographicRegionSetId": "China",
        "Bandwidth": 2,
        "RemainingBandwidth": 2,
        "Status": "Available",
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "BusinessStatus": "Normal",
        "BillingType": 1,
        "DeletedTime": "2021-05-07 23:23:23",
        "ExpiredTime": "2021-05-07 23:23:23",
        "Allocations": [
          {
            "TransitRouterPeerAttachmentId": "tr-attach-12w7hruhlhlrd****",
            "AllocateTime": "2021-05-07 23:23:23",
            "LocalRegionId": "cn-beijing",
            "PeerRegionId": "cn-guangzhou",
            "Bandwidth": 2
          }
        ],
        "AccountId": "200000****"
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
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag key for filtering is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag value for filtering is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |You have reached the maximum number of instances that you can query in a single request. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
