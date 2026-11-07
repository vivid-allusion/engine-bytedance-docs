---
title: "DeleteMediaTosFile"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/deletemediatosfile"
---

Call the `DeleteMediaTosFile` interface to delete the media file by the `FileName`(the file path).

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">This API is currently available only in the Asia Pacific (Johor) region.</div>


<span id="HTTP request"></span>
## HTTP request

Endpoint：https://vod.byteplusapi.com?Action=DeleteMediaTosFile&Version=2023\-07\-01

<span id="Request parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|**Parameter**  |**Data Type**  |**Required**  |**Sample Value**  |**Description**  |
|---|---|---|---|---|
|Action |String |Yes |`DeleteMediaTosFile` |The API action. For the current API, the value is `DeleteMediaTosFile`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|FileNames |Array of String |No |`["testFileName1","testFileName2"]` |An array of file paths, supporting up to 1000 entries. |
|SpaceName |String |No |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. |


<span id="Response parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|**Parameter**  |**Data Type**  |**Sample Value**  |**Description**  |
|---|---|---|---|
|FailedFileNames |Array of String |`["/path/to/failed/file1.txt","/path/to/failed/file2.jpg"]` |An array of file paths that failed to be deleted. |


<span id=".6K-35rGC56S65L6L"></span>
## 请求示例

```JSON
https://vod.byteplusapi.com?Action=DeleteMediaTosFile&Version=2023-07-01
{
    "FileNames": [
        "testFileName1",
        "testFileName2"
    ],
    "SpaceName": "test"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## 返回示例

```JSON
{
    "Result": {
        "FailedFileNames": [
            "/path/to/failed/file1.txt",
            "/path/to/failed/file2.jpg"
        ]
    },
    "ResponseMetadata": {
        "Action": "DeleteMediaTosFile",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="Error codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).
