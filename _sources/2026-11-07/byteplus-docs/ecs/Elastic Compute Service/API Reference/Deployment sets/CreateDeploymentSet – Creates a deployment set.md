---
title: "CreateDeploymentSet – Creates a deployment set"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/CreateDeploymentSet"
---

Call the CreateDeploymentSet operation to create a deployment set.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

For the policies, precautions, and operation instructions of deployment sets, refer to [Managing deployment sets](https://docs.byteplus.com/en/docs/ecs/Deployment-set-overview).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

When you call this operation, if you do not pass in optional parameters, the original configuration is retained.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateDeploymentSet&groupName=%E9%83%A8%E7%BD%B2%E9%9B%86&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|TkWtry">必选</span> `Sample value: CreateDeploymentSet`

The action that you want to perform. Value: CreateDeploymentSet.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|subccr">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**ClientToken** <span data-label="purple">string</span> `Optional` `Sample value: 333456899ff****`

The ClientToken is used to ensure the request idempotency. You can use the client to automatically generate a token, but you must make sure that the token is unique among different requests. This prevents repeated actions due to multiple client retries when the call of the API action times out or an internal server error occurs.

Value: Only ASCII characters are supported. The length is no more than 64 ASCII characters.



**DeploymentSetName** <span data-label="purple">string</span> <span data-api-tag="require|RX0B6h">必选</span> `Sample value: testDeploymentSetName`

The name of the deployment set.


* Cannot start with a number, a hyphen (\-), or an underscore (_).

* Only Chinese characters, letters, numbers, underscores, and hyphens are allowed.

* The length limit is 1 to 128 characters.



**Description** <span data-label="purple">string</span> `Optional` `Sample value: testDescription`

The description of the deployment set.


* It must start with a letter or Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When an empty string is passed in, the existing description is cleared.</div>




**Granularity** <span data-label="purple">string</span> `Optional` `Sample value: host`

The deployment granularity. Valid values:


* host: physical machine

* rack: rack

* switch: switch



**GroupCount** <span data-label="purple">integer</span> `Optional` `Sample value: 3`

Set the number of availability groups.


* Value range: 1–7.

* Default value: 7


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When the value of <code>Strategy</code> is <code>AvailabilityGroup</code>, this parameter is required.</div>




**Strategy** <span data-label="purple">string</span> `Optional` `Sample value: Availability`

The deployment policy. Valid values:


* Availability (default): Availability policy.

* AvailabilityGroup: Availability Group policy.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DeploymentSetId** <span data-label="purple">string</span> `Sample value: dps-yc1o9aahks5m57nk****`

The ID of the deployment set.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateDeploymentSet&Version=2020-04-01&DeploymentSetName=testDeploymentSetName&Strategy=Availability&Granularity=host HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2021110417394001022514606307*****",
        "Action": "CreateDeploymentSet",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "DeploymentSetId": "dps-yc1o9aahks5m57nk****"
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
|400 |InvalidDeploymentSetDescription.Malformed |The specified deployment set description is malformed. |The specified deployment set description is invalid. |
|400 |InvalidDeploymentSetGranularity.Malformed |The specified deployment set granularity is malformed. |The specified deployment set granularity is invalid. |
|400 |InvalidDeploymentSetName.Malformed |The specified DeploymentSetName is malformed. |The specified deployment set name is invalid. |
|400 |InvalidDeploymentSetStrategy.Malformed |The specified deployment set strategy is malformed. |The specified deployment set policy is invalid. |
|412 |IdempotentProcessing |The request uses the same client token as a previous one that is still in process. |The previous idempotent request is still in process. Please try again later. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
