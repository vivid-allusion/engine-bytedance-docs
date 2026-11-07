---
title: "ListUploadedFilesAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listuploadedfilesapi"
---

Gets the list of files uploaded on the live streaming page in a web browser or sent under the menu for interaction tools in a specific live room. To get the download URL of a file, you can use the file ID from the response to call [GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi).

<span id="requirements"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisite: A BytePlus account or an IAM user with Live control \> Edit permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListUploadedFilesAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|FileType |Integer |No |`0` |Specifies the type of files to return.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Documents and pictures uploaded on the live streaming page in a web browser and those sent under the menu for interaction tools.<br><br>* `1`: Documents and pictures uploaded on the live streaming page in a web browser.<br><br>* `2`: Documents sent under the menu for interaction tools.<br><br>* `3`: Pictures sent under the menu for interaction tools. |
|OrderType |Integer |No |`0` |Specifies the sort order for the files to be returned based on the upload time or send time.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: In descending order.<br><br>* `1`: In ascending order. |
|PageNumber |Long |No |`1` |The number of the page to return. Default value: `1`. |
|PageSize |Long |No |`100` |The number of results to return on each page. Default value: `100`.<br><br>Value range: [1,1000]. |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNumber |Long |`1` |The returned page number. |
|PageSize |Long |`100` |The number of results per page. |
|TotalCount |Long |`3` |The total number of files. |
|Files |Array of [UploadedFile](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi) |`-` |List of returned files. |


<span id="uploadedfile"></span>
### UploadedFile


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|FileId |Long |`180092831972****` |The file ID. |
|FileName |String |`File_180089679222****.pdf` |The file name. |
|UploadTime |Long |`1717499084` |The Unix timestamp (in seconds) when the file was uploaded or sent. |
|FileSize |Long |`330971` |The file size. Unit: bytes. |
|FileType |Integer |`0` |The type of the file.<br><br><br>* `1`: Documents and pictures uploaded on the live streaming page in a web browser.<br><br>* `2`: Documents sent under the menu for interaction tools.<br><br>* `3`: Pictures sent under the menu for interaction tools. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01&ActivityId=17218312****&FileType=0&OrderType=0&PageNumber=1&PageSize=100
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "20180604110420010010****0022D30",
    "Action": "ListUploadedFilesAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1717593301
  },
    "Result": {
        "PageNumber": 1,
        "PageSize": 100,
        "TotalCount": 3,
        "Files": [
            {
                "FileId": 180092831972****,
                "FileName": "01e997353a734b5c93b153bc27c6844e~tplv-fhdptw****-image.image",
                "UploadTime": 1717499084,
                "FileSize": 1024,
                "FileType": 3
            },
            {
                "FileId": 1800928594348037,
                "FileName": "File_180089679222****.pdf",
                "UploadTime": 1717499346,
                "FileSize": 330971,
                "FileType": 2
            },
            {
                "FileId": 1800929606862854,
                "FileName": "File_180089679222****.pdf",
                "UploadTime": 1717500309,
                "FileSize": 330971,
                "FileType": 1
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
