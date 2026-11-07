---
title: "DescribeHpcInstancePosition - Queries network location of an HPC instance"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeHpcInstancePosition"
---

Call the DescribeHpcInstancePosition operation to query the location of an HPC\-optimized instance in the RDMA network.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeHpcInstancePosition&groupName=%E9%AB%98%E6%80%A7%E8%83%BD%E8%AE%A1%E7%AE%97%E9%9B%86%E7%BE%A4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|FYGhej">必选</span> `Sample value: DescribeHpcInstancePosition`

The action that you want to perform. Value: DescribeHpcInstancePosition.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|8iybFz">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|3tbFHM">必选</span> `Sample value: i-ybn5lkhxa*******`

The ID of the HPC\-optimized instance.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**HpcInstancePositionInfos** <span data-label="purple">object[]</span> `Sample value: --`

The RDMA network location of the HPC\-optimized instance that meets the condition.


**InstanceId** <span data-label="purple">string</span> `Sample value: i-ybn5lkhxa*******`

The ID of the HPC\-optimized instance.



**RdmaMinipod** <span data-label="purple">string</span> `Sample value: 1c6d7fa******`

The hash value of the Minipod associated with the HPC\-optimized instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the same Minipod, the hash value returned by <code>RdmaMinipod</code> varies based on the specified account ID.</div>




**SwitchName** <span data-label="purple">string</span> `Sample value: febd30c******`

The hash value of the uplink switch.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the same switch, the hash value varies based on the specific value of AccountId.</div>





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeHpcInstancePosition&InstanceId=i-ybn5lkhxa*******&Version=2020-04-01 HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn 
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202206011341030102121020921F******",
        "Action": "DescribeHpcInstancePosition",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "HpcInstancePositionInfos":[
            {
                "InstanceId":"i-ybn5lkhxa*******",
                "SwitchName":"febd30c1e4******",
                "RdmaMinipod": "1c6d7fa******"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MissingParameter.Instance |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
