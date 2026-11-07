---
title: "DescribeSslVpnServerSamlData - Querying identity provider metadata"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServerSamlData"
---

Call DescribeSslVpnServerSamlData to query two\-factor authentication SAML metadata of an SSL\-VPN server.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Two\-Factor Authentication is in the beta stage. To request a trial, please contact your account manager.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeSslVpnServerSamlData&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple"> String </span><span data-api-tag="require|R_dEL2">必选</span> `Example: DescribeSslVpnServerSamlData`

The action to perform. Value: DescribeSslVpnServerSamlData.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|U-H8sl">必选</span> `Example: 2020-04-01`

The API version.



**SslVpnServerId ** <span data-label="purple"> String </span><span data-api-tag="require|CipUGf">必选</span> `Example: vss-zm55pqtvk17oq32zd****`

The ID of the SSL\-VPN server.

You can call [DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) to query the ID of the SSL\-VPN server.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple"> String </span>`Example: 0ED8D006-F706-4D23-88ED-E11ED28DCAC0`

The request ID.



**SamlData ** <span data-label="purple"> String </span>`Example: <md:EntityDescriptor entityID="https://fwleyr***.authing.cn/6a326e***" ID="pfxd542c086-c02***" xmlns:md="urn:oasis:names:tc:SAML:2.0:metadata">`

The SAML metadata information of the identity provider (IdP).



**SsoAuthEnabled ** <span data-label="purple"> Boolean  </span>`Example: true`

Describe whether two\-factor authentication is enabled.


* true: Enabled.

* false: Disabled.



<span id=".6K-35rGC56S65L6L"></span>
## Request example

```JSON
GET /?Action=DescribeSslVpnServerSamlData&Version=2020-04-01&SslVpnServerId=vss-zm55pqtvk17oq32zd**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeSslVpnServerSamlData",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "0ED8D006-F706-4D23-88ED-E11ED28DCAC0",
        "SamlData": "<md:EntityDescriptor entityID=\"https://fwleyr***.authing.cn/6a326e***\" ID=\"pfxd542c086-c02***\" xmlns:md=\"urn:oasis:names:tc:SAML:2.0:metadata\">",
        "SsoAuthEnabled": true
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).
