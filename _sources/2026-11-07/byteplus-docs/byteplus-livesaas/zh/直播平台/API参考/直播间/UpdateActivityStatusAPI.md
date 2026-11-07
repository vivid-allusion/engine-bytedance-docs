---
title: "UpdateActivityStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitystatusapi-zh-CN"
---

更新直播间状态。你可以将直播间恢复到**预告**状态、锁定预告，以及解锁预告。

<span id="requirement"></span>
## 要求

配额：每个账号每分钟最多 120 次查询

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01`

* 方法：POST


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见[通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`UpdateActivityStatusAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |此 API 操作的版本。取值为`2020-06-01`。 |


<span id="body"></span>
### 请求体


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |长整型 |是 |`17218346****` |直播间的活动 ID。你可以通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|IsStreamViewEnable |整数 |是 |`4` |指定你要执行的操作。<br><br>有效值：<br><br><br>* `3`：将直播间恢复到**预告**状态。<br><br>* `4`：锁定预告。观看页将被锁定在**预告**状态，无法播放直播视频或回放。<br><br>* `5`：解锁预告。观看页随后可以播放直播视频和回放。 |


<span id="response-parameters"></span>
## 返回调用结果


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |长整型 |`-` |已弃用。 |
|ActivityIdStr |字符串 |`-` |已弃用。 |
|状态 |整数 |`-` |已弃用。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01
{    
    "ActivityId": 17218346****,
    "IsStreamViewEnable": 4
}
```


<span id="sample-response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1696235450
    },
    "Result": {
        "ActivityId": 0,
        "ActivityIdStr": "",
        "Status": 0
    }
}
```


<span id="error-codes"></span>
## 错误码

通用错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
