---
title: "ModifySslVpnClientCert - Modifying an SSL client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifySslVpnClientCert"
---

Call ModifySslVpnClientCert to modify the name and description of an SSL client certificate.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySslVpnClientCert&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|CGVhAn">必选</span> Example: `ModifySslVpnClientCert`

The action that you want to perform. Value: ModifySslVpnClientCert.



**Version ** `String` <span data-api-tag="require|yBaAnD">必选</span> Example: `2020-04-01`

The API version.



**SslVpnClientCertId ** `String` <span data-api-tag="require|w1a-NM">必选</span> Example: `vsc-zm55pqtvk17oq32zd****`

ID of the SSL client certificate. You can call [DescribeSslVpnClientCerts](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts) to query the ID of the SSL client certificate.



**SslVpnClientCertName ** `String` `optional` Example: `Ssl_VpnClient`

Name of the SSL client certificate.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If left blank, the original configuration remains.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the SSL client certificate.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifySslVpnClientCert&Version=2020-04-01&SslVpnClientCertId=vsc-12ads0g2fsmps17q7y2w8****&SslVpnClientCertName=test-cicd&Description=abc HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727195755AB2EA1B996A4739C****",
        "Action": "ModifySslVpnClientCert",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20230727195755AB2EA1B996A4739C****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidSslVpnServer.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified SSL VPN server cannot respond to this request due to its status. |
|404 |InvalidSslVpnClientCert.NotFound |The specified SSL client certificate does not exist. |The specified SSL client certificate does not exist. |
