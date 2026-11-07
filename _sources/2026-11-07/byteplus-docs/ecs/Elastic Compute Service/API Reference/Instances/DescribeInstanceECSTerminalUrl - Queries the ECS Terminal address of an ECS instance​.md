---
title: "DescribeInstanceECSTerminalUrl - Queries the ECS Terminal address of an ECS instance​"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstanceECSTerminalUrl"
---

Call the DescribeInstanceECSTerminalUrl operation to query the ECS Terminal address of an ECS instance.

<span id=".5L2_55So6K-05piO"></span>
## Usage notes


* You can also call [DescribeInstanceVncUrl](https://docs.byteplus.com/en/docs/ecs/DescribeInstanceVncUrl) to obtain the VNC management terminal address of an ECS instance, and then use VNC to log in to the instance.

* Compared with VNC, the ECS Terminal supports remote connections to the same instance by multiple operating system users, enables text copying and pasting, and allows visual browsing of system file resources. This makes the ECS Terminal more efficient and convenient than VNC. For more information, see [Using the console to log in to a Linux instance](https://docs.byteplus.com/en/docs/ecs/Using-the-console-to-log-on-to-a-Linux-instance).


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceECSTerminalUrl&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|GMtVsv">必选</span> `Sample value: DescribeInstanceECSTerminalUrl`

The operation that you want to perform. Valid value: DescribeInstanceECSTerminalUrl.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|BRv7dw">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|wKddyJ">必选</span> `Sample value: i-3tiefmkskq3vj0******`

Instance ID



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**EcsTerminalUrl** <span data-label="purple">string</span> `Sample value: wss://cn-beijing-a01-vncproxy-ecs.volcengine.com:443/instance/login/18a948b9-00bd-4e56-b2a2-5de5f*******`

The URL of the ECS Terminal.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstanceECSTerminalUrl&Version=2020-04-01&InstanceId=i-3tiefmkskq3vj0****** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202106111445100102252431000052****",
        "Action": "DescribeInstanceECSTerminalUrl",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "EcsTerminalUrl": "wss://cn-beijing-a01-vncproxy-ecs.volcengine.com:443/instance/login/18a948b9-00bd-4e56-b2a2-5de5f3******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidPrimaryNetworkInterface.NotFound |The specified PrimaryNetworkInterface does not exist. |The specified primary network interface does not exist. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
