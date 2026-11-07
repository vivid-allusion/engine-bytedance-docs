---
title: "GetConsoleOutput - Obtains command-line output"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/GetConsoleOutput"
---

Call the GetConsoleOutput API to retrieve the system command\-line output at the latest start, restart, or shutdown of an instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes

When you cannot access a display device for the ECS instance or capture screenshots of the instance, you can call this operation to obtain the latest system command\-line output, up to 64 KB in size.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Windows instances currently do not support this feature.

* Elastic Bare Metal (EBM) instances currently do not support this feature.

* This API action is only applicable to instances in the **Running** state.

* This operation has a request limit in frequency. The recommended interval between requests is around 10s to avoid exceeding the operation frequency limit.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=GetConsoleOutput&groupName=%E8%BF%90%E7%BB%B4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|LDN094">必选</span> `Sample value: GetConsoleOutput`

The action that you want to perform. Value: GetConsoleOutput.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|2fpM3i">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|xlcCki">必选</span> `Sample value: i-3tiefmkskq3vj0******`

The instance ID. To query the instance ID, call the [DescribeInstances operation](https://docs.byteplus.com/en/docs/ecs/DescribeInstances).



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId** <span data-label="purple">string</span> `Sample value: i-3tiefmkskq3vj0******`

Instance ID



**LastUpdateAt** <span data-label="purple">string</span> `Sample value: 2017-12-08T00:00:00.00Z`

The update time of the latest Console output.



**Output** <span data-label="purple">string</span> `Sample value: WzUg3NzY5LjgxMjQ4NF0gUlNQOiAwMDJiOjAwMDAwMGMwMD*******`

The Base64\-encoded output of the system command line in the instance.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=GetConsoleOutput&Version=2020-04-01&InstanceId=i-3tiefmkskq3vj0****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
ServiceName: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "GetConsoleOutput",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "i-3tiefmkskq3vj0******",
        "LastUpdateAt": "2017-12-08T00:00:00.00Z",
        "Output": "WzUg3NzY5LjgxMjQ4NF0gUlNQOiAwMDJiOjAwMDAwMGMwMD*******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceTypeForGetConsoleOutput.Unsupported |The specified InstanceType does not support get instance console output. |The specified instance type does not support obtaining instance console output. |
|400 |InvalidOperationForWindows.Unsupported |The OSType of this specified instance is Windows, which does not support the operation. |The specified instance is based on the Windows operating system and does not support this operation. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Request rate of resources exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
