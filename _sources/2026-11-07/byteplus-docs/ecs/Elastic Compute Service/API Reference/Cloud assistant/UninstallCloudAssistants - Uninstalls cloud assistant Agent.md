---
title: "UninstallCloudAssistants - Uninstalls cloud assistant Agent"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/UninstallCloudAssistants_-_Uninstall_Cloud_assistant_Agent"
---

Call the UninstallCloudAssistants operation to uninstall the cloud assistant Agent from ECS instances.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=UninstallCloudAssistants&groupName=%E4%BA%91%E5%8A%A9%E6%89%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|q3nUev">必选</span> `Sample value: UninstallCloudAssistants`

The action that you want to perform. Value: UninstallCloudAssistants.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|Cz2uyN">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceIds.N** <span data-label="purple">string[]</span> <span data-api-tag="require|qgefSF">必选</span> `Sample value: InstanceIds.1=i-ervasv*****&InstanceIds.2=i-uihrdgh*****`

The instance ID. Up to 50 instance IDs are supported. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query and obtain the instance ID.


* Argument \- N: specifies the serial number of the instance.

* Separate multiple instance IDs with ampersands (&).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**UninstallingInstanceIds** <span data-label="purple">string[]</span> `Sample value: \["i-ycm4ru8\*\*\*\*","i-yclwwbhblsggsw5\*\*\*\*" \]`

The ID list of instances for which uninstallation requests are successfully submitted.



**FailedInstances** <span data-label="purple">object[]</span> `Sample value: --`

The information about instances that meet the conditions and for which uninstallation failed.


**Id** <span data-label="purple">string</span> `Sample value: i-yci89z1gpml8j1\*\*\*\*`

The ID of the instance for which the installation fails.



**ErrorMessage** <span data-label="purple">string</span> `Sample value: --`

The failure information.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=UninstallCloudAssistants&Version=2020-04-01&IntanceIds.1=i-ervasv***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id="B3xCXQpu"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202308301A86D*******",
        "Action": "UninstallCloudAssistants",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "UninstallingInstanceIds": [
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
