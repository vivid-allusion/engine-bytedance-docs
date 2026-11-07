---
title: "ListO11yAgentECSInstanceMetadata"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentECSInstanceMetadata"
---

Query metadata of the ECS instance collection add\-on.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListO11yAgentECSInstanceMetadata&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListO11yAgentECSInstanceMetadata&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListO11yAgentECSInstanceMetadata |The API name. The API name is `ListO11yAgentECSInstanceMetadata`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|InstanceIds |Array of String |Yes |["i\-ye\*\*\*\*\*"] |Instance IDs. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListO11yAgentECSInstanceMetadata&Version=2018-01-01
Content-Type: application/json
{
    "InstanceIds": [
        "i-ye*****"
    ]
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Instances |Array of [InstanceMetadataInfo](https://docs.byteplus.com/en/docs/39/76284#instancemetadatainfo) |\- |Instance metadata. |


<span id="instancemetadatainfo"></span>
### InstanceMetadataInfo


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|InstanceId |String |i\-3ti9101aju3vj0\*\*\*\*\*\* |Instance ID. |
|MetricPrecision |String |10s |Metric precision supported by the instance, for example, 10s or 30s. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListO11yAgentECSInstanceMetadata",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "Instances": [
            {
                "InstanceId": "i-ye*****",
                "MetricPrecision": "10s"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
