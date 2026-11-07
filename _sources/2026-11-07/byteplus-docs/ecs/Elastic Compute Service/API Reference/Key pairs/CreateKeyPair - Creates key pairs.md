---
title: "CreateKeyPair - Creates key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateKeyPair"
---

Call the CreateKeyPair operation to create a key pair.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* After the key pair is successfully created, the system stores the public key of the key pair for you, and the private key file is automatically downloaded to your local device. The default file name is KeyName.pem. You have only one opportunity to download the private key. BytePlus does not store your private key. Make sure that you keep your private key safe. [Learn more.](https://docs.byteplus.com/en/docs/ecs/Key-pair-overview)

* You can create up to 500 key pairs in the same region.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateKeyPair&groupName=%E5%AF%86%E9%92%A5%E5%AF%B9&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|08nEFG">必选</span> `Sample value: CreateKeyPair`

The action that you want to perform. Value: CreateKeyPair.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|iVLEfk">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: ssh_key_pair description`

The description of the key pair. Default value: empty string.


* It must start with a letter or Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**KeyPairName** <span data-label="purple">string</span> <span data-api-tag="require|ycIPu4">必选</span> `Sample value: ssh_key_pair`

The name of the key pair.


* The name must be unique.

* It must be 2 to 64 characters in length.

* Periods "." are allowed to separate the string into multiple segments, and each segment can contain uppercase or lowercase letters, digits, or hyphens "\-".

* Cannot start or end with "\-" or ".". Hyphens and periods cannot be used consecutively.






**ProjectName** <span data-label="purple">string</span> `Optional` `Sample value: project_a`

The project to which the resource belongs. A resource can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**Tags.N.Key** <span data-label="purple">string[]</span> <span data-api-tag="require|SIXSMx">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The tag key of the user tag.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with ampersands (&).


Naming rules:


* It cannot start with `volc:` or `sys:` in any case form.

* Only language characters, digits, spaces, and English symbols of "_", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value** <span data-label="purple">string[]</span> `Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The tag value of the user tag.


* Argument \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple key values with ampersands (&).


Naming rules:


* Only language characters, digits, spaces, and English symbols of " _", ".", ":", "/", "=", "+", "\-", and "@" are allowed.

* It must be 0 to 256 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**FingerPrint** <span data-label="purple">string</span> `Sample value: kp-ybqcopwrdwl8j1******`

This parameter is generated based on the MD5 message\-digest algorithm in the RFC4716\-defined format for public key fingerprints.



**KeyPairId** <span data-label="purple">string</span> `Sample value: 4158f40dbc0814eb04f0dcac4e******`

The unique ID of the key pair.



**KeyPairName** <span data-label="purple">string</span> `Sample value: ssh_key_pair`

The name of the key pair.



**PrivateKey** <span data-label="purple">string</span> `Sample value: "-----BEGIN RSA PRIVATE KEY-----MIIEogIBAAKCAQEAw7ked3y+qiEoWcGqJB8eK5U+NEzopTrx5zyC4l2QbVc9NFh1x5DQGs5YFvum3EOExdv1RZP1b/+vT4CWaHE7yw8dfYU6WZK/CFFVAsn1855RhPgT******"`

The private key information of the key pair.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateKeyPair&Version=2020-04-01&KeyPairName=ssh_key_pair HTTP/1.1
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
        "Action": "CreateKeyPair",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "KeyPairName": "ssh_key_pair",
        "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\nMIIEogIBAAKCAQEAw7ked3y+qiEoWcGqJB8eK5U+NEzopTrx5zyC4l2QbVc9NFh1\nx5DQGs5YFvum3EOExdv1RZP1b/+vT4CWaHE7yw8dfYU6WZK/CFFVAsn1855RhPgT******",
        "KeyPairId": "kp-ybqcopwrdwl8j1******",
        "FingerPrint": "4158f40dbc0814eb04f0dcac4e******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidKeyPairDescription.Malformed |The specified KeyPairDescription is malformed. |The description of the specified key pair is invalid. |
|400 |InvalidKeyPairName.Malformed |The specified KeyPairName is malformed. |The specified key pair name is invalid. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |LimitExceeded.MaximumKeyPairs |You've reached the limit on the number of KeyPairs that you can create. |The number of key pairs that you create exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |MissingParameter.KeyPairName |The required parameter KeyPairName is not supplied. |The key pair name cannot be empty. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidKeyPairName.Conflict |The specified KeyPairName already exists. |The specified key pair name is not unique. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still being processed. Please try again later. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified action was rejected because your resource has been locked by other actions. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
