---
title: "Sample responses"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/Sample-responses-v1"
---

After sending the request message, you will receive a response from the message queue server with a status code, response header, and message body.

<span id="6ce8d094"></span>
## Status code

Status code is a set of digital codes from 1xx to 5xx. The status code indicates the status of the request response. For example, the HTTP status code of the response is 2xx, indicating that the call was successful; the returned HTTP status code is 4xx or 5xx, indicating that the call failed.

<span id="48b1a072"></span>
## The response header

corresponds to the request header, and the response also has a header, such as Content\-type.

<span id="38cd4829"></span>
## Response message body

The response message body is usually returned in JSON structured format, corresponding to the Content\-Type in the response message header, and passes content other than the response message header. When an interface call fails, an error code and an error message description are returned.


* The HTTP status code is 200, indicating that the request was successful. At this time, the server level return result will contain ResponseMetadata and Result parts.

* All non\-200 status codes indicate that the request failed. The details of the failure are returned in the form of JSON, and the returned content only contains ResponseMetadata, not the Result field. The fields in


ResponseMetadata are described as follows. Except for the following fixed fields, other fields returned by the API are business fields independently defined by an API. For business\-related fields returned by different APIs, please refer to the definitions in each API document.


|**field** ||**explain** |
|---|---|---|
|RequestID ||Unique identifier for each API request.<br><br>If an unknown exception occurs when calling the API, please pass ticket system Contact technical support and provide the RequestID of the request. Technical support will locate the problematic request according to the RequestID and assist you in troubleshooting. |
|Action ||The interface name is a public parameter of the request. |
|Version ||Version number, which is a public parameter of the request. |
|Service ||The service name is a public parameter of the request. |
|Region ||Region, which is a public parameter of the request. |
|Error |*  |An Error appears indicating that the request failed. |
||Code |For the specific error code, you can query the document according to the error code to solve the problem by yourself. |
||CodeN |A numeric ID that identifies the error code for easy problem finding. Only some interfaces provide CodeN. |
||Message |Error message, describing the specific reason for the error, for your troubleshooting reference.<br><br>With business development or experience optimization, this text may be changed or updated frequently, and users should not rely on this return value. |


<span id="5365f754"></span>
### Example of successful request

```json
{
  "ResponseMetadata": {
    "RequestId": "****************",
    "Action": "DescribeSaslUsers",
    "Version": "2018-01-01",
    "Service": "kafka",
    "Region": "ap-southeast-1"
  },
  "Result": {
        "Total": 1,
        "Users": [
            {
                "AllAuthority": true,
                "CreateTime": "2022-04-07T21:12:50+08:00",
                "Description": "",
                "PasswordType": "Plain",
                "UserName": "test"
            }
        ]
    }
}
```


<span id="f1b0c13b"></span>
### Example of request failure

```json
{
    "ResponseMetadata": {
        "RequestId": "****",
        "Action": "QueryMessageByMessageId",
        "Version": "2018-01-01",
        "Service": "Kafka",
        "Region": "ap-southeast-1",
        "Error": {
            "Code": "InternalError",
            "Message": "The request processing has failed due to some unknown error, exception or failure."
        }
    },
    "Result": null
}
```
