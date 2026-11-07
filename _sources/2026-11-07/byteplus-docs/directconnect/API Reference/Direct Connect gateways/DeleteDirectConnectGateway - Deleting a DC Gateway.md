---
title: "DeleteDirectConnectGateway - Deleting a DC Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGateway"
---

Call DeleteDirectConnectGateway to delete a specified Direct Connect (DC) Gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* The DC Gateway to be deleted is not attached to a Cloud Enterprise Network (CEN). If it is attached, first call [DetachInstanceFromCen](https://docs.byteplus.com/en/docs/cen/DetachInstanceFromCen) to detach the DC Gateway instance from the CEN.

* The DC Gateway to be deleted has no static routes or BGP peers. If any exist, call [DeleteDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGatewayRoute) to delete static route entries and [DeleteBgpPeer](https://docs.byteplus.com/en/docs/directconnect/DeleteBgpPeer) to delete BGP peers.

* The DC Gateway to be deleted is not associated with any virtual interface. If an interface is associated, first call [DeleteDirectConnectVirtualInterface](https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectVirtualInterface) to delete the virtual interface. Ensure that the DC Gateway is detached from the CEN before detaching the last virtual interface.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectGateway&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|hOrrtX">必选</span> `Example: DeleteDirectConnectGateway`

The interface name. The current API name is `DeleteDirectConnectGateway`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|jGBeGR">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|vOsgfO">必选</span> `Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway to be deleted.

You can call the [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) API to query the DC Gateway ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectGateway&Version=2020-04-01&DirectConnectGatewayId=dcg-7qthudw0ll6jmc**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "DeleteDirectConnectGateway",
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
|400 |InvalidDirectConnectGateway.HasRoute |The specified direct connect gateway has routes, and cannot be deleted. |The specified DC Gateway has routes and cannot be deleted. |
|400 |InvalidDirectConnectGateway.HasAssociation |The specified direct connect gateway has associations with direct connect virtual interface, and cannot be deleted. |The specified DC Gateway has associated virtual interfaces and cannot be deleted. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
