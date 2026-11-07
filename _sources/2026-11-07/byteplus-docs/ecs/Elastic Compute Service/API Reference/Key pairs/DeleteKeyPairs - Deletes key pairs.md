---
title: "DeleteKeyPairs - Deletes key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteKeyPairs"
---

Call the DeleteKeyPairs operation to delete one or multiple key pairs.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

You cannot delete key pairs associated with instances. If you want to delete a key pair associated with one or more instances, disassociate it first via the [DetachKeyPair](https://docs.byteplus.com/en/docs/ecs/DetachKeyPair) operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteKeyPairs&groupName=%E5%AF%86%E9%92%A5%E5%AF%B9&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|rOb3IF">必选</span> `Sample value: DeleteKeyPairs`

The action that you want to perform. Value: DeleteKeyPairs.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|yNv7wx">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**KeyPairNames.N** <span data-label="purple">string[]</span> <span data-api-tag="require|7JuPdi">必选</span> `Sample value: KeyPairNames.1=ssh_key_pair1&KeyPairNames.2=ssh_key_pair2`

The key pair name. A maximum of 100 key pair names are supported.


* Argument \- N: specifies the serial number of the key pair.

* Separate multiple key pairs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response?lang=en).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/49/12943#.6ZSZ6K-v56CB">error codes</a> for the operation are returned only when invalid values are specified for request parameters. If valid values are specified for the request parameters, no error code is displayed, and a status code of 200 is returned. However, this does not mean that the operation on all key pairs is successful. To view the operation result on one key pair, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span> `Sample value: --`

The error message for the key pair being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidKeyPair.NotFound`

The error code for the failure of a specific individual request during batch operations. Valid values:


* MissingParameter.KeyPairName: The key pair name cannot be empty.

* InvalidKeyPair.NotFound: The specified key pair does not exist.

* InvalidKeyPair.InUse: The specified key pair is currently in use.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified KeyPair does not exist.`

The error information for the failure of a specific individual request during batch operations. Valid values:


* The required parameter KeyPairName is not supplied.

* The specified KeyPair does not exist.

* The specified KeyPair is in use.

* You've reached the limit on request rate of resources.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**KeyPairName** <span data-label="purple">string</span> `Sample value: ssh_key_pair1`

The name of the operated key pair.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteKeyPairs&Version=2020-04-01&KeyPairNames.1=ssh_key_pair1&KeyPairNames.2=ssh_key_pair2 HTTP/1.1
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
        "Action": "DeleteKeyPairs",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "KeyPairName": "ssh_key_pair1",
                "Error": null
            },
            {
                "KeyPairName": "ssh_key_pair2",
                "Error": {
                    "Code": "InvalidKeyPair.NotFound",
                    "Message": "The specified KeyPair does not exist."
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumKeyPairNames |You've reached the limit on the number of KeyPairNames that you can set. |The number of specified key pair names exceeds the upper limit. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |MissingParameter.KeyPairNames |The required parameter KeyPairNames is not supplied. |The key pair name cannot be empty. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Request rate of resources exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
