---
title: "ModifyDirectConnectGatewayAttributes - Modifying a DC Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifyDirectConnectGatewayAttributes"
---

Call ModifyDirectConnectGatewayAttributes to modify the name and description of the specified Direct Connect (DC) Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyDirectConnectGatewayAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|0bumUS">必选</span> `Example: ModifyDirectConnectGatewayAttributes`

The interface name. The current API name is `ModifyDirectConnectGatewayAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|T8tKpD">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|wTs4OU">必选</span> `Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway to be modified. You can call [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) to query the DC Gateway ID.



**DirectConnectGatewayName ** <span data-label="purple">String </span>`optional` `Example: test`

Name of the DC Gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the name of the DC Gateway.



**Description ** <span data-label="purple">String </span>`optional` `Example: This is a sample description`

Description of the DC Gateway.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not modify this parameter, its original configuration remains. That is, do not modify the description of the DC Gateway.



**EnableIpv6 ** <span data-label="purple">Boolean </span>`orptional` `Example: false`

Specify whether to enable IPv6. Values:


* true: Enable.

* false: Disable.

* If you do not modify this parameter, the original configuration remains.

> If IPv6 is enabled, it cannot be disabled.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifyDirectConnectGatewayAttributes&Version=2020-04-01&DirectConnectGatewayId=dcg-7qthudw0ll6jmc****&DirectConnectGatewayName=test&Description=This is a sample description&EnableIpv6=false HTTP/1.1
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
        "Action": "ModifyDirectConnectGatewayAttributes",
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
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectGateway.InvalidBusinessStatus |The specified direct connect gateway is not in the correct status for the request. The specified direct connect gateway is in freeze. |The specified DC Gateway cannot respond to this request due to its status. The current DC Gateway is frozen. |
|400 |InvalidDirectConnectGateway.DisableIPv6 |The specified direct connect gateway does not support disabling IPv6. |The specified DC Gateway does not support disabling IPv6. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to operate IPv6. |
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
