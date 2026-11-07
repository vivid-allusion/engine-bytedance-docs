---
title: "ListO11yAgentVpcEndpoints"
product: "Cloud Monitor"
product_code: "cloudmonitor"
source: "https://docs.byteplus.com/en/docs/cloudmonitor/ListO11yAgentVpcEndpoints"
---

Obtain the list of endpoints associated with the O11yAgent Service.

<span id=".6K-35rGC6K-05piO"></span>
## Request descriptions

Cloud Monitor is deployed across multiple regions worldwide to deliver more stable and low\-latency access. You can refer to the [Service addresses](https://docs.byteplus.com/en/docs/cloudmonitor/Service_address) topic to choose an access point that is optimal for the region of your services.


* Request method: POST

* Request URL: https://cloudmonitor.cn\-beijing.byteplusapi.com.cn?Action=ListO11yAgentVpcEndpoints&Version=2018\-01\-01


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=ListO11yAgentVpcEndpoints&serviceCode=cloudmonitor&version=2018-01-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameters** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListO11yAgentVpcEndpoints |The name of the API. The API name is `ListO11yAgentVpcEndpoints`. |
|Version |String |Yes |2018\-01\-01 |The API version. The current API version is `2018-01-01`. |
|PageNumber |Integer |No |1 |Page number. The starting value is 1, and the default value is 1. |
|PageSize |Integer |No |10 |Page size. The default value is 10 and the maximum value is 100. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://cloudmonitor.cn-beijing.byteplusapi.com.cn?Action=ListO11yAgentVpcEndpoints&Version=2018-01-01
Content-Type: application/json
{
    "PageNumber": 1,
    "PageSize": 10
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|TotalCount |Long |1 |Total count. |
|Endpoints |Array of [VpcEndpoint](https://docs.byteplus.com/en/docs/39/76282#vpcendpoint) |\- |A list of endpoints. |


<span id="vpcendpoint"></span>
### VpcEndpoint


|**Parameters** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|VpcId |String |vpc\-2bzq\*\*\*\*\*pm22 |VPC ID. |
|Status |String |Available |Endpoint status. Enumerated values:<br><br><br>* Available<br><br>* Unavailable<br><br>* Unrelated |
|VpcName |String |vpc\-1 |VPC name. |
|ServiceId |String |epsvc\-2fe6\*\*\*\*rkl37k5gfuy33\*\*\*\* |Service ID. |
|EndpointId |String |ep\-273yuq\*\*\*\*gn47fap8squ\*\*\*\* |Endpoint ID. |
|ServiceName |String |com.volces.o11yagent.cn\-guangzhou.epsvc\-2fe630gur\*\*\*\*k5gfuy33\*\*\*\* |Service name. |
|EndpointName |String |endpoint\-01 |Endpoint name. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListO11yAgentVpcEndpoints",
        "Version": "2018-01-01",
        "Service": "cloudmonitor",
        "Region": "cn-beijing"
    },
    "Result": {
        "TotalCount": 1,
        "Endpoints": [
            {
                "VpcId": "vpc-2bzq*****pm22",
                "Status": "Available",
                "VpcName": "vpc-1",
                "ServiceId": "epsvc-2fe630gurkl37k5gfuy33****",
                "EndpointId": "ep-273yuq6q7bgn47fap8squ****",
                "ServiceName": "com.volces.o11yagent.cn-guangzhou.epsvc-2fe630gurkl37k5gfuy33****",
                "EndpointName": "endpoint-01"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There are no error codes specific to this API. For more information, see [Error codes](https://docs.byteplus.com/en/docs/cloudmonitor/Common-error-codes).
