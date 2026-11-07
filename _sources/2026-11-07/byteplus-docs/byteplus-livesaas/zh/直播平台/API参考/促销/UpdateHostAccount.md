---
title: "UpdateHostAccount"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/UpdateHostAccount-zh-CN"
---

在您的账号下添加主播账号，或更新已有主播账号的信息。

<span id="Usage scenario"></span>
## 使用场景

您可以通过`Id`参数添加或更新主播账号。


* 要添加主播账号，可在请求参数中省略`Id`（主播账号ID），或将`Id`设置为`0`。

* 要更新主播账号信息，请在请求参数中将`Id`设置为需更新的主播账号ID。您可以通过调用[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts)获取ID。


<span id="Requirements"></span>
## 使用要求


* 限速：每个账号每分钟最多120次请求

* 前提条件：需拥有BytePlus账号，或具备Marketing toolkits \> Edit权限的IAM用户。更多信息，请参见[Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHostAccount` |API操作。 |
|Version |String |是 |`2023-08-01` |本API操作的版本。当前版本：`2023-08-01`。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|HostAccount |[HostAccount](https://docs.byteplus.com/en/docs/11/113611#hostaccount)对象 |否 |`-` |主播账号信息列表。 |
|GetFollowDataUrl |String |否 |`https://example.com` |查询请求URL。您需自行开发OpenAPI，用于查询观众是否关注主播。更多信息，请参见[Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live)。 |
|UpdateFollowDataUrl |String |否 |`https://example.com` |更新请求URL。您需自行开发OpenAPI，用于更新观众对主播的关注状态。更多信息，请参见[Integrating your system with BytePlus Live](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-adding-a-brand-account#integrating-your-system-with-byteplus-live)。 |


<span id="hostaccount"></span>
### HostAccount


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Id |Long |否 |`114333` |主播账号ID。<br><br><br>* 添加主播账号：可省略该参数，或将参数值设置为`0`。<br><br>* 更新主播账号信息：将需更新的主播账号ID作为参数值。您可以通过调用[ListHostAccounts](https://docs.byteplus.com/en/docs/byteplus-livesaas/listhostaccounts)获取ID。 |
|Name |String |是 |`Host A` |主播账号名称。<br><br>取值长度需为1\-260个字符。 |
|AvatarUrl |String |是 |`https://example.com/a.png` |主播账号头像URL，需以https开头。 |
|IsFollowEnable |Integer |否 |`1` |指定是否允许观众在观看页关注主播。默认值：`0`。可选值：<br><br><br>* `0`：不允许观众关注主播。<br><br>* `1`：允许观众关注主播。<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">若更新主播账号信息，只有当与该主播账号关联的直播间在<strong>Producer</strong> \> <strong>Viewing restrictions</strong>页面将认证类型或评论限制设置为自定义时，观众才可关注主播。更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-applying-advanced-viewing-restrictions">Custom authentication login</a>。   </div><br>    |
|HomeUrl |String |否 |`https://example.com` |主播账号主页URL。观众在观看页点击主播头像或名称时，将跳转至该URL。 |
|ExternalPlatformId |String |否 |`abc123` |外部平台 ID，仅可包含大小写字母和数字，且长度不得超过 128 个字符。 |
|ExtraInfo |String |No |`abc` |与主播账号关联的额外信息。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|主播账号 ID |Long |`114333` |新增或更新的主播账号的 ID。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://livesaas.byteplusapi.com/?Action=UpdateHostAccount&Version=2023-08-01
{
    "HostAccount": {
        "Id": 114333,
        "Name": "Host A",
        "AvatarUrl": "https://example.com/a.png",
        "IsFollowEnable": 1,
        "HomeUrl": "https://example.com",
        "ExternalPlatformId": "abc123",
        "ExtraInfo": "abc"
    },
    "GetFollowDataUrl": "https://example.com",
    "UpdateFollowDataUrl": "https://example.com"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateHostAccount",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1715326286
    },
    "Result": {
        "HostAccountId": 114333
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
