---
title: "GetFileInfos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/getfileinfos"
---

Call `GetFileInfos`to obtain the file information in DirectUrl mode.

<span id="requirements"></span>
## Requirements


* This API is currently available only in the Asia Pacific (Johor) region. To enable this feature, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) to contact BytePlus support team.

* For the `EncodedFileNames` request parameter, any `FileName` value must be URL\-encoded to ensure special characters are handled correctly.

   * For `FileName` containing reserved characters (`$`, `&`, `+`, `,`, `/`, `:`, `;`, `=`, `?`, `@`), except for safe characters (`@`, `&`, `=`, `+`, `$`) which are considered safe and must be retained as\-is, other characters must be URL encoded according to the RFC3986 standard.

   * Example:

      * **Original** \*\*`FileName`: \*\*`abc/ /!/*/'/(/;/:/@/&/=/+/$/,/?/#/[/1.mp4`

      * **Correctly Encoded** **`FileName`** **:** `abc%2F%20%2F%21%2F%2A%2F%27%2F%28%2F%3B%2F%3A%2F@%2F&%2F=%2F+%2F$%2F%2C%2F%3F%2F%23%2F%5B%2F1.mp4`


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=GetFileInfos&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetFileInfos` |The API action. For the current API, the value is `GetFileInfos`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`test` |The space name. You can call the [ListSpace](https://www.volcengine.com/docs/4/107686) API to obtain the names of all spaces under the current account. |
|EncodedFileNames |String |Yes |`a%2Fb%2Fc,d%2Fe%2Ff` |The URL\-encoded file path `FileName` to be queried. Multiple paths should be connected with commas `,`, with a maximum of 30 paths per request. |
|BucketName |String |No |`tos-vod-v-r3984tu***` |The storage bucket name. |
|NeedDownloadUrl |Boolean |No |`true` |Whether to return the file download URL. The possible values are as follows:<br><br><br>* `true`: Return the file download URL.<br><br>* `false`: (Default) Do not return the file download URL. |
|DownloadUrlNetworkType |String |No |`vpc-inner` |The network type of the file download URL. This field is required when `NeedDownloadUrl` is set to `true`. Currently, only `vpc-inner`([Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/What-is-VPC)) is supported. |
|DownloadUrlExpire |Long |No |`3600` |The expiration time of the file download URL, in seconds. This field takes effect only when `NeedDownloadUrl` is set to `true`. The default value is `3600`, and the maximum supported value is 12 hours (43200 seconds). |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|FileInfos |Array of [VodFileInfo](https://docs.byteplus.com/en/docs/25/63300#vodfileinfo) |`-` |The file information. |
|NotExistFileNames |Array of String |`["nonexistent_file1.txt","nonexistent_file2.jpg"]` |An array of file names that do not exist. |
|NotExistEncodedFileNames |Array of String |`["nonexistent%2Ffile1.txt","nonexistent%2Ffile2.jpg"]` |An array of file names that do not exist in the storage, provided in URL\-encoded format. |


#{.custom\-md\-table\-4}#

<span id="vodfileinfo"></span>
### VodFileInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Size |Long |`32202259` |The file size, in bytes. |
|FileName |String |`a/b/c` |The file path. |
|HashCrc64 |String |`13315235144480327334` |The download URL of the file. This field is returned only when the `NeedDownloadUrl` parameter is set to `true`. The URL includes necessary authentication parameters for secure access. |
|DownloadUrl |String |`https://examplebucket.example.com/example.flv?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=example&X-Tos-Date=20240913T092453Z&X-Tos-Expires=3600&X-Tos-Security-Token=example&X-Tos-Signature=example&X-Tos-SignedHeaders=host` |The file download URL. It is returned only when the `NeedDownloadUrl` is `true`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default storage bucket region is <strong>Asia Pacific (Johor)</strong>. Please ensure that your VPC can connect to this region.</div><br> |
|StorageClass |String |`STANDARD` |The file storage type:<br><br><br>* `STANDARD`: The standard storage |
|EncodedFileName |String |`a%2Fb%2Fc` |The URL\-encoded file path. |
|LastModifiedTime |String |`2024-05-11T11:51:06Z` |The latest modification time. The date format is required to comply with the RFC3339 standard. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=GetFileInfos&Version=2023-07-01&SpaceName=test&EncodedFileNames=a/b/c&BucketName=tos-vod-v-r3984tu***&NeedDownloadUrl=true&DownloadUrlNetworkType=vpc-inner&DownloadUrlExpire=3600
```


<span id="Sample response"></span>
### Sample response

```json
{
    "Result": {
        "FileInfos": [
            {
                "Size": 32202259,
                "FileName": "a/b/c",
                "HashCrc64": "13315235144480327334",
                "DownloadUrl": "https://examplebucket.tos-cn-beijing.example.com/example.flv?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=example&X-Tos-Date=20240913T092453Z&X-Tos-Expires=3600&X-Tos-Security-Token=example&X-Tos-Signature=example&X-Tos-SignedHeaders=host",
                "StorageClass": "STANDARD",
                "EncodedFileName": "a%2Fb%2Fc",
                "LastModifiedTime": "2024-05-11T11:51:06Z"
            }
        ],
        "NotExistFileNames": [
            "nonexistent_file1.txt",
            "nonexistent_file2.jpg"
        ],
        "NotExistEncodedFileNames": [
            "nonexistent%2Ffile1.txt",
            "nonexistent%2Ffile2.jpg"
        ]
    },
    "ResponseMetadata": {
        "Action": "GetFileInfos",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
