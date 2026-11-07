---
title: "SearchTraces"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/SearchTraces"
---

Call the SearchTraces API to query the trace details list based on specific conditions.

<span id=".6K-35rGC6K-05piO"></span>
## Request instructions


* Request method: POST

* Request URL: https://{tls\-endpoint}/SearchTraces


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tls/common-parameters).

<span id="Body"></span>
### Body


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Query |Object of [TraceQueryParameters](https://docs.byteplus.com/en/docs/38/83202#tracequeryparameters) |Yes |/ |Query criteria used to filter Trace details that match the specified conditions Supports multiple query criteria combinations, including sorting, pagination, time range, service name, and more |
|TraceInstanceId |String |Yes |0fdaa6b6\-3c9f\-424c\-8664\-fc0d222c\*\*\*\* |Trace instance ID |


<span id="tracequeryparameters"></span>
### TraceQueryParameters


|**Parameters** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|Asc |Boolean |No |true |Specify whether the query results should be sorted in ascending order `true` means ascending order; `false` means descending order |
|Kind |String |No |`internal` |Type. |
|Limit |Integer |No |10 |Specifies the maximum number of records returned in query results for pagination control. |
|Order |String |No |Start |Specify the field by which to sort the query results. Sorting supports the following fields:<br><br><br>* `Kind`: type<br><br>* `Name`: name<br><br>* `ServiceName`: service name<br><br>* `Start`: start time<br><br>* `End`: end time<br><br>* `Duration`: duration<br><br>* Explicitly add and enable statistical index fields in `Attributes` (such as `Attributes.request_id`). |
|Offset |Integer |No |0 |Offset for paginated queries, indicating which record to return first in the results Usually used together with `Limit` to implement pagination |
|TraceId |String |No |ef97a7\*\*\*\* |Trace ID。 |
|Attributes |JSON Map |No |`[object Object]` |In `Attributes`, the field is `key`, and `value` represents all possible values for that field. |
|StatusCode |String |No |OK |The status code of `Trace`, used for filtering `Trace` records by specific status. |
|DurationMax |Integer |No |1000000 |Maximum `Trace` duration in microseconds. Filters `Trace` records with durations not exceeding the specified value. |
|DurationMin |Integer |No |1000 |`Trace` minimum duration in microseconds. Used to filter `Trace` records with durations exceeding the specified value. |
|ServiceName |String |No |mysql |Used to filter `Trace` records for specific service names This field supports exact match. The query results will include only `Trace` records with service names that are exactly the same as the specified value |
|StartTimeMax |Integer |No |1625097600000000 |Maximum start time of `Span`, in microseconds (timestamp). Used to filter `Trace` records with start times no greater than the specified value. |
|StartTimeMin |Integer |No |1625097600000000 |The minimum start time for `Span`, in microseconds timestamp. Used to filter `Trace` records that start after the specified time. |
|OperationName |String |No |create |Operation name of `Trace`, used to filter `Trace` records with a specific operation name. This field supports exact matching; the query results will only include `Trace` records whose operation name exactly matches the specified value. |


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

The table below lists only the return parameters unique to this interface. For more information, see [Return structure](https://docs.byteplus.com/en/docs/tls/response-message).


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Total |Integer |100 |Total number of qualified `Trace` details |
|TraceInfos |Array of [TraceInfo](https://docs.byteplus.com/en/docs/38/83202#traceinfo) |\- |Includes a list of `Trace` details. Each item contains information such as `TraceID`, service name, operation name, start time, end time, duration, status code, and custom attributes. |


<span id="traceinfo"></span>
### TraceInfo


|**Parameters** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|EndTime |Integer |1625097600000000 |The `Trace` end time in microseconds, indicating the precise moment this trace operation is completed |
|TraceId |String |ef97a7\*\*\*\* |Trace ID。 |
|Duration |Integer |1500000 |The `Trace` duration, in microseconds, represents the time difference from `StartTime` to `EndTime`. |
|StartTime |Integer |1625097600000000 |The start time of `Trace` in microseconds, indicating the precise moment when the tracing operation began. |
|Attributes |JSON Map |[object Object] |In `Attributes`, the field is `key`, and `value` represents the possible values for that field. |
|StatusCode |String |OK |Status code of `Trace`, used to filter `Trace` records with specific status. |
|ServiceName |String |mysql |Used to filter `Trace` records for a specific service name. This field supports exact matching; only trace records with the service name exactly matching the specified value will be returned. |
|OperationName |String |create |Operation name of `Trace`, used to filter `Trace` records by specific operation name This field supports exact match. The query results will only include `Trace` records where the operation name exactly matches the specified value |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
POST https://{tls-endpoint}/SearchTraces HTTP/1.1
Content-Type: application/json
{
    "Query": {
        "Asc": true,
        "Kind": "internal",
        "Limit": 10,
        "Order": "Start",
        "Offset": 0,
        "TraceId": "ef97a7****",
        "Attributes": {
            "request_id": "12345****"
        },
        "StatusCode": "OK",
        "DurationMax": 1000000,
        "DurationMin": 1000,
        "ServiceName": "mysql",
        "StartTimeMax": 1625097600000000,
        "StartTimeMin": 1625097600000000,
        "OperationName": "create"
    },
    "TraceInstanceId": "0fdaa6b6-3c9f-424c-8664-fc0d222c****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```JSON
Content-Type: application/json; charset=utf-8
{
    "Total": 100,
    "TraceInfos": [
        {
            "EndTime": 1625097600000000,
            "TraceId": "ef97a7****",
            "Duration": 1500000,
            "StartTime": 1625097600000000,
            "Attributes": {
                "request_id": "12345****"
            },
            "StatusCode": "OK",
            "ServiceName": "mysql",
            "OperationName": "create"
        }
    ]
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error Code

You can visit [General error codes](https://docs.byteplus.com/en/docs/tls/common-error-codes) for more details.
