---
title: "UpdateFloatingAdvertisementAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateFloatingAdvertisement-zh-CN"
---

调用 `UpdateFloatingAdvertisementAPI`，可更新指定直播间内浮标广告的状态、链接及其他配置详情。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每秒最多 10 次查询。

* 前提条件：需拥有 BytePlus 账号，或具备 **营销工具包** \> **编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整参数列表请参见 [通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateFloatingAdvertisementAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |该 API 操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|ActivityId |Long |是 |1798615803\*\*\*\* |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |
|IsEnable |Integer |否 |`1` |指定是否启用浮标广告。支持以下取值，默认值为 `0`。<br><br><br>* `0`：禁用<br><br>* `1`：启用 |
|ImageUrl |String |否 |https://p.example.org/6ed59yyum2\-z75.png |浮标广告图片 URL。地址必须包含 https 协议头。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">首次通过该 API 配置浮标广告时，此参数为必填项。</div><br> |
|HomeUrl |String |否 |`https://example.com` |浮标广告的内嵌链接必须包含 https 协议头。 |
|IsCloseEnable |Integer |否 |`1` |指定观众是否可关闭浮标广告。支持以下取值，默认值为 `0`。<br><br><br>* `0`：广告可关闭<br><br>* `1`：广告不可关闭 |
|EnableFloating |Boolean |否 |true |指定是否启用浮标展示。支持以下取值，默认值为 `false`。<br><br><br>* `true`：设置为 `true` 时，点击浮标广告将在当前直播流观看页展开，观众可边观看直播流边查看广告。该选项仅在移动端观看页生效。<br><br>* `false`：设置为 `false` 时，点击浮标广告会在新浏览器标签页打开广告。因此，观众无法同时观看直播流和广告。 |


<span id="Response parameters"></span>
## 返回调用结果


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Status |Boolean |`true` |配置更新成功时返回 `true`。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateFloatingAdvertisementAPI&Version=2023-08-01
{
    "ActivityId": 1798615803****,
    "ImageUrl": "https://p.example.org/6ed59yyum2-z75.png",
    "HomeUrl": "https://example.com",
    "IsCloseEnable": 1,
    "IsEnable": 1,
    "EnableFloating": true
}
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateFloatingAdvertisementAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见 [常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
