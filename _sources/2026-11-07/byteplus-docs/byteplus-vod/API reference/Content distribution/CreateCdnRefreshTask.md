---
title: "CreateCdnRefreshTask"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createcdnrefreshtask"
---

This interface is used to refresh the cache under the specified space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CreateCdnRefreshTask&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateCdnRefreshTask` |The API action. For the current API, the value is `CreateCdnRefreshTask`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|Urls |String |Yes |`https://example.com` |Refresh the URL. Each URL must start with `http://` or `https://`. Multiple URLs should be separated by a newline character (`\n`). A maximum of 100 URLs can be entered.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The daily file and directory refresh quotas per space are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When the refresh task type is URL refresh, you can refresh up to 1,000 single files per day.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the refresh task type is directory refresh, you can refresh up to 50 directories per day.</div><br> |
|Type |String |Yes |`refresh_file` |Refresh the task types. The values are as follows:<br><br><br>* `refresh_file`: The URL refresh.<br><br>* `refresh_dir`: The directory refresh. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TaskId |String |`6242b7c******451a4003` |The task ID. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=CreateCdnRefreshTask&Version=2023-01-01&SpaceName=test&Urls=https://example.com&Type=refresh_file
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": {
        "TaskId": "6242b7c******451a4003"
    },
    "ResponseMetadata": {
        "Action": "CreateCdnRefreshTask",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidAccountId |\- |Invalid account ID, please adjust and try again. |
|400 |InvalidParameter.InvalidTaskType |\- |The type of the refresh task must be either URL refresh or directory refresh. The current input does not meet the specifications. Please adjust and try again. |
|400 |InvalidParameter.NoActionQuota |\- |The refresh quota has been exhausted. |


#{.custom\-md\-table\-4}#

&nbsp;
