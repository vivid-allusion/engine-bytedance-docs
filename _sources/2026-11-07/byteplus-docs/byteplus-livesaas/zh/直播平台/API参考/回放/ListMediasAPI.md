---
title: "ListMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listmediasapi-zh-CN"
---

调用此 API 获取特定直播活动回放列表中的视频信息。该 API 支持分页，并允许你获取视频 ID、名称、时长和在线状态等详细信息。

<span id="Request"></span>
## 请求

<span id="Details"></span>
### 详情


* API 接口行为：`ListMediasAPI`

* 请求方式：GET

* 请求 URI：`http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01`

* 配额：每个账号每分钟最多 120 次查询


<span id="Query string parameters"></span>
### 查询字符串参数

下表未包含所有共享请求参数。完整列表请参见[共享请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**参数名称** |**是否必填** |**数据类型** |**接口行为** |
|---|---|---|---|
|Action |是 |String |API 接口行为。 |
|Version |是 |String |此 API 接口行为的版本。当前版本：`2020-06-01`。 |
|ActivityId |是 |Integer |直播活动的 ID。 |
|IsNeedTotalCount |否 |Boolean |是否返回回放列表中的视频总数。 |
|PageNo |是 |Integer |要返回的结果页码。指定此参数后，结果将分页显示。 |
|PageItemCount |是 |Integer |每页返回的结果数量。 |
|Name |否 |String |若指定此字段，BytePlus Live 将返回名称包含指定字符串的所有视频。 |
|Vid |否 |String |若指定此参数，BytePlus Live 将返回指定 Vid 的视频。 |


<span id="Sample request"></span>
### 请求示例

```JSON
Get http://livesaas.byteplusapi.com/?Action=ListMediasAPI&Version=2020-06-01&ActivityId=1231231231&PageNo=1&PageItemCount=10
```


<span id="Response"></span>
## 返回调用结果

<span id="Response schema"></span>
### 返回结构


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|PageNo |Integer |页码。 |
|PageItemCount |Integer |每页结果数量。 |
|TotalItemCount |Integer |回放列表中的视频总数。 |
|Medias |Array |视频信息。 |


<span id="Media"></span>
#### 媒体


|**参数名称** |**数据类型** |**接口行为** |
|---|---|---|
|MediaId |String |回放列表中视频的 ID。调用 UpdateMediaOnlineStatusAPI 时可使用该信息。 |
|Name |String |视频名称。 |
|时长 |Integer |视频时长（单位：秒）。 |
|SourceType |Integer |视频来源：<br><br><br>* 1：上传的视频文件<br><br>* 2：录制回放 |
|OnlineStatus |Integer |视频状态：<br><br><br>* 1：在线<br><br>* 2：离线 |
|Vid |String |媒体库中视频的 ID。 |
|CreateTime |Integer |通过调用`UpdateMediaOnlineStatusAPI`发布视频时的时间戳。 |
|封面图 |String |回放的封面图。 |


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"ListMediasAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1"
    },
    "Result":{
        "Medias":[
            {
                "MediaId":1,
                "Name":"example",
                "Duration":111,
                "SourceType":1,
                "OnlineStatus":0,
                "vid":"idexample",
                "CreateTime":1541154433671,
                "CoverImage": "//p-example.e.org/example.img"
            }
        ],
        "TotalItemCount":1,
        "PageNo":1,
        "PageItemCount":10           
    }
}
```
