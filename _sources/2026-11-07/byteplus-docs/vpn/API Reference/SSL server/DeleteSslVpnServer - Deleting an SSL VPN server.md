---
title: "DeleteSslVpnServer - Deleting an SSL VPN server"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteSslVpnServer"
---

Call DeleteSslVpnServer to delete a specified SSL VPN client.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Once an SSL VPN server is deleted, any SSL client certificates that were created for that server become invalid. Connection requests using those certificates will be rejected.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteSslVpnServer&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|Rfk5pQ">必选</span> Example: `DeleteSslVpnServer`

The action that you want to perform. Value: DeleteSslVpnServer.



**Version ** `String` <span data-api-tag="require|OLvX76">必选</span> Example: `2020-04-01`

The API version.



**SslVpnServerId ** `String` <span data-api-tag="require|2nRnOA">必选</span> Example: `vss-zm55pqtvk17oq32zd****`

ID of the SSL VPN server to be deleted. You can call [DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) to query the ID of the SSL VPN server.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteSslVpnServer&Version=2020-04-01&SslVpnServerId=vss-zm55pqtvk17oq32zd**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSslVpnServer",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28D****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidSslVpnServer.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified SSL VPN server cannot respond to this request due to its status. |
|400 |InvalidVpnGateway.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|404 |InvalidSslVpnServer.NotFound |The specified SSL server does not exist. |The specified SSL VPN server does not exist. |
