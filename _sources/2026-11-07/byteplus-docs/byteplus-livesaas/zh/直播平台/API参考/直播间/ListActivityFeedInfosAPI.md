---
title: "ListActivityFeedInfosAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi-zh-CN"
---

获取您账号下所有现有直播间的基本信息，包括封面图、虚拟人气、主播账号和创建时间。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每分钟最多120次请求

<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* 接口地址：https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListActivityFeedInfosAPI` |API操作。 |
|Version |String |是 |`2023-08-01` |此API操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|PageNumber |Integer |否 |`1` |要返回的页码。默认值：`1`。该值必须大于或等于1。 |
|PageSize |Integer |否 |`10` |每页返回的结果数量。默认值：`10`。取值范围：[1,100]。 |
|SortBy |String |否 |`Status` |直播间排序规则。默认值：`Status`。如果您传递的值不是以下之一，则会使用默认值。<br><br>有效值：<br><br><br>* `Status`：先按直播间状态排序，再在每个状态内按直播间开始时间降序排列。<br><br>* `LiveTime`：按直播间开始时间排序。<br><br>* `CreateTime`：按直播间创建时间排序。 |
|SortOrder |String |否 |`Desc` |直播间排序顺序。默认值：`Asc`。如果您传递的值不是以下之一，则会使用默认值。<br><br>有效值：<br><br><br>* `Desc`：降序。<br><br>* `Asc`：升序。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当<code>SortBy</code>的值设置为<code>Status</code>时，直播间状态的升序为：Live、预告、回放、结束。无论<code>SortOrder</code>的值为何，直播间在每个状态内均按开始时间降序排列。</div><br> |
|SiteTagNews |[SiteTagNews](https://docs.byteplus.com/en/docs/11/99264#sitetagnews)数组 |否 |`-` |包含任意这些分类标签值的直播间将被返回。<br><br>您可以通过调用[ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2)获取分类标签列表。 |


<span id="sitetagnews"></span>
### SiteTagNews


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Value |String数组 |是 |`["1","2"]` |分类标签值。<br><br>包含任意这些分类标签值的直播间将被返回。 |
|Name |String |否 |`标签A` |分类标签名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅需传递<code>Name</code>或<code>Index</code>之一。若同时传递，则仅<code>Name</code>生效。若均未传递，则使用<code>Index</code>的默认值。</div><br> |
|Index |Integer |否 |`0` |分类标签的索引，用于标识在[BytePlus Live控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>默认值：`0`。取值范围：[0,19]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅需传递<code>Name</code>或<code>Index</code>之一。若同时传递，则仅<code>Name</code>生效。若均未传递，则使用<code>Index</code>的默认值。</div><br> |


<span id="Response parameters"></span>
## 返回参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PageNumber |Integer |`1` |返回的页码。 |
|PageSize |Integer |`10` |每页返回的结果数量。 |
|TotalCount |Integer |`1` |返回的直播间总数。 |
|列表 |[列表](https://docs.byteplus.com/en/docs/11/99264#list)数组 |`-` |返回的直播间列表。 |


<span id="list"></span>
### 列表


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityId |Long |`1810625882058998` |返回直播间的活动 ID。 |
|ActivityName |String |`直播间 A` |返回直播间的名称。 |
|Status |Integer |`2` |返回直播间的状态。有效值：<br><br><br>* `1`：直播。<br><br>* `2`：预告。<br><br>* `3`：回放。<br><br>* `4`：结束。 |
|CoverImageUrl |String |`//example.image` |返回直播间横屏模式封面图的 URL。<br><br>若通过 API 调用设置封面图，URL 包含协议头。若通过控制台设置，则不包含协议头。 |
|VerticalCoverImageUrl |String |`//example.image` |返回直播间竖屏模式封面图的 URL。<br><br>若通过 API 调用设置封面图，URL 包含协议头。若通过控制台设置，则不包含协议头。 |
|Token |String |`qIZSTa` |Web 观播 SDK 公共模式下的用户 token。<br><br>集成 Web 观播 SDK 时，将 `token` 的值设置为当前参数值，将 `mode` 的值设置为 `1`。 |
|VirtualPeopleCount |Integer |`100` |返回直播间的虚拟人气值。 |
|HostName |String |`主播 A` |主播账号名称。 |
|HostAvatarImageUrl |String |`//example.image` |主播账号头像的 URL。<br><br>若通过 API 调用设置主播账号头像，URL 包含协议头。若通过控制台设置，则不包含协议头。 |
|CreateTime |Integer |`1726818793` |返回直播间的创建时间，Unix 时间戳格式。单位：秒。 |
|SiteTags |[SiteTags](https://docs.byteplus.com/en/docs/11/99264#sitetags)数组 |`-` |返回直播间的分类标签列表。 |


<span id="sitetags"></span>
### SiteTags


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Name |String |`标签 A` |分类标签名称。 |
|Value |String |`1` |分类标签值。 |
|Index |Integer |`0` |分类标签的索引，标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的展示顺序。<br><br>取值范围：[0,19]。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023-08-01
{
    "PageNumber": 1,
    "PageSize": 10,
    "SortBy": "Status",
    "SortOrder": "Desc",
    "SiteTagNews": [
        {
            "Value": [
                "1",
                "2"
            ],
            "Name": "Tag A",
            "Index": 0
        }
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "Action": "ListActivityFeedInfosAPI",
        "Version": "2023-08-01",
        "SystemTime": 1826818793
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "List": [
            {
                "ActivityId": 181062****058998,
                "ActivityName": "Live room A",
                "Status": 2,
                "CoverImageUrl": "//example.image",
                "VerticalCoverImageUrl": "//example.image",
                "Token": "qI****",
                "VirtualPeopleCount": 100,
                "HostName": "Host A",
                "HostAvatarImageUrl": "//example.image",
                "CreateTime": 1726818793,
                "SiteTags": [
                    {
                        "Name": "Tag A",
                        "Value": "1",
                        "Index": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误码和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
