---
title: "GetBusinessAccountInfoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi-zh-CN"
---

调用此 API 获取指定直播间的主播账号信息。

配额：每个账号每分钟最多查询 120 次

<span id="106bf19e"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01`

* 方法：GET


<span id="44564612"></span>
## 请求参数

以下表格未包含所有常用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="1d297938"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetBusinessAccountInfoAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |
|ActivityId |Long |是 |`17218346****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="19c0a580"></span>
## 响应参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|IsBusinessAccountEnable |Integer |`1` |表示主播账号功能是否已开启。<br><br><br>* `0`：未开启。<br><br>* `1`：已开启。 |
|BusinessAccountInfo |BusinessAccountInfo 对象 |`-` |主播账号的信息。 |


<span id="1d108f6f"></span>
### BusinessAccountInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|AccountName |String |`Host A` |主播账号的名称。 |
|HostAccountId |Integer |`112038` |主播账号的 ID。 |
|AccountHeadImage |String |`https://example-image.image` |头像地址。 |
|AccountHeadRedirectUrl |String |`https://example.com` |主播账号的内嵌链接。观众点击账号头像后可跳转至该链接。 |
|ExternalPlatformId |String |`abc123` |外部平台 ID，仅包含大小写字母和数字，长度不超过 128 个字符。 |
|ExtraInfo |String |`abc` |与主播账号关联的附加信息。 |


<span id="e5a3129b"></span>
## 示例

<span id="78aee2a5"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetBusinessAccountInfoAPI&Version=2023-08-01&ActivityId=17218346****
```


<span id="e4dbc391"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetBusinessAccountInfoAPI",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1702896398
    },
    "Result": {
        "IsBusinessAccountEnable": 1,
        "BusinessAccountInfo": {
            "AccountName": "Host A",
            "HostAccountId": 112038,
            "AccountHeadImage": "https://example-image.image",
            "AccountHeadRedirectUrl": "https://example.com",
            "ExternalPlatformId": "abc123",
            "ExtraInfo": "abc"
        }
    }
}
```


<span id="55b7cc9a"></span>
## 错误码

常见错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
