---
title: "ListPullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023"
---

Call the `ListPullToPushGroup` API to query a list of group name.

<span id="requirements"></span>
## Requirements

Rate limit: 10 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListPullToPushGroup` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNum |Integer |Yes |`1` |Page number. BytePlus MediaLive divides the query results into pages and only returns the results on the specified page. Valid range: 1–1000. |
|PageSize |Integer |Yes |`10` |The number of results on each page. Valid range: 1–1000. |
|StatusList |Array of Integer |No |`0` |The status of the group, and the values and their meanings are as follows.<br><br><br>* `0`: (default) Available;<br><br>* `1`: Deleted, not available. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|List |Array of [List](https://docs.byteplus.com/en/docs/24/28691#list) |`-` |The list of group infomations. |
|Total |Integer |`1` |The number of data bars for the query result. |


<span id="list"></span>
### List


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`group001` |Group name. |
|ProjectName |String |`default` |The project to which the group belongs. |
|Status |Integer |`0` |The status of the group, and the values and their meanings are as follows.<br><br><br>* `0`: (default) Available;<br><br>* `1`: Deleted, not available. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListPullToPushGroup&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListPullToPushGroup",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "List": [
            {
                "Name": "Group001",
                "ProjectName": "default",
                "Status": 0
            }
        ],
        "Total": 1
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/28691#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParameter.Tags.Key |The specified parameter Tags.Key is invalid. |The parameter `Tags.Key` fails the verification. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags.Value |The specified parameter Tags.Value is invalid. |The parameter `Tags.Value` fails the validation. Please check if the parameter is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded.Exist |the resource requested to be created already exists, please rename it |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
