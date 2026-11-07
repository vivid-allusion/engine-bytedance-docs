---
title: "UpdateSpaceUploadConfig"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatespaceuploadconfig"
---

This interface is used to update the space upload configuration. You can update the following configurations:


* Whether the file path can be customized.

* Whether to automatically publish after the file upload is completed.


<span id="requirements"></span>
## Requirements

Prerequisite: [CreateSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-createspace) has been completed.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateSpaceUploadConfig&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateSpaceUploadConfig` |The API action. For the current API, the value is `UpdateSpaceUploadConfig`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|ConfigKey |String |Yes |`1` |The configuration that needs to be updated:<br><br><br>* `1`: Whether the file path can be customized.<br><br>* `2`: Whether to automatically publish after the file upload is completed. |
|ConfigValue |String |Yes |`true` |The configuration value, which is related to the `ConfigKey`.<br><br><br>* When the `ConfigKey` is set to `1`, the supported values for `ConfigValue` are as follows:<br><br>   * `true`: (Default) You can customize the file path using the `FileName` parameter of the [ApplyUploadInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-applyuploadinfo) interface.<br><br>   * `false`: You cannot customize the file path.<br><br>* When the `ConfigKey` is set to `2`, the supported values for `ConfigValue` are as follows:<br><br>   * `Available`: The file will be automatically published after the upload is complete.<br><br>   * `Unavailable`: (Default) The file will not be automatically published. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateSpaceUploadConfig&Version=2023-01-01&SpaceName=test&ConfigKey=1&ConfigValue=true
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "UpdateSpaceUploadConfig",
        "Region": "ap-singapore-1",
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
|400 |InvalidParameter.InvalidSpaceName |\- |Invalid `SpaceName`. |
|400 |InvalidParameter.InvalidConfigKey |\- |Invalid `ConfigKey`. |
|400 |InvalidParameter.InvalidConfigValue |\- |Invalid `ConfigValue`. |


#{.custom\-md\-table\-4}#

&nbsp;
