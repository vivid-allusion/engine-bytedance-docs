---
title: "ModifyDeploymentSetAttribute - Modifies deployment set information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/ModifyDeploymentSetAttribute"
---

Call the ModifyDeploymentSetAttribute operation to modify the name and description of a deployment set.

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ModifyDeploymentSetAttribute&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|NCMapk">必选</span> `Sample value: ModifyDeploymentSetAttribute`

The action that you want to perform. Value: ModifyDeploymentSetAttribute.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|7AeRcP">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. The client can automatically generate a token, but you need to ensure that it is unique across requests. This prevents duplicate operations caused by multiple retries when the API request times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DeploymentSetId** <span data-label="purple">string</span> <span data-api-tag="require|5UNkd5">必选</span> `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set.

You can call [DescribeDeploymentSets](https://docs.byteplus.com/en/docs/ecs/DescribeDeploymentSets) to query deployment set IDs.



**DeploymentSetName** <span data-label="purple">string</span> `Optional` `Sample value: testDeploymentSet`

The name of the deployment set.


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese characters, letters, numbers, underscores, and hyphens are allowed.

* The length limit is 1 to 128 characters.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: testDescription`

The description of the deployment set.


* Start with a letter or Chinese character only.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an empty string is passed in, the existing description is cleared.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This operation has no specific response parameters. For more information, refer to [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=ModifyDeploymentSetAttribute&Version=2020-04-01&DeploymentSetId=dps-yc1o9aahks5m57nk****&DeploymentSetName=testDeploymentSet HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


&nbsp;

```text
GET /?Action=ModifyDeploymentSetAttribute&Version=2020-04-01&DeploymentSetId=dps-yc1o9aahks5m57nk****&DeploymentSetName=testDeploymentSet HTTP/1.1
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
        "Action": "ModifyDeploymentSetAttribute",
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
|400 |InvalidClientToken.Malformed |The specified ClientToken is malformed. |The specified ClientToken is invalid. |
|400 |InvalidDeploymentSetDescription.Malformed |The specified deployment set description is malformed. |The specified deployment set description is invalid. |
|400 |InvalidDeploymentSetName.Malformed |The specified DeploymentSetName is malformed. |The specified deployment set name is invalid. |
|400 |MissingParameter.DeploymentSetId |The required parameter DeploymentSetId is not supplied. |The deployment set ID cannot be empty. |
|404 |InvalidDeploymentSet.NotFound |The specified DeploymentSet does not exist. |The specified deployment set does not exist. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
