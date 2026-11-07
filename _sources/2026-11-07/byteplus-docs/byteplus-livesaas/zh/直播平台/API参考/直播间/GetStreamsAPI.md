---
title: "GetStreamsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN"
---

调用此 API 以获取将流推送到直播间，或从第三方平台拉流到直播间指定直播频道所需的信息。

<span id="requirement"></span>
## 需求

配额：每个账号每分钟最多 120 次查询

<span id="http-request"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01`

* 方法：GET


<span id="request-parameters"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整列表请参见 [通用参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN)。

<span id="query"></span>
### 查询


|名称 |数据类型 |必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |字符串 |是 |`GetStreamsAPI` |API 操作。 |
|Version |字符串 |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |长整型 |是 |`17218312****` |直播间的活动 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-CN) 获取该 ID。 |


<span id="response-parameters"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|LineDetails |[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)数组 |`-` |直播频道信息。 |


<span id="linedetails"></span>
### LineDetails


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|LineId |长整型 |`3606624` |频道 ID。 |
|LineName |字符串 |`Default` |频道名称。 |
|MainPushInfo |[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)数组 |`-` |用于推流到直播间的主流信息。 |
|BackPushInfo |[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)数组 |`-` |用于推流到直播间的备流信息。 |
|Ratio |字符串 |`1280x720` |频道的分辨率。 |
|ForwardInfo |[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)数组 |`-` |用于从第三方平台拉取主流到直播间的信息。<br><br>拉流任务在启动后有效期为 48 小时。 |
|BackupForwardInfo |[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-CN)数组 |`-` |用于从第三方平台拉流到直播间的备流信息。<br><br>拉流任务在启动后有效期为 48 小时。 |
|ExpireTime |长整型 |`1697167355` |推流地址的过期时间，采用 Unix 时间戳格式。单位为秒。 |


<span id="mainpushinfo"></span>
### MainPushInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PushPath |字符串 |`rtmps://push-rtmp-l1-act.****.com/live/` |服务器 URL。 |
|PushUrl |字符串 |`rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |推流地址。 |
|StreamingCode |字符串 |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |流密钥。 |


<span id="backpushinfo"></span>
### BackPushInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PushPath |字符串 |`rtmps://push-rtmp-f5-act.****.com/live/` |服务器 URL。 |
|PushUrl |字符串 |`rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |推流地址。 |
|StreamingCode |字符串 |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |流密钥。 |


<span id="forwardinfo"></span>
### ForwardInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PullStreamUrl |字符串 |`https://example/livesaas?key=example` |主流 URL。 |
|PullStreamStatus |字符串 |`0` |拉流任务的状态。调用 [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-CN) 后，状态会发生变化以启动或停止拉流。<br><br><br>* `0`：初始化中。<br><br>* `1`：进行中。<br><br>* `2`：完成。 |
|PullStreamCheckStatus |字符串 |`0` |流拉取检查的状态。<br><br><br>* `0`：检查中。<br><br>* `1`：源流未推送。<br><br>* `2`：流拉取成功。<br><br>* `3`：流拉取结束。<br><br>* `4`：流拉取出错。 |


<span id="backupforwardinfo"></span>
### BackupForwardInfo


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PullStreamUrl |字符串 |`https://example/livesaas?key=example` |备流 URL。 |
|PullStreamStatus |字符串 |`0` |拉流任务的状态。调用 [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-CN) 后，状态会发生变化以启动或停止拉流。<br><br><br>* `0`：初始化中。<br><br>* `1`：进行中。<br><br>* `2`：完成。 |
|PullStreamCheckStatus |字符串 |`0` |流拉取检查的状态。<br><br><br>* `0`：检查中。<br><br>* `1`：源流未推送。<br><br>* `2`：流拉取成功。<br><br>* `3`：流拉取结束。<br><br>* `4`：流拉取出错。 |


<span id="samples"></span>
## 示例

<span id="sample-request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="sample-response"></span>
### 返回调用结果示例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetStreamsAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1697163541        
   },
  "Result": {
    "LineDetails": [
      {
        "LineId": 3606624,
        "ExpireTime": 1697167355,
        "MainPushInfo": {
          "PushUrl": "rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushPath": "rtmps://push-rtmp-l1-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "BackPushInfo": {
          "PushPath": "rtmps://push-rtmp-f5-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushUrl": "rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "ForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "LineName": "Default",
        "BackupForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "Ratio": "1280x720"
      }
    ]
  }
}
```
