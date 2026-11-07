---
title: "ListPullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023"
---

Call the `ListPullToPushTask` API to query the relay task list in pagination, supporting fuzzy search by Task name.

## Requirements

Rate limit: 15 queries per second per account.

## HTTP request

* Method: GET

* Endpoint: https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListPullToPushTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |
|Page |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|Size |Integer |No |`20` |The number of query results per page. Valid values: [1,500]. Default value: `20`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |
|Title |String |No |`doc` |The name of the relay task. The search is case\-insensitive and fuzzy search is supported. For example, if you set `Title` as `doc`, you may get a list of relay tasks with `doc` in their names, such as `docspace`, `docs`, and `DOC`. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/27471#list) |`-` |A list of your relay tasks. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/27471#pagination) |`-` |Page information. |

### List

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Title |String |`task001` |The name of the relay task. |
|TaskId |String |`fde6aa0281d*******9a6e24236` |The Task ID. |
|StartTime |String |`2022-04-01T00:00:00Z` |The start time of the relay task (UTC time in RFC 3339 format). |
|EndTime |String |`2022-04-02T00:00:00Z` |The end time of the relay task (UTC time in RFC 3339 format). |
|CallbackURL |String |`http://example.mtime.cn/live/example/callbackapi` |The callback address for receiving relay task events. |
|Type |Integer |`0` |The stream source type. Valid values include:<br><br><br>* `0`: The streamed content is pulled from a live\-stream source.<br><br>* `1`: The streamed content is pulled from on\-demand videos. |
|CycleMode |Integer |`-1` |The loop mode of the stream. The only valid value is `-1`: sequential loop. |
|DstAddr |String |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |The push stream address. |
|SrcAddr |String |`http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |The pull stream address, which is returned if Type is 0. |
|SrcAddrS |Array of String |`["http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |The list of on\-demand videos, which is returned if Type is 1. |
|Status |String |`Pending` |The status of the relay task.<br><br><br>* `Disabled`: The relay task is disabled.<br><br>* `Pending`: The relay task is ready to start.<br><br>* `Enabled`: This indicates an ongoing relay task and is activated upon the defined start time..<br><br>* `Ended`: This status appears after the defined end time of the relay task. |
|DstAddrType |Integer |`1` |The type of the push stream address. Valid values include:<br><br><br>* `1`: BytePlus MediaLive's push stream address.<br><br>* `2`: Third\-party push stream address. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The current page number. |
|PageSize |Integer |`10` |The number of results on each page. |
|PageTotal |Integer |`108` |The total number of pages. |
|TotalCount |Integer |`1073` |The total number of results. |

## Samples

### Sample request

```json
GET https://open.byteplusapi.com/?Action=ListPullToPushTask&Version=2023-01-01&Page=1&Size=20&Title=doc
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457440101742350380352BCC7",
        "Action": "ListPullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "CallbackURL": "",
                "CycleMode": -1,
                "DstAddr": "rtmp://example.org/Video/2022/02/04/mp4/190204084208765161.mp4",
                "EndTime": "2022-01-01T23:44:32+08:00",
                "SrcAddr": "http://example.org/Video/2003/02/04/mp4/190204084208765161.mp4",
                "SrcAddrS": [],
                "DstAddrType": 2,
                "StartTime": "2021-12-31T22:44:23+08:00",
                "Status": "Pending",
                "TaskId": "8fde6aa0281d9f6e15e6059a6e242365",
                "Title": "sutest007",
                "Type": 0
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 108,
            "TotalCount": 1073
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27471#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There are no requested resources (domain space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|403 |AccessDenied |User is not authorized to perform: %s on resource: %s |The request is rejected. There is no requested resources (resources include domain name space, domain name, application, configuration template, certificate) or API permission under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
