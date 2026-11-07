---
title: "DeleteDeploymentSet - Deletes a deployment sets"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DeleteDeploymentSet"
---

Call the DeleteDeploymentSet operation to delete a deployment set.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes

A deployment set can be deleted only when there are no instances in the deployment set.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeleteDeploymentSet&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|gBkqSW">必选</span> `Sample value: DeleteDeploymentSet`

The action that you want to perform. Value: DeleteDeploymentSet.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|Bc534N">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DeploymentSetId** <span data-label="purple">string</span> <span data-api-tag="require|8J6tLB">必选</span> `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set.

You can call [DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) to query deployment set IDs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DeleteDeploymentSet&Version=2020-04-01&DeploymentSetId=dps-yc1o9aahks5m57nk**** HTTP/1.1
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
        "Action": "DeleteDeploymentSet",
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
|400 |MissingParameter.DeploymentSetId |The required parameter DeploymentSetId is not supplied. |The deployment set ID cannot be empty. |
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|404 |InvalidDeploymentSet.NotFound |The specified DeploymentSet does not exist. |The specified deployment set does not exist. |
|412 |InvalidDeploymentSet.InUse |The specified DeploymentSet is in use. |An instance in the specified deployment set is being used. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Please try again. If multiple attempts fail, submit a ticket. |
