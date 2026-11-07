---
title: "DescribeInstanceVncUrl - Queries VNC management terminal address"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeInstanceVncUrl"
---

Call the DescribeInstanceVncUrl operation to query the VNC management terminal address of an ECS instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* If you cannot use the **ECS Terminal** to log in to a Linux instance, log in to the instance via **VNC** in the console to view the real\-time status of the ECS operation interface.

* You can generate a VNC login link (JS format) by performing the following operation:

   Add `Region=****`, `host=****`, and `name=****` to the end of `https://console.byteplus.com/ecs/connect/vnc/?`. Separate the parameters with  `&`.

   
   |Name |Description |Sample value |
   |---|---|---|
   |Region |The region of the instance. |cn\-beijing |
   |host |The value of `VncUrl` returned by calling the DescribeInstanceVncUrl operation. |cn\-beijing\-a01\-vncproxy\-ecs.volcengine.com:443/websockify/destInfoToken/01495659\-06ab\-49ca\-9aa7\-d1b226\*\*\*\*\*\*\* |
   |name |Instance name. |instance\-host\-name |
   

   Sample link (JS format):

   ```Plain Text
   https://console.byteplus.com/ecs/connect/vnc/?Region=cn-beijing&host=cn-beijing-a01-vncproxy-ecs.volcengine.com:443/websockify/destInfoToken/01495659-06ab-49ca-9aa7-d1b226*******&name=instance-host-name
   ```
   

* After you log in to the instance via VNC, if there is no interactive operation within 180 seconds in your management terminal window, the connection will be automatically disconnected.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeInstanceVncUrl&groupName=%E5%AE%9E%E4%BE%8B&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the request parameters specific to this operation and some common parameters. For more information, please refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|OwklTC">必选</span> `Sample value: DescribeInstanceVncUrl`

The operation that you want to perform. Valid value: DescribeInstanceVncUrl.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|glVFuW">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|Xq7KaS">必选</span> `Sample value: i-l8u10sauiu9qj0h*****`

Instance ID



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The table below lists only the response parameters specific to this operation. For more information, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**VncUrl** <span data-label="purple">string</span> `Sample value: wss://cn-beijing-a01-vncproxy-ecs.volcengine.com:443/websockify/destInfoToken/01495659-06ab-49ca-9aa7-d1b226*******`

The URL of the management terminal.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeInstanceVncUrl&Version=2020-04-01&InstanceId=i-l8u10sauiu9qj0h***** HTTP/1.1
Host: ecs.cn-beijing.byteplusapi.com.cn
Region: cn-beijing
Service: ecs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
        "ResponseMetadata": {
                "RequestId": "20211104180426010194099035220C****",
                "Action": "DescribeInstanceVncUrl",
                "Version": "2020-04-01",
                "Service": "ecs",
                "Region": "cn-beijing"
        },
        "Result": {
                "VncUrl": "wss://cn-beijing-a01-vncproxy-ecs.volcengine.com:443/websockify/destInfoToken/01495659-06ab-49ca-9aa7-d1b226*******"
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
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
