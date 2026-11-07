---
title: "DescribeTransitRouterMulticastDomains - Querying the list of multicast domains"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterMulticastDomains"
---

Call the DescribeTransitRouterMulticastDomains API to query the list of multicast domains that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterMulticastDomains&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|gR18GP">必选</span> `Example value: DescribeTransitRouterMulticastDomains`

The interface name. The current API name is `DescribeTransitRouterMulticastDomains`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|GLtPP1">必选</span> `Example value: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple"> String  </span><span data-api-tag="require|ZlNAVj">必选</span> `Example value: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**TransitRouterMulticastDomainName ** <span data-label="purple">String </span>`optional` `example value: tr-multicast-name`

The name of the multicast domain.


* Must start with a letter, number, or Chinese character. May include letters, numbers, Chinese characters, and the following symbols: periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, it defaults to the ID of the multicast domain.



**TagFilters.N.Key ** <span data-label="purple"> String  </span>`Optional` `Example value: k1`

The tag key of the tag.


* N represents the serial number of the tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* If multiple tag keys are specified, this action queries the multicast domain associated with all the specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple"> String  </span>`Optional` `Example: v1`

The tag value.


* The first N represents the serial number of the tag key, ranging from 1 to 10.

* The second N represents the serial number of the tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">To provide this parameter, you must first provide TagFilters.N.Key.</div>


* <div data-tips="true" data-tips-type="default">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




**PageNumber ** <span data-label="purple"> Integer </span>`Optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Example value: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterMulticastDomainIds.N ** <span data-label="purple">String </span>`optional` `example value: tr-md-hy13n2l4c6c0v****`

ID list of the transit router multicast domain.


* N: indicates the serial number of the multicast domain, ranging from 1 to 100.

* Use `&` to separate multiple multicast domain IDs.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TransitRouterMulticastDomains ** <span data-label="purple"> Object[]  </span>`Example value: -`

Details of qualified multicast domains.


**CreationTime ** <span data-label="purple"> String </span>`Example value: 2021-04-09T08:36:47+08:00`

The time when the multicast domain is created.



**Description ** <span data-label="purple"> String </span>`Example value: description`

Description of the multicast domain.



**UpdateTime ** <span data-label="purple"> String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the multicast domain is last modified.



**TransitRouterMulticastDomainName ** <span data-label="purple"> String  </span>`Example: name`

The name of the multicast domain.



**TransitRouterMulticastDomainId ** <span data-label="purple"> String  </span>`Example value: tr-md-hy13n2l4c6c0v****`

The ID of the multicast domain.



**Status ** <span data-label="purple"> String  </span>`Example value: Available`

Status of the multicast domain.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Tags ** <span data-label="purple"> Object[]  </span>`Example value: -`

The tag information of the multicast domain.


**Key ** <span data-label="purple"> String </span>`Example: k1`

The tag key of the tag.



**Value ** <span data-label="purple"> String </span>`Example value: v1`

The tag value.





**PageSize ** <span data-label="purple"> Integer  </span>`Example value: 20`

Number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple"> Integer  </span>`Example value: 1`

The current page number.



**TotalCount ** <span data-label="purple"> Integer  </span>`Example value: 1`

Total number of multicast domains that meet the condition.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterMulticastDomains&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250721T122038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250721/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20250721202048196216228017B62AE2",
    "Action": "DescribeTransitRouterMulticastDomains",
    "Version": "2020-04-01",
    "Service": "transitrouter",
    "Region": "cn-beijing"
  },
  "Result": {
    "TransitRouterMulticastDomains": {
      "CreationTime": "2021-04-09T08:36:47+08:00",
      "Description": "description",
      "UpdateTime": "2021-04-10T09:18:28+08:00",
      "TransitRouterMulticastDomainName": "name",
      "TransitRouterMulticastDomainId": "tr-md-hy13n2l4c6c0v****",
      "Status": "Available",
      "Tags": [
        {
          "Key": "k1",
          "Value": "v1"
        }
      ]
    },
    "PageSize": 20,
    "PageNumber": 1,
    "TotalCount": 1
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
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
