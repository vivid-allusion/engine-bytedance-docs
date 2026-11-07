---
title: "GetUploadedFilesDownloadUrlAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getuploadedfilesdownloadurlapi-zh-CN"
---

调用此 API 以获取在网页端直播页面上传或在特定直播间的互动工具菜单下发送的文件的下载 URL。

<span id="requirements"></span>
## 要求


* 配额：每个账号每分钟 120 次查询

* 前提条件：

   * 调用[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN)以获取文件 ID。

   * 具备 BytePlus 账号或拥有 Live control \> Edit 权限的 IAM 用户。关于如何添加 IAM 用户的更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见[通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetUploadedFilesDownloadUrlAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取 ID。 |
|FileIds |Long 数组 |是 |`[1800928319729670,1800928594348037,1800929606862854]` |需要获取下载 URL 的文件 ID。可通过调用[ListUploadedFilesAPI](https://docs.byteplus.com/docs/byteplus-livesaas/listuploadedfilesapi-zh-CN)获取 ID。<br><br>该数组最多可包含 100 个文件 ID。 |
|ExpiredTime |Long |否 |`60` |下载 URL 的过期时间，单位为秒。<br><br>单位：秒。<br><br>默认值：`60`。<br><br>取值范围：[1,300] |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|FileDownloadUrls |JSON 映射 |`-` |一个映射表，每个键为文件 ID，对应的值为其下载 URL。<br><br><br>* `“Key”`：Long。文件 ID。<br><br>* `“Value”`：String。文件的下载 URL，包含协议头。 |
|FailedFileIds |Long 数组 |`[1800928319729123,1800928319729222]` |获取 URL 失败的文件 ID。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetUploadedFilesDownloadUrlAPI&Version=2020-06-01&ActivityId=17218312****&FileIds=1800928319729670&FileIds=1800928594348037&FileIds=1800929606862854&ExpiredTime=60
```


<span id="sample-response"></span>
### 返回示例

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
## 错误码

下表列出了此 API 操作特有的错误码。通用错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。


|状态码 |错误码 |错误信息 |**接口行为** |
|---|---|---|---|
|400 |InvalidParameter.FileIdsLengthExceed100 |FileIds 参数中的文件 ID 数量超过 100。 |请减少`FileIds`参数中的文件 ID 数量。 |
