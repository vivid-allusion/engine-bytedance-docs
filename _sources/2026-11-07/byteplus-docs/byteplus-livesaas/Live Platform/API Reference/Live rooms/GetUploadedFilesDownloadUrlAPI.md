---
title: "GetUploadedFilesDownloadUrlAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi"
---

Call this API to get the download URLs of files uploaded on the live streaming page in a web browser or sent under the menu for interaction tools in a specific live room.

<span id="requirements"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisites:

   * Call [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) to get the file ID.

   * A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetUploadedFilesDownloadUrlAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|FileIds |Array of Long |Yes |`[1800928319729670,1800928594348037,1800929606862854]` |The IDs of the files for which to get download URLs. You can get the ID by calling [ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi).<br><br>The array can contain at most 100 file IDs. |
|ExpiredTime |Long |No |`60` |The expiration time for the download URLs, in seconds.<br><br>Unit: seconds.<br><br>Default value: `60`.<br><br>Value range: [1,300] |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|FileDownloadUrls |JSON Map |`-` |A map where each key is a file ID and the corresponding value is its download URL.<br><br><br>* `"Key"`: Long. The file ID.<br><br>* `"Value"`: String. The download URL of the file, including a protocol header. |
|FailedFileIds |Array of Long |`[1800928319729123,1800928319729222]` |The IDs of files for which URL retrieval failed. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01&ActivityId=17218312****&FileIds=1800928319729670&FileIds=1800928594348037&FileIds=1800929606862854&ExpiredTime=60
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "GetUploadedFilesDownloadUrlAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "FileDownloadUrls": {
            "1800928319729670": "https://p-imagex-boei18n.byted.org/tos-boei18n-i-fhdptwgppv/01e997353a734b5c93b153bc27c6844e~tplv-****-image.image",
            "1800928594348037": "https://livesaas-medialib.tos-ap-southeast-1.bytepluses.com/1800896790231062/File_1800896790231062.pdf?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKAPMzY3NDY5NzMyNGM2NDhkNDk2ZTQ****1NWNlZGRkOWY%2F20240604%2Ftos-ap-southeast-1%2Ftos%2Frequest&X-Tos-Date=20240604T135040Z&X-Tos-Expires=60&X-Tos-Signature=9dd51f458d2331fbd0d085f933a8e3933582e8cb5e4b8b9164b611b99****827&X-Tos-SignedHeaders=host",
            "1800929606862854": "https://livesaas-cloud-doc-sg1.tos-cn-beijing.volces.com/68a5b5e6d27740a89fe45da566a52329.pdf?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Credential=AKLTZGNlMmM1NDQwMmUxNDFkMzg5MDA3MTUwNz****IwMGY%2F20240604%2Fcn-beijing%2Ftos%2Frequest&X-Tos-Date=20240604T135040Z&X-Tos-Expires=60&X-Tos-Signature=f4525013f3436f50e784d999d3093de28c4b5fcfdd5f2f1a5ca37de****dbd7e&X-Tos-SignedHeaders=host&response-content-disposition=attachment%3Bfilename%3DFile_1800896792223766+%281%29.pdf"
        },
        "FailedFileIds": []
    }
}
  
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |**Description** |
|---|---|---|---|
|400 |InvalidParameter.FileIdsLengthExceed100 |The number of file IDs in the FileIds parameter exceeds 100. |Reduce the number of file IDs in the `FileIds` parameter. |
