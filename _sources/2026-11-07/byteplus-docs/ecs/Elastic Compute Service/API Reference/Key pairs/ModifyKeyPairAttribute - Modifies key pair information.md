---
title: "ModifyKeyPairAttribute - Modifies key pair information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyKeyPairAttribute"
---

Call ModifyKeyPairAttribute to modify the description of a key pair.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyKeyPairAttribute&groupName=%E5%AF%86%E9%92%A5%E5%AF%B9&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|8LSoNm">必选</span> `Sample value: ModifyKeyPairAttribute`

The action that you want to perform. Value: ModifyKeyPairAttribute.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|G6NxjY">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Description** <span data-label="purple">string</span> <span data-api-tag="require|elvB6p">必选</span> `Sample value: ssh_key_pair aaa`

The description of the key pair. Default value: empty string.


* It must start with a letter or a Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.

* When an empty string is passed in, the existing description is cleared.



**KeyPairId** <span data-label="purple">string</span> `Optional` `Sample value: kp-ybqcopwrdwl8j1******`

The unique ID of the key pair. You can call the [DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) interface to query and obtain key pair information.


* The `KeyPairName` and `KeyPairId` parameters cannot both be empty.

* If the `KeyPairName` and `KeyPairId` parameters are configured at the same time, `KeyPairId` takes precedence.



**KeyPairName** <span data-label="purple">string</span> `Optional` `Sample value: ssh_key_pair`

The name of the key pair.


* The `KeyPairName` and `KeyPairId` parameters cannot both be empty.

* If the `KeyPairName` and `KeyPairId` parameters are configured at the same time, `KeyPairId` takes precedence.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**KeyPairName** <span data-label="purple">string</span> `Sample value: ssh_key_pair`

The name of the key pair.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyKeyPairAttribute&Version=2020-04-01&KeyPairName=ssh_key_pair&Description=ssh_key_test_description HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "ModifyKeyPairAttribute",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "KeyPairName": "ssh_key_pair"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |MissingParameter.Description |The required parameter Description is not supplied. |The specified value for parameter Description cannot be empty. |
|400 |InvalidKeyPairDescription.Malformed |The specified KeyPairDescription is malformed. |The specified description of the key pair is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |MissingParameter.KeyPairNameAndKeyPairId |The required parameters KeyPairName and KeyPairId are not supplied. |The key pair name and ID cannot be both empty. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
