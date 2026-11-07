---
title: "DescribeTransitRouterAttachments - Querying the attachment list"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterAttachments"
---

Call DescribeTransitRouterAttachments to query attachments that meet specified conditions. The list encompasses network instance attachments (VPC, VPN, DC Gateway) and inter\-region attachments.​

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterAttachments&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|oEUfEX">必选</span> `Example: DescribeTransitRouterAttachments`

The interface name. The current API name is `DescribeTransitRouterAttachments`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|3sBu9S">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple">String </span>`optional` `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**ResourceType ** <span data-label="purple">String </span>`optional` `Example: VPC`

The network instance type. Values:


* VPC: Virtual Private Cloud.

* VPN: Virtual Private Network.

* DCGW: Direct Connect Gateway.

* TransitRouter: Transit Router.



**ResourceId ** <span data-label="purple">String </span>`optional` `Example: vpc-bp1aevy8sofi8mh1****`

The network instance ID.


* You can call the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) API to obtain the ID of the VPC instance.

* You can call the [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) API to obtain the ID of the VPN instance.

* You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to obtain the ID of the DC Gateway instance.

* You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the ID of the TR instance.



**TransitRouterForwardPolicyTableId ** <span data-label="purple">String </span>`optional` `Example: tr-fpt-hy13n2l4c6c0v****`

The ID of the forwarding policy associated with the inter\-region attachment. You can call the [DescribeTransitRouterForwardPolicyTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterForwardPolicyTables) API to obtain the forwarding policy ID.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple">String </span>`optional` `Example: tr-tmp-hy13n2l4c6c0v****`

The ID of the traffic marking policy. You can call the [DescribeTransitRouterTrafficQosMarkingPolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosMarkingPolicies) API to obtain the ID of the traffic marking policy.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span>`optional` `Example: tr-tqp-hy13n2l4c6c0v****`

The ID of the traffic queue policy. You can call the [DescribeTransitRouterTrafficQosQueuePolicies](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterTrafficQosQueuePolicies) API to obtain the traffic queue policy ID.



**TransitRouterAttachmentIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* N represents the sequence number of a network instance attachment, ranging from 1 to 100.

* Separate multiple attachment IDs with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpcAttachments">DescribeTransitRouterVpcAttachments</a> API to obtain the ID of the VPC attachment.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments">DescribeTransitRouterVpnAttachments</a> API to obtain the ID of the VPN attachment.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterDirectConnectGatewayAttachments">DescribeTransitRouterDirectConnectGatewayAttachments</a> API to obtain the ID of the DC Gateway attachment.</div>


* <div data-tips="true" data-tips-type="tip">You can call the <a href="https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterPeerAttachments">DescribeTransitRouterPeerAttachments</a> API to obtain the ID of the inter\-region attachment.</div>




**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key of the network instance attachment.


* N represents the sequence number of a tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the network instance attachments that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value of the network instance attachment.


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



**TransitRouterAttachments ** <span data-label="purple">Object[] </span>`Example: --`

The details of TR instances that match the conditions.


**ResourceId ** <span data-label="purple">String </span>`Example: vpc-bp1aevy8sofi8mh1****`

The network instance ID of the attachment.



**OverdueTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when the network instance attachment is suspended due to overdue payments.



**DeletedTime ** <span data-label="purple">String </span>`Example: 2021-05-07 23:23:23`

The time when the network instance attachment is deleted.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the network instance attachment is created.



**Description ** <span data-label="purple">String </span>`Example: This attachment is used for test.`

The description of the network instance attachment.



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.



**TransitRouterId ** <span data-label="purple">String </span>`Example: tr-3tehy13n2l4c6c0v****`

The ID of the Transit Router (TR) instance.



**TransitRouterAttachmentName ** <span data-label="purple">String </span>`Example: trattachment-01`

The name of the network instance attachment.



**TransitRouterRouteTableId ** <span data-label="purple">String </span>`Example: tr-rtb-hy13n2l4c6c0v****`

The route table ID associated with forwarding for the network instance attachment.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the network instance attachment is last modified.



**AccountId ** <span data-label="purple">String </span>`Example: 200001****`

The account ID of the network instance attachment.



**Tags ** <span data-label="purple">Object[]</span>

The tag information of the network instance attachment.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**TransitRouterForwardPolicyTableId ** <span data-label="purple">String </span>`Example: tr-fpt-hy13n2l4c6c0v****`

The ID of the forwarding policy associated with the inter\-region attachment.



**TransitRouterTrafficQosMarkingPolicyId ** <span data-label="purple">String </span>`Example: tr-tmp-hy13n2l4c6c0v****`

The ID of the traffic marking policy associated with the network instance attachment.



**TransitRouterTrafficQosQueuePolicyId ** <span data-label="purple">String </span>`Example: tr-tqp-hy13n2l4c6c0v****`

The ID of the traffic queue policy associated with the network instance attachment.



**ResourceType ** <span data-label="purple">String </span>`Example: VPC`

The network instance ID of the attachment.


* VPC: Virtual Private Cloud.

* VPN: Virtual Private Network.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Transit Router.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the network instance attachment.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**Ipv6Enabled ** <span data-label="purple">Boolean </span>`Example: true`

Describes whether to enable IPv6.


* true: Yes

* false: No.



**AutoPublishRouteEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether to automatically publish TR routes to the route table of the network instance.


* true: Yes

* false: No.



**BusinessStatus ** <span data-label="purple">String </span>`Example: Normal`

The operational status of the network instance attachment.


* Normal

* FinancialLocked: Locked.



**BillingAccountId ** <span data-label="purple">String </span>`Example: 2000****59`

The ID of the account to which TR intra\-region attachments are billed. This parameter is not returned for inter\-region attachments.


* For network instance attachments, it returns the billing account ID.

* For local peer attachments, it returns the account ID of the local TR instance.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterAttachments&Version=2020-04-01 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033345Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterAttachments",
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
                "AccountId": "200001****",
                "ResourceId": "vpc-bp1aevy8sofi8mh1****",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "DeletedTime": "2021-05-07 23:23:23",
                "Description": "This attachment is used for test.",
                "Ipv6Enabled": true,
                "OverdueTime": "2021-05-07 23:23:23",
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "ResourceType": "VPC",
                "BusinessStatus": "Normal",
                "TransitRouterId": "tr-3tehy13n2l4c6c0v****",
                "BillingAccountId": "2000****59",
                "AutoPublishRouteEnabled": true,
                "TransitRouterAttachmentId": "tr-attach-13n2l4c****",
                "TransitRouterRouteTableId": "tr-rtb-hy13n2l4c6c0v****",
                "TransitRouterAttachmentName": "trattachment-01",
                "TransitRouterForwardPolicyTableId": "tr-fpt-hy13n2l4c6c0v****",
                "TransitRouterTrafficQosQueuePolicyId": "tr-tqp-hy13n2l4c6c0v****",
                "TransitRouterTrafficQosMarkingPolicyId": "tr-tmp-hy13n2l4c6c0v****"
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
