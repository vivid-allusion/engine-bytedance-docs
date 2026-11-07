---
title: "ListPullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpullrecordtask"
---

This API is used to query the live broadcast recording task list created under the current account, and supports combined queries by conditions such as pagination, domain name, application name, and stream name. Through this API, you can obtain specific information about the task, such as the recording period, task status, etc., which helps you track the recording progress, monitor the task status, and support subsequent resource management work.

## Requirements

* Rate limit: 50 queries per second per account.

* Billing: This API is used to query the recorded task records that have been created, and does not involve real\-time recording or data storage operations, so there will be no fees.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListPullRecordTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNum |Integer |Yes |`1` |The page number. The value must be greater than or equal to `1`. |
|PageSize |Integer |Yes |`5` |The number of query results per page. Valid values: `[1,500]`. |
|Vhost |String |No |`example` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|Domain |String |No |`push.example.com` |The push domain name or pull domain name used by the live stream. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|App |String |No |`live` |The application name, which has the same value as the `AppName` field in the live stream address, is used to specify the recording configuration to be updated. It is empty by default. You can call the  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the `App` value. |
|Stream |String |No |`example_stream` |The stream name, whose value corresponds to the value of the `StreamName` field in the live stream address, is used to specify the recording task to be queried and is empty by default. You can call the  [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API to obtain the value of `Stream`. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/48204#list) |`-` |List of live recording tasks. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/48204#pagination) |`-` |Paging information of the query results. |

### List

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskId |String |`f831f3b0dc******aa4dcf7621` |Task ID, the unique identifier of the task. |
|StartTime |String |`2023-06-30T15:04:05Z` |The start time of the recording, the UTC time in RFC3339 format, with a precision of seconds. |
|EndTime |String |`2023-06-30T15:05:05Z` |The end time of the recording, in UTC time in RFC3339 format, with a precision of seconds. |
|Vhost |String |`push.example.com` |Domain namespace name. |
|Domain |String |`push.example.com` |Push domain name or pull domain name. |
|App |String |`Live` |Application Name. |
|Stream |String |`example_stream` |Stream Name. |
|Status |String |`Finished` |The status of the recording task. Possible values are as follows.<br><br><br>* `停用`：The recording task has been stopped;<br><br>* `未开始`：The recording task has not started yet;<br><br>* `生效中`：The recording task is in progress;<br><br>* `已结束`：The recording has been completed. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The page number of the current page. |
|PageSize |Integer |`2` |The number of data items displayed per page. |
|PageTotal |Integer |`43` |The total number of pages of the query result data. |
|TotalCount |Integer |`86` |The total number of data items in the query result. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListPullRecordTask&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 2
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "TaskId": "f831f3b0dc******aa4dcf7621",
                "StartTime": "2023-06-30T15:04:05Z",
                "EndTime": "2023-06-30T15:05:05Z",
                "Vhost": "push.example.com",
                "Domain": "push.example.com",
                "App": "Live",
                "Stream": "example_stream",
                "Status": "Finished"
            },
            {
                "TaskId": "a1b2c3d4e5******f6g7h8i9j0",
                "StartTime": "2023-06-30T16:04:05Z",
                "EndTime": "2023-06-30T16:05:05Z",
                "Vhost": "pull.example.com",
                "Domain": "pull.example.com",
                "App": "Live",
                "Stream": "another_stream",
                "Status": "InProgress"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 2,
            "PageTotal": 43,
            "TotalCount": 86
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Unclassified error. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the description of [Request Parameters](#Request Parameters) for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter fails the validation. Please check whether the parameter type is correct. |
|403 |RequestForbidden |\- |The request is rejected. There are no requested resources (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected. There is no requested resource (domain name space, domain name, application, configuration template, certificate) under the current account. |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live broadcast service is not activated or the account is in arrears, resulting in the unavailability of the bill. Please check the activation status of the service and the arrears situation of the account. |
|404 |ResourceNotFound |\- |The resource (domain namespace, domain name, application, configuration template, certificate) was not found. It is recommended to retry. If this error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An error occurred between services, please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |There is an error between services, please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal service timeout, please [contact support](https://console.byteplus.com/workorder/create). |
