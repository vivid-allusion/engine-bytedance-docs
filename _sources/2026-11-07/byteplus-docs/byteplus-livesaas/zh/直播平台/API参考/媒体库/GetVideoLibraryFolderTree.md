---
title: "GetVideoLibraryFolderTree"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetVideoLibraryFolderTree-zh-CN"
---

获取您的账户下默认分类或指定分类及其子分类的信息。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">使用IAM用户调用该API时，仅可获取该IAM用户可见的视频库分类信息。如需了解如何配置IAM用户的分类范围，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织和角色管理</a>。</div>


<span id="Requirements"></span>
## 要求


* 请求频率限制：每个账户每分钟最多120次请求

* 前提条件：需拥有BytePlus账户，或IAM用户具备**媒体库** \> **视频** \> **视频库** \> **编辑**或**仅查看**权限。如需了解如何添加IAM用户，请参见[用户、组织和角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP请求


* 方法：GET

* 接口地址：https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetVideoLibraryFolderTree` |API操作。 |
|Version |String |是 |`2023-08-01` |该API操作的版本。当前版本：`2023-08-01`。 |
|FolderId |Long |否 |`0` |分类ID。默认值为`0`，表示返回默认分类下所有子分类。 |


<span id="Response parameters"></span>
## 返回调用结果


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|FolderNode |[FolderNode](https://docs.byteplus.com/en/docs/11/113729#foldernode)对象 |`-` |分类信息。 |


<span id="foldernode"></span>
### FolderNode


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|FolderId |Long |`0` |分类ID。 |
|FolderName |String |`分类1` |分类名称。 |
|FolderTypeForSubAccount |Integer |`-` |子分类信息。 |
|Children |[Children](https://docs.byteplus.com/en/docs/11/113729#children)数组 |`0` |IAM用户调用该API时，对分类的操作权限。有效值：<br><br><br>* `0`：最高权限。IAM用户可查看并操作该分类及其资源，如删除资源或编辑分类。<br><br>* `1`：IAM用户可查看并操作该分类下的资源，但无法操作分类本身，如编辑分类或创建子分类。<br><br>* `2`：IAM用户仅可查看该分类，无法查看或操作分类下的资源。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用BytePlus账户调用该API时，该参数值固定为<code>0</code>。</div><br> |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetVideoLibraryFolderTree&Version=2023-08-01&FolderId=0
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetVideoLibraryFolderTree",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "FolderNode": {
            "FolderId": 0,
            "FolderName": "All files",
            "Children": [
                {
                    "FolderId": 17959466895819,
                    "FolderName": "Subcategory 1",
                    "Children": [
                        {
                            "FolderId": 17959465298105,
                            "FolderName": "Subcategory 2",
                            "Children": []
                        }
                    ]
                }
            ],
            "FolderTypeForSubAccount": 0
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误码和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
