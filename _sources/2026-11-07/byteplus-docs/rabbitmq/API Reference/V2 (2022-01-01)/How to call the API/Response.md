---
title: "Response"
product: "Message Queue for RabbitMQ"
product_code: "rabbitmq"
source: "https://docs.byteplus.com/en/docs/rabbitmq/Response"
---

After sending the request message, you will receive a response from the message queue server. The response includes a status code, response headers, and the message body.

<span id=".54q25oCB56CB"></span>
## Status code

A status code is a set of numerical codes ranging from 1xx to 5xx. It indicates the request response status. For example, an HTTP status code of 2xx means the call was successful; an HTTP status code of 4xx or 5xx means the call failed.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers 

Corresponding to the request headers, the response also contains headers, such as **Content\-type**.

<span id=".5ZON5bqU5raI5oGv5L2T"></span>
## Response body 

The response body usually returns in a JSON structured format, matching the Content\-Type in the response headers. It delivers content beyond the response headers. When an API call fails, an error code and error description are returned.


* An HTTP status code of 200 means the request succeeded. At this time, the server's response includes two parts: `ResponseMetadata` and `Result`.

* Any status code other than 200 means the request failed. Failure details are returned in JSON format, containing only ResponseMetadata and no Result field.

   The fields in ResponseMetadata are explained as follows. Aside from the fixed fields below, other fields returned by the API are business fields independently defined by each API. Please refer to each API's documentation for the business fields they return.



|**Field** ||**Description** |
|---|---|---|
|RequestID ||A unique identifier for each API request. If an unknown error occurs when calling the API, contact technical support through the [ticket system](https://console.byteplus.com/workorder/create/?step=2&SubProductID=P00000257) and provide the RequestID. Technical support will use the RequestID to locate the problematic request and assist in troubleshooting. |
|Action ||Interface name, a common request parameter. |
|Version ||Version number, a common parameter of the request. |
|Service ||Service name, a common parameter of the request. |
|Region ||Region, which belongs to the common parameters of the request. |
|Error |*  |Error indicates that this request has failed. |
||Code |Specific error codes. You can consult the documentation to resolve issues based on these codes. |
||CodeN |Numeric ID identifying the error code for easier issue tracking. Only some interfaces provide CodeN. |
||Message |Error message. It describes the specific cause of the error for your troubleshooting reference. With business development or experience optimization, this text may remain updated. Users should not rely on this return value. |


<span id=".6K-35rGC5oiQ5Yqf56S65L6L"></span>
### Example of successful request

```JSON
{
  "ResponseMetadata": {
    "RequestId": "********",
    "Action": "DescribeOperationEvents",
    "Version": "2022-01-01",
    "Service": "rabbitmq",
    "Region": "cn-beijing"
  },
  "Result": {
    "OperationEvents": [
      {
        "OperationName": "ModifyPlugin",
        "EventSource": "OpenAPI",
        "StartTime": 1645523741,
        "Status": "Executing",
        "EndTime": 1645523741,
        "Duration": 10,
        "OperationDetail": "enable rabbitmq_web_mqtt",
        "InstanceId": "rbtmq-*******",
        "OperationType": "ModifyPlugin",
        "EventID": "1"
      }
    ],
    "Total": 1
  }
}
```


<span id=".6K-35rGC5aSx6LSl56S65L6L"></span>
### Example of failed request

```JSON
{
    "ResponseMetadata": {
        "RequestId": "********",
        "Action": "CreateInstance",
        "Version": "2022-01-01",
        "Service": "rabbitmq",
        "Region": "cn-beijing",
        "Error": {
            "Code": "InternalError",
            "Message": "The request processing has failed due to some unknown error, exception or failure."
        }
    },
    "Result": null
}
```
