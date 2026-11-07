---
title: "PollingChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-pollingchatapi-zh-CN"
---

调用此 API 以获取直播间内的评论。通过指定评论 ID 和轮询方向，可以定期获取新的评论或加载历史聊天消息。

<span id="bae63780"></span>
## 需求

配额：每个账号每分钟最多 120 次查询

<span id="35ca73aa"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01`

* 方法：GET


<span id="f3f5b32b"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="ca18801e"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`PollingChatAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|ChatId |Long |是 |`0` |评论的 ID，用作分页游标。API 会返回在该 ID 之前或之后发送的评论，但不会包含该 ID 的评论。<br><br><br>* 若值为 `0`，API 会返回请求时间之前发布的评论。<br><br>* 若将此参数设置为前一次返回结果中的 `ChatId`，API 会根据 `PollingType` 的值，检索该评论之前或之后发送的评论。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">你也可以将此参数设置为 <code>1</code>，并将 <code>PollingType</code> 设置为 <code>0</code>，以获取当前直播间最早发送的评论。</div><br> |
|Count |Integer |否 |`0` |返回的评论最大数量。<br><br>默认值：`0`。<br><br>若值为 `0`，API 会根据 `ChatId` 和 `PollingType` 返回所有符合条件的评论。 |
|PollingType |Integer |否 |`0` |指定是否返回 `ChatId` 所指评论之前或之后发送的评论。<br><br>默认值：`0`。<br><br>有效值：<br><br><br>* `0`：返回指定 `ChatId` 之后发送的评论。<br><br>* `1`：返回指定 `ChatId` 之前发送的评论。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>ChatId</code> 为 <code>0</code>，此参数会被忽略，API 会返回请求时间之前发布的评论。</div><br> |


<span id="34e67e49"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Data |Array of[聊天](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-CN#d762709f) |`-` |评论列表。 |


<span id="d762709f"></span>
### 聊天


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ChatId |Integer |`1672920235409489` |评论 ID。 |
|CreateTime |Long |`1714658888` |评论发送时间，Unix 时间戳格式。单位：秒。 |
|TextContent |String |`Hello` |评论内容。 |
|User |Array of[用户](https://docs.byteplus.com/docs/byteplus-livesaas/docs-pollingchatapi-zh-CN#60fb2ff7) |`-` |发送评论用户的信息。 |
|IsDelete |Boolean |`false` |表示评论是否被删除。<br><br><br>* `true`：已删除。<br><br>* `false`：未删除。 |
|LikeCount |Integer |`10` |评论点赞数。 |
|IsPresenter |Boolean |`true` |表示评论是否由主播发送。<br><br><br>* `true`：主播发送。<br><br>* `false`：其他用户发送。 |
|reviewStatus |Integer |`0` |评论的审核状态。<br><br><br>* `0`：无需审核。<br><br>* `1`：审核中。<br><br>* `2`：审核通过。<br><br>* `3`：审核不通过。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果<code>IsPresenter</code>的值为<code>true</code>，则参数值始终为<code>2</code>。</div><br> |
|IsTipOff |Integer |`0` |表示评论是否被举报。<br><br><br>* `0`：未举报。<br><br>* `1`：已举报。 |


<span id="60fb2ff7"></span>
#### 用户


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|UserId |Long |`17975829****` |用户 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">主播的ID始终为<code>0</code>。</div><br> |
|Nickname |String |`观众 A` |用户昵称。 |


<span id="90d4a741"></span>
## 示例

<span id="c9d65ee4"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=PollingChatAPI&Version=2020-06-01&ActivityId=17218346****&ChatId=0&Count=0&PollingType=0
```


<span id="Response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PollingChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1714662740
    },
    "Result": {
        "Data": [
            {
                "ChatId": 1672920235409489,
                "CreateTime": 1714658888,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Viewer A",
                    "UserId": 17975829****
                },
                "IsDelete": false,
                "LikeCount": 10,
                "IsPresenter": false,
                "reviewStatus": 0,
                "IsTipOff": 0
            },
            {
                "ChatId": 1672920235409492,
                "CreateTime": 1714660078,
                "TextContent": "Hello",
                "User": {
                    "Nickname": "Host",
                    "UserId": 0
                },
                "IsDelete": false,
                "LikeCount": 0,
                "IsPresenter": true,
                "reviewStatus": 2,
                "IsTipOff": 0
            }
        ]
    }
}
```


<span id="f9940149"></span>
## 错误码

有关通用错误码列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
