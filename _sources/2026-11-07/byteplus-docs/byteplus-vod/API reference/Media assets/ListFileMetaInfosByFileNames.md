---
title: "ListFileMetaInfosByFileNames"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/listfilemetainfosbyfilenames"
---

Call the `ListFileMetaInfosByFileNames` API to obtain media assets information by the `FileName`, including the corresponding video ID (`Vid`), material ID (`MaterialId`), or image ID (`Pid`).

## Requirements

* This API is currently available only in the Asia Pacific (Johor) region. To enable this feature, please [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112) to contact BytePlus support team.

* For the `FileNameEncodeds` request parameter, any `FileName` value must be URL\-encoded to ensure special characters are handled correctly.

   * For `FileName` containing reserved characters (`$`, `&`, `+`, `,`, `/`, `:`, `;`, `=`, `?`, `@`), except for safe characters (`@`, `&`, `=`, `+`, `$`) which are considered safe and must be retained as\-is, other characters must be URL encoded according to the RFC3986 standard.

   * Example:

      * **Original** \*\*`FileName`: \*\*`abc/ /!/*/'/(/;/:/@/&/=/+/$/,/?/#/[/1.mp4`

      * **Correctly Encoded** **`FileName`** **:** `abc%2F%20%2F%21%2F%2A%2F%27%2F%28%2F%3B%2F%3A%2F@%2F&%2F=%2F+%2F$%2F%2C%2F%3F%2F%23%2F%5B%2F1.mp4`

## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListFileMetaInfosByFileNames&Version=2023\-07\-01

## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListFileMetaInfosByFileNames` |The API action. For the current API, the value is `ListFileMetaInfosByFileNames`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`test` |The space name. You can call [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) to obtain the names of all spaces under the current account. |
|FileNameEncodeds |String |No |`a%2Fb%2Fc,b%2Fb%2Fc` |The URL\-encoded file path `FileName` to be queried. Multiple paths should be connected with commas `,`, with a maximum of 30 paths per request. |
|BucketName |String |No |`tos-vod-v-r3984tu***` |The storage bucket name. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|VodFileMetaInfos |Array of [VodFileMetaInfos](https://docs.byteplus.com/en/docs/25/63299#vodfilemetainfos) |`-` |An array containing the metadata information of media files. |

### VodFileMetaInfos

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vid |String |`v02e61g10001**9s1v0h2fqmdk80` |Video ID. If the media assets file has no transcoded output, the returned `Vid` and `FileId` values are the same. |
|Pid |String |`i18f06gm0018db8at0itgd6bem70tiug` |The image asset ID, returned for image files whose `FileType` is `ImageUri`. |
|FileId |String |`v02e61g10001***9s1v0h2fqmdk80` |The file ID. For image files, this identifies the corresponding image file. For audio/video assets without transcoded output, `FileId` and `Vid` are the same. |
|MaterialId |String |`v02e61g10001**9s1v0h2fqmdk80` |Material ID.<br><br>> **Note**<br><br><br>> When the `FileType` parameter in the returned list is `MaterialUri`, the returned `MaterialId` parameter contains a specific ID.<br> |
|FileType |String |`MediaUri` |The type of the file indicated by the URI. Possible values are as follows:<br><br><br>* `PosterUri`: the cover image URI<br><br>* `TranscodeUri`: the transcoded stream URI<br><br>* `MediaUri`: the original media assets URI<br><br>* `MaterialUri`: the material URI<br><br>* `ImageUri`: the image asset file URI<br><br>* `PostCandidateUri`: the cover candidate URI<br><br>* `AnimatedImageUri`: the looped screenshot URI<br><br>* `DynpostUri`: the animated image URI<br><br>* `PosterUriEx`: the static screenshot URI<br><br>* `DrsChoiceUri`<br><br>* `Unknown`: the unknown type |
|FileName |String |`a/b/c` |The file path |
|FileNameEncoded |String |`a%2Fb%2Fc` |The URL\-encoded file path |

## Samples

### Sample request

```text
https://vod.byteplusapi.com?Action=ListFileMetaInfosByFileNames&Version=2023-07-01&BucketName=tos-vod-v-r3984tu***&FileNameEncodeds=a/b/c,b/b/c&SpaceName=test
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListFileMetaInfosByFileNames",
        "Version": "2023-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "VodFileMetaInfos": [
            {
                "Vid": "v02e61g10001**9s1v0h2fqmdk80",
                "FileId": "v02e61g10001***9s1v0h2fqmdk80",
                "MaterialId": "v02e61g10001**9s1v0h2fqmdk80",
                "FileType": "MediaUri",
                "FileName": "a/b/c",
                "FileNameEncoded": "a%2Fb%2Fc"
            }
        ]
    }
}
```

## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
