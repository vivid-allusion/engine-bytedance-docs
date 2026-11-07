---
title: "DescribeTransitRouterLocalPeerAttachments - Querying the list of local peer attachments."
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterLocalPeerAttachments"
---

Call DescribeTransitRouterLocalPeerAttachments to query local peer attachments that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterLocalPeerAttachments&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|emTsyT">必选</span> `Example: DescribeTransitRouterLocalPeerAttachments`

The interface name. The current API name is `DescribeTransitRouterLocalPeerAttachments`.



**Version ** <span data-label="purple"> String </span><span data-api-tag="require|obhM7m">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple"> String  </span>`optional` `Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**TransitRouterAttachmentName ** <span data-label="purple"> String  </span>`optional` `Example: attachment-01`

The name of the local peer attachment.



**TransitRouterAttachmentIds.N ** <span data-label="purple"> String  </span>`optional` `Example: tr-attach-7qthudw0ll6jmc****`

The ID of the local peer attachment


* N represents the sequence number of a local peer attachment, ranging from 1 to 100.

* Separate multiple local peer attachment IDs with ampersands (&).



**PeerTransitRouterId ** <span data-label="purple"> String </span>`optional` `Example: tr-q3wuhuumlho9r****`

The ID of the peer TR instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the ID of the TR instance.



**TagFilters.N.Key ** <span data-label="purple"> String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the local peer attachments that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">string </span>`optional` `Example: v1`

The tag value.


* The first N represents the sequence number of a tag key, ranging from 1 to 10.

* The second N represents the sequence number of a tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).

* To provide this parameter, you must first provide TagFilters.N.Key.

* When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.



**PageNumber ** <span data-label="purple"> Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer  </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple"> Integer  </span>`Example: 1`

Pagination page number.



**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

The number of entries per page in a pagination query.



**TotalCount ** <span data-label="purple"> Integer </span>`Example: 2`

The total number of local peer attachments matching the specified conditions.



**TransitRouterAttachments ** <span data-label="purple"> Object[]  </span>`Example: -`

The details of the local peer attachment.


**Tags ** <span data-label="purple"> Object[]  </span>`Example: --`

Tag information of the local peer attachment.


**Key ** <span data-label="purple"> String  </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple"> String </span>`Example: v1`

The tag value.




**Status ** <span data-label="purple"> String  </span>`Example: Available`

The status of the local peer attachment.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Bandwidth ** <span data-label="purple"> Integer </span>`Example: 10`

The bandwidth of the local peer attachment, measured in Mbps.

The maximum bandwidth must not exceed the remaining unallocated bandwidth of the specified TR bandwidth package.



**UpdateTime ** <span data-label="purple"> String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the local peer attachment is last updated.



**Description ** <span data-label="purple"> String  </span>`Example: This is a sample description`

The description of the local peer attachment.



**Ipv6Enabled ** <span data-label="purple"> Boolean  </span>`Example: false`

Describe whether to enable IPv6.


* true: Yes.

* false: No.



**CreationTime ** <span data-label="purple"> String  </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the local peer attachment is created.



**TransitRouterId ** <span data-label="purple"> String  </span>`Example: tr-7qthudw0ll6jmc****`

The ID of the local TR instance.



**PeerTransitRouterId ** <span data-label="purple"> String </span>`Example: tr-3tehy13n2l4c6c0v****`

The ID of the peer TR instance.



**AutoPublishRouteEnabled ** <span data-label="purple"> Boolean </span>`Example: false`

Describe whether to automatically publish routes to the peer TR.


* `true`: Auto publish.

* `false`: Not auto publish.



**PeerTransitRouterOwnerId ** <span data-label="purple"> String  </span>`Example: 20122202249`

The ID of the account that owns the peer TR instance.



**TransitRouterAttachmentId ** <span data-label="purple"> String  </span>`Example: tr-attach-13n2l4c6c0v****`

Local peer attachment ID of the local TR instance.



**TransitRouterRouteTableId ** <span data-label="purple"> String  </span>`Example: tr-rtb-3tehy13n2l4c6c0v****`

The ID of the TR route table associated with forwarding.



**TransitRouterAttachmentName ** <span data-label="purple"> String  </span>`Example: abc`

The name of the local peer attachment.



**PeerTransitRouterAttachmentId ** <span data-label="purple"> String </span>`Example: tr-attach-zy249****`

Local peer attachment ID of the peer TR instance.



**TransitRouterForwardPolicyTableId ** <span data-label="purple"> String  </span>`Example: tr-fpt-2z6bymo5r1af4805s5cy7****`

The ID of the forwarding policy associated with the local TR.




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeTransitRouterLocalPeerAttachments&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc****&TransitRouterAttachmentName=attachment-01&TransitRouterAttachmentIds.N=tr-attach-7qthudw0ll6jmc****&PeerTransitRouterId=tr-q3wuhuumlho9r****&TagFilters.N.Key=k1&TagFilters.N.Values.N=v1&PageNumber=1&PageSize=20 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterLocalPeerAttachments",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 2,
        "TransitRouterAttachments": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Status": "Available",
                "Bandwidth": 10,
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "Description": "This is a sample description",
                "Ipv6Enabled": true,
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "TransitRouterId": "tr-7qthudw0ll6jmc****",
                "PeerTransitRouterId": "tr-3tehy13n2l4c6c0v****",
                "AutoPublishRouteEnabled": true,
                "PeerTransitRouterOwnerId": "20122202249",
                "TransitRouterAttachmentId": "tr-attach-13n2l4c6c0v****",
                "TransitRouterRouteTableId": "tr-rtb-3tehy13n2l4c6c0v****",
                "TransitRouterAttachmentName": "abc",
                "PeerTransitRouterAttachmentId": "tr-attach-zy249****",
                "TransitRouterForwardPolicyTableId": "tr-fpt-2z6bymo5r1af4805s5cy7****"
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
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
