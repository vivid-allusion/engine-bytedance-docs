---
title: "GetO11yAgentECSAutoInstall"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/GetO11yAgentECSAutoInstall"
---

Query whether automatic installation of the collection add\-on is enabled for newly purchased ECS instances.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=GetO11yAgentECSAutoInstall&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetO11yAgentECSAutoInstall&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetO11yAgentECSAutoInstall |The name of the API. The API name is `GetO11yAgentECSAutoInstall`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=GetO11yAgentECSAutoInstall&Version=2018-01-01
Content-Type: application/json
{}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Enable |Boolean |false |Whether automatic installation is enabled. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetO11yAgentECSAutoInstall",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Enable": false
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
