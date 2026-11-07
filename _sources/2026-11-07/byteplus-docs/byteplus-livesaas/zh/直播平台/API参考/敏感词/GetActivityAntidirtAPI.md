---
title: "GetActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityantidirtapi-zh-CN"
---

要管理直播间的音视频内容安全，可以调用此 API 获取已配置的敏感词列表。该 API 支持获取全部敏感词，或仅获取包含指定关键词的敏感词。

<span id="6012f85b"></span>
## 需求

配额：每个账号每分钟最多查询 120 次

<span id="9ee8c1eb"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01`

* 方法：GET


<span id="7ad60001"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="7ccae2e4"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398113630****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取活动 ID。 |
|PageNo |Integer |是 |`1` |返回的页码。 |
|PageItemCount |Integer |是 |`10` |每页返回的结果数量。 |
|Content |String |否 |`a` |关键词。API 仅返回包含该关键词的敏感词。 |


<span id="c45a43ea"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|EnablePhoneNumberFilter |Integer |`1` |指定是否屏蔽包含手机号的评论和昵称。<br><br><br>* `1`：已开启。包含手机号的评论仅对发送者可见。<br><br>* 其他值：未开启。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">目前该功能支持新加坡、日本、韩国、印度尼西亚、泰国及中国大陆的手机号。</div><br> |
|EnableSensitiveForLetter |Integer |`1` |表示是否开启大小写敏感。<br><br><br>* `1`：已开启。<br><br>* 其他值：未开启。 |
|TotalItemCount |Integer |`2` |返回的敏感词总数。 |
|WordList |Array of String |`["a","ab"]` |返回的敏感词列表。 |


<span id="cd1e512b"></span>
## 示例

<span id="af8ea841"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAntidirtAPI&Version=2020-06-01&ActivityId=178398113630****&PageNo=1&PageItemCount=10&Content=a
```


<span id="2ea02c1c"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846
    },
    "Result": {
        "WordList": ["a","ab"],
        "TotalItemCount": 2,
        "EnablePhoneNumberFilter": 1,
        "EnableSensitiveForLetter": 1
    }
}
```


<span id="21a1266f"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
