---
title: "DeleteDirectConnectVirtualInterface - Deleting a DC Virtual Interface"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectVirtualInterface"
---

Call DeleteDirectConnectVirtualInterface to delete a specified Direct Connect (DC) Virtual Interface instance.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If a DC Virtual Interface to be deleted is the only virtual interface of a DC Gateway, you must first call [DetachInstanceFromCen](https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen) to detach the DC Gateway from the Cloud Enterprise Network (CEN), then delete the DC Virtual Interface.

* A DC Virtual Interface to be deleted must have no static routes or BGP peers. If any exist, call [DeleteDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGatewayRoute) to delete static route entries and [DeleteBgpPeer](https://docs.byteplus.com/en/docs/directconnect/DeleteBgpPeer) to delete BGP peers, respectively.

* If a DC Virtual Interface to be deleted is a Shared Virtual Interface, the provider (Account A) must ensure that the user (Account B) of the Shared Virtual Interface has either rejected, deleted, or accepted the Shared Virtual Interface but has not associated it with any BGP peers or static routes. Otherwise, the provider (Account A) cannot delete it.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectVirtualInterface&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|DEW93x">必选</span> `Example: DeleteDirectConnectVirtualInterface`

The interface name. The current API name is `DeleteDirectConnectVirtualInterface`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|13ZQTc">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**VirtualInterfaceId ** <span data-label="purple">String </span><span data-api-tag="require|M2iP1s">必选</span> `Example: dcv-7qthudw0ll6jmc****`

The ID of the DC Virtual Interface instance to be deleted.

You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the DC Virtual Interface instance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectVirtualInterface&Version=2020-04-01&VirtualInterfaceId=dcv-7qthudw0ll6jmc**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "DeleteDirectConnectVirtualInterface",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDirectConnectVirtualInterface.InUse |The specified virtual interface is in use. If you are trying to delete the virtual interface, ensure that its routes have been deleted. |The specified DC Virtual Interface is currently in use. Before attempting to delete it, ensure all associated routes have been deleted. |
|400 |InvalidDirectConnectVirtualInterface.InUse |The specified virtual interface is in use. If you are trying to delete the virtual interface, ensure that its BGP peers have been deleted. |The specified DC Virtual Interface is currently in use. Before attempting to delete it, ensure all associated BGP peers have been deleted. |
|400 |InvalidDirectConnectVirtualInterface.InUse |The specified virtual interface is in use. If you are trying to delete the virtual interface, ensure that its associated direct connect gateway has been detached from CEN. |The specified DC Virtual Interface is currently in use. Before attempting to delete it, ensure that its associated DC Gateway has been detached from the CEN. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectVirtualInterface.InUse |The specified virtual interface is in use. If you are trying to delete the virtual interface, ensure that its associated direct connect gateway has been detached from Transit Router. |The specified DC Virtual Interface is currently in use. Before attempting to delete it, ensure that its associated DC Gateway has no Transit Router (TR) network instance attachments. |
|400 |InvalidDirectConnectVirtualInterface.InvalidStatus |The specified direct connect virtual interface is not in the correct status for the request. |The specified DC Virtual Interface cannot respond to this request due to its status. |
|404 |InvalidDirectConnectVirtualInterface.NotFound |The specified direct connect virtual interface does not exist. |The specified DC Virtual Interface does not exist. |
