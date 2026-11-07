---
title: "DescribeLiveCallbackData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivecallbackdata"
---

This API allows you to query callback records related to live streaming, including event types, statuses, request and response data. It helps you troubleshoot callback exceptions and verify whether callbacks were successfully delivered.

## Requirements

Rate limit: 30 queries per second per account.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveCallbackData` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["example.com", "example2.com"]` |The list of domain names to be queried. By default, it represents all domain names under the current account. |
|App |String |No |`example_app` |Name of the application. Must match the one used in the stream URL. |
|Stream |String |No |`example_stream` |Stream name, used to accurately locate a specific live stream. |
|CallbackEventType |Array of String |No |`["push_start"]` |Supported callback event types:<br><br><br>* `push_start`: Streaming start<br><br>* `push_end`: Streaming end<br><br>* `snapshot_event`: Screenshot callback<br><br>* `record_event`: Recording callback |
|CallbackStatus |Array of String |No |`["success"]` |Callback status. The following values are supported:<br><br><br>* `success`: Success.<br><br>* `fail`: Failure. |
|StartTime |String |Yes |`2021-08-16T00:01:59Z` |The start time of the query, in UTC time in RFC3339 format, with a precision of seconds.<br><br>> **说明**<br><br><br>> The maximum time span for a single query is 31 days, and the maximum time range for a historical query is 366 days.<br> |
|EndTime |String |Yes |`2021-08-16T00:01:59Z` |The end time of the query, in UTC time in RFC3339 format, with a precision of seconds. |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|PageSize |Integer |No |`100` |The number of query results per page. Valid values: [1,1000]. Default value: `100`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["example.com", "example2.com"]` |Domain name list. |
|App |String |`example_app` |Application Name. |
|Stream |String |`example_stream` |Stream name. |
|CallbackEventType |Array of String |`["push_start"]` |Callback event types. |
|CallbackStatus |Array of String |`["success"]` |Callback status values. |
|StartTime |String |`2021-08-16T00:01:59Z` |The start time of the query, UTC time in RFC3339 format, with a precision of seconds. |
|EndTime |String |`2022-11-11T00:00:00Z` |The end time of the query, the UTC time in RFC3339 format with a precision of seconds. |
|CallbackInfoList |Array of [CallbackInfoList](https://docs.byteplus.com/en/docs/24/45496#callbackinfolist) |`-` |Details of the callback event. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/45496#pagination) |`-` |Pagination information of the query results. |

### CallbackInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`example.com` |Domain name. |
|App |String |`example_app` |Application name. |
|Stream |String |`example_stream` |Stream Name. |
|CallbackTime |String |`2022-11-11T00:00:00Z` |The time of the callback execution. |
|CallbackEventType |String |`push_start` |Callback event types. |
|CallbackMethod |String |`post` |Callback request method. |
|CallbackAddress |String |`http://example.com/xxx` |Callback destination URL. |
|CallbackStatus |String |`success` |Callback status. |
|CallbackBody |String |`{}` |Callback request body. |
|CallbackResponseCode |String |`200` |HTTP status code of the response. |
|CallbackResponseHeader |String |`Content-Type: application/json; charset=utf-8\r\nContent-Length: 29` |HTTP response headers. |
|CallbackResponseBody |String |`{"error_code":200,"msg":"ok"}` |Response body of the callback. |
|CallbackResponseTime |String |`2022-11-11T00:00:00Z` |Callback response time. |
|CallbackErrorMessage |String |`InternalServiceError` |Error message, returned when the callback fails. |
|CallbackErrorCode |String |`The callback receiving service is unreachable. Please check whether the callback address is available.` |Error description. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |The page number of the current page. |
|PageSize |Integer |`100` |The number of data items displayed per page. |
|TotalCount |Integer |`100` |The total number of data in the query result. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveCallbackData&Version=2023-01-01
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250410201942D5628AA78C98A0C818D0",
        "Action": "DescribeLiveCallbackData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CallbackEventType": [
            "push_end"
        ],
        "StartTime": "2025-03-18T00:00:00Z",
        "EndTime": "2025-03-19T00:00:00Z",
        "CallbackInfoList": [
            {
                "Domain": "example.com",
                "App": "app_test",
                "Stream": "stream-111",
                "CallbackTime": "2025-03-18T23:30:52Z",
                "CallbackEventType": "push_end",
                "CallbackMethod": "post",
                "CallbackAddress": "http://example.com/callback/record",
                "CallbackStatus": "success",
                "CallbackBody": "{}",
                "CallbackResponseCode": "200",
                "CallbackResponseHeader": "HTTP/1.1 200 OK",
                "CallbackResponseBody": "{\"error_code\":200,\"msg\":\"ok\"}",
                "CallbackResponseTime": "2025-03-18T23:30:53Z",
                "CallbackErrorCode": "",
                "CallbackErrorMessage": ""
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 100,
            "TotalCount": 1
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Unclassified error. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the description of Request Parameters for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter fails the verification. Please check whether the parameter type is correct. |
|403 |RequestForbidden |\- |The request is rejected. There is no requested resource (domain name space, domain name, application, configuration template, certificate) under the current account. |
|404 |ResourceNotFound |\- |The resource (domain namespace, domain name, application, configuration template, certificate) was not found. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An error occurred between services. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An error occurred between services. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout, please [contact support](https://console.byteplus.com/workorder/create). |
