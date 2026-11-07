---
title: "GetWebPushLiveClientAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getwebpushliveclientapi-zh-CN"
---

获取直播间直播页面的 URL，允许主播在网页浏览器中开播，无需登录。

<span id="d1ad3925"></span>
## 需求

配额：每个账号每分钟最多 120 次查询

<span id="a61cce88"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01`

* 方法：GET


<span id="11dd5e64"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="4e52a872"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetWebPushLiveClientAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="c917226e"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|Url |String |`http://livesaas.example.com/***` |直播页面的 URL。主播可在网页浏览器中打开该 URL 进行开播，无需登录。 |


<span id="7d9b305a"></span>
## 示例

<span id="2c69e10f"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="59f3352f"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "Url": "http://livesaas.example.com/***"
    }
}
```


<span id="cb06ddde"></span>
## 错误码

通用错误码列表请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
