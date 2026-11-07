---
title: "GetConsoleScreenshot - Obtains a screenshot"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/GetConsoleScreenshot"
---

Call the GetConsoleScreenshot operation to obtain a JPG screenshot of a running instance.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* You can only obtain the instance screenshot of an instance in the **Running** state.

* Elastic Bare Metal (EBM) instances currently do not support this feature.

* The returned JPG screenshot of the instance is Base64\-encoded and requires manual decoding.

* This operation has a request limit in frequency. The recommended interval between requests is around 10s to avoid exceeding the operation frequency limit.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=GetConsoleScreenshot&groupName=%E8%BF%90%E7%BB%B4&serviceCode=ecs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action** <span data-label="purple">string</span> <span data-api-tag="require|qITf7r">必选</span> `Sample value: GetConsoleScreenshot`

The action that you want to perform. Value: GetConsoleScreenshot.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|JHrZ2u">必选</span> `Sample value: 2020-04-01`

The version of the API. Valid value: 2020\-04\-01.



**InstanceId** <span data-label="purple">string</span> <span data-api-tag="require|2Kmtsr">必选</span> `Sample value: i-3tiefmkskq3vj0******`

The instance ID. You can call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation to query the instance ID.



**WakeUp** <span data-label="purple">boolean</span> `Optional` `Sample value: false`

Specifies whether to wake up the instance in hibernation. Value:


* true: Wakes up the instance in hibernation.

* false (default): Does not wake up the instance in hibernation.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**InstanceId** <span data-label="purple">string</span> `Sample value: i-3tiefmkskq3vj0******`

The instance ID.



**Screenshot** <span data-label="purple">string</span> `Sample value: /9j/2wCEAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBwkIBgcJBwYGCAsICQoKC******`

The Base64\-encoded JPG screenshot of the instance.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can add the prefix <code>data:image/jpeg;base64,</code> to the returned value and then enter the full string in the browser to open the screenshot.</div>




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=GetConsoleScreenshot&Version=2020-04-01&InstanceId=i-3tiefmkskq3vj0****** HTTP/1.1
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
        "Action": "GetConsoleScreenshot",
        "Version": "2020-04-01",
        "Service": "ecs",
        "Region": "cn-beijing"
    },
    "Result": {
        "InstanceId": "i-3tiefmkskq3vj0******",
        "Screenshot": "/9j/2wCEAAIBAQEBAQIBAQECAgICAgQDAgICAgUEBAMEBgUGBgYFBgYGBwkIBgcJBwYGCAsICQoKC******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidInstanceStatus |The status of the specified instance does not support this request. |The current status of the instance does not support this operation. |
|400 |InvalidInstanceTypeForGetConsoleScreenshot.Unsupported |The specified InstanceType does not support get instance console screenshot. |The specified instance type does not support the screenshot feature. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be left empty. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|429 |FlowLimitExceeded |You've reached the limit on request rate of resources. |Request rate of resources exceeds the limit. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
