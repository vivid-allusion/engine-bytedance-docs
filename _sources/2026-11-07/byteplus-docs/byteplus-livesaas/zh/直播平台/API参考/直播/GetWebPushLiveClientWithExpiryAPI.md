---
title: "GetWebPushLiveClientWithExpiryAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi-zh-CN"
---

调用此 API 以获取直播间直播页的 URL。这使主播可以在无需登录的情况下，通过网页浏览器开播。返回的 URL 在指定时间段后失效。

<span id="88078564"></span>
## 要求


* 配额：每个账号每分钟 120 次查询

* 前提条件：拥有 BytePlus 账号，或具有 Live 控制 \> 仅查看或编辑权限的 IAM 用户。更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="d8d3af2c"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01`

* 方法：POST


<span id="82b326f4"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见[Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="3998820f"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetWebPushLiveClientWithExpiryAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="763ef914"></span>
### 正文


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|ActivityId |Long |是 |`17218312****` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN)获取该 ID。 |
|ExpiredTime |Long |否 |`10` |URL 的过期时间。该时间段后 URL 失效。<br><br>单位：秒。<br><br>默认值：`10`。<br><br>取值范围：[1,300] |


<span id="3bbf0ac3"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|ActivityId |Long |`17218312****` |直播间的活动 ID。 |
|Url |String |`https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0=` |直播页的 URL。主播可使用该 URL 在无需登录的情况下，通过网页浏览器开播。该 URL 在指定时长后失效。 |


<span id="29a8e2eb"></span>
## 示例

<span id="4bcaf942"></span>
### 请求示例

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "ExpiredTime": 10  
}
```


<span id="57c6761e"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientWithExpiryAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "ActivityId": 17218312****,
        "Url": "https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0="
    }
}
```


<span id="6e60f4b7"></span>
## 错误码

常见错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
