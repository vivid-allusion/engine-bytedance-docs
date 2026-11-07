---
title: "ListActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi-zh-CN"
---

获取您账号下所有现有直播间的基本信息。

此 API 操作最多可返回最近的 10,000 个直播间。您可以配置房间状态（`Status`）和直播流时间（`LiveTime`）等条件以筛选搜索。

<span id="requirement"></span>
## 需求

速率限制：每个账号每分钟最多 120 次请求

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有常用请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### Query


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`ListActivityAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |API 操作的版本。该操作的值为 `2020-06-01`。 |


<span id="body"></span>
### Body


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|PageNo |整数 |否 |`1` |返回的页码。默认值：`1`。<br><br>该 API 操作最多支持返回 10,000 条结果，即 `PageNo` × `PageItemCount` 必须小于或等于 10,000。 |
|PageItemCount |整数 |否 |`10` |每页返回的结果数量。默认值：`10`。<br><br>该 API 操作最多支持返回 10,000 条结果，即 `PageNo` × `PageItemCount` 必须小于或等于 10,000。 |
|Name |字符串 |否 |`直播间 A` |返回名称包含该值的直播间。<br><br>例如，若参数值为 `直播间 A`，则返回名称中包含关键字“直播间 A”的直播间，如“直播间 ABC”、“直播间 a”以及“直播间 ab”。 |
|Status |整数 |否 |`0` |返回指定状态的直播间。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`: 全部。<br><br>* `1`: 直播中。<br><br>* `2`: 预告。<br><br>* `3`: 回放。<br><br>* `4`: 已结束。<br><br><br>已结束表示直播流已结束但未发布回放到观看页。 |
|LiveTime |长整型 |否 |`1680193976` |直播流时间，Unix 时间戳格式。单位：秒。<br><br>返回直播流时间大于或等于该值的直播间。<br><br>该时间可能不是直播流实际开始的时间。 |
|IsLockPreview |整数 |否 |`0` |指定是否返回预告被锁定的直播间。默认值：`0`。<br><br>有效值：<br><br><br>* `-1`: 返回所有直播间。<br><br>* `0`: 返回预告未锁定的直播间。<br><br>* `1`: 返回预告已锁定的直播间。 |
|SiteTagNews |数组[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |否 |`-` |返回包含任意这些分类标签值的直播间。<br><br>可通过调用 [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN) 获取分类标签列表。 |
|HostAccountId |整数 |否 |`112038` |主播账号 ID。<br><br>返回与该主播账号关联的直播间。<br><br>可通过调用 [GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) 获取 ID。 |
|HostAccountName |字符串 |否 |`主播 A` |主播账号名称。支持模糊搜索。<br><br>返回与该主播账号关联的直播间。<br><br>可通过调用 [GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi) 获取名称。 |
|LiveMode |整数 |否 |`0` |返回指定直播延时类型的直播间。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`: 同时支持超低延迟和普通延迟。<br><br>* `1`: 超低延迟，延迟为 1 到 2 秒。<br><br>* `2`: 普通延迟，延迟为 5 到 10 秒。 |
|SortBy |String |否 |`Status` |直播间排序规则。默认值：`Status`。有效值：<br><br><br>* `Status`: 先按直播间状态排序，再在每个状态内按直播间开始时间降序排列。<br><br>* `LiveTime`: 按直播间开始时间排序。<br><br>* `CreateTime`: 按直播间创建时间排序。 |
|SortOrder |String |否 |`Desc` |直播间排序顺序。默认值：`Asc`。有效值：<br><br><br>* `Desc`: 降序。<br><br>* `Asc`: 升序。<br><br><br>当`SortBy`设置为`Status`时，结果按状态升序分组（直播、预告、回放、已结束）。每组内，直播间始终按开始时间降序排列，无论`SortOrder`值为何。 |
|FollowerUserName |String |否 |`admin@bytedance.com` |用于创建直播间的账号。默认返回所有账号创建的直播间。如需获取 BytePlus 账号创建的直播间，请将参数值设置为`admin@bytedance.com`。如需获取某个 IAM 用户创建的直播间，请将参数值设置为该 IAM 用户的账号。你可以在**账号中心** \> **授权** \> **用户**页面的[BytePlus Live 控制台](https://console.byteplus.com/livesaas/accountManagement/userManage)获取 IAM 用户的账号。 |


<span id="sitetagnews"></span>
#### SiteTagNews


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Value |Array of String |是 |`["1","2"]` |分类标签值。<br><br>返回包含任意这些分类标签值的直播间。 |
|Name |String |否 |`标签A` |分类标签名称。<br><br>指定`Name`或`Index`其中之一。如同时提供，优先使用`Name`。如均未提供，则使用`Index`的默认值。 |
|Index |Integer |否 |`0` |分类标签的索引，用于标识在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。<br><br>默认值：`0`。取值范围：[0,19]。<br><br>指定`Name`或`Index`其中之一。如同时提供，优先使用`Name`。如均未提供，则使用`Index`的默认值。 |


<span id="response-parameters"></span>
## 返回调用结果


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PageNo |Integer |`1` |返回页的页码。 |
|PageItemCount |Integer |`10` |每页返回的结果数量。 |
|TotalItemCount |Integer |`1` |返回的直播间总数。 |
|Activities |Array of[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |`-` |返回的直播间列表。 |


<span id="activities"></span>
### Activities


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Id |Long |`17218346****` |返回的直播间活动 ID。 |
|Name |String |`直播间A` |返回的直播间名称。 |
|Status |Integer |`1` |返回的直播间状态。<br><br><br>* `1`: 直播。<br><br>* `2`: 预告。<br><br>* `3`: 回放。<br><br>* `4`: 已结束。 |
|CoverImage |String |`https://p1-live.****.image` |返回的直播间横屏模式封面图 URL，包含协议头。 |
|CreateTime |Integer |`1680093000` |返回的直播间创建时间，Unix 时间戳格式。单位：秒。 |
|ViewUrl |String |`https://live.byteplus.com/7420/******` |返回的直播间观看页地址。 |
|LiveTime |Integer |`1680193976` |直播流时间，采用 Unix 时间戳格式。单位：秒。<br><br>此时间可能不是直播流实际开始的时间。 |
|StreamStartTime |Integer |`1681094000` |返回直播间最后一次推送直播流的时间，采用 Unix 时间戳格式。单位：秒。<br><br>值为 `0` 表示该直播流从未被推送。<br><br>这是直播流实际开始的时间。 |
|OnlineStatus |Integer |`-` |已弃用。 |
|IsLockPreview |Integer |`0` |指示返回直播间的预告是否被锁定。<br><br><br>* `0`：预告未锁定。<br><br>* `1`：预告已锁定。 |
|SiteTags |Array of[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |`-` |返回直播间的分类标签列表。 |
|TextSiteTags |Array of[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) |`-` |返回直播间的文本标签列表。 |
|HostAccountId |Integer |`112038` |与返回直播间关联的主播账号 ID。 |
|HostAccountName |String |`Host A` |与返回直播间关联的主播账号名称。 |
|LiveMode |Integer |`0` |返回直播间的直播延时类型。<br><br><br>* `0`：如果直播间创建于 BytePlus Live 支持超低延时功能之前，并且未更新直播延时类型，则参数值为 `0`。换句话说，延时类型为普通延时。关于超低延时功能的更多信息，请参见 [超低延时直播](https://docs.byteplus.com/docs/byteplus-livesaas/docs-ultra-low-latency-zh-CN)。<br><br>* `1`：超低延时，延时为 1 到 2 秒。<br><br>* `2`：普通延时，延时为 5 到 10 秒。 |
|VerticalCoverImage |String |`https://p2-live.xxxx.image` |返回直播间竖屏模式封面图的 URL，包含协议头。 |
|SubAccountName |String |`admin@bytedance.com` |用于创建直播间的账号。参数值 `admin@bytedance.com` 表示该直播间由 BytePlus 账号创建。 |


<span id="sitetags"></span>
#### SiteTags


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Name |String |`Tag A` |分类标签名称。 |
|Value |String |`1` |分类标签值。 |
|Index |Integer |`0` |分类标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。 |
|DbIndex |Integer |`-` |已弃用。 |
|Show |Integer |`-` |已弃用。 |
|Id |Integer |`-` |已弃用。 |


<span id="textsitetags"></span>
#### TextSiteTags


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Name |String |`Tag B` |文本标签名称。 |
|Value |String |`3` |文本标签值。 |
|Index |Integer |`0` |文本标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。 |
|DbIndex |Integer |`-` |已弃用。 |
|Show |Integer |`-` |已弃用。 |
|Id |Integer |`-` |已弃用。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01
{ 
    "PageNo": 1, 
    "PageItemCount": 10, 
    "SiteTagNews": [ 
            { 
                  "Index": 0, 
                  "Value": ["1","2"] 
            } 
    ]    
} 
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202201201826170101501312091D1C09D2",
    "Action": "ListActivityAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1690293975
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "TotalItemCount": 1,
    "Activities": [
      {
        "Id": 17218346****,
        "Name": "Live Room A",
        "Status": 1,
        "CoverImage": "https://p1-live.****.image",
        "CreateTime": 1680093000,
        "ViewUrl": "https://live.byteplus.com/7420/******",
        "LiveTime": 1680193976,
        "StreamStartTime": 1681094000,
        "IsLockPreview": 0,
        "SiteTags": [
          {
            "Index": 0,
            "Name": "Tag A",
            "Value": 1,
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "TextSiteTags": [
          {
            "Index": 0,
            "Name": "Tag B",
            "Value": "3",
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "HostAccountId": 112038,
        "HostAccountName": "Host A",
        "LiveMode": 0,  
        "VerticalCoverImage": "https://p2-live.****.image",      
        "OnlineStatus": 0,
        "SubAccountName": "admin@bytedance.com"
      }
    ]
  }
}
```


<span id="error-codes"></span>
## 错误码

常见错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
