---
title: "AddActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addactivityantidirtapi-zh-CN"
---

调用此 API 向指定直播间添加敏感词列表。这有助于你管理聊天内容，维护安全的互动环境。

<span id="6ca3ae9b"></span>
## 需求

配额：每个账号每分钟 120 次查询

<span id="3e5e18b2"></span>
## HTTP 请求


* URL: `https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01`

* 方法：POST


<span id="a7e0438d"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="dc691b28"></span>
### Query


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`AddActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="e9034e45"></span>
### Body


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`178398113630****` |直播间的活动 ID。你可以通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|WordList |Array of String |是 |`["a","b"]` |要添加的敏感词数组。可添加的词数量没有限制。<br><br>注意：词语不能包含逗号（,），因为逗号用于分隔。 |


<span id="eceb3e71"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Status |Boolean |`true` |表示敏感词是否添加成功。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="4cf59303"></span>
## 示例

<span id="45d8e74f"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="8e3de267"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "AddActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846
    },
    "Result": {
        "Status": true
    }
}
```


<span id="2c603933"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
