---
title: "DescribeTransitRouterRouteEntries - Querying the list of route entries"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries"
---

Call DescribeTransitRouterRouteEntries to query route entries that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeTransitRouterRouteEntries&serviceCode=transitrouter&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|qj08BL">必选</span> `Example: DescribeTransitRouterRouteEntries`

The interface name. The current API name is `DescribeTransitRouterRouteEntries`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|zQ7Wsl">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**TransitRouterRouteEntryType ** <span data-label="purple">String </span>`optional` `Example: Static`

The route type.


* Static: Static route

* Propagated: Auto\-learned route.



**TransitRouterRouteEntryNextHopType ** <span data-label="purple">String </span>`optional` `Example: Attachment`

The next hop type of the route.


* Attachment: A network instance, indicating that traffic matching the route is forwarded to the specified network instance.

* BlackHole: A blackhole, indicating that traffic matching the route is discarded.



**TransitRouterRouteEntryNextHopResourceType ** <span data-label="purple">String </span>`optional` `Example: VPC`

The network instance type of the route's next hop.


* VPC: Virtual Private Cloud.

* VPN: Virtual Private Network.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Transit Router.



**TransitRouterRouteTableId ** <span data-label="purple">String </span><span data-api-tag="require|z2nXqn">必选</span> `Example: tr-rtb-hy13n2l4c6c0v****`

The ID of the route table associated with the TR instance. You can call the [DescribeTransitRouterRouteTables](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTables) API to obtain the TR route table ID.



**DestinationCidrBlock ** <span data-label="purple">String </span>`optional` `Example: 192.168.XX.XX/24`

The destination CIDR block of the route.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries on each page in a pagination query. Valid values: 1–100. Default: 20.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

The route status.


* Available

* Creating

* Pending: ​​Configuration in progress.

* Deleting

* Conflicted: Not effective.



**TransitRouterRouteEntryName ** <span data-label="purple">String </span>`optional` `Example: routeentry-01`

The name of the route in the TR route table.



**TransitRouterRouteEntryIds.N ** <span data-label="purple">String </span>`optional` `Example: tr-rte-1i5i8khf9m58gae5kcx6****`

The ID of the TR route.


* N represents the sequence number of a TR route, with a valid range of 1 to 100.

* Separate multiple TR route IDs with ampersands (&).



**TransitRouterRouteEntryNextHopId ** <span data-label="purple">String </span>`optional`

The ID of the route entry next hop.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of rows on the current page.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

Total number of qualified route entries.



**TransitRouterRouteEntries ** <span data-label="purple">Object[] </span>`Example: --`

The details of qualified route entries.


**Description ** <span data-label="purple">String </span>`Example: This is a sample description.`

Description of the route.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 192.168.XX.XX/24`

The destination CIDR block of the route.



**TransitRouterRouteEntryId ** <span data-label="purple">String </span>`Example: tr-rte-12ghy8jkmg****`

The route ID.



**TransitRouterRouteEntryName ** <span data-label="purple">String </span>`Example: trentry01`

The route name.



**TransitRouterRouteEntryNextHopType ** <span data-label="purple">String </span>`Example: Attachment`

The next hop type of the route.


* Attachment: A network instance, indicating that traffic matching the route is forwarded to the specified network instance.

* BlackHole: A blackhole, indicating that traffic matching the route is discarded.



**TransitRouterRouteEntryType ** <span data-label="purple">String </span>`Example: Static`

The route type.


* Static: Static route

* Propagated: Learned route.



**AsPath ** <span data-label="purple">String[] </span>`Example: 20314`

The AS path of the route.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the route is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the route is last modified.



**Status ** <span data-label="purple">String </span>`Example: Available`

The route status.


* Available

* Creating

* Pending: ​​Configuration in progress.

* Deleting

* Conflicted: Not effective.



**TransitRouterRouteEntryNextHopId ** <span data-label="purple">String </span>`Example: tr-attach-vx6iwhjr1x****`

The next hop ID of the route.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>TransitRouterRouteEntryNextHopType</code> is set to “Attachment”.</div>




**DestinationPrefixListId ** <span data-label="purple">String </span>`Example: pl-1234567890abcdef0`

The ID of the target prefix list for the route entry. It specifies the destination address range of the route entry.



**TransitRouterRouteEntryNextHopResourceId ** <span data-label="purple">String </span>`Example: vpc-zyq1wxy1zy249`

The next\-hop resource ID of the route entry. It indicates the ID of the target resource to which traffic matching this route entry will be forwarded.



**TransitRouterRouteEntryNextHopVpnTunnelId ** <span data-label="purple">String </span>`Example: tunnel-123456`

The tunnel ID of the VPN which is the Next Hop of the route entry.

This parameter is returned when the Next Hop of the route entry is a VPN attachment with dual tunnels.



**TransitRouterRouteEntryNextHopResourceType ** <span data-label="purple">String </span>`Example: VPC`

The network instance type of the route's next hop.


* VPC: Virtual Private Cloud.

* VPN: Virtual Private Network.

* DirectConnectGateway: Direct Connect Gateway.

* TransitRouter: Transit Router.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeTransitRouterRouteEntries&Version=2020-04-01&TransitRouterRouteTableId=tr-rtb-hy13n2l4c6c0v**** HTTP/1.1
Host: transitrouter.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T093131Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/transitrouter/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20250804173134071211148112D3F0A8",
        "Action": "DescribeTransitRouterRouteEntries",
        "Version": "2020-04-01",
        "Service": "transitrouter",
        "Region": "cn-beijing"
    },
    "Result": {
        "TransitRouterRouteEntryNextHopResourceType": "VPC",
        "TransitRouterRouteEntryNextHopResourceID": "vpc-az1289azgaqsa125",
        "PageSize": 20,
        "PageNumber": 1,
        "TotalCount": 2,
        "TransitRouterRouteEntries": [
            {
                "Description": "This is a sample description.",
                "DestinationCidrBlock": "192.168.XX.XX/24",
                "TransitRouterRouteEntryId": "tr-rte-12ghy8jkmg****",
                "TransitRouterRouteEntryName": "trentry01",
                "TransitRouterRouteEntryNextHopType": "Attachment",
                "TransitRouterRouteEntryType": "Static",
                "AsPath": [
                    "20314"
                ],
                "CreationTime": "2021-04-09T08:36:47+08:00",
                "UpdateTime": "2021-04-09T08:36:47+08:00",
                "Status": "Available",
                "TransitRouterRouteEntryNextHopId": "tr-attach-vx6iwhjr1x****"
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
