---
title: "CreateSpace"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createspace"
---

This interface is used to set the `SpaceName`, select parameters such as `ProjectName`, and create a space under the Video on Demand (VOD) account. Space is the basic unit of isolation for VOD resources.

<span id="requirements"></span>
## Requirements


* The space name cannot be duplicated.

* Once the space is created, the space name and region cannot be changed.

* By default, a single account can create up to 20 spaces.


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CreateSpace&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateSpace` |The API action. For the current API, the value is `CreateSpace`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`ch-test` |Space Name. The length should be between 3 to 40 characters. The following characters are supported:<br><br><br>* Lowercase letters<br><br>* Numbers<br><br>* Hyphens (\-)<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Notes</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The beginning and end must be either a lowercase letter or a number.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Once the space is created, the space name and region cannot be changed. It is recommended to use a space name that clearly identifies your business.</div><br> |
|ProjectName |String |Yes |`default` |Project Name. A project represents a way to group resources. You need to add the space to a specific project. You can obtain the project name on the BytePlus console [Project Management](https://console.byteplus.com/auth/login?redirectURI=%2Fiam%2Fresourcemanage%2Fproject) page. |
|Description |String |Yes |`test` |Space description. Length should be between 0 and 140 characters. |
|Region |String |Yes |`ap-southeast-1` |Space region. Only `ap-southeast-1` is supported. |
|UserName |String |Yes |`test` |The user name of the space creator. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=CreateSpace&Version=2023-01-01&SpaceName=ch-test&ProjectName=default&Description=test&Region=ap-southeast-1&UserName=test
{
    "SpaceName": "ch-test",
    "ProjectName": "default",
    "Description": "test",
    "Region": "ap-southeast-1",
    "UserName": "test"
}
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateSpace",
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
|400 |InvalidParameter.InvalidSpaceName |*  |Invalid space name. The reasons for the error are as follows:<br><br><br>* Incorrect length of input. The space name must be between 3 and 40 characters in length.<br><br>* Incorrect format. The format must consist of a combination of lowercase letters, numbers, and hyphens (\-), with the start and end of the name being a lowercase letter or number. |
|400 |InvalidParameter.InvalidProjectName |\- |Invalid project name. |
|400 |InvalidParameter.InvalidDescription |\- |Invalid description. |
|400 |InvalidParameter.InvalidRegion |\- |Invalid region. |
|403 |RequestForbidden.AccessIsRestricted |\- |Account access is restricted. |


#{.custom\-md\-table\-4}#

&nbsp;
