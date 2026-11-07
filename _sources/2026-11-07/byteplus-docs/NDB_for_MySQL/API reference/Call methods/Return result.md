---
title: "Return result"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Response_results"
---

This document describes the API return result.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the interface request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate that the interface request failed. The specific failure message is returned in JSON format.</div>



<span id=".6L-U5Zue57uT5p6c"></span>
## Return result

<span id=".6K-35rGC6LCD55So5oiQ5Yqf6L-U5Zue57uT5p6c"></span>
### Return result of the successful request call

```Plain Text
{
        "ResponseMetadata" : {
          "RequestId": "52ece640-60ba-4cf9-bf34-302fb45eef4f",
          "Action": "DescribeRegions",
          "Version": "2022-01-01",
          "Service": "vedbm",
          "Region": "cn-beijing"
          },
        "Result": { /* 具体业务的返回信息 */
          "Regions":[
             { 
              "RegionId": "cn-beijing", 
              "RegionName": "华北 2（北京）"
             }
          ] 
    }
}
```


The parameter information returned by the request call is as follows:


* `ResponseMetadata` and its internal fields `RequestId`, `Action`, `Version`, `Service`, and `Region` are fixed fields that are always returned for any API request, regardless of the outcome.

* `RequestId` is the unique identifier for an API request. If an API error occurs, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support and provide this ID to help locate the problem.

* `Result` is a fixed field, and the content of this field may vary depending on the product. Refer to the actual return. This field will not be returned when the request call fails.

* In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.


<span id=".6K-35rGC6LCD55So5aSx6LSl6L-U5Zue57uT5p6c"></span>
### Return result of the failed request call

```Plain Text
{
   "ResponseMetadata" : {
        "RequestId": "d78bbf4e-63a5-4937-ac3c-3767e7eddfbe",
        "Action": "DescribeRegions",
        "Version": "2022-01-01",
        "Service": "vedbm",
        "Region": "cn-beijing",
        "Error": {
            "Code": "Failed",
            "Message": "The request processing has failed due to some unknown error, exception or failure."
        }
   }
}
```


The `Error` field will definitely appear when the request call fails. The `Error` field contains the `Code` and `Message` fields, where:


* `Code` indicates the error code. Refer to the common error codes and the error codes for the current interface to find the corresponding cause and solution.

* `Message` will give the specific reason for the error. This text may change with business development or experience optimization.

* The `Result` field is not returned when the request call fails.
