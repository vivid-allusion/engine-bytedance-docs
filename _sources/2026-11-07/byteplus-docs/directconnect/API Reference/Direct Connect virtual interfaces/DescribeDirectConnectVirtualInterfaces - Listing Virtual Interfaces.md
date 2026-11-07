---
title: "DescribeDirectConnectVirtualInterfaces - Listing Virtual Interfaces"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces"
---

Call DescribeDirectConnectVirtualInterfaces to query the details of Virtual Interfaces that meet conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If you do not provide the request parameter of `VirtualInterfaceIds`, the system queries based on other parameters and returns all Virtual Interfaces that meet conditions.

* If you do not provide any optional request parameters, the system queries based on the current account and returns all Virtual Interfaces under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectVirtualInterfaces&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|YT6arZ">必选</span> `Example: DescribeDirectConnectVirtualInterfaces`

The interface name. The current API name is `DescribeDirectConnectVirtualInterfaces`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|GnrEEA">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VirtualInterfaceIds.N ** <span data-label="purple">String </span>`optional` `Example: dcv-7qthudw0ll6jmc****`

The ID of the Virtual Interface.


* N represents the sequence number of a Virtual Interface. You can call up to 100 IDs per request.

* Separate multiple Virtual Interface IDs with ampersands (&).



**DirectConnectConnectionId ** <span data-label="purple">String </span>`optional` `Example: dcc-3tehy13n2l4c6c0v****`

The ID of the DC Connection associated with the Virtual Interface.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`optional` `Example: dcg-2fe3zsmkshs59g****`

The ID of the DC Gateway associated with the Virtual Interface.



**VirtualInterfaceName ** <span data-label="purple">String </span>`optional` `Example: test`

The name of the Virtual Interface.



**RouteType ** <span data-label="purple">String </span>`optional` `Example: BGP`

The route type of the Virtual Interface.



**VlanId ** <span data-label="purple">Integer </span>`optional` `Example: 2000`

The VLAN ID of the Virtual Interface.



**LocalIp ** <span data-label="purple">String </span>`optional` `Example: 192.XX.XX.10/24`

Cloud gateway peer IP of the Virtual Interface.



**PeerIp ** <span data-label="purple">String </span>`optional` `Example: 192.XX.XX.20/24`

Your gateway peer IP of the Virtual Interface



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a paginated query. Maximum: 100. Default: 20.



**Status ** <span data-label="purple">String </span>`optional` `Example: Available`

The status of the Virtual Interface.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the cloud resource instance.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with ampersands (`&`).

* If you set multiple `TagFilters.N.Key` values, these `TagFilters.N.Key` values must be unique and are combined with a logical AND​​.



**TagFilters.N.Values.M ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the cloud resource instance.


* N represents the sequence number of a tag key. Values: 1\-10.

* M represents the sequence number of a tag value. Valid range: 1–3. That is, you can query up to 3 tag values for the same tag key.

* Separate multiple tag values with ampersands (&).

* To provide this parameter, you must provide `TagFilters.N.Key`.

* If you only provide `TagFilters.N.Key` without this parameter, the system queries all tag values of the same tag key.

* If you provide an empty string, the system queries tags with an empty tag value.

* If you set multiple `TagFilters.N.Values.M` values for the same `TagFilters.N.Key`, these `TagFilters.N.Values.M` values are combined with a logical OR.



**GatewayType ** <span data-label="purple">String </span>`optional` `Example: DXGW`

The gateway type associated with the Virtual Interface.


* DCGW: Direct Connect Gateway

* DXGW: Global Direct Exchange Gateway



**DirectExchangeGatewayId ** <span data-label="purple">String </span>`optional` `Example: dxg-273w1ti8gr***`

The ID of the DXGW associated with the Virtual Interface



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 10`

Total number of Virtual Interfaces meeting the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

Current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

The number of entries per page in the current pagination.



**VirtualInterfaces ** <span data-label="purple">Object[] </span>`Example: -`

Details of the Virtual Interface.


**Tags ** <span data-label="purple">Object[] </span>`Example: -`

The information about all tags added to the Virtual Interface.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**PeerIp** <span data-label="purple">String</span> `Example: 200.30.0.101/24`

Your gateway peer IP of the Virtual Interface



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the Virtual Interface.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**VlanId ** <span data-label="purple">Integer </span>`Example: 325`

The VLAN ID of the Virtual Interface.



**LocalIp ** <span data-label="purple">String </span>`Example: 200.30.0.100/24`

Cloud gateway peer IP of the Virtual Interface.



**AccountId ** <span data-label="purple">String </span>`Example: 20******57`

The ID of the current BytePlus account.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 10000`

Limited bandwidth of the Virtual Interface. Unit: Mbps.



**EnableBfd ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether BFD control packet is enabled.


* true: Enabled

* false: Not enabled



**EnableNqa ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether the NQA is enabled.


* true: Enabled

* false: Not enabled


NQA is available only when RouteType is Static.



**RouteType ** <span data-label="purple">String </span>`Example: BGP`

The route type of the Virtual Interface.



**DxgwStatus ** <span data-label="purple">String </span>`Example: Available`

