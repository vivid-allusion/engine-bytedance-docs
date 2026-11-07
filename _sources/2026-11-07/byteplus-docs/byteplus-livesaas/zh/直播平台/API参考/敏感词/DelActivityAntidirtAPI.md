---
title: "DelActivityAntidirtAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-delactivityantidirtapi-zh-CN"
---

该 API 用于从指定的直播间删除敏感词。

<span id="9a06e2dd"></span>
## 需求

配额：每个账号每分钟最多可查询 120 次

<span id="3dda4933"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01`

* 方法：POST


<span id="44d1b454"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="19f7773f"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`DelActivityAntidirtAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="e8b5e6dd"></span>
### 请求体


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`178398113630****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |
|WordList |String 数组 |是 |`["a","b"]` |待删除的敏感词。<br><br>敏感词不能包含逗号（,），因为逗号用于在列表中分隔词语。 |
|DeleteAll |Boolean |否 |`true` |指定是否删除直播间中的所有敏感词。<br><br>默认值：`false`。<br><br>有效值：<br><br><br>* `true`：删除所有敏感词。<br><br>* `false`：不删除所有敏感词。 |


<span id="c86c0d63"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Status |Boolean |`true` |表示操作是否成功。<br><br><br>* `true`：成功。<br><br>* `false`：失败。 |


<span id="cae97f6d"></span>
## 示例

<span id="691dfa76"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=DelActivityAntidirtAPI&Version=2020-06-01
{
    "ActivityId": 178398113630****,
    "WordList": ["a","b"]
}
```


<span id="31e7c378"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "DelActivityAntidirtAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681971407
    },
    "Result": {
        "Status": true
    }
}
```


<span id="bd73d2c5"></span>
## 错误码

有关通用错误码列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
