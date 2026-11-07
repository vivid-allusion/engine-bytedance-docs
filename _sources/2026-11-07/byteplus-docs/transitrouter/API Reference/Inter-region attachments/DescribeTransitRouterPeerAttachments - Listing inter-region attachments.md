---
title: "DescribeTransitRouterPeerAttachments - Listing inter-region attachments"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments"
---

Call DescribeTransitRouterPeerAttachments to query inter\-region attachments that meet the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterPeerAttachments&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|mPd4mD">必选</span>`Example: DescribeTransitRouterPeerAttachments`

The interface name. The current API name is `DescribeTransitRouterPeerAttachments`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|v2Iu36">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**TransitRouterId ** <span data-label="purple">String </span>`optional` `Example: tr-7qthudw0ll6jmc****`

The ID of the local TR instance associated with the inter\-region attachment.



**TransitRouterAttachmentName ** <span data-label="purple">String </span>`optional` `Example: tr-attachment`

The name of the inter\-region attachment.



**TransitRouterAttachmentIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-attach-7qthudw0ll6jmc****`

The ID of the inter\-region attachment.


* N represents the sequence number of an inter\-region attachments, ranging from 1 to 100.

* Separate multiple inter\-region attachment IDs with ampersands (&).



**PeerTransitRouterId ** <span data-label="purple">String </span>`optional` `Example: tr-q3wuhuumlho9r****`

The ID of the peer TR instance. You can call [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) to obtain the ID of the TR instance.



**PeerTransitRouterRegionId ** <span data-label="purple">String </span>`optional` `Example: cn-beijing`

The ID of the region where the peer TR belongs. You can review [Regions](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-05) to get the region ID.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key of the inter\-region attachment.


* N represents the sequence number of a tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the inter\-region attachments that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value of the inter\-region attachment.


* The first N represents the sequence number of a tag key, ranging from 1 to 10.

* The second N represents the sequence number of a tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide TagFilters.N.Key.</div>


* <div data-tips="true" data-tips-type="tip">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of entries per page in the current pagination.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of inter\-region attachments matching the specified conditions.



**TransitRouterAttachments ** <span data-label="purple">Object[] </span>`Example: -`

The details of the inter\-region attachment.


**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-abb******`

The ID of the inter\-region attachment.



**TransitRouterAttachmentName ** <span data-label="purple">String </span>`Example: trattachment-01`

The name of the inter\-region attachment.



**Description ** <span data-label="purple">String </span>`Example: This attachment is used for test.`

The description of the inter\-region attachment.



**TransitRouterRouteTableId ** <span data-label="purple">String </span>`Example: tr-rtb-123567****`

The route table associated with forwarding for the inter\-region attachment.



**PeerTransitRouterId ** <span data-label="purple">String </span>`Example: tr-3tex2x1cwd4c6c0v****`

The ID of the peer TR instance.



**PeerTransitRouterRegionId ** <span data-label="purple">String </span>`Example: cn-beijing`

The ID of the region where the peer TR instance belongs.



**TransitRouterBandwidthPackageId ** <span data-label="purple">String </span>`Example: tr-bp-1234****`

The ID of the TR bandwidth package associated with the inter\-region attachment.



**TransitRouterForwardPolicyTableId ** <span data-label="purple">String </span>`Example: tr-fpt-hy13n2l4c6c0v****`

The ID of the forwarding policy associated with the inter\-region attachment.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 10`

The bandwidth of the inter\-region attachment, measured in Mbps.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the inter\-region attachment.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple">String </span>`Example: tr-tmp-hy13n2l4c6c0v****`

The ID of the traffic marking policy associated with the inter\-region attachment.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span>`Example: tr-tqp-hy13n2l4c6c0v****`

The ID of the traffic queue policy associated with the inter\-region attachment.



**TransitRouterId ** <span data-label="purple">String </span>`Example: tr-1aaaaaaa***`

The ID of the Transit Router (TR) instance.



**Ipv6Enabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether IPv6 is enabled.


* true: Yes.

* false: No.



**AutoPublishRouteEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether auto\-publishing of TR routes to the network instance's route table is enabled.


* true: Yes.

* false: No.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the inter\-region attachment.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**UpdateTime ** <span data-label="purple">String </span>`Example: 2023-08-14T18:05:17+08:00`

The time when the inter\-region attachment is last modified.



**CreationTime ** <span data-label="purple">String </span>`Example: 2023-08-14T18:05:17+08:00`

The time when the inter\-region attachment is created.



**Line Operator ** <span data-label="purple">String </span>`Example: China Unicom`

The provider of the cross\-border bandwidth package.


* ChinaUnicom: China Unicom.

* ChinaTelecom: China Telecom.



**BandwidthType ** <span data-label="purple">String </span>`Example: BandwidthPackage`

The bandwidth allocation method for the inter\-region peering attachment.


* BandwidthPackage: Bandwidth is allocated from a bandwidth package.

* CloudDataTransfer: Bill by traffic via Cloud Data Transfer.



**PeerTransitRouterOwnerId ** <span data-label="purple">String </span>`Example: 2100****63`

The ID of the account that owns the peer TR instance.



**TransitRouterBandwidthPackageOwnerId ** <span data-label="purple">String </span>`Example: 20122****49`

The ID of the account who owns the TR bandwidth package.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeTransitRouterPeerAttachments&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T034726Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterPeerAttachments",
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
                "UpdateTime": "2023-08-14T18:05:17+08:00",
                "Description": "This attachment is used for test.",
                "Ipv6Enabled": true,
                "CreationTime": "2023-08-14T18:05:17+08:00",
                "LineOperator": "ChinaUnicom",
                "BandwidthType": "BandwidthPackage",
                "TransitRouterId": "tr-1aaaaaaa***",
                "PeerTransitRouterId": "tr-3tex2x1cwd4c6c0v****",
                "AutoPublishRouteEnabled": true,
                "PeerTransitRouterOwnerId": "2100****63",
                "PeerTransitRouterRegionId": "cn-beijing",
                "TransitRouterAttachmentId": "tr-attach-abb******",
                "TransitRouterRouteTableId": "tr-rtb-123567****",
                "TransitRouterAttachmentName": "trattachment-01",
                "TransitRouterBandwidthPackageId": "tr-bp-1234****",
                "TransitRouterForwardPolicyTableId": "tr-fpt-hy13n2l4c6c0v****",
                "TransitRouterBandwidthPackageOwnerId": "20122****49",
                "TransitRouterTrafficQosQueuePolicyId": "tr-tqp-hy13n2l4c6c0v****",
                "TransitRouterTrafficQosMarkingPolicyId": "tr-tmp-hy13n2l4c6c0v****"
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
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |This request contains an invalid or unsupported parameter. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
