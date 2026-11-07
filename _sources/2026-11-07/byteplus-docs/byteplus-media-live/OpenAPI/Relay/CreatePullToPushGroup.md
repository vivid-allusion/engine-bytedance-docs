---
title: "CreatePullToPushGroup"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushgroup-2023"
---

Call the `CreatePullToPushGroup` API to create a relay task group and bind it to a project, which allows you to manage sub\-account permissions based on the project by configuring the group.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreatePullToPushGroup` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Name |String |Yes |`group001` |The group name. It can include Chinese characters, uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), with a length ranging from 1 to 20 characters. |
|ProjectName |String |Yes |`default` |By default, it is empty, indicating that it belongs to the 'default' project.<br><br>After the group name is associated with a project, you can manage your resource usage and billing by project. You cannot change the project setting once the group name is created. To manage projects, visit the [Project](https://console.byteplus.com/iam/resourcemanage/project) page on the BytePlus console. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreatePullToPushGroup&Version=2023-01-01
{
    "Name": "RelayGroup001",
    "ProjectName": "default"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullToPushGroup",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/28688#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParameter.Tags.Key |The specified parameter Tags.Key is invalid. |The parameter `Tags.Key` fails to pass the verification. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags.Value |The specified parameter Tags.Value is invalid. |The parameter `Tags.Value` fails the verification. Please check if the parameter is correct. |
|400 |InvalidParameter.Tags |The specified parameter Tags is invalid. |The parameter `Tags` failed the validation. Please check if the parameter is correct. |
|400 |Duplicate.Tags.Key |The specified object of tags contains duplicate keys. |The value of the parameter `Tags.Key` is duplicated. Please check if the parameter is correct. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected, and there are no requested resources (domain name space, domain name, application, configuration template, certificate) under the current account. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded.Exist |the resource requested to be created already exists, please rename it |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created already exists. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.DB |an internal error related to database occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
