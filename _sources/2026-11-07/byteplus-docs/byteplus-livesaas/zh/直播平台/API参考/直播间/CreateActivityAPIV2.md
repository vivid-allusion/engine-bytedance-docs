---
title: "CreateActivityAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN"
---

要以编程方式创建一个直播间，可以调用 CreateActivityAPIV2 API。该 API 支持从零开始创建新的直播间、基于预先配置的模版创建，或通过复制现有直播间来创建。创建成功后，API 会返回唯一的活动 ID，你可以通过该活动 ID 配合其他 API 管理和定制直播间。

<span id="requirement"></span>
## 需求

配额：每个账号每分钟最多 120 次查询

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### Query


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`CreateActivityAPIV2` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。设置为 `2020-06-01`。 |


<span id="body"></span>
### Body


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Name |String |是 |`直播间 A` |创建直播间的名称，最长不超过 1950 个字符。 |
|LiveTime |Long |否 |`1680193976` |直播流的开播时间，采用 Unix 时间戳格式。单位：秒。时间精确到分钟。<br><br>默认值：当前时间。<br><br>此为预定开播时间，实际开播时间可能有所不同。<br><br>`LiveTime` 必须早于 `EndTime`，最大时间差为 259,200（72 小时）。 |
|IsBeginLiveEnable |Integer |否 |`0` |指定是否强制执行预定的开播时间。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。只能在指定的开播时间之后开播。 |
|IsAutoEndEnable |Integer |否 |`0` |指定是否在设定的 EndTime 自动结束直播流。默认值：`0`。<br><br>有效值：<br><br><br>* `0`：关闭该功能。<br><br>* `1`：开启该功能。<br><br><br>若通过复制现有直播间创建新直播间，现有直播间的此配置不会复制到新直播间。可通过此参数配置新直播间是否启用该功能。 |
|EndTime |Long |否 |`1680293976` |以 Unix 时间戳格式表示的直播流结束时间。单位：秒。时间可精确到分钟。<br><br><br>* `EndTime` 必须晚于 `LiveTime`，最大时间差为 259,200（72 小时）。<br><br>* 当 `IsAutoEndEnable` 的值为 `1` 时，此参数为必填且有效。<br><br>* 复制直播间时，此设置不会从原房间继承。使用此参数配置新房间的结束时间。 |
|LiveMode |Integer |否 |`2` |直播延时类型。<br><br>默认值：`0`。<br><br>可选值：<br><br><br>* `0`：超低延时或普通延时，匹配直播间模版中配置的类型。<br><br>* `1`：超低延时，延时为 1~2 秒。<br><br>* `2`：普通延时，延时为 5~10 秒。<br><br><br>如指定`OldId`，则该参数不生效。此时，新直播间的延时类型与被复制的原直播间配置一致。 |
|ViewUrlPath |String |否 |`1234` |观看页地址由基础 URL（如`https://DomainName/****/`）拼接`ViewUrlPath`生成。例如，若参数值为`abc`，则观看页地址为`https://DomainName/****/abc`。如未指定，则随机生成一个值。<br><br>长度需在 [1, 20] 个字符之间。支持的字符包括：<br><br><br>* 大写字母 A–Z<br><br>* 小写字母 a–z<br><br>* 数字 |
|CoverImage |String |否 |`https://tplv-gjr25qtd0-image.image` |直播间横屏模式封面图的 URL。如未指定，则使用默认封面图。<br><br>通常，参数值需为带协议头的 URL。但若通过[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上传图片获取的 URL（例如，通过调用[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)获取直播间内通过控制台上传的封面图 URL），则可使用无协议头的 URL 作为参数值。 |
|VerticalCoverImage |String |否 |`https://gjr293lqtd0-image.image` |直播间竖屏模式封面图的 URL。如未指定，则参数值与`CoverImage`一致。<br><br>通常，参数值需为带协议头的 URL。但若通过[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上传图片获取的 URL（例如，通过调用[GetActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitybasicconfigapi-zh-CN)获取直播间内通过控制台上传的封面图 URL），则可使用无协议头的 URL 作为参数值。 |
|OldId |Long |否 |`17218346****` |已有直播间的活动 ID，其配置将被复制到新直播间。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。<br><br>若需将已有直播间的配置复制到新直播间，则该参数为必填项。 |
|CopyStream |Boolean |否 |`true` |指定在复制已有直播间时，是否复制直播流。<br><br>默认值：`false`。<br><br>可选值：<br><br><br>* `true`：复制直播流。<br><br>* `false`：不复制直播流。 |
|TemplateId |Long |否 |`4984658` |直播间模版的 ID。新直播间将与该模版拥有相同的配置。你可以通过调用 [GetAccountTemplateAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccounttemplateapi-zh-CN) 获取该 ID。如果省略该参数，则使用默认模版。若不存在默认模版，则房间会在无模版情况下创建。<br><br>若需基于模版创建直播间，该参数为必填项。<br><br><br>* 若设置了参数 `OldId` 的值，则该参数无效。<br><br>* 如果模版包含大量抽奖配置，并且你希望复制基于该模版创建的直播间，请在直播间创建后至少等待 5 分钟再进行复制。否则，抽奖配置可能无法被完整复制。 |
|SiteTags |Array of[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |否 |`-` |直播间中的分类标签列表。你可以通过调用 [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN) 获取支持的分类标签。<br><br>如果你即将通过复制现有直播间来创建新的直播间，现有直播间配置的分类标签值不会被复制到新直播间。你可以通过该参数为新直播间配置分类标签值。 |
|TextSiteTags |Array of[CreateActivityAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-createactivityapiv2-zh-CN) |否 |`-` |直播间中的文本标签列表。你可以通过调用 [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2-zh-CN) 获取支持的文本标签。<br><br>如果你即将通过复制现有直播间来创建新的直播间，现有直播间配置的文本标签值不会被复制到新直播间。你可以通过该参数为新直播间配置文本标签值。 |


<span id="sitetags"></span>
#### SiteTags


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Value |String |是 |1 |分类标签的值。 |
|Index |Integer |是 |0 |分类标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。索引值越小，标签显示顺序越靠前。<br><br>取值范围：[0,19] |


<span id="textsitetags"></span>
#### TextSiteTags


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Value |String |是 |2 |文本标签的值。 |
|Index |Integer |是 |0 |文本标签的索引，用于标识在 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)上的显示顺序。索引值越小，标签显示顺序越靠前。<br><br>取值范围：[0,4] |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |所创建直播间的活动 ID。 |
|ActivityIdStr |String |`-` |已弃用。 |
|Status |Integer |`-` |已弃用。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=CreateActivityAPIV2&Version=2020-06-01
{ 
    "Name": "Live Room A", 
    "LiveTime": 1680193976,
    "LiveMode": 2    
} 
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
  "ResponseMetadata":{
                "RequestId":"2018060411042001001002322800209D2",
                "Action":"CreateActivityAPIV2",
                "Version":"2020-06-01",        
                "Service":"livesaas",
                "Region":"ap-singapore-1"，
                "SystemTime":1656067132
        },
        "Result":{
                "ActivityId":17218312****,
                "ActivityIdStr":"",
                "Status":
        }
}
```


<span id="error-codes"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
