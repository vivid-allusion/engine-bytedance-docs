---
title: "GetRealTimeOnlineNumberAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getrealtimeonlinenumberapi-zh-CN"
---

调用此 API 获取指定直播间的在线人数（包括虚拟人气）。数据每分钟更新一次。

<span id="a5e47365"></span>
## 要求

配额：每个账号每分钟最多 120 次请求

<span id="b64eac6a"></span>
## HTTP 请求


* 方法：GET

* 接口地址：`https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01`


<span id="3f1a15e7"></span>
## 请求参数

<span id="f6822206"></span>
### 通用参数

下表未包含所有通用请求参数。完整列表请参见[通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="ce9592c2"></span>
### 查询


|参数 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetRealTimeOnlineNumberAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`178398****301234` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |


<span id="21aa01c9"></span>
## 返回参数


|参数 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|RealPopularity |Integer |`1` |直播间的实际观众人数。 |
|FakePopularity |Integer |`2` |直播间的虚拟人气。 |


<span id="e910ff53"></span>
## 示例

<span id="9fe44dd6"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01&ActivityId=178398****301234
```


<span id="6ff71fa6"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetRealTimeOnlineNumberAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681979936
    },
    "Result": {
        "RealPopularity": 1,
        "FakePopularity": 2
    }
}
```


<span id="9ccfe9d9"></span>
## 错误码

常见错误码请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
