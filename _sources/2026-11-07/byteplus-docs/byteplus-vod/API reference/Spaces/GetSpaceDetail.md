---
title: "GetSpaceDetail"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getspacedetail"
---

This interface is used to obtain detailed information about the VOD space using the `SpaceName` parameter. The space information includes the region to which the space belongs, a specific description of the space, and the creation time of the space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetSpaceDetail&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetSpaceDetail` |The API action. For the current API, the value is `GetSpaceDetail`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`doc-test` |The VOD space name. You can call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`doc-test` |The VOD space name. |
|Region |String |`ap-singapore-1` |The account ID region. |
|ProjectName |String |`default` |The IAM project name. |
|BucketName |String |`tos-vod-cn-v-16fd9e8343bb****` |The bound storage bucket name. |
|BucketStatus |String |`configure_success` |The status of the bound storage bucket. The values are as follows:<br><br><br>* `configure_success`: Configuration successful.<br><br>* `configuring`: Configuring.<br><br>* `configure_error`: Configuration failed. |
|Description |String |`test` |The VOD space description. |
|UserName |String |`byte_****` |The user name of the space creator. |
|CreatedAt |String |`2022-04-15T19:42:59Z` |The space creation time, which follows the RFC 3339 standard, formatted as yyyy\-MM\-ddTHH:mm:ssZ. |
|Type |String |`space` |The type. The current value is only `space`. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetSpaceDetail&Version=2023-07-01&SpaceName=doc-test
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSpaceDetail",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Type": "space",
        "Region": "ap-singapore-1",
        "UserName": "byte_****",
        "CreatedAt": "2022-04-15T19:42:59Z",
        "SpaceName": "doc-test",
        "BucketName": "tos-vod-cn-v-16fd9e8343bb****",
        "Description": "test",
        "ProjectName": "default",
        "BucketStatus": "configure_success"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
