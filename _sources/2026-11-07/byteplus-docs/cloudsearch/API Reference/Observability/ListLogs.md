---
title: "ListLogs"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ListLogs"
---

Call the ListLogs API to query running logs related to the instance, supporting filters by time range, keywords, nodes, log levels, components, and file types.

<span id=".6LCD6K-V"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|d74096">必选</span>`Example: ListLogs`

Action to execute, values: ListLogs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|sj2mXA">必选</span> `Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**StartTime ** <span data-label="purple">long </span>`optional` `Example value: 1712052000000`

Query start time, in Unix timestamp format. Default is `current time - 15 minutes`, and only data from the last 7 days can be queried (exceeding this will revert to the default range).



**EndTime ** <span data-label="purple">long </span>`optional` `Example value: 1712052900000`

Query end time, in Unix timestamp format. Defaults to current time and allows querying data from the last 7 days only.



**InstanceId ** <span data-label="purple">string </span>`optional` `example: o-0080**iu98`

Instance ID: if provided, the ownership of the instance will be verified and used for log filtering; if not provided, the search will be based only on the account dimension.



**NodeName ** <span data-label="purple">string </span>`optional` `example: es-data-****j8ilw8-0`

Node name.



**Keyword ** <span data-label="purple">string </span>`Optional` `Example: failed`

Keyword filtering, matching the log content.



**Cursor ** <span data-label="purple">string </span>`optional` `example: eyJ***`

Cursor (paging/continuation): obtain from the last response's cursor and return it back.



**LogLevel ** <span data-label="purple">string </span>`optional` `example: INFO`

Log level filtering, valid values are: `TRACE`, `DEBUG`, `INFO`, `WARN`, `ERROR`, `FATAL`.



**LogRole ** <span data-label="purple">string </span>`optional` `Example value: elasticsearch`

Component role filter, values: `elasticsearch`, `kibana`. The default value is `elasticsearch`.



**LogType ** <span data-label="purple">string </span>`optional` `example: cluster`

File type filter for logs. `cluster`: cluster logs. `searchSlow`: slow query logs. `indexSlow`: slow write logs. `gc`: GC log. `kibana`: Kibana/Dashboard logs.

The default value is `cluster`. When `LogRole` = `kibana`, Kibana is enforced.



**Sort ** <span data-label="purple">string </span>`Optional` `Example: desc`

Sort order. Supported: asc, desc. The default value is desc.



**PageSize ** <span data-label="purple">integer </span>`optional` `example value: 100`

Number of logs returned per request, range: [10, 1000]. The default value is 100. Values outside the range revert to the default value.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Logs ** <span data-label="purple">object[] </span>`example value: -`

List of logs.


**InstanceId ** <span data-label="purple">string </span>`Example: o-0080**iu98`

Instance ID.



**NodeName ** <span data-label="purple">string </span>`Example: es-data-0080**iu98-0`

Node name.



**LogTime ** <span data-label="purple">string </span>`example value: 2026-04-01T19:33:01+08:00`

Log time, formatted as an RFC 3339 string.



**LogLevel ** <span data-label="purple">string </span>`Example: ERROR`

Log level.



**Message ** <span data-label="purple">string </span>`example: [ERROR] ...`

Log content.




**Total ** <span data-label="purple">integer </span>`Example value: 10`

Total hits.



**Cursor ** <span data-label="purple">string </span>`example value: eyJ***`

Cursor for the next page.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=ListLogs&Version=2023-01-01 HTTP/1.1
Host: escloud.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20260402T124105Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260402/cn-beijing/escloud_dev/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260402204109199056095028EE4168",
    "Action": "ListLogs",
    "Version": "2023-01-01",
    "Service": "escloud_dev",
    "Region": "cn-beijing"
  },
  "Result": {
    "Logs": [
      {
        "InstanceId": "o-0080**iu98",
        "NodeName": "es-data-0080**iu98-0",
        "LogTime": "2026-04-01T19:33:01+08:00",
        "LogLevel": "ERROR",
        "Message": "[ERROR] ..."
      }
    ],
    "Total": 10,
    "Cursor": "eyJ***"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
