---
title: "DeletePlaylist"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteplaylist"
---

Delete the designated playlist. Only playlists outside their active playback time window can be deleted.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeletePlaylist&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeletePlaylist` |The API action. For the current API, the value is `DeletePlaylist`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|Id |String |Yes |`pb2d500c119ddOne4cjc77u86s7pnfag` |The playlist ID. |
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. If not provided, it will query all playlists under the current account. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DeletePlaylist&Version=2023-01-01&SpaceName=test&Id=pb2d500c119ddOne4cjc77u86s7pnfag
{
    "SpaceName": "test",
    "Id": "pb2d500c119ddOne4cjc77u86s7pnfag"
}
```


<span id="Sample response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeletePlaylist",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
