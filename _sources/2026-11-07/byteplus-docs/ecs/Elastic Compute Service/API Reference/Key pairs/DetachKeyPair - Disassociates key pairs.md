---
title: "DetachKeyPair - Disassociates key pairs"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DetachKeyPair"
---

Call the DetachKeyPair operation to disassociate a key pair from one or more Linux instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* You can disassociate a key pair from an instance only when the instance has the password plugin installed. Please [install the password plugin](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in) first.

* Currently, you can disassociate a key pair from an instance only when the instance is in the **Running** or **Stopped** status.

* After a key pair is disassociated from an instance, it is no longer valid in that instance. If the instance supports password login, you can still log in with your password after disassociation. Otherwise, you need to re\-associate a key pair or reset the password to log in again. Proceed with caution.

* After you disassociate the key pair, you need to restart the instances for the new settings to take effect.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DetachKeyPair&groupName=%E5%AF%86%E9%92%A5%E5%AF%B9&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For details, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|LO8b8V">必选</span> `Sample value: DetachKeyPair`

The action that you want to perform. Value: DetachKeyPair.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|yMYd3E">必选</span>  ` Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken ** <span data-label="purple">string </span>`Optional` `Sample value: 333456899ff****`

ClientToken is used to ensure the idempotency of the request. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**InstanceIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|Yx1PjS">必选</span> `Sample value: InstanceIds.1=i-ahipakt2gcg95jpv****&InstanceIds.2=i-ahipakt2gdg95lbe****`

The instance ID. A maximum of 100 instance IDs are supported.


* Parameter \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with ampersands (&).



**KeyPairId ** <span data-label="purple">string </span>`Optional` `Sample value: kp-ybqcopwrdwl8j1******`

The unique ID of the key pair. You can call the [DescribeKeyPairs](https://docs.byteplus.com/en/docs/ecs/DescribeKeyPairs) operation to query and obtain it.


* The` KeyPairName `and` KeyPairId `parameters cannot both be empty.

* If the `KeyPairName` and `KeyPairId` parameters are configured at the same time, `KeyPairId` takes precedence.



**KeyPairName ** <span data-label="purple">string </span>`Optional` `Sample value: ssh_key_pair`

The name of the key pair.


* The` KeyPairName `and` KeyPairId `parameters cannot both be empty.

* If the `KeyPairName` and `KeyPairId` parameters are configured at the same time, `KeyPairId` takes precedence.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, please refer to [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following<a href="https://docs.byteplus.com/en/docs/49/12948#.6ZSZ6K-v56CB"> error codes </a>for the operation are returned only when you specify invalid request parameter values. If you specify valid request parameter values, no error code is displayed, and status code 200 is returned. However, this does not mean all key pairs are successfully operated on. To check the operation result of one key pair, refer to the following response parameters.</div>




**OperationDetails ** <span data-label="purple">object[] </span>`Sample value: --`

The operation details.


**Error ** <span data-label="purple">object </span>`Sample value: --`

The error message for the key pair being operated on.


**Code ** <span data-label="purple">string </span>`Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific request during batch operations. Valid values:


* InvalidInstance.NotFound: The specified instance does not exist.

* InvalidKeyPairForWindows.Unsupported: The specified instance is based on the Windows operating system and does not support key pairs.

* InvalidResetAuthenticationAgent.NotFound: The specified reset\-authentication plug\-in does not exist.

* InvalidInstanceStatus: The current status of the instance does not support this operation.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message ** <span data-label="purple">string </span>`Sample value: The specified instance does not exist.`

The error information for the failure of a specific request during batch operations. Valid values:


* The specified instance does not exist.

* The OSType of this specified instance is Windows, which does not support key pairs.

* The specified reset\-authentication agent does not install on the instance.

* The status of the specified instance does not support this request.

* You've reached the limit on request rate of resources.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**InstanceId ** <span data-label="purple">string </span>`Sample value: i-ybo349sxoncm9t******`

The ID of the instance on which the operation is performed.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DetachKeyPair&Version=2020-04-01&KeyPairName=ssh_key_pair1&InstanceIds.1=i-ahipakt2gcg95jpv****&InstanceIds.2=i-ahipakt2gdg95lbe**** HTTP/1.1
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
        "Action": "DetachKeyPair",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "OperationDetails": [
            {
                "InstanceId": "i-ahipakt2gcg95jpv****",
                "Error": null
            },
            {
                "InstanceId": "i-ahipakt2gdg95lbe****",
                "Error": {
                    "Code": "InvalidInstance.NotFound",
                    "Message": "The specified instance does not exist."
                }
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |LimitExceeded.MaximumInstanceIds |You've reached the limit on the number of InstanceIds that you can set. |The specified number of instance IDs exceeds the upper limit. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be left empty. |
|400 |MissingParameter.KeyPairNameAndKeyPairId |The required parameters KeyPairName and KeyPairId are not supplied. |The key pair name and ID can not be both empty. |
|404 |InvalidKeyPair.NotFound |The specified KeyPair does not exist. |The specified key pair does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
