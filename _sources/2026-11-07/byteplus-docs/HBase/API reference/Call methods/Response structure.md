---
title: "Response structure"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Response_results"
---

This article describes the API response structure for Table Storage for HBase.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">An HTTP status code of 200 indicates that the interface request succeeded.</div>


* <div data-tips="true" data-tips-type="tip">All non\-200 HTTP status codes indicate that the interface request failed. The specific failure message is returned in JSON format.</div>



<span id=".6L-U5Zue57uT5p6c56S65L6L"></span>
## Response example

<span id=".6K-35rGC6LCD55So5oiQ5Yqf6L-U5Zue57uT5p6c"></span>
### Return result of the successful request call

```json
{
    "ResponseMetadata": {
        "RequestId": "202204151506390101940591001265****",
        "Action": "DescribeRegions",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing"
    },
    "Result": { /* Service-specific response information */
        "Regions": [{
            "RegionId": "cn-beijing",
            "RegionName": "华北2（北京）"
        }]
    }
}
```


The parameter information returned by the request call is as follows:


* `ResponseMetadata` and its internal fields `RequestId`, `Action`, `Version`, `Service`, and `Region` are fixed fields that are always returned for any API request, regardless of the outcome.

* `RequestId` is the unique identifier for an API request. If an API error occurs, you can [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support and provide this ID to help locate the problem.

* `Result` is a fixed field, and its content is defined by each product. This field will not be returned when the request call fails.

* In addition to the fixed fields, the rest are fields defined by the specific API. For the fields returned by different APIs, refer to the specific definitions in the API documentation.


<span id=".6K-35rGC6LCD55So5aSx6LSl6L-U5Zue57uT5p6c"></span>
### Return result of the failed request call

```json
{
    "ResponseMetadata": {
        "RequestId": "202211161553430102251451520191****",
        "Action": "DescribeRegions",
        "Version": "2018-01-01",
        "Service": "hbase",
        "Region": "cn-beijing",
        "Error": {
            "Code": "Failed",
            "Message": "The request processing has failed due to some unknown error, exception or failure.",
        }
    }
}
```


The `Error` field will definitely appear when the request call fails. The `Error` field contains the `Code` and `Message` fields, where:


* `Code` indicates the error code. Refer to the common error codes and the error codes for the current interface to find the corresponding cause and solution.

* `Message` will give the specific reason for the error. This text may change with business development or experience optimization.

* The `Result` field is not returned when the request call fails.
