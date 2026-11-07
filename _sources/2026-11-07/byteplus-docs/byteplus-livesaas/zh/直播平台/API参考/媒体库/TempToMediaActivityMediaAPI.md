---
title: "TempToMediaActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/TempToMediaActivityMediaAPI-zh-CN"
---

将视频从临时存储转移到视频库中的指定分类，以实现永久存储。视频在转移后将从临时存储中删除。

<span id="Requirements"></span>
## 要求


* 请求频率限制：每个账号每分钟最多120次请求

* 前提条件：需拥有BytePlus账号，或具有**媒体库** \> **视频** \> **临时存储** \> **编辑**权限的IAM用户。如需了解如何添加IAM用户，请参见[用户、组织和角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* 接口地址：https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`TempToMediaActivityMediaAPI` |API操作。 |
|Version |String |是 |`2020-06-01` |该API操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Ids |字符串数组 |是 |`["409144","409154"]` |需转移的视频ID。你可以根据`Id`返回调用结果参数获取[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi)中的视频ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">最多可配置100个ID。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">使用IAM用户调用该API时，请确保IAM用户可访问或编辑视频。如需了解如何配置IAM用户的用户范围和分类范围，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织和角色管理</a>。</div><br> |
|FolderId |Long |否 |`48921` |分类ID。视频将转移到该ID对应的分类。默认值为`0`，表示视频将转移到默认分类。你可以通过调用[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree)获取分类ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用IAM用户调用该API时，如需传递该参数，请确保该ID对应的分类对IAM用户可见。如需了解如何配置IAM用户的分类范围，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织和角色管理</a>。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Success |Boolean |`false` |视频是否转移成功。有效值：<br><br><br>* `true`：成功，表示所有视频均转移成功。<br><br>* `false`：失败，表示有一个或多个视频转移失败。 |
|FailedList |[FailedList](https://docs.byteplus.com/en/docs/11/113728#failedlist)数组 |`-` |转移失败的视频列表。仅当有一个或多个视频转移失败时返回该列表，即`Success`值为`false`。 |


<span id="failedlist"></span>
### FailedList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Id |String |`409144` |视频ID。 |
|Name |String |`video1` |视频名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=TempToMediaActivityMediaAPI&Version=2020-06-01
{
    "Ids": [
        "409144",
        "409154"
    ],
    "FolderId": 48921
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "TempToMediaActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Success": false,
        "FailedList": [
            {
                "Id": "409144",
                "Name": "video1"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误码及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
