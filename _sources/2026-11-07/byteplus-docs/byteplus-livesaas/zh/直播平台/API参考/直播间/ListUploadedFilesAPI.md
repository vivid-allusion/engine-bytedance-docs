---
title: "ListUploadedFilesAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN"
---

获取通过网页浏览器在直播页面上传或在特定直播间的互动工具菜单下发送的文件列表。要获取文件的下载 URL，可使用返回调用结果中的文件 ID 调用[GetUploadedFilesDownloadUrlAPI](https://docs.byteplus.com/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN)。

<span id="requirements"></span>
## 要求


* 配额：每个账号每分钟 120 次查询

* 前提条件：拥有 BytePlus 账号或具备 Live control \> Edit 权限的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见[通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListUploadedFilesAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|FileType |Integer |否 |`0` |指定要返回的文件类型。<br><br>默认值：`0`。<br><br>可选值：<br><br><br>* `0`：通过网页浏览器在直播页面上传的文档和图片，以及在互动工具菜单下发送的文档和图片。<br><br>* `1`：通过网页浏览器在直播页面上传的文档和图片。<br><br>* `2`：在互动工具菜单下发送的文档。<br><br>* `3`：在互动工具菜单下发送的图片。 |
|OrderType |Integer |否 |`0` |指定返回文件的排序方式（按上传时间或发送时间）。<br><br>默认值：`0`。<br><br>可选值：<br><br><br>* `0`：降序。<br><br>* `1`：升序。 |
|PageNumber |Long |否 |`1` |要返回的页码。默认值：`1`。 |
|PageSize |Long |否 |`100` |每页返回的结果数量。默认值：`100`。<br><br>取值范围：[1,1000]。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PageNumber |Long |`1` |返回的页码。 |
|PageSize |Long |`100` |每页返回的结果数。 |
|TotalCount |Long |`3` |文件总数。 |
|Files |Array of[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN) |`-` |返回的文件列表。 |


<span id="uploadedfile"></span>
### UploadedFile


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|FileId |Long |`180092831972****` |文件 ID。 |
|FileName |String |`File_180089679222****.pdf` |文件名。 |
|UploadTime |Long |`1717499084` |文件上传或发送时的 Unix 时间戳（单位：秒）。 |
|FileSize |Long |`330971` |文件大小。单位：字节。 |
|FileType |Integer |`0` |文件类型。<br><br><br>* `1`：通过网页浏览器在直播页面上传的文档和图片。<br><br>* `2`：在互动工具菜单下发送的文档。<br><br>* `3`：在互动工具菜单下发送的图片。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListUploadedFilesAPI&Version=2020-06-01&ActivityId=17218312****&FileType=0&OrderType=0&PageNumber=1&PageSize=100
```


<span id="sample-response"></span>
### 返回示例

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
## 错误码

通用错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
