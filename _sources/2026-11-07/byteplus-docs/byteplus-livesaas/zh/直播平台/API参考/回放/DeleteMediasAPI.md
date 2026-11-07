---
title: "DeleteMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediasapi-zh-CN"
---

一次最多可从直播活动的回放列表中删除100个视频。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">如果某个视频被包含在多个活动的回放列表中，删除该视频会将其从所有这些列表中移除。</div>


* <div data-tips="true" data-tips-type="tip">被删除的视频会从BytePlus Live中永久移除，无法恢复。</div>


* <div data-tips="true" data-tips-type="tip">如果被删除的视频是观看页上的当前回放，删除后活动状态将变为<strong>Over</strong>。但如果活动配置为在直播流结束后自动发布回放，且该活动的回放列表中有多个视频，则删除后列表中的下一个视频将自动播放。</div>



<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API操作：`DeleteMediasAPI`

* 请求方式：POST

* 请求URI：`http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10`

* 配额：每个账号每分钟120次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API操作。 |
|Version |String |是 |本API操作的版本。当前版本：`2019-10-10`。 |


<span id="Body parameter"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Vids |Array of String |是 |待删除视频的ID。最多可指定100个ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10
{
    "Vids": [
        "v0c251g7007abc1",
        "v0c251g7007abc2"
    ]
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Success |Boolean |表示删除操作是否成功。<br><br><br>* `true`：所有视频均已删除。<br><br>* `false`：有一个或多个视频删除失败。 |
|FailedList |Array of String |删除失败的视频ID。当`Success`的值为`false`时返回该参数。 |


<span id="Sample response"></span>
### **返回示例**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediasAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": false,
        "FailedList": ["v0c251g7007abc1"]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码请参见[通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
