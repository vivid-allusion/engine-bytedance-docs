---
title: "ListActivityMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ListActivityMediaAPI-zh-CN"
---

获取媒体库下视频库或临时存储中的视频信息，包括视频ID和名称。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">使用IAM用户调用本API时，仅可获取该IAM用户有权限访问或编辑的视频信息。有关如何配置IAM用户的用户范围和分类范围的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织和角色管理</a>。</div>


<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每分钟最多120次请求

* 前提条件：需拥有BytePlus账号或具备以下权限的IAM用户。有关如何添加IAM用户的更多信息，请参见[用户、组织和角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

   * **媒体库** \> **视频** \> **临时存储** \> **编辑**或**仅查看**权限：用于获取临时存储中的视频信息。

   * **媒体库** \> **视频** \> **视频库** \> **编辑**或**仅查看**权限：用于获取视频库中的视频信息。


<span id="HTTP request"></span>
## HTTP请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityMediaAPI` |API操作。 |
|Version |String |是 |`2020-06-01` |本API操作的版本。当前版本：`2020-06-01`。 |
|PageNum |Integer |否 |`1` |要返回的页码。默认值：`1`。该值必须大于等于1。 |
|PageSize |Integer |否 |`10` |每页返回的结果数量。默认值：`10`。 |
|SearchType |Integer |是 |`2` |视频的存储位置。可选值：<br><br><br>* `1`：视频库<br><br>* `2`：临时存储 |
|Vid |String |否 |`v02a49g10000ckitq63c77u8uhf09ebg` |视频的Vid。 |
|Name |String |否 |`A` |视频名称，支持模糊搜索，不区分大小写。例如，若参数值为`A`，则会返回名称为`Video A`和`video abc`等视频。 |
|SourceType |Integer |否 |`2` |视频来源。默认返回所有来源的视频。可选值：<br><br><br>* `1`：上传，即本地上传的视频。<br><br>* `2`：录制，即直播流结束后自动生成的视频。<br><br>* `3`：云剪辑，即通过云剪辑功能剪辑生成的视频。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>SearchType</code>的值为<code>1</code>时，该参数才生效。</div><br> |
|OrderKey |String |否 |`create_time` |视频的排序方式。默认按更新时间倒序排列。可选值：<br><br><br>* `create_time`：按视频创建时间倒序排列。<br><br>* `Other values`：按视频更新时间倒序排列。更新时间指视频信息（如封面图、名称）被更新的时间。 |
|FolderId |Long |否 |`0` |分类ID。返回该ID分类下的视频。默认值为`0`，表示返回所有分类下的视频。可通过调用[GetVideoLibraryFolderTree](https://docs.byteplus.com/en/docs/byteplus-livesaas/getvideolibraryfoldertree)获取分类ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当<code>SearchType</code>的值为<code>1</code>时，该参数才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">使用 IAM 用户调用此 API 时，若需要传递此参数，请确保具有该 ID 的分类对 IAM 用户可见。关于如何配置 IAM 用户的分类范围的更多信息，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles">用户、组织和角色管理</a>。</div><br> |
|IncludeSubFolder |Boolean |否 |`false` |是否包含子分类。默认值：`false`。可选值：<br><br><br>* `true`：包含，表示会返回当前分类及其子分类下的所有视频。<br><br>* `false`：不包含，表示只返回当前分类下的视频。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>SearchType</code>的值为<code>1</code>时，此参数才生效。</div><br> |
|IsCloseDated |Boolean |No |`true` |是否筛选30天内到期的直播暂存，仅在SearchType为2时生效。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/11/113726#data)数组 |`-` |返回的视频列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/11/113726#pagination)对象 |`-` |分页信息。 |


<span id="data"></span>
### 数据


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Id |String |`430998` |视频的ID。 |
|MediaName |String |`video A` |视频名称。 |
|CoverImage |String |`https://www.example.com.image` |视频封面图URL。默认封面图的URL带有协议头，通过控制台上传的封面图URL不带协议头。 |
|Vid |String |`v02a49g10000ckitq63c77u8uhf09ebg` |视频的Vid。 |
|MediaVideoDuration |Integer |`191` |视频时长。单位：秒。 |
|MediaLibraryVideoType |Integer |`2` |视频的存储位置。有效值：<br><br><br>* `1`：视频库<br><br>* `2`：临时存储 |
|ReviewStatus |Integer |`2` |视频的审核状态。有效值：<br><br><br>* `1`：未审核。<br><br>* `2`：已审核 |
|CreateTime |Integer |`1696980251` |视频的创建时间，Unix时间戳格式。单位：秒。若视频从临时存储转移到视频库，则表示转移到视频库的时间。 |
|UpdateTime |Integer |`1696990559` |视频最近一次更新时间，Unix时间戳格式，表示视频信息（如封面图、名称）最后一次被更新的时间。单位：秒。 |
|Creator |String |`admin@bytedance.com` |视频的创建者。值`admin@bytedance.com`表示当前视频由BytePlus账号创建。 |
|SourceType |Integer |`2` |视频来源。有效值：<br><br><br>* `1`：上传，表示视频为本地上传。<br><br>* `2`：录制，表示直播流结束后自动生成视频。<br><br>* `3`：云剪辑，表示通过云剪辑功能剪辑视频。 |
|ActivityVideo |[ActivityVideo](https://docs.byteplus.com/en/docs/11/113726#activityvideo)数组 |`-` |与视频关联的直播间，表示正在使用该视频的直播间。 |
|FailureTime |Integer |`1796980251` |视频的过期时间。值`0`表示视频永久保存，无过期时间。 |
|MediaSize |Integer |`24725029` |视频大小。单位：字节。 |
|VideoWidth |Long |`1080` |视频的水平像素数。`VideoWidth`和`VideoHeight`共同决定视频分辨率。 |
|VideoHeight |Long |`1920` |视频的垂直像素数。`VideoWidth`和`VideoHeight`共同决定视频分辨率。 |
|FolderName |String |`Category A` |分类名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>MediaLibraryVideoType</code>的值为<code>1</code>时，此参数才生效。</div><br> |
|FolderId |Long |`0` |分类ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>MediaLibraryVideoType</code>的值为<code>1</code>时，此参数才生效。</div><br> |


<span id="pagination"></span>
### 分页


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageNum |Integer |`1` |返回页码。 |
|PageSize |Integer |`10` |每页返回的结果数量。 |
|TotalCount |Integer |`1` |返回的视频总数。 |


<span id="activityvideo"></span>
### ActivityVideo


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Id |Long |`1779341234622756` |直播间的活动ID。 |
|Name |String |`Live room A` |直播间名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListActivityMediaAPI&Version=2020-06-01&PageNum=1&PageSize=10&SearchType=2&Vid=v02a49g10000ckitq63c77u8uhf09ebg&Name=A&SourceType=2&OrderKey=create_time&FolderId=0&IncludeSubFolder=false
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListActivityMediaAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Data": [
            {
                "Id": "430998",
                "MediaName": "video A",
                "CoverImage": "https://www.example.com.image",
                "Vid": "v02a49g10000ckitq63c77u8uhf09ebg",
                "MediaVideoDuration": 191,
                "MediaLibraryVideoType": 2,
                "ReviewStatus": 2,
                "CreateTime": 1696980251,
                "UpdateTime": 1696990559,
                "Creator": "admin@bytedance.com",
                "SourceType": 2,
                "ActivityVideo": [
                    {
                        "Id": 1779341234622756,
                        "Name": "Live room A"
                    }
                ],
                "FailureTime": 1796980251,
                "MediaSize": 24725029,
                "FolderId": 0,
                "FolderName": "Category A",
                "VideoHeight": 1920,
                "VideoWidth": 1080
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 10,
            "TotalCount": 1
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
