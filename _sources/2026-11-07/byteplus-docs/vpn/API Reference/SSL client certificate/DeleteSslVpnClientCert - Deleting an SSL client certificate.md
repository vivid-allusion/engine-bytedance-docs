---
title: "DeleteSslVpnClientCert - Deleting an SSL client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DeleteSslVpnClientCert"
---

Call DeleteSslVpnClientCert to delete a specified SSL client certificate.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteSslVpnClientCert&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|eFBbSi">必选</span> Example: `DeleteSslVpnClientCert`

The action that you want to perform. Value: DeleteSslVpnClientCert.



**Version ** `String` <span data-api-tag="require|zBZ0uq">必选</span> Example: `2020-04-01`

The API version.



**SslVpnClientCertId ** `String` <span data-api-tag="require|Dnw2t-">必选</span> Example: `vsc-zm55pqtvk17oq32zd****`

ID of the SSL client certificate to be deleted. You can call [DescribeSslVpnClientCerts](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts) to query the ID of the SSL client certificate.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28D****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DeleteSslVpnClientCert&Version=2020-04-01&SslVpnClientCertId=vsc-12ads0g2fsmps17q7y2w8**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727200910D1A9871FEA36064F****",
        "Action": "DeleteSslVpnClientCert",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20230727200910D1A9871FEA36064F****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidSslVpnServer.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified SSL VPN server cannot respond to this request due to its status. |
|404 |InvalidSslVpnClientCert.NotFound |The specified SSL client certificate does not exist. |The specified SSL client certificate does not exist. |
