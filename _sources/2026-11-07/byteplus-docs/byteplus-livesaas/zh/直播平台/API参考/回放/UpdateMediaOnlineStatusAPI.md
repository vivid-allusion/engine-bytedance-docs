---
title: "UpdateMediaOnlineStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi-zh-CN"
---

调用此 API 管理直播流活动的回放在线状态。您可以调用此 API 发布、撤回或移除回放。在执行此操作前，必须先上传一个视频作为回放。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`UpdateMediaOnlineStatusAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|ActivityId |Integer |是 |直播流的活动 ID。 |
|MediaId |Integer |是 |回放的视频 ID。 |
|OnlineStatus |Integer |是 |回放的状态。<br><br>有效值：<br><br><br>* `0`：已从观看页撤回。回放仍然绑定至直播流，可随时重新发布。<br><br>* `1`：已发布至观看页。<br><br>* `2`：已从直播流移除，但仍存在于媒体库中。在发布至观看页前，需调用[UploadReplayAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/uploadreplayapi)将其绑定至直播流。 |
|ForceReplayStatus |Boolean |否 |指定回放发布后是否将直播流状态从**预告**或**结束**变更为**回放**。<br><br><br>* `true`：将直播流状态变更为**回放**，允许观众观看已发布的回放。<br><br>* `false`：不变更直播流状态。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "MediaId":3706016,   
    "OnlineStatus":1,
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"UpdateMediaOnlineStatusAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1", 
        "SystemTime":1655978114
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[共享错误码与状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
