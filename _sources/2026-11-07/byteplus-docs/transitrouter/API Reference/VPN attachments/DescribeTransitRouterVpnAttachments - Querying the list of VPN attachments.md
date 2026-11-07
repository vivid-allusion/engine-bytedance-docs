---
title: "DescribeTransitRouterVpnAttachments - Querying the list of VPN attachments"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterVpnAttachments"
---

Call DescribeTransitRouterVpnAttachments to query Virtual Private Network (VPN) attachments that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterVpnAttachments&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|vMpGwo">必选</span>`Example: DescribeTransitRouterVpnAttachments`

The interface name. The current API name is `DescribeTransitRouterVpnAttachments`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Uui2Qi">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterId ** <span data-label="purple">String </span><span data-api-tag="require|AZDEf4">必选</span> `Example: tr-7qthudw0ll6jmc****`

The TR instance ID. You can call the [DescribeTransitRouters](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouters) API to obtain the TR instance ID.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**TransitRouterAttachmentIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.


* N represents the serial number of the network instance attachment, ranging from 1 to 100.

* Separate multiple attachment IDs with ampersands (&).



**VpnConnectionId ** <span data-label="purple">String </span>`optional` `Example: vgc-3tex2x1cwd4c6c0v****`

The ID of the IPsec\-VPN connection. You can call the [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) API to obtain the ID of the IPsec\-VPN connection.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key of the network instance attachment.


* N represents the serial number of the tag key, ranging from 1 to 10. Separate multiple tag keys with ampersands (&).

* Specifying multiple tag keys means querying the network instance attachments that contain all specified tag keys.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value of the network instance attachment.


* The first N represents the serial number of the tag key, ranging from 1 to 10.

* The second N represents the serial number of the tag value, ranging from 1 to 3. The relationship between multiple tag values for the same tag key is a logical "OR". That is, the query returns resources tagged with any one of the specified values for that key.

* Separate multiple tags with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To provide this parameter, you must first provide TagFilters.N.Key.</div>


* <div data-tips="true" data-tips-type="tip">When an empty value is set for this parameter, it means querying resources where the tag value is empty under the specified tag key.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of qualified VPN attachments.



**TransitRouterAttachments ** <span data-label="purple">Object[] </span>`Example: -`

The qualified VPN attachments.


**TransitRouterId ** <span data-label="purple">String </span>`Example: tr-7qthudw0ll6jmc****`

The ID of the Transit Router (TR) instance.



**TransitRouterAttachmentId ** <span data-label="purple">String </span>`Example: tr-attach-13n2l4c****`

The ID of the network instance attachment.



**Description ** <span data-label="purple">String </span>`Example: This attachment is used for test.`

The description of the network instance attachment.



**VpnConnectionId ** <span data-label="purple">String </span>`Example: vgc-3tex2x1cwd4c6c0v****`

The ID of the IPsec\-VPN connection.



**ZoneId ** <span data-label="purple">String </span>`Example: cn-beijing-a`

The ID of the availability zone to which the network instance attachment belongs.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the network instance attachment.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**AutoPublishRouteEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether to automatically publish TR routes to the route table of the network instance.


* true: Yes.

* false: No.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the network instance attachment is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the network instance attachment is last modified.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

The tag information of the network instance attachment.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**TransitRouterAttachmentName ** <span data-label="purple">String </span>`Example: trattachment-01`

The name of the network instance attachment.



**Ipv6Enabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether to enable IPv6.


* true: Yes.

* false: No.



**HealthCheckRevokeRouteEnabled ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether to enable health check convergence routing.


* true: Yes. The health check convergence routing feature takes effect only if health check is enabled on the IPsec\-VPN connection. It only supports converging static routes, not BGP routes.

* false: No.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterVpnAttachments&Version=2020-04-01&TransitRouterId=tr-7qthudw0ll6jmc****&PageNumber=1&PageSize=20&TransitRouterAttachmentIds.1=tr-attach-13n2l4c****&VpnConnectionId=vgc-3tex2x1cwd4c6c0v****&TagFilters.1.Key=k1&TagFilters.1.Values.1=v1 HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeTransitRouterVpnAttachments",
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
                "ZoneId": "cn-beijing-a",
                "UpdateTime": "2021-04-10T09:18:28+08:00",
                "Description": "This attachment is used for test.",
                "Ipv6Enabled": false,
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "TransitRouterId": "tr-7qthudw0ll6jmc****",
                "VpnConnectionId": "vgc-3tex2x1cwd4c6c0v****",
                "AutoPublishRouteEnabled": false,
                "TransitRouterAttachmentId": "tr-attach-13n2l4c****",
                "TransitRouterAttachmentName": "trattachment-01",
                "HealthCheckRevokeRouteEnabled": false
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.ResourceIds |You've reached the limit of 100 resource IDs that can be specified in this request. |The request contains invalid or unsupported parameters. The maximum number of resource query results is 100. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag keys that you can specify for filtering in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag values that you can specify for filtering in a single request. |
