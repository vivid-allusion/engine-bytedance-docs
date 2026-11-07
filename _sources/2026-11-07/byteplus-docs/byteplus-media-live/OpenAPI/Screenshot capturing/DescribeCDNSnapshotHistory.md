---
title: "DescribeCDNSnapshotHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdnsnapshothistory-2023"
---

Call the `DescribeCDNSnapshotHistory` API to query the screenshot file information of the live stream.

## Requirements

Rate limit: 1 query per second per account.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeCDNSnapshotHistory` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |Yes |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |Yes |`stream-123` |The StreamName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters. |
|DateFrom |String |Yes |`2022-04-01T00:00:00Z` |The start time of your query's range (Local time in RFC 3339 format with second precision). When you query the details of a specified recording task, DateFrom should be set to any time before the start time of the recording task. |
|DateTo |String |Yes |`2022-04-02T00:00:00Z` |The end time of your query's range (Local time in RFC 3339 format with second precision). The DateTo needs to be later than the DateFrom, and the interval between DateTo and DateFrom should not exceed 7 days. |
|PageNum |Integer |No |`1` |The page number. The value must be greater than or equal to `1`. Default value: `1`. |
|PageSize |Integer |No |`10` |The number of query results per page. Valid values: [1,1000]. Default value: `10`.<br><br>> **说明**<br><br><br>> If you set this parameter to `0`, the default value is used.<br> |
|Type |String |No |`tos` |Storage type. Always set it to `tos`. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Data |Array of [Data](https://docs.byteplus.com/en/docs/24/27449#data) |`-` |A list of screenshot records. |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/27449#pagination) |`-` |Page information. |

### Data

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|Stream |String |`stream-123` |The StreamName field. |
|Path |String |`20210830135051697.jpeg` |The path where the screenshot file is saved. |
|TimeStamp |String |`2021-08-30 21:48:25.000` |Screenshot timestamp with millisecond precision. |
|Width |Integer |`720` |Screenshot width in px. |
|Height |Integer |`1280` |Screenshot height in px. |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageCur |Integer |`1` |The current page number. |
|PageSize |Integer |`10` |The number of results on each page. |
|PageTotal |Integer |`231` |The total number of pages. |
|TotalCount |Integer |`4613` |The total number of recording files retrieved.。 |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNSnapshotHistory&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2022-04-01T00:00:00Z",
    "DateTo": "2022-04-02T00:00:00Z"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeCDNSnapshotHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "App": "live",
                "FileSize": 0,
                "Height": 1280,
                "Path": "20210830135051697.jpeg",
                "Stream": "testStream413",
                "TimeStamp": "2021-08-30 21:48:25.000",
                "Vhost": "example.org",
                "Width": 720
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 231,
            "TotalCount": 4613
        }
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27449#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
