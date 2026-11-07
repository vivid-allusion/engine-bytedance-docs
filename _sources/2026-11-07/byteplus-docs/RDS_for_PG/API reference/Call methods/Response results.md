---
title: "Response results"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/response_results"
---

This topic describes the response information for calls to RDS for PostgreSQL APIs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">The HTTP status code 200 indicates a successful API request.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate a failed API request. Detailed failure information is returned in JSON format.</div>



<span id="response-examples"></span>
## Response examples

<span id="response-results-for-a-successful-request"></span>
### Response results for a successful request

```json
{
    "ResponseMetadata" : {
            "RequestId": "52ece640-60ba-4cf9-bf34-302fb45eef4f",
            "Action": "DescribeRegions",
            "Version": "2022-01-01",
            "Service": "rds_postgresql",
            "Region": "ap-southeast-1"
        },
    "Result": { /* Response from specific service */
            "Regions":[
               { 
                "RegionId": "ap-southeast-1", 
                "RegionName": "ap-southeast-1"
               }
            ] 
      }
 }
```


After a request is processed normally, the response contains two parts, namely `ResponseMetadata` and `Result`.

`ResponseMetadata` and its internal `RequestId`, `Action`, `Version`, `Service`, and `Region` are fixed fields and their information is returned regardless of whether the initiated API request succeeds. This field will not be returned if the request fails. `ResponseMetadata` fields are described below:


|**Field** |**Description** |
|---|---|
|RequestID |RequestID is the unique identifier of each API request. If an API exception occurs, you can [submit a ticket](https://www.byteplus.com/en/support/customer) to contact technical support and provide the ID to help locate the problem. |
|Action |Name of the API in a request. It is a common request parameter. |
|Version |The version number in a request. It is a common request parameter. |
|Service |Service in a request. It is a common request parameter. |
|Region |Request region. It is a common parameter of the request. |


`Result` is a fixed field and its response content varies depending on the requested API.

<span id="response-results-for-a-failed-request"></span>
### Response results for a failed request

```json
{
     "ResponseMetadata" : {
          "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
          "Action": "DescribeRegions",
          "Version": "2022-01-01",
          "Service": "rds_postgresql",
          "Region": "ap-southeast-1",
          "Error": {
              "Code": "Failed",
              "Message": "The request processing has failed due to some unknown error, exception or failure."
          }
     }
 }
```


Compared with a successful result, a failed result does not contain `Result`, and its `ResponseMetadata` part contains an additional `Error` field. The `Error` field contains `Code` and `Message` sub\-fields. `Error` fields are described below:


|**Field** |**Description** |
|---|---|
|Code |Provides the specific error code. Use the code to find the corresponding cause of the error and solutions in the list of common error codes and the error codes specific to this API. |
|Message |Indicates the specific reason for the error. |
