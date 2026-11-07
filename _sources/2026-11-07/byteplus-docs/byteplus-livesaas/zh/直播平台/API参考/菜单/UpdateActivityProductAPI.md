---
title: "UpdateActivityProductAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN"
---

调用此 API 以更新直播间内商品卡片的配置。

<span id="Request"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="36bded50"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01`

* 方法：POST


<span id="53aa7d97"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="f145b498"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`UpdateActivityProductAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="8cd6fc93"></span>
### 请求体


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`1783981136301234` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|Products |[Products](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN#a460b55a) 的数组 |是 |`-` |商品卡片的配置。 |


<span id="a460b55a"></span>
#### Products


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|`-` |JSON Map |是 |`-` |商品卡片菜单的序号以及商品卡片的配置。格式：`"Key":"Value"`。<br><br><br>* `"Key"`：商品卡片菜单的序号。可通过调用 [GetActivityMenuAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivitymenuapi-zh-CN) 获取序号。例如，若 `GetActivityMenuAPI` 返回商品卡片菜单的 `Location` 为 `1`，则应使用 `"1"` 作为 `"Key"`。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">请确保该位置对应商品卡片菜单，其<code>Type</code>值在<code>GetActivityMenuAPI</code>返回调用结果中为<code>2</code>。   </div><br>   <br><br>* `"Value"`：商品卡片的配置。更多信息请参见 [ProductConfig](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN#993adfaa)。 |


<span id="993adfaa"></span>
##### **ProductConfig**


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|EnableFloating |Boolean |是 |`false` |指定观众点击商品卡片后，是否在直播间以浮窗页面展示商品详情页。<br><br>有效值：<br><br><br>* `true`：是。在直播间以浮窗页面展示商品详情页。观众可同时观看视频和商品详情页。该配置仅在移动端生效。<br><br>* `false`：否。在新页面展示商品详情页。观众无法同时观看视频和商品详情页。 |
|EnableUA |Boolean |否 |`false` |指定是否启用直达链接功能。该功能仅在移动端可用。<br><br>默认值：`false`。<br><br>有效值：<br><br><br>* `true`：启用该功能。<br><br>* `false`：关闭该功能。 |
|UAAddress |String |否 |`Mozilla` |特定环境下的 User Agent。<br><br>当观众在 User Agent 包含该参数值的平台点击商品卡片时，将跳转至商品卡片的直达链接。但若观众在其他平台点击商品卡片，则会跳转至商品链接（RedirectUrl）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅配置单一环境，并保留用于兼容历史版本。如需配置最多5个环境，请使用<code>UAInfo</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若<code>EnableUA</code>为<code>true</code>且未传递<code>UAInfo</code>，则该参数为必填项。如同时传递，则以<code>UAInfo</code>为准。</div><br> |
|UAInfo |[UAInfoMsg](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN#3a35fa91) 的数组 |否 |`-` |直达链接功能的环境列表。最多可配置 5 个环境。环境顺序需与每个商品卡片 `DirectUrls` 参数中的链接顺序一致。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若<code>EnableUA</code>为<code>true</code>且未传递<code>UAAddress</code>，则该参数为必填项。如同时传递，则以<code>UAInfo</code>为准。</div><br> |
|ProductsPosition |Integer |否 |`0` |指定商品浮窗在 PC 端观看页的展示位置。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：播放器右上角。<br><br>* `1`：播放器左上角。<br><br>* `2`：播放器左下角。<br><br>* `3`：在播放器的右下角。 |
|DefaultRedirectImage |String |否 |`https://example.com` |默认按钮图片的 URL，对应控制台的**Button image**字段。<br><br>图片必须为 JPG、GIF、PNG 或 BMP 格式，并替换系统默认图片。推荐分辨率为 160×60。 |
|Product |Array of[Product](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivityproductapi-zh-CN#Product) |是 |`-` |商品卡片的配置。 |


<span id="3a35fa91"></span>
###### **UAInfoMsg**


|Name |Data Type |Required |Sample Value |接口行为 |
|---|---|---|---|---|
|UAName |String |是 |`TikTokiOSEnv1` |环境名称，最多 20 个字符。配置商品卡片时，该名称用于标记对应的直达链接。 |
|UAAddress |String |是 |`TikTok` |环境的 User Agent 字符串，最多 500 个字符。当观众在 User Agent 包含该值的平台点击商品卡片时，将跳转到商品卡片对应的直达链接。 |


<span id="244cef61"></span>
###### **Product**


|Name |Data Type |Required |Sample Value |接口行为 |
|---|---|---|---|---|
|Title |String |是 |`Dress` |商品名称，对应控制台的**Product name**字段。<br><br>取值长度为 1\-3315 个字符。 |
|Highlight |String |否 |`800` |商品的零售价，对应控制台的**Retail price**字段。<br><br>取值长度为 1\-260 个字符。 |
|IntroduceImage |String |否 |`www.example.com` |商品图片的 URL，对应控制台的**Product image**字段。图片显示在商品卡片的左侧。<br><br>商品图片支持的格式：JPG、GIF、PNG 和 BMP。 |
|RedirectImage |String |否 |`www.example.com` |按钮图片的 URL，对应控制台的**Button image**字段。图片显示在商品卡片的右下角。观众点击按钮后将跳转到商品 URL 或直达链接。<br><br>按钮图片支持的格式：JPG、GIF、PNG 和 BMP。 |
|RedirectUrl |String |否 |`www.example.com` |商品详情页的 URL，对应控制台的**Product URL**字段。 |
|Index |Integer |否 |`-` |已废弃。 |
|Id |Long |否 |`-` |已废弃。 |
|EnableStatus |Integer |否 |`1` |指定是否展示商品卡片。默认值：`0`。<br><br>可选值：<br><br><br>* `0`：不展示商品卡片。<br><br>* `1`：展示商品卡片。 |
|DirectUrl |String |否 |`www.example.com` |商品详情页的直达链接，对应控制台的**Direct URL**字段。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">仅当<code>EnableUA</code>值为<code>true</code>时，直达链接才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅设置第一个环境的直达链接，并保留用于兼容历史版本。如需为每个环境设置直达链接，请使用<code>DirectUrls</code>。</div><br> |
|DirectUrls |Array of String |否 |`["www.example.com"]` |商品详情页的直达链接，对应菜单的直达链接配置项（`UAInfo`）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">仅当<code>EnableUA</code>值为<code>true</code>时，直达链接才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip"><code>DirectUrls</code>的数量应与<code>UAInfo</code>环境数量一致：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">若<code>DirectUrls</code>数量多于<code>UAInfo</code>环境数量，则多余的链接不生效。例如，若配置了2个UA环境并传递<code>["https://direct_url1", "https://direct_url2", "https://direct_url3"]</code>，则<code>https://direct_url3</code>不生效。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">若<code>DirectUrls</code>数量少于<code>UAInfo</code>环境数量，则缺失位置会以空字符串补齐。例如，若配置了2个UA环境并传递<code>["https://direct_url1"]</code>，则UA1的直达链接为<code>https://direct_url1</code>，UA2的直达链接为空（<code>""</code>）。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若不希望为某个UA环境配置直达链接，请在对应位置传递<code>""</code>。例如，若环境1和3需要直达链接，环境2不需要，则传递<code>["https://direct_url1", "", "https://direct_url3"]</code>。</div><br> |
|Remark |String |否 |`XL` |商品的附加信息，如服装尺码。该参数对应控制台的**Product description**字段。<br><br>取值长度为 1\-3315 个字符。 |
|Strikethrough |String |否 |`1000` |商品的刊例价，对应控制台的**List price**字段。<br><br>取值长度为 1\-260 个字符。 |
|TagName |String |否 |`Clothing` |商品分类，对应控制台的**Product category**字段。<br><br>取值长度为 1\-20 个字符。 |
|ExternalProductId |String |否 |`20866` |外部商品ID。该ID可防止同一商品被多次添加到同一商品卡片菜单。<br><br>该值长度必须为1\-128个字符。 |


<span id="d57c9da0"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|状态 |布尔值 |`true` |表示商品卡片是否已成功更新。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="8865deac"></span>
## 示例

<span id="c6eb5b80"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityProductAPI&Version=2020-06-01
{
     "ActivityId":1783981136301234,
     "Products":{
         "1":{
             "EnableFloating":false,
             "EnableUA":true,
             "UAInfo":[
                {
                     "UAName":"MozillaEnv1",
                     "UAAddress":"Mozilla/5.0 (env1)"
                },
                {
                     "UAName":"MozillaEnv2",
                     "UAAddress":"Mozilla/5.0 (env2)"
                }
             ],
             "ProductsPosition":0, 
             "DefaultRedirectImage":"https://example.com",
             "Product":[
                {
                     "Title":"Dress", 
                     "Highlight":"800", 
                     "IntroduceImage":"www.example.com", 
                     "RedirectImage":"www.example.com", 
                     "RedirectUrl":"www.example.com", 
                     "EnableStatus":1,
                     "DirectUrls":[
                        "www.example.com/env1/dress",
                        "www.example.com/env2/dress"
                     ],
                     "Remark":"XL",
                     "Strikethrough":"1000",
                     "TagName":"Clothing",
                     "ExternalProductId": "20866"
                }
            ]
        }
    }
}
```


<span id="da670bbe"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityProductAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1708782797
    },
    "Result": {
        "Status": true
    }
}
```


<span id="f0c323f3"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
