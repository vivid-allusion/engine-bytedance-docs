---
title: "DeleteMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediaapi-zh-CN"
---

从直播活动的回放列表中删除一个视频。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">如果一个视频被包含在多个活动的回放列表中，删除该视频会将其从所有相关列表中移除。</div>


* <div data-tips="true" data-tips-type="tip">被删除的视频会永久从 BytePlus Live 移除，无法恢复。</div>


* <div data-tips="true" data-tips-type="tip">如果被删除的视频作为回放正在展示，活动状态会变为<strong>Over</strong>。但如果活动配置为自动播放下一个视频，且回放列表中还有其他视频，则会播放下一个视频。</div>



<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 操作：`DeleteMediaAPI`

* 请求方式：POST

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。当前版本：`2019-10-10`。 |


<span id="Body parameter"></span>
### 请求体参数


|**参数名称** |**数据类型** |**是否必填** |**接口行为** |
|---|---|---|---|
|Vid |String |是 |待删除视频的 ID。 |


<span id="Sample request"></span>
### 请求示例

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10
{
    "Vid": "v0c251g7007abc1"
}
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|Success |Boolean |表示删除操作是否成功。<br><br><br>* `true`：视频已被删除。<br><br>* `false`：删除失败。 |


<span id="Sample response"></span>
### **返回示例**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediaAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": true
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[共享错误和状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
