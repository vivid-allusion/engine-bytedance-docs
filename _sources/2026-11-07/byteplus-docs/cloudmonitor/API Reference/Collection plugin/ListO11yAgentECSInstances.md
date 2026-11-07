---
title: "ListO11yAgentECSInstances"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstances"
---

Query the collection add\-on list on ECS instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListO11yAgentECSInstances&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListO11yAgentECSInstances&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListO11yAgentECSInstances |The name of the API. The API name is `ListO11yAgentECSInstances`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|InstanceIds |Array of String |Yes |["i\-ye\*\*\*\*\*"] |Instance IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListO11yAgentECSInstances&Version=2018-01-01
Content-Type: application/json
{
    "InstanceIds": [
        ""
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Instances |Array of [InstanceInfo](https://docs.byteplus.com/en/docs/39/76280#instanceinfo) | |ECS instance collection add\-on list |


<span id="instanceinfo"></span>
### InstanceInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Version |String |3.27.1 |Agent version |
|AgentError |String |LoseHeartbeat |Reason for the Agent error. The supported value is LoseHeartbeat, which indicates heartbeat interruption from the collection add\-on. |
|InstanceId |String |i\-3ti9101aju3vj0\*\*\*\*\*\* |Instance ID |
|AgentStatus |String |online |Running status. Enumerated values include online, error, and noinstall. |
|DeployError |String |InstallTimeout |Reason for the deployment error. Possible values:<br><br><br>* InstanceNotRunning: The ECS instance is not running.<br><br>* CloudAssistantNotRunning: The cloud assistant is not running.<br><br>* CloudAssistantNotInstalled: The cloud assistant is not installed.<br><br>* InstallTimeout: Installation timed out.<br><br>* InvalidInstanceType: This instance specification is not supported.<br><br>* InvocationCommandFailed: The cloud assistant job failed to be created.<br><br>* UnSupportSystem: The operating system is not supported. |
|DeployStatus |String |installed |Deployment status. Enumerated values:<br><br><br>* noinstall<br><br>* installing<br><br>* installed<br><br>* install_failed<br><br>* upgrading<br><br>* failed<br><br>* noinstall_cloudassistant<br><br>* install_ignored |
|IsUpgradeable |Boolean |false |Whether the collection add\-on is upgradeable. |
|IsLatestVersion |Boolean |true |Whether it is the latest version. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListO11yAgentECSInstances",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "Version": "3.27.1",
                "AgentError": "LoseHeartbeat",
                "InstanceId": "i-ye*****",
                "AgentStatus": "online",
                "DeployError": "InstallTimeout",
                "DeployStatus": "installed",
                "IsUpgradeable": true,
                "IsLatestVersion": true
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
