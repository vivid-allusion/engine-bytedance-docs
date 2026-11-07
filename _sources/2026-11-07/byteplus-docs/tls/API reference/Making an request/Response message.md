---
title: "Response message"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/response-message"
---

After sending a request message, you will receive a response from the server, which includes the status code, response message headers, and message body.

<span id="status-code"></span>
## Status Code

The status code is a set of digital codes from 1xx to 5xx, which represents the status of the request response. For example, if the response HTTPS status code is 2xx, it indicates a successful call; if the returned HTTPS status code is 4xx or 5xx, it indicates a failed call.

The corresponding status codes for each interface please refer to the documentation of each interface, and the common status code list please refer to the status code.

<span id="response-message-header"></span>
## Response Message Header

Response message headers usually include the following common parameters.


|Name |Description |
|---|---|
|Content\-Length |Length of the response message body. |
|Connection |Identifies whether the connection established by the request is long or short. |
|X\-Tls\-Requestid |Unique identifier for each API request.<br><br>If an unknown exception occurs when calling the API, please contact the technical support and provide the X\-Tls\-Requestid of the request. The technical support will locate the problematic request based on the X\-Tls\-Requestid and assist you in troubleshooting the fault. |
|Date |Date of the response request. |


The example of the returned message header:

```http
Content-Type:  application/json; charset=utf-8
Content-Length:  73    
Connection: keep-alive
X-Tls-Requestid:  3a********
Date:  Sun, 22 Aug 2021 02:10:34 GMT
```


<span id="response-message-body"></span>
## Response message body

The response message body is usually returned in a JSON structured format, corresponding to the Content\-Type in the response message header, and conveys the content other than the response message header. When an interface call fails, an error code and an error message description will be returned.


* An HTTP status code of 200 indicates that the request was successful. At this time, the server's return result will include specific business information, that is, the return information independently defined in each API. For detailed instructions, please refer to the API documentation of each interface.

* All status codes other than 200 indicate that the request failed. The detailed failure information is returned in the form of JSON, and the returned content includes two parts: ErrorCode and ErrorMessage.



|Field |Description |
|---|---|
|ErrorCode |Specific error code. You can query the documentation to solve the problem yourself based on the error code. |
|ErrorMessage |Error message, describing the specific cause of the error for your reference in troubleshooting. |


<span id="example-of-successful-request"></span>
### Example of successful request

```json
{
    "Projects": [
        {
            "ProjectId": "6fd4bbb0-e0a9-454e-b165-5a640c85****",
            "ProjectName": "test3",
            "Description": "",
            "CreateTime": "2021-08-22T14:53:45Z",
            "TopicCount": 0,
            "InnerNetDomain": "tls-ap-southeast-1.bytepluses.com"
        },
        {
            "ProjectId": "d1598af5-fa2d-4571-855e-c41d1114****",
            "ProjectName": "ffff",
            "Description": "",
            "CreateTime": "2021-08-20T14:37:20Z",
            "TopicCount": 0,
            "InnerNetDomain": "tls-ap-southeast-1.bytepluses.com"
        }
    ],
    "Total": 30
}
```


<span id="example-of-request-failure"></span>
### Example of request failure

```json
{
    "ErrorCode": "ProjectAlreadyExist",
    "ErrorMessage": "Project already exist"
}
```
