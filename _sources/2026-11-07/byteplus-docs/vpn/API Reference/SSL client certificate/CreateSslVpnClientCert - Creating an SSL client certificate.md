---
title: "CreateSslVpnClientCert - Creating an SSL client certificate"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateSslVpnClientCert"
---

Call CreateSslVpnClientCert to create an SSL client certificate.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

The SSL client certificate is a sub\-resource of the SSL VPN server. A new SSL client certificate belongs to the same project as the SSL VPN server, which is selected at creation. You can only migrate the SSL client certificate to another project with the SSL VPN server, but not migrate it separately. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpn/Project-management).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSslVpnClientCert&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|l7PlKH">必选</span> Example: `CreateSslVpnClientCert`

The action that you want to perform. Value: CreateSslVpnClientCert.



**Version ** `String` <span data-api-tag="require|chkLsS">必选</span> Example: `2020-04-01`

The API version.



**SslVpnServerId ** `String` <span data-api-tag="require|DP0c5t">必选</span> Example: `vss-zm55pqtvk17oq32zd****`

ID of the SSL VPN server that is used to create the SSL client certificate. You can call [DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) to query the ID of the SSL VPN server.



**SslVpnClientCertName ** `String` `optional` Example: `Ssl_VpnClient`

Name of the SSL client certificate.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If left blank, this parameter defaults to the ID of the SSL client certificate.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the SSL client certificate.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**ClientToken ** `String` `optional` Example: `123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**Tags.N.Key ** `String` `optional` Example: `key1`

The tag key of the SSL client certificate.


* N represents the sequence number of a tag key. Valid range: 1 to 20.

* Separate multiple tag keys with &.


Naming rules are as follows:


* Must not start with volc: or sys: (case\-insensitive).

* May include language characters, numbers, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* Must be 1 to 128 characters.


> Note: Tag keys of the same resource must be unique.



**Tags.N.Value ** `String` `optional` Example: `value1`

The tag value of the SSL client certificate.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&).


Naming rules are as follows:


* May include language characters, numbers, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* May be left blank. Must be 0 to 256 characters in length.

* It is case\-sensitive. Cannot start or end with a space.


> Note: To provide Tags.N.Value, you must provide Tags.N.Key.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `0ED8D006-F706-4D23-88ED-E11ED28****`

Request ID.



**SslVpnClientCertId ** `String` `optional` Example: `vsc-zm55pqtvk17oq32zd****`

ID of the new SSL VPN client.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateSslVpnClientCert&Version=2020-04-01&SslVpnServerId=vss-imwoo6i1dfk08gbssxfj****&SslVpnClientCertName=test-cicd&Description=abc&ClientToken=abc HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230727195508EA4507984CE7A7F9ED0D",
        "Action": "CreateSslVpnClientCert",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20230727195508EA4507984CE7A7F9****",
        "SslVpnClientCertId": "vsc-12ads0g2fsmps17q7y2w8****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format specified for CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidSslVpnServer.InvalidStatus |The specified SSL server is not in the correct status for the request. |The specified SSL VPN server cannot respond to this request due to its status. |
|400 |QuotaExceeded.SSLClientCert |You've reached the limit on the number of SSL client certificates per SSL server that you can create. |You have reached the maximum of SSL client certificates that can be created per SSL VPN server. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The format specified for the tag index order is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|404 |InvalidSslVpnServer.NotFound |The specified SSL server does not exist. |The specified SSL VPN server does not exist. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
