---
title: "Response"
product: "LLM Application Firewall"
product_code: "LLM-Application-Firewall"
source: "https://docs.byteplus.com/en/docs/LLM-Application-Firewall/Response"
---

After sending a request message, you will receive a response from the server. The returned result includes a status code, response headers, and a response body.

<span id="51e9e0b5"></span>
## Status codes

Status codes indicate the status of a request and are a set of numeric codes ranging from `1XX` to `5XX`.


* A status code of 200 indicates that the API request was successful.

* Any status code other than 200 indicates that the API request has failed. Specific information is returned in JSON format.


<span id="1732ebda"></span>
## Response headers

Like requests, responses also have headers, such as `Content-Type`.

<span id="2212e95e"></span>
## Response bodies

The response body contains the main content of the response, separate from the headers. It is typically returned in `JSON` format, as specified by the `Content-Type` header.


* A status code of 200 indicates that the request was successful. A successful response contains two parts: `ResponseMetadata` and `Result`.

* All status codes other than 200 indicate a failed request. Failure information is returned in JSON format, and the response body contains an `Error` object with `Code` and `Message` fields.


<span id="05020ccf"></span>
## Response examples

<span id="9b87fd11"></span>
### Successful response examples

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20240529152920190057222220AC****",
    "Action": "Moderate",
    "Version": "2025-08-31",
    "Service": "llmshield",
    "Region": "cn-beijing"
  },
  "Result": {
        "MsgID": "4b090cdd06314c19a9e324b52a09****",
        "RiskInfo": {
            "Risks": null
        },
        "Decision": {
            "DecisionType": 1,
            "DecisionDetail": {
                "ReplaceDetail": {
                    "Replacement": null
                }
            }
        },
        "PermitInfo": {
            "Permits": null
        }
    }
}
```



* The ResponseMetadata object and its fields (`RequestId`, `Action`, `Version`, `Service`, and `Region`) are always returned, regardless of whether the request succeeds or fails.

* `RequestId` is the unique identifier of an API request. If an API exception occurs, you can use this ID to help locate the issue.

* `Result` is a fixed field, and the structure of this field varies by API.


<span id="5ba7c342"></span>
### Failed request response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202310091403564A8CA5A23A12AEA5****",
        "Action": "Moderate",
        "Version": "2025-08-31",
        "Region": "cn-hongkong",
        "Error": {
            "CodeN": 10001,
            "Code": "InvalidParameter",
            "Message": "The specified parameter Action is invalid."
        }
    }
}
```



* When a request fails, the `Result` field will not be returned.

* When a request fails, the response includes an `Error` field. The `Error` field contains a `Code` and a `Message`.

   * `Code`: A unique code identifying the specific error.

   * `Message`: A human\-readable description of the error. This text is subject to change and should not be parsed programmatically.
