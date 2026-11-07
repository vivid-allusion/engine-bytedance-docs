---
title: "AssociateInstancesIamRole - Associates IAM roles with instances"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/AssociateInstancesIamRole"
---

Call the AssociateInstancesIamRole operation to associate an IAM role with one or more instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Before you call this operation, you need to have an IAM role with a trusted identity of **ECS**. For more information, see [Role management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-roles-management).

* When you call this operation, you can associate only one IAM role (excluding service\-linked roles) with an ECS instance.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=AssociateInstancesIamRole&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|hm5Cug">必选</span> `Sample value: AssociateInstancesIamRole`

The operation that you want to perform. Valid value: AssociateInstancesIamRole.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|NDIVAP">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**IamRoleName** <span data-label="purple">string</span> <span data-api-tag="require|Z18npt">必选</span> `Sample value: EcsTestRole`

The name of the IAM role that you want to associate with the instance.

You can use [ListRoles](https://docs.byteplus.com/en/docs/byteplus-platform/reference-listroles) to query the IAM roles of instances you have created.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|PMVx7V">必选</span> `Sample value: InstanceIds.1=i-3ti9101aju3vj0******&InstanceIds.2=i-3tiegs1y963vj0******`

The instance ID. A maximum of 100 instance IDs are supported.


* Argument \- N: specifies the serial number of the instance.

* Multiple instance IDs are separated by &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The following <a href="https://docs.byteplus.com/en/docs/49/12902#.6ZSZ6K-v56CB">error code</a> for the operation is displayed only when an invalid value is specified for a request parameter. If valid values are specified for the request parameters, no error code is displayed, and a status code of 200 is returned. However, this does not mean that the operation on all instances is successful. To view the operation result on a single instance, see the information in the following response parameters.</div>




**OperationDetails** <span data-label="purple">object[]</span> `Sample value: --`

The operation details.


**Error** <span data-label="purple">object</span>

The error message for the instance being operated on.


**Code** <span data-label="purple">string</span> `Sample value: InvalidInstance.NotFound`

The error code for the failure of a specific individual request during batch operations. Valid values:


* InvalidInstance.NotFound: The specified instance does not exist.

* FlowLimitExceeded: You have exceeded the rate limit for resource requests.

* LimitExceeded.MaximumIamRoles: The maximum number of IAM roles that can be associated is reached.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>




**Message** <span data-label="purple">string</span> `Sample value: The specified instance does not exist.`

The error information for the failure of a specific request during batch operations. Valid values:


* The specified instance does not exist.

* You've reached the limit on request rate of resources.

* You've reached the limit on the number of IamRoles that can be associated with the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Each <code>Code</code> corresponds to a <code>Message</code> in sequence.</div>





**InstanceId** <span data-label="purple">string</span> `Sample value: i-bp67acfmxazb4p****`

The ID of the instance on which the operation is performed.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=AssociateInstancesIamRole&Version=2020-04-01&InstanceIds.1=i-3tiefmkskq3vj0******&IamRoleName=EcsTestRole HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021110417394001022514606307D7****",
        "Action": "AssociateInstancesIamRole",
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
                "InstanceId": "i-ahipakt2hgg95k5c****",
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


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidCount.Malformed |The specified count is malformed. |The specified parameter Count is invalid. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidArgument |The specified argument is invalid. |The specified parameter is invalid. |
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|404 |InvalidIamRole.NotFound |The specified IAMRoleName does not exist. |The specified IAM role was not found. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
