---
title: "ListLiveVideoQualityAnalysisTasks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023"
---

Call the `ListLiveVideoQualityAnalysisTasks` API to query the list of video quality analysis task information.

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListLiveVideoQualityAnalysisTasks` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Names |Array of String |No |`["test"]` |List of queried task names, default is empty, indicating that the query results will not be filtered by task name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> and <code>ID</code> cannot be input at the same time.</div><br> |
|IDs |Array of Long |No |`[23123523]` |The list of task IDs for query, default is empty, which means the query result does not filter by task ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> and <code>ID</code> cannot be input at the same time.</div><br> |
|PageNum |Integer |Yes |`1` |Page number for data retrieval, which must be a positive integer. |
|PageSize |Integer |Yes |`10` |The number of data entries displayed per page is maximum 1000. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Tasks |Array of [Tasks](https://docs.byteplus.com/en/docs/24/27710#tasks) |`-` |Video quality analysis task list. |
|PageNum |Integer |`1` |The page number of the queried data. |
|PageSize |Integer |`10` |Number of items displayed per page. |


<span id="tasks"></span>
### Tasks


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`concert` |Task name. |
|SrcURL |String |`https://pull.example.com/live/example_stream.flv` |The streaming address for analysis. |
|Interval |Integer |`5` |The interval for quality analysis points, in seconds. The default is 10, with a valid range between 3 and 10. |
|Duration |Integer |`300` |The duration of the analysis task |
|ID |Long |`23123523` |Task ID. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10,
    "IDs": [
        23123523
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListLiveVideoQualityAnalysisTasks",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "Name": "test",
                "SrcURL": "https://pull.example.com/live/example_stream.flv",
                "Interval": 5,
                "Duration": 300,
                "ID": 23123523
            }
        ],
        "PageNum": 1,
        "PageSize": 10
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27710#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Empty |%s is required |The parameter is missing. Please check if the parameter specified in the error message is passed in. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.Length |%s should not be longer than %d |The parameter length is incorrect. Please check if the length of the specified parameter in the error message exceeds the limit. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|400 |InvalidParam.TimeLogic |startTime later than endTime, etc. |The passed\-in time parameter does not conform to the logic of time. Please check if the following problems exist:<br><br><br>* The start time is later than the end time.<br><br>* The expiration time is earlier than the current time. |
|400 |InvalidParam.DomainAndApp |domain and app exist can not exist at the same time |You cannot pass in Domain and App simultaneously. Please modify the input parameters. |
|400 |InvalidParam.VhostOrDomainEmpty |Please enter vhost or domain |One of Vhost or Domain needs to be passed in as an input parameter. Please modify the input parameters. |
|400 |InvalidParam.StillUsing |%s is still in use, can't delete |The resource specified in the error message is in use, which causes it to not be deleted. Please release the resource and try again. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|404 |ResourceNotFound.VhostNotExist |vhost not found |The domain name space (Vhost) was not found. Please check if the passed\-in domain name space is consistent with the actual domain name space in use. |
|404 |ResourceNotFound.DomainNotExist |domain not found |The domain name (Domain) was not found. Please check if the passed\-in domain name is consistent with the actual domain name in use. |
|404 |ResourceNotFound.AppNotExist |app not found |The app name (App) was not found. Please check if the passed\-in app name is consistent with the actual app name in use. |
|404 |ResourceNotFound.PresetNotExist |preset not found |The configuration was not found. Please check if the passed\-in configuration is consistent with the created configuration. |
|429 |RequestLimitExceeded |\- |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created exceeds the limit. |
|429 |RequestLimitExceeded.Exist |%s already exist |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name space (Vhost) or domain name (Domain) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.ServicesOrBilling |an internal error related to service or billing occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Stream |an internal error related to stream occurred, please contact the administrator. |An internal error related to stream occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
