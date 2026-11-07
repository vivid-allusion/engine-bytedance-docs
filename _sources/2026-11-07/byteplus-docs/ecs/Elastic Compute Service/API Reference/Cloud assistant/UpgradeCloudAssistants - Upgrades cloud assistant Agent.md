---
title: "UpgradeCloudAssistants - Upgrades cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/UpgradeCloudAssistants_-_Upgrade_Cloud_assistant_Agent"
---

Call the UpgradeCloudAssistants operation to upgrade the cloud assistant Agent installed in ECS instances to the latest version.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UpgradeCloudAssistants&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|14u913">必选</span> `Sample value: UpgradeCloudAssistants`

The action that you want to perform. Value: UpgradeCloudAssistants.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|fBmO9o">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|Uiplzj">必选</span> `Sample value: InstanceIds.1=i-ervasv*****&InstanceIds.2=i-uihrdgh*****`

The instance ID. Up to 50 instance IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Multiple instance IDs are separated by &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**UpgradingInstanceIds** <span data-label="purple">string[]</span> `Sample value: \["i-ycm4ru8\*\*\*\*" \]`

The ID list of instances for which upgrade requests are successfully submitted.



**FailedInstances** <span data-label="purple">object[]</span> `Sample value: --`

Information about the instance that failed to upgrade and meets the specified conditions.


**Id** <span data-label="purple">string</span> `Sample value: i-yci89z1gpml8j1\*\*\*\*`

The ID of the instance for which the installation fails.



**ErrorMessage** <span data-label="purple">string</span> `Sample value: --`

The failure information.


&nbsp;


**Id** <span data-label="purple">string</span> `Sample value: i-yci89z1gpml8j1\*\*\*\*`

The ID of the instance for which the installation fails.



**ErrorMessage** <span data-label="purple">string</span> `Sample value: --`

The failure information.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UpgradeCloudAssistants&Version=2020-04-01&IntanceIds.1=i-ervasv***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308301A86D*******",
        "Action": "UpgradingCloudAssistants",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "UpgradingInstanceIds": [
            "i-ervasv*****"
        ],
        "FailedInstances": []
    }
}
```


&nbsp;

```json
{
    "ResponseMetadata": {
        "RequestId": "202308301A86D*******",
        "Action": "UpgradingCloudAssistants",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "UpgradingInstanceIds": [
            "i-ervasv*****"
        ],
        "FailedInstances": []
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
