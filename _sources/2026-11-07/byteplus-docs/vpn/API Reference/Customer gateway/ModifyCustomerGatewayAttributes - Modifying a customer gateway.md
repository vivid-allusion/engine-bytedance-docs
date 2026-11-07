---
title: "ModifyCustomerGatewayAttributes - Modifying a customer gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/ModifyCustomerGatewayAttributes"
---

Call ModifyCustomerGatewayAttributes to modify the name and description of a specified customer gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifyCustomerGatewayAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|ZSMPvE">必选</span> Example: `ModifyCustomerGatewayAttributes`

The action that you want to perform. Value: ModifyCustomerGatewayAttributes.



**Version ** `String` <span data-api-tag="require|sHHMlx">必选</span> Example: `2020-04-01`

The API version.



**CustomerGatewayId ** `String` <span data-api-tag="require|gOJShA">必选</span> Example: `cgw-3tehy13n2l4c6c0v****`

ID of the customer gateway instance. You can call [DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) to query the customer gateway ID.



**CustomerGatewayName ** `String` `optional` Example: `CGW-q04n`

Name of the customer gateway instance.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters in length.

* If left blank, the original configuration remains.



**Description ** `String` `optional` Example: `This is a sample description`

Description of the customer gateway instance.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If left blank, the original configuration remains.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `202203211611080102121461940900****`

Request ID.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=ModifyCustomerGatewayAttributes&Version=2020-04-01&CustomerGatewayId=cgw-2d670j2o9lc0058ozfddg****&CustomerGatewayName=test&Description=test HTTP/1.1
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
        "Action": "ModifyCustomerGatewayAttributes",
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
|400 |InvalidName.Malformed |The specified name is malformed.Ensure the maximum length of name is 128. |The format specified for the name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format specified for the name is invalid. Correct the name format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed.Ensure the maximum length of description is 255. |The format specified for the description is invalid. A description must not exceed 255 characters. |
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format specified for the description is invalid. Correct the description format and retry. |
|400 |InvalidCustomerGateway.InvalidStatus |The specified customer gateway is not in the correct status for the request. |The specified customer gateway cannot respond to this request due to its status. |
|404 |InvalidCustomerGateway.NotFound |The specified customer gateway does not exist. |The specified customer gateway does not exist. |
