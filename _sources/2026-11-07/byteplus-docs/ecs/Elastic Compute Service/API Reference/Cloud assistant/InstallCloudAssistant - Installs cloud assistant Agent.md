---
title: "InstallCloudAssistant - Installs cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/InstallCloudAssistant_-_Install_Cloud_assistant_Agent"
---

Call the InstallCloudAssistant operation to install the cloud assistant Agent for one or multiple specified ECS instances.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

After installing the cloud assistant Agent by calling this operation, you need to call the [RebootInstances](https://docs.byteplus.com/en/docs/ecs/RebootInstances) operation to restart the instance. Then, the Agent can take effect.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=InstallCloudAssistant&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|p9AMzH">必选</span> `Sample value: InstallCloudAssistant`

The action that you want to perform. Value: InstallCloudAssistant.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|0Mgrle">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|D5AlzL">必选</span> `Sample value: InstanceIds.1=i-ervasv*****&InstanceIds.2=i-uihrdgh*****`

The instance ID. Up to 50 instance IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with &.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstallingInstanceIds** <span data-label="purple">string[]</span> `Sample value: \["i-ycm4ru8\*\*\*\*","iyclwwbhbls\*\*\*\*" \]`

The ID of an instance for which the Agent installation request is submitted.



**FailedInstances** <span data-label="purple">object[]</span> `Sample value: --`

The information about the instance for which the installation failed, and that meets the condition.


**Id** <span data-label="purple">string</span> `Sample value: i-yci89z1gpml8j1\*\*\*\*`

The ID of the instance for which the installation fails.



**ErrorMessage** <span data-label="purple">string</span> `Sample value: --`

The failure information.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Version=2020-04-01&Action=InstallCloudAssistant&=InstanceIds.1=i-ervasv***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308301A86D*******",
        "Action": "InstallCloudAssistant",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstallingInstanceIds": [
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
|400 |MissingParameter.AccountId |The required parameter AccountId is not supplied. |The user ID cannot be empty. |
|400 |MissingParameter.InstanceIds |The required parameter InstanceIds is not supplied. |The instance ID cannot be empty. |
|400 |LimitExceeded.MaximumInstanceIds |The specified InstanceIds exceeds the limit. |The number of instances exceeds the limit. |
|400 |InvalidInstanceIds.Conflict |InvalidInstanceIds.Conflict |Duplicate instance IDs are passed in |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
