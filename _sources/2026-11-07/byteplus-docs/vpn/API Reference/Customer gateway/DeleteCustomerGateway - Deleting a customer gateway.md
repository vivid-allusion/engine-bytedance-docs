---
title: "DeleteCustomerGateway - Deleting a customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteCustomerGateway"
---

Call DeleteCustomerGateway to delete a specified customer gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You can only delete customer gateways that are not used by any IPsec\-VPN connections. If used, call [DeleteVpnConnection](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnection) to delete the IPsec\-VPN connection before deleting the customer gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteCustomerGateway&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|jjz2ks">必选</span> Example: `DeleteCustomerGateway`

The action that you want to perform. Value: DeleteCustomerGateway.



**Version ** `String` <span data-api-tag="require|KoPOWV">必选</span> Example: `2020-04-01`

The API version.



**CustomerGatewayId ** `String` <span data-api-tag="require|wT4yS3">必选</span> Example: `cgw-3tex2x1cwd4c6c0v****`

The ID of the customer gateway to be deleted. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteCustomerGateway&Version=2020-04-01&CustomerGatewayId=cgw-2d670j2o9lc0058ozfddg**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202203211611080102121461940900****",
        "Action": "DeleteCustomerGateway",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202203211611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidCustomerGateway.InvalidStatus |The specified customer gateway is not in the correct status for the request. |The specified customer gateway cannot respond to this request due to its status. |
|400 |InvalidCustomerGateway.InUse |The specified customer gateway has dependent resource of connection. |The specified customer gateway cannot be deleted because it has a connection. |
|404 |InvalidCustomerGateway.NotFound |The specified customer gateway does not exist. |The specified customer gateway does not exist. |
