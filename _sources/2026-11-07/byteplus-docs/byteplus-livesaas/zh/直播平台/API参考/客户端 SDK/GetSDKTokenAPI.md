---
title: "GetSDKTokenAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN"
---

调用此 API 以获取授权 Token，允许观众通过集成了观播 SDK 的网页或应用进入直播间。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">为防止恶意攻击，请确保在调用此 API 操作前校验所有请求参数。</div>


<span id="61e03047"></span>
## 要求

配额：每个账号每分钟 5,000 次查询

<span id="8fc08545"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01`

* 方法：POST


<span id="06d777a9"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="513dbfbc"></span>
### Query


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetSDKTokenAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`179758233282****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|Mode |Integer |是 |`2` |直播间的鉴权模式。<br><br>有效值：<br><br><br>* `1`：公开模式。观众无需登录即可进入直播间。但在需要用户信息的场景（如点击评论输入框或点赞评论）时，观众需先输入昵称。<br><br>* `2`：自定义模式。观众登录你自有账号体系后，需将观众昵称和用户 ID 传递给此 API 操作。观众通过你账号体系的凭证进入直播间。因此，观众可直接进行发送评论、点赞等操作。 |
|Nickname |String |否 |`观众 A` |观众的昵称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>Mode</code> 的值为 <code>2</code> 时，该参数为必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">为防止个人信息泄露，建议不要使用如手机号等信息作为观众昵称。</div><br> |
|UserIdStr |String |否 |`57584` |观众的用户 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当 <code>Mode</code> 的值为 <code>2</code> 时，该参数为必填。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">为防止个人信息泄露，建议不要使用如手机号等信息作为观众用户 ID。</div><br> |
|InviteToken |String |否 |`abcd` |若观众从集成了 Web 观播 SDK 的页面分享直播间，则该值为分享 URL 中的 inviter_token。例如，路径为 `https://test.live.com/123/456?inviter_token=abcd` 时，参数值为 `abcd`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>Mode</code> 的值为 <code>2</code> 时，该参数生效。</div><br> |
|AvatarUrl |String |否 |`http://xxx.example` |观众头像的 URL。该头像仅在集成了 iOS 观播 SDK 或 Android 观播 SDK 的观看页展示。 |
|CustomComment |String |否 |`Singapore` |指定自定义信息（如获奖者所在地），用于在获奖名单中展示在观众昵称右侧。该值最长可为 50 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>Mode</code>的值为<code>2</code>时，此参数才会生效。</div><br> |


<span id="f9131aea"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Token |String |`ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D` |允许观众通过集成了观播 SDK 的网页或应用进入直播间所需的授权 Token。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>Mode</code>的值为<code>2</code>，则会生成一个经过 URL 编码的令牌，您必须在将其传递给观众 SDK 之前对其进行 URL 解码。否则，观众 SDK 将无法验证该令牌。</div><br> |


<span id="eebe5d33"></span>
## 示例

<span id="5e5b0957"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetSDKTokenAPI&Version=2020-06-01
{
     "ActivityId": 179758233282****,
     "Mode": 2,
     "Nickname": "Viewer A",
     "UserIdStr": "57584"
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetSDKTokenAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714572349
    },
    "Result": {
        "Token": "ENYVfBwV6kdV14QDnGO****teQmSYmeHiiGOJcIxdII%3D"
    }
}
```


<span id="6e0e0a4d"></span>
## 错误码

有关通用错误码的列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
