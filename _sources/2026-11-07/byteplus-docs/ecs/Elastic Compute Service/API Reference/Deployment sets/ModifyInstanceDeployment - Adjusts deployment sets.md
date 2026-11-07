---
title: "ModifyInstanceDeployment - Adjusts deployment sets"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyInstanceDeployment"
---

Call the ModifyInstanceDeployment operation to adjust the deployment set to which an instance belongs. You can add an instance to a specified deployment set, or remove an instance from a deployment set.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

Before you call this API, refer to [Adjusting deployment sets to which instances belong](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview#XpZ3oj5N) to fully understand the relevant precautions and ensure the accuracy and compliance of the operation.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyInstanceDeployment&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|OT2X4X">必选</span> `Sample value: ModifyInstanceDeployment`

The action that you want to perform. Value: ModifyInstanceDeployment.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|7msB07">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DeploymentSetGroupNumber** <span data-label="purple">integer</span> `Optional` `Sample value: 1`

The serial number of the deployment set group. The value range is 1 to 7.

This parameter is required only when `Strategy` is `AvailabilityGroup`.



**DeploymentSetId** <span data-label="purple">string</span> <span data-api-tag="require|EwaTkj">必选</span> `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the target deployment set.


* When an empty string is passed in, the instance is removed from the deployment set.

* You can call [DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) to query the deployment set ID.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|BbNuLc">必选</span> `Sample value: i-3tigy72q3u3vj0x2****`

The instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyInstanceDeployment&Version=2020-04-01&DeploymentSetId=dps-yc1o9aahks5m57nk****&InstanceId=i-3tigy72q3u3vj0x2**** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021062415303301022514515207C4****",
        "Action": "ModifyInstanceDeployment",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |IdempotentParameterMismatch |The request uses the same client token as a previous, but non\-identical request. Do not reuse a client token with different requests, unless the requests are identical. |The idempotent parameters are inconsistent. |
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDedicatedHostInstanceForModifyInstanceDeploymentSet.Unsupported |The specified dedicated host instance does not support modify instance deployment set. |The specified instance deployed on a dedicated host does not support deployment set adjustment. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceTypeForModifyInstanceDeployment.Unsupported |The specified InstanceType does not support modification of deployment set. |The specified instance type does not support deployment set adjustment. |
|400 |InvalidScheduledInstanceForModifyInstanceDeploymentSet.Unsupported |The specified scheduled instance does not support modify instance deployment set. |The specified ESI does not support deployment set adjustment. |
|400 |InvalidStoppedModeForModifyInstanceDeploymentSet.Unsupported |The specified instance of StoppedMode cannot be added to DeploymentSet. |The specified instance in economical mode cannot be added to the deployment set. |
|400 |LimitExceeded.MaximumDeploymentSetInstances |You've reached the limit on the number of instances that can be added to the deployment set. |The number of instances in the specified deployment set exceeds the maximum limit. |
|400 |MissingParameter.DeploymentSetId |The required parameter DeploymentSetId is not supplied. |The deployment set ID cannot be empty. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|404 |InvalidDeploymentSet.NotFound |The specified DeploymentSet does not exist. |The specified deployment set does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|412 |OperationDenied.ResourceLocked |The specified operation is denied as your resource is locked for another operation. |The specified action was rejected because your resource has been locked by other actions. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
