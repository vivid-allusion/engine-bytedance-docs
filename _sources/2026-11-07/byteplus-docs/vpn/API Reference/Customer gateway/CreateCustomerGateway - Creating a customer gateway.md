---
title: "CreateCustomerGateway - Creating a customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway"
---

Call CreateCustomerGateway to create a customer gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateCustomerGateway&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|alQ3yb">必选</span> `Example: CreateCustomerGateway`

The action that you want to perform. Value: CreateCustomerGateway.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|f5mL54">必选</span> `Example: 2020-04-01`

The API version.



**CustomerGatewayName ** <span data-label="purple">String </span>`optional` `Example: CGW-t26c`

The name of the customer gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If left blank, this parameter defaults to the customer gateway ID.



**IpAddress ** <span data-label="purple">String </span><span data-api-tag="require|6Amys7">必选</span> `Example: 8.XX.XX.8`

The static elastic IP address (EIP) of the peer's on\-premises data center gateway or the egress IP address of the VPN gateway in another VPC. If the peer does not have a fixed static EIP, enter `0.0.0.0` here.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the customer gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, it defaults to an empty string.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: Project_1`

The project to which the customer gateway belongs. If left blank, the default is used. That is, the created resource belongs to the default project. You can call [ListProjects](https://docs.byteplus.com/en/docs/6649/1131880) to query project information under the current account.



**Asn ** <span data-label="purple">Integer </span>`optional` `Example: 65000`

ASN (Autonomous System Number) of the customer gateway.


* To use BGP, this parameter is required.

* Valid ASN range is 1 to 4294967295 (excluding 137718, 150436, and 65533).

* 137718 and 150436 are BytePlus ASNs, and 65533 is a special ASN. None are usable.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

The tag key of the customer gateway.


* N represents the sequence number of a tag key. Valid range: 1\-20.

* Separate multiple tag keys with &. Naming rules are as follows:

* Cannot start with `volc:` or `sys:` in any case form.

* May include language characters, numbers, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* Must be 1 to 128 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Duplicate tag keys are not allowed for the same resource.</div>




**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

The tag value of the customer gateway.


* N represents the sequence number of a tag value. Valid range: 1–20.

* Separate multiple tag values with ampersands (&). Naming rules are as follows:

* May include language characters, numbers, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@".

* May be left blank. Must be 0 to 256 characters in length.

* Case\-sensitive. Cannot start or end with a space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide <code>Tags.N.Value</code>, you must provide <code>Tags.N.Key</code>.</div>




**IpVersion ** <span data-label="purple">String </span>`optional` `Example: ipv4`

The IP protocol type of the VPN gateway. Values:


* ipv4 (default)

* ipv6



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2022032111142501022524314704AF****`

Request ID.



**CustomerGatewayId ** <span data-label="purple">String </span>`Example: cgw-3tex2x1cwd4c6c0v****`

ID of the new customer gateway.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateCustomerGateway&Version=2020-04-01&CustomerGatewayName=test&Description=test&IpAddress=1.1.1.1 HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2022032111142501022524314704AF****",
        "Action": "CreateCustomerGateway",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2022032111142501022524314704AF****",
        "CustomerGatewayId": "cgw-2d670j2o9lc0058ozfddg****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidCustomerGatewayIp.Malformed |The specified customer gateway ip is malformed. |The specified customer gateway IP is invalid. |
|400 |QuotaExceeded.CustomerGateway |You've reached the limit on the number of customer gateway per region that you can create. |You have reached the maximum of customer gateways that you can create per region. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The specified CientToken is malformed. It cannot be more than 64 ASCII characters. |
|400 |InvalidCustomerGateway.InvalidASN |The Customer Gateway ASN is invalid and it should be in the range of 1\-4294967294, excluding 65535, 137718 and 150436. |The specified ASN is invalid. The value must be within the range of 1\-4294967294, excluding 65535, 137718, and 150436. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that can be processed in a single request. |
|403 |Forbidden.VpnGatewayBgpPermissionNotGranted |The specified account is not granted VPN gateway BGP permission. |The current account is not authorized to use BGP for Virtual Private Network (VPN) service. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
