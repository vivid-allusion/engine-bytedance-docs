---
title: "GetActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN"
---

调用此 API 以获取指定直播间中展示的商品卡片配置。

<span id="Request"></span>
## 需求

配额：每个账号每分钟最多查询 120 次

<span id="ecda79a5"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01`

* 方法：GET


<span id="8387d019"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="Query string parameters"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityProductAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`1783981136301234` |直播间的活动 ID。你可以通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="Sample request"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|`-` |JSON Map |`-` |一个 JSON 映射，键为商品卡片菜单的序号，值为对应的配置。格式：`"Key":"Value"`。<br><br><br>* `"Key"`：商品卡片菜单的序号，与 `Location` 字段在 [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-CN) 返回调用结果中的值一致。例如，若商品卡片菜单的 `Location` 值为 `1`，则 `"Key"` 的值为 `1`。<br><br>* `"Value"`：商品卡片的配置。详细信息请参见 [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN#d514de4f)。 |


<span id="d514de4f"></span>
### ProductConfig


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|EnableFloating |Boolean |`false` |表示观众点击商品卡片后，是否在直播间内打开浮窗页面展示商品详情页。<br><br><br>* `true`：在直播间内浮窗页面展示商品详情页。观众可同时观看视频和商品详情页。该配置仅在移动端生效。<br><br>* `false`：在新页面展示商品详情页。观众无法同时观看视频和商品详情页。 |
|EnableUA |Boolean |`false` |表示是否开启直达链接功能。该功能仅支持移动端。<br><br><br>* `true`：已开启。<br><br>* `false`：未开启。 |
|UAAddress |String |`Mozilla` |指定用于匹配特定客户端环境的 User\-Agent 字符串。<br><br>当观众在 User Agent 包含该参数值的平台点击商品卡片时，将跳转至商品卡片的直达链接。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在<code>EnableUA</code>为<code>true</code>时生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当<code>UAAddress</code>和<code>UAInfo.UAAddress</code>均有值时，以<code>UAInfo.UAAddress</code>为准。</div><br> |
|UAInfo |Array of[UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN#e22e1601) |`-` |配置直达链接功能的环境列表。最多可配置 5 个环境。环境的顺序与每个商品卡片 `DirectUrls` 参数中的 URL 顺序一致。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在<code>EnableUA</code>为<code>true</code>时生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当<code>UAAddress</code>和<code>UAInfo.UAAddress</code>均有值时，以<code>UAInfo.UAAddress</code>为准。</div><br> |
|ProductsPosition |Integer |`0` |表示商品浮窗在桌面端观看页中的展示位置。<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：播放器右下角。 |
|DefaultRedirectImage |String |`www.example.com` |默认按钮图片的 URL，对应控制台的 **按钮图片** 字段。 |
|Product |Array of[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityproductapi-zh-CN#0a61e327) |`-` |商品卡片的配置。 |


<span id="e22e1601"></span>
#### UAInfoMsg


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|UAName |String |`Env1` |环境名称，对应控制台**特定环境的 User Agent**字段中配置的环境名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">历史单环境配置命名为<code>Env1</code>。</div><br> |
|UAAddress |String |`Mozilla/5.0 (env1)` |环境的 User\-Agent 字符串。当观众在 User Agent 包含该值的平台点击商品卡片时，观众将被重定向至商品卡片对应的直达链接。 |


<span id="0a61e327"></span>
#### Product


|Name |Data Type |Sample Value |接口行为 |
|---|---|---|---|
|Title |String |`Dress` |你的商品名称，对应控制台**商品名称**字段。 |
|Highlight |String |`800` |你的商品零售价，对应控制台**零售价**字段。 |
|IntroduceImage |String |`www.example.com` |商品图片的 URL，对应控制台**商品图片**字段。图片显示在商品卡片的左侧。 |
|RedirectImage |String |`www.example.com` |按钮图片的 URL，对应控制台**按钮图片**字段。图片显示在商品卡片的右下角。观众点击按钮后将被重定向至商品 URL 或直达链接。 |
|RedirectUrl |String |`www.example.com` |商品详情页的 URL，对应控制台**商品 URL**字段。 |
|Index |Integer |`-` |已弃用。 |
|Id |Long |`20867` |商品卡片的 ID。 |
|EnableStatus |Integer |`1` |表示商品卡片是否已上架。<br><br><br>* `0`: 未上架。<br><br>* `1`: 已上架。 |
|Remark |String |`7天无条件退货政策` |你的商品的附加信息，如服装尺码。该参数对应控制台**商品描述**字段。 |
|Strikethrough |String |`1000` |你的商品刊例价，对应控制台**刊例价**字段。 |
|DirectUrl |String |`www.example.com` |商品详情页的直达链接，对应控制台**直达链接**字段。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数仅返回第一个环境的直达链接。如需获取所有已配置环境的直达链接，请使用<code>DirectUrls</code>。</div><br> |
|DirectUrls |Array of String |`["https://www.direct_url1", "", "https://www.direct_url3"]` |商品详情页的直达链接，对应控制台**直达链接**字段。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅在<code>EnableUA</code>为<code>true</code>时有值。最多返回 5 个直达链接，分别对应<code>UAInfo</code>列表中的每个环境，顺序与配置环境一致。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">空位置将作为空字符串返回，以保持与<code>UAInfo</code>的对齐。</div><br> |
|FloatingStatus |Integer |`1` |表示商品卡片是否在悬浮窗中展示。<br><br><br>* `1`: 在悬浮窗中展示。<br><br>* 其他值：不在悬浮窗中展示。 |
|TagName |String |`Clothing` |商品分类，对应控制台**商品分类**字段。 |
|ExternalProductId |String |`20866` |外部商品 ID。该 ID 可防止同一商品被重复添加到商品卡片菜单。 |


<span id="20349dad"></span>
## 示例

<span id="3675694e"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityProductAPI&Version=2020-06-01&ActivityId=1783981136301234
```


<span id="39032423"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708786019
    },
    "Result": {
        "1": {
            "EnableFloating": false,
            "Product": [
                {
                    "Title": "Dress",
                    "Highlight": "800",
                    "IntroduceImage": "www.example.com",
                    "RedirectImage": "www.example.com",
                    "RedirectUrl": "www.example.com",
                    "Index": 0,
                    "Id": 20867,
                    "EnableStatus": 1,
                    "Strikethrough": "1000",
                    "DirectUrl": "www.example.com/env1/dress",
                    "DirectUrls": [
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                    ],
                    "Remark": "7-day unconditional return policy",
                    "FloatingStatus": 1,                    
                    "TagName": "Clothing",
                    "ExternalProductId": "20866"
                }
            ],
            "EnableUA": true,
            "UAAddress": "Mozilla/5.0 (env1)",
            "UAInfo": [
                {
                    "UAName": "Env1",
                    "UAAddress": "Mozilla/5.0 (env1)"
                },
                {
                    "UAName": "Env2",
                    "UAAddress": "Mozilla/5.0 (env2)"
                }
            ],
            "ProductsPosition": 0,
            "DefaultRedirectImage": ""            
        }
    }
}
```


<span id="35b66db0"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