The status of the DXGW.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**PeerIpv6Ip ** <span data-label="purple">String </span>`Example: 2001:2300:1328:0015:0000:0000:0000:2/126`

The IPv6 address of Your gateway peer IP for the Virtual Interface.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-12-08T11:49:06+08:00`

The time when the Virtual Interface is updated.



**Description ** <span data-label="purple">String </span>`Example: a test vif`

The description of the Virtual Interface.



**DxgwOwnerId ** <span data-label="purple">String </span>`Example: 2108892****`

The account ID of the DXGW associated with the Virtual Interface



**GatewayType ** <span data-label="purple">String </span>`Example: DCGW`

The gateway type associated with the Virtual Interface.


* DCGW: Direct Connect Gateway

* DXGW: Global Direct Exchange Gateway



**LocalIpv6Ip** <span data-label="purple">String</span> `Example: 2001:2300:1328:0015:0000:0000:0000:1/126`

The IPv6 address of Cloud gateway peer IP for the Virtual Interface.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-11-15T14:53:24+08:00`

The time when the Virtual Interface is created.



**EnableBfdEcho ** <span data-label="purple">Boolean </span>`Example: false`

Describes whether BFD echo packet is enabled.


* true: Enabled

* false: Not enabled



**OwnerAccountId ** <span data-label="purple">String </span>`Example: 2108892****`

The BytePlus account to which the Virtual Interface belongs.



**BfdDetectInterval ** <span data-label="purple">Integer </span>`Example: 1000`

The time interval for detection. Unit: ms.



**NqaDetectInterval ** <span data-label="purple">Integer </span>`Example: 2000`

The time interval for Network Quality Analyzer (NQA) to send consecutive packets. Unit: ms.



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-273w1tcbdf***`

The ID of the Virtual Interface.



**BfdDetectMultiplier ** <span data-label="purple">Integer </span>`Example: 3`

The number of Bidirectional Forwarding Detection (BFD) attempts.



**NqaDetectMultiplier** <span data-label="purple">Integer</span> `Example: 5`

The number of NQA detection attempts. If consecutive failure count reaches the set value for the detect multiplier, the system declares a faulty line.



**VirtualInterfaceName ** <span data-label="purple">String </span>`Example: VIF-sj2x`

The name of the Virtual Interface.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-273w1ti8gr***`

The ID of the DC Gateway associated with the Virtual Interface.



**DirectExchangeGatewayId ** <span data-label="purple">String </span>`Example: dxg-273w1ti8grfnk***`

The ID of the DXGW associated with the Virtual Interface



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-274342y***`

The ID of the DC Connection associated with the Virtual Interface.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeDirectConnectVirtualInterfaces&Version=2020-04-01&VirtualInterfaceIds.1=dcv-7qthudw0ll6jmc****&DirectConnectConnectionId=dcc-3tehy13n2l4c6c0v****&DirectConnectGatewayId=dcg-2fe3zsmkshs59g****&VirtualInterfaceName=test&RouteType=BGP&VlanId=2000&LocalIp=192.XX.XX.10/24&PeerIp=192.XX.XX.20/24&PageNumber=1&PageSize=20&Status=Available&TagFilters.1.Key=key1&TagFilters.1.Values.M=value1&GatewayType=DXGW&DirectExchangeGatewayId=dxg-273w1ti8gr*** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeDirectConnectVirtualInterfaces",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 10,
        "VirtualInterfaces": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "PeerIp": "200.30.0.101/24",
                "Status": "Available",
                "VlanId": 325,
                "LocalIp": "200.30.0.100/24",
                "AccountId": "20******57",
                "Bandwidth": 10000,
                "EnableBfd": false,
                "EnableNqa": true,
                "RouteType": "BGP",
                "DxgwStatus": "Available",
                "PeerIpv6Ip": "2001:2300:1328:0015:0000:0000:0000:2/126",
                "UpdateTime": "2021-12-08T11:49:06+08:00",
                "Description": "a test vif",
                "DxgwOwnerId": "2108892****",
                "GatewayType": "DCGW",
                "LocalIpv6Ip": "2001:2300:1328:0015:0000:0000:0000:1/126",
                "CreationTime": "2021-11-15T14:53:24+08:00",
                "EnableBfdEcho": true,
                "OwnerAccountId": "2108892****",
                "BfdDetectInterval": 1000,
                "NqaDetectInterval": 2000,
                "VirtualInterfaceId": "dcv-273w1tcbdf***",
                "BfdDetectMultiplier": 3,
                "NqaDetectMultiplier": 5,
                "VirtualInterfaceName": "VIF-sj2x",
                "DirectConnectGatewayId": "dcg-273w1ti8gr***",
                "DirectExchangeGatewayId": "dxg-273w1ti8grfnk***",
                "DirectConnectConnectionId": "dcc-274342y***"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.DirectConnectVirtualInterfaceId |You've reached the limit on the number of virtual interface IDs that you can describe. |You have reached the maximum number of Virtual Interface IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of tag filter keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |You have reached the maximum number of tag filter values that can be specified in a single request. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format specified for the tag filter is invalid. |
