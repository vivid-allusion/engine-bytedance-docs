---
title: "DeleteVpnConnectionHealthChecker - Deleting a health check instance"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnectionHealthChecker"
---

Call DeleteVpnConnectionHealthChecker to delete a health check from an IPsec\-VPN connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteVpnConnectionHealthChecker&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|vM-_LR">必选</span> Example: `DeleteVpnConnectionHealthChecker`

The action that you want to perform. Value: DeleteVpnConnectionHealthChecker.



**Version ** `String` <span data-api-tag="require|fZSb4q">必选</span> Example: `2020-04-01`

The API version.



**CheckerId ** `String` <span data-api-tag="require|9NUuqV">必选</span> Example: `vhc-fejwn8dfnkmr****`

The ID of the health check to be deleted. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the health check ID of the IPsec\-VPN connection.



**VpnConnectionId ** `String` `optional` Example: `vgc-3tex2x1cwd4c6c0v****`

The ID of the IPsec\-VPN connection whose health check you want to delete. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



**ClientToken ** `String` `optional` Example: `123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteVpnConnectionHealthChecker&Version=2020-04-01&CheckerId=vhc-12b9ncfrstuyo17q7y1d****&VpnConnectionId=vgc-3tex2x1cwd4c6c0v**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20240318144816D8EA7D60EC762084****",
        "Action": "DeleteVpnConnectionHealthChecker",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20240318144816D8EA7D60EC762084****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidVpnConnection.InvalidStatus |The specified VPN connection is not in the correct status for the request. |The specified VPN cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|404 |InvalidVpnConnectionHealthChecker.NotFound |The specified VPN connection health checker does not exist. |The specified VPN health check does not exist. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
