---
title: "CreateDirectConnectGateway - Creating a DC Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGateway"
---

Call CreateDirectConnectGateway to create a Direct Connect (DC) Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectGateway&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|8tf0ft">必选</span> `Example: CreateDirectConnectGateway`

The interface name. The current API name is `CreateDirectConnectGateway`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|qfyTxI">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayName ** <span data-label="purple">String </span><span data-api-tag="require|CHJMiH">必选</span> `Example: test`

Name of the DC Gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it unset, it defaults to the ID of the DC Gateway.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the DC Gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



**ClientToken ** <span data-label="purple">String </span>`optional` `Example: 123e4567-e89b-12d3-a456-42665544****`

Client Token that is used to ensure the request idempotency.


* You can use the client to automatically generate a token, but must confirm that the tokens for different requests are unique. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

* Must not exceed 64 ASCII characters.

* If you do not provide ClientToken, this API call does not verify idempotency.



**EnableIpv6 ** <span data-label="purple">Boolean </span>`optional` `Example: false`

Specify whether to enable IPv6. Type the enumerated values strictly in the case form as follows. Do not set other values.


* true: Enable

* false: Disable.



**Tags.N.Key ** <span data-label="purple">String </span>`optional` `Example: key1`

Tag key (Key) of the DC Gateway.


* N represents the sequence number of a tag key. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag keys with ampersands (&).

* Must not start with `volc:` or `sys:` in any case form. `volc:` and `sys:` prefixes are reserved for system tags. You cannot create tags starting with these prefixes.

* Must be 1 to 128 characters. May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).



**Tags.N.Value ** <span data-label="purple">String </span>`optional` `Example: value1`

Tag value (Value) of the DC Gateway.


* N represents the sequence number of a tag value. It must be set in consecutive, ascending order starting from 1 up to 50.

* Separate multiple tag values with ampersands (&).

* Must be 0 to 256 characters in length. If left blank, this parameter defaults to an empty string.

* May include characters in different languages, numbers, spaces ( ), underscores (_), periods (.), half\-width colons (:), slashes (/), equal signs (=), plus signs (+), hyphens (\-), and at signs (@).

* It is case\-sensitive. Cannot start or end with a space.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To provide <code>Tags.N.Value</code>, you must provide <code>Tags.N.Key</code>.</div>




**BgpAsn ** <span data-label="purple">Integer </span>`optional` `Example: 137718`

ASN (Autonomous System Number) of the DC Gateway.


* The valid range for DC Gateway ASN is 137718, 64512\-65534, and 4200000000\-4294967294, among which 137718 is the ASN of BytePlus.

* If a DC Gateway is used only in a common scenario (such as an on\-premises data center connecting to a single Virtual Private Cloud resource via DC), use the BytePlus ASN (137718).

* If a DC Gateway is used in a special scenario (such as an on\-premises data center connecting to multiple CENs via DC), you need to customize an ASN to each DC Gateway and avoid using the BytePlus ASN (137718) to ensure no duplicate ASNs among different DC Gateways.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-7qthudw0ll6jmc****`

ID of the newly created DC Gateway.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectGateway&Version=2020-04-01&DirectConnectGatewayName=test&Description=This is a sample description&ClientToken=123e4567-e89b-12d3-a456-42665544****&EnableIpv6=false&Tags.1.Key=key1&Tags.1.Value=value1&BgpAsn=137718 HTTP/1.1
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
        "Action": "CreateDirectConnectGateway",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****",
        "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |PreOrderError |Failed to create preorder for direct connect gateway. |Failed to create the configuration order for the DC Gateway. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is denied due to the sum of both account balance and available coupons being less than USD 100. |
|400 |OrderError |Failed to create an order for direct connect gateway in one step. |Failed to create the DC Gateway order and complete the payment. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |QuotaExceeded.DirectConnectGateway |You've reached the limit on the number of direct connect gateways that you can create. |You have reached the maximum number of DC Gateways that can be created. |
|400 |IdempotentParameterMismatch |Arguments on this idempotent request are inconsistent with arguments used in previous request(s). |The parameters of this idempotent request are inconsistent with those used in the previous request. |
|400 |InvalidParameter.ClientTokenMalformed |The specified parameter ClientToken is malformed. |The format of specified CientToken is invalid. It must not exceed 64 ASCII characters. |
|400 |InvalidTagKey.Malformed |The specified parameter tag key is invalid. |The tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified parameter tag value is invalid. |The tag value is invalid. |
|400 |LimitExceeded.Tags |You've reached the limit on the number of tags that you can operate at one time. |You have reached the maximum number of tags that you can manage in a single request. |
|400 |InvalidTag.Disorder |The specified index order of tag is malformed. |The index order format of the specified tag is invalid. |
|400 |InvalidDirectConnectGateway.InvalidBgpAsn |The specified ASN is invalid. It should be 137718 or fall within the range of 64512\-65534 or 4200000000\-4294967294. |The specified ASN number is invalid. It must be 137718 or within the range of 64512\-65534 or 4200000000\-4294967294. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to perform IPv6 actions. |
|403 |Forbidden.DirectConnectGatewayBgpAsn |You are not authorized to create direct connect gateway with ASN. |No permission to perform ASN actions on the specified DC Gateway. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The idempotent request is in progress. |
