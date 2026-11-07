---
title: "Sample responses"
product: "Message Queue for Kafka"
product_code: "kafka"
source: "https://docs.byteplus.com/en/docs/kafka/sample-responses-v2"
---

After sending the request message, you will receive a response from the message queue server with a status code, response header, and message body.

<span id="a2324975"></span>
## Status code

The status code is a set of numeric codes from 1xx to 5xx. The status code indicates the status of the request response. For example, the HTTP status code of the response is 2xx, indicating that the call was successful; the returned HTTP status code is 4xx or 5xx, indicating that the call failed.

<span id="24916186"></span>
## Response header

Corresponding to the request header, the response also has a header, such as Content\-type.

<span id="c5bf5ec1"></span>
## Response message body

The response message body is usually returned in JSON structured format, corresponding to the Content\-Type in the response message header, and passes the content other than the response message header. When an interface call fails, an error code and an error message description will be returned.


* The HTTP status code is 200, indicating that the request was successful. At this time, the server level return result will contain ResponseMetadata and Result parts.

* All non\-200 status codes indicate that the request failed. The details of the failure are returned as JSON, and the returned content only contains ResponseMetadata, not the Result field.


Each field in ResponseMetadata is described as follows. Except for the following fixed fields, other fields returned by the API are business fields independently defined by an API. For business\-related fields returned by different APIs, please refer to the definitions in each API document.


|**field** ||**explain** |
|---|---|---|
|RequestID ||A unique identifier for each API request.<br><br>If an unknown exception occurs while calling the API, please pass ticket system Contact technical support and provide the RequestID of the request. Technical support will locate the problematic request according to the RequestID and assist you in troubleshooting. |
|Action ||Interface name, which is a public parameter of the request. |
|Version ||The version number, which belongs to the public parameter of the request. |
|Service ||The service name, which is a public parameter of the request. |
|Region ||Region, which is a public parameter of the request. |
|Error |*  |An Error appears indicating that this request failed. |
||Code |For the specific error code, you can query the document according to the error code to solve the problem by yourself. |
||CodeN |A numeric ID that identifies the error code for easy problem finding. Only some interfaces provide CodeN. |
||Message |Error message, describing the specific reason for the error, for your reference in troubleshooting the problem.<br><br>As the business evolves or the experience is optimized, this text may be changed or updated frequently, and users should not rely on this return value. |


<span id="6d73b2be"></span>
### Example of successful request

```json
{
    "ResponseMetadata": {
        "RequestId": "2023022720461429AE2FDCE34FC0788D62",
        "Action": "DescribeGroups",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "cn-beijing"
    },
    "Result": {
        "GroupsInfo": [
            {
                "GroupId": "kafka-cnng3s31v076****-connect-cluster",
                "State": "Stable"
            }
        ],
        "Total": 1
    }
}
```


<span id="5b694048"></span>
### Example of request failure

```json
{
    "ResponseMetadata": {
        "RequestId": "202303271631047025808FFB8F08B25A60",
        "Action": "DescribeGroups",
        "Version": "2022-05-01",
        "Service": "Kafka",
        "Region": "cn-beijing",
        "Error": {
            "Code": "InvalidParameter.PageSize,PageNumber",
            "Message": "The specified parameter PageSize,PageNumber is not valid."
        }
    },
    "Result": null
}
```
