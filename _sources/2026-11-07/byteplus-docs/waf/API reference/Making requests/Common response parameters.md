---
title: "Common response parameters"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/common_response_parameters"
---

After sending a request message, you will receive a response from the server, which contains a status code, response headers, and a response body.

<span id="51e9e0b5"></span>
## Status Code

A status code indicates the status of the request response and is a series of numerical codes ranging from `1XX` to `5XX`.


* If the status code is 200, it means the interface request was successful.

* Any status code other than 200 indicates that the interface request has failed. Specific information is returned in JSON format.


<span id="1732ebda"></span>
## Response Header

Corresponding to the request header, the response also has headers, such as `Content-Type`.

<span id="2212e95e"></span>
## Response Body

The response Body usually returns in a structured `JSON` format, corresponding to the `Content-Type` in the response Header, conveying content other than the response message headers.


* Status code 200 indicates that the request was successful. At this point, the server's return result includes two parts: `ResponseMetadata` and `Result`.

* Any status code other than 200 indicates that the interface request has failed. The failure information is returned in JSON format, and the content includes an Error field, which consists of Code and Message.


<span id="05020ccf"></span>
## Sample response

<span id="9b87fd11"></span>
### Sample of a successful request

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202310091729184CEFD57F221FFCBF****",
        "Action": "CreateCCRule",
        "Version": "2023-12-25",
        "Service": "waf",
        "Region": "byteplus-global"
    },
    "Result": {
        "Id": 144565
    }
}
```



* `ResponseMetadata` and its internal fields, including `RequestId`, `Action`, `Version`, `Service`, `Region`, are fixed fields. No matter whether the request is successful or not, as long as an API request is made, it will certainly return these fields.

* The `RequestId` is a unique identifier for an API request; if there is an issue with the API, this ID can help pinpoint the problem.

* The `Result` is a fixed field, the content of which is defined by different products themselves.


<span id="5ba7c342"></span>
### Sample of a failed request

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202310091403564A8CA5A23A12AEA5****",
        "Action": "GetVulnerabilityConfig",
        "Version": "2023-12-25",
        "Region": "byteplus-global",
        "Error": {
            "CodeN": 100025,
            "Code": "InvalidCredential",
            "Message": "Invalid credential in 'Authorization', Pls check your authorization header."
        }
    }
}
```



* When a request call fails, the `Result` field will not be returned.

* When a request call fails, an `Error` field will appear, composed of the `Error` field by `Code` and `Message`, where:

   * `Code` indicates the specific error code, which you can use to troubleshoot the problem on your own.

   * `Message` indicates the error message, providing a description of the specific cause of the error for your troubleshooting reference. As the business develops or the experience is optimized, this text is likely to be frequently changed or updated, and it is not recommended to rely completely on this return value.
