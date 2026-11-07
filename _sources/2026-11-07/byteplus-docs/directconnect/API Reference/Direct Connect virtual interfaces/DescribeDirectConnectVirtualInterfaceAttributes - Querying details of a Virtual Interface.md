---
title: "DescribeDirectConnectVirtualInterfaceAttributes - Querying details of a Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaceAttributes"
---

Call DescribeDirectConnectVirtualInterfaceAttributes to query the details of a specified Virtual Interface.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectVirtualInterfaceAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|GfYemS">必选</span> `Example: DescribeDirectConnectVirtualInterfaceAttributes`

The interface name. The current API name is `DescribeDirectConnectVirtualInterfaceAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|DDT11C">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VirtualInterfaceId ** <span data-label="purple">String </span><span data-api-tag="require|tC6uTg">必选</span> `Example: dcv-7qthudw0ll6jmc****`

The ID of the Virtual Interface to be queried. You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the Virtual Interface.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the current BytePlus account.



**VirtualInterfaceId ** <span data-label="purple">String </span>`Example: dcv-7qthudw0ll6jmc****`

The ID of the Virtual Interface.



**VirtualInterfaceName ** <span data-label="purple">String </span>`Example: test`

The name of the Virtual Interface.



**Description ** <span data-label="purple">String </span>`Example: This is a sample description`

The description of the Virtual Interface.



**DirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-3tehy13n2l4c6c0v****`

The ID of the DC Connection associated with the Virtual Interface.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-2fe3zsmkshs59g****`

The ID of the DC Gateway associated with the Virtual Interface.



**RouteType ** <span data-label="purple">String </span>`Example: BGP`

The route type of the Virtual Interface.



**VlanId ** <span data-label="purple">Integer </span>`Example: 2000`

The VLAN ID of the Virtual Interface.



**LocalIp ** <span data-label="purple">String </span>`Example: 192.XX.XX.10/24`

Cloud gateway peer IP of the Virtual Interface.



**PeerIp ** <span data-label="purple">String </span>`Example: 192.XX.XX.20/24`

Your gateway peer IP of the Virtual Interface



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the Virtual Interface is created.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2021-04-10T09:18:28+08:00`

The time when the Virtual Interface is updated.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the Virtual Interface.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**BfdDetectInterval ** <span data-label="purple">Integer </span>`Example: 1000`

The time interval for detection. Unit: ms.



**BfdDetectMultiplier ** <span data-label="purple">Integer </span>`Example: 3`

The number of Bidirectional Forwarding Detection (BFD) attempts.



**Bandwidth ** <span data-label="purple">Integer </span>`Example: 100`

Limited bandwidth of the Virtual Interface. Unit: Mbps.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

The information about all tags added to the Virtual Interface.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**EnableNqa ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether the NQA is enabled.


* true: Enabled

* false: Not enabled



**NqaDetectInterval ** <span data-label="purple">Integer </span>`Example: 3000`

The time interval for Network Quality Analyzer (NQA) to send consecutive packets.



**NqaDetectMultiplier ** <span data-label="purple">Integer </span>`Example: 8`

The number of NQA detection attempts. If consecutive failure count reaches the set value for the detect multiplier, the system declares a faulty line.



**LocalIpv6Ip ** <span data-label="purple">String </span>`Example: fe80:XX::1/120`

The IPv6 address of Cloud gateway peer IP for the Virtual Interface.



**PeerIpv6Ip ** <span data-label="purple">String </span>`Example: fe80:XX::2/120`

The IPv6 address of Your gateway peer IP for the Virtual Interface.



**OwnerAccountId ** <span data-label="purple">String </span>`Example: 21000522****`

The BytePlus account to which the Virtual Interface belongs.



**EnableBfd ** <span data-label="purple">Boolean </span>`Example: false`

Describe whether BFD is enabled.


* true: Enabled

* false: Not enabled



**EnableBfdEcho ** <span data-label="purple">Boolean </span>`Example: false`

Describes whether BFD echo packet is enabled.


* true: Enabled

* false: Not enabled



**DirectExchangeGatewayId ** <span data-label="purple">String </span>`Example: dxg-273w1ti8gr***`

The ID of the DXGW associated with the Virtual Interface



**DxgwOwnerId ** <span data-label="purple">String </span>`Example: 2108892****`

The account that owns the DXGW resource.



**DxgwStatus ** <span data-label="purple">String </span>`Example: Available`

The status of the DXGW.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available



**GatewayType ** <span data-label="purple">String </span>`Example: DCGW`

The gateway type associated with the Virtual Interface.


* DCGW: Direct Connect Gateway

* DXGW: Global Direct Exchange Gateway



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
GET /?Action=DescribeDirectConnectVirtualInterfaceAttributes&Version=2020-04-01&VirtualInterfaceId=dcv-7qthudw0ll6jmc**** HTTP/1.1
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
        "Action": "DescribeDirectConnectVirtualInterfaceAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-north-1"
    },
    "Result": {
        "AccountId": "21000*****",
        "Bandwidth": 100,
        "BfdDetectInterval": 1000,
        "BfdDetectMultiplier": 3,
        "CreationTime": "2021-04-09T08:36:47+08:00",
        "Description": "This is a sample description",
        "DirectConnectConnectionId": "dcc-3tehy13n2l4c6c0v****",
        "DirectConnectGatewayId": "dcg-2fe3zsmkshs59g****",
        "DirectExchangeGatewayId": "dxg-273w1ti8grfnk7fap8tnkmfp9",
        "DxgwOwnerId": "2108892****",
        "DxgwStatus": "Available",
        "EnableBfd": false,
        "EnableBfdEcho": false,
        "EnableNqa": true,
        "GatewayType": "DCGW",
        "LocalIp": "192.XX.XX.10/24",
        "LocalIpv6Ip": "fe80:XX::1/120",
        "NqaDetectInterval": 3000,
        "NqaDetectMultiplier": 8,
        "OwnerAccountId": "21000522****",
        "PeerIp": "192.XX.XX.20/24",
        "PeerIpv6Ip": "fe80:XX::2/120",
        "RouteType": "BGP",
        "Status": "Available",
        "Tags": [
            {
                "Key": "k1",
                "Value": "v1"
            }
        ],
        "UpdateTime": "2021-04-10T09:18:28+08:00",
        "VirtualInterfaceId": "dcv-7qthudw0ll6jmc****",
        "VirtualInterfaceName": "test",
        "VlanId": 2000
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectVirtualInterface.NotFound |The specified direct connect virtual interface does not exist. |The specified Virtual Interface does not exist. |
