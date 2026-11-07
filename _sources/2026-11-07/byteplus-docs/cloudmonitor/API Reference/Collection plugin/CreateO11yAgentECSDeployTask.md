---
title: "CreateO11yAgentECSDeployTask"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/CreateO11yAgentECSDeployTask"
---

Create an installation or upgrade task for the ECS instance collection add\-on.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=CreateO11yAgentECSDeployTask&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateO11yAgentECSDeployTask&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |CreateO11yAgentECSDeployTask |The name of the API. The API name is `CreateO11yAgentECSDeployTask`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|TaskType |String |Yes |install |Task type. Supported enumerated values include upgrade and install. |
|Filter |Object of [InstanceFilter](https://docs.byteplus.com/en/docs/39/76285#instancefilter) |Yes |\- |Filter. |


<span id="instancefilter"></span>
### InstanceFilter


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|SelectAll |Boolean |Yes |false |Whether to select all. |
|InstanceIds |Array of String |No |["i\-3ti9101aju3vj0\*\*\*\*\*\*"] |Instance IDs. This field is valid if SelectAll is set to false. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=CreateO11yAgentECSDeployTask&Version=2018-01-01
Content-Type: application/json
{
    "TaskType": "install",
    "Filter": {
        "SelectAll": true,
        "InstanceIds": [
            ""
        ]
    }
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

None

<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateO11yAgentECSDeployTask",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
