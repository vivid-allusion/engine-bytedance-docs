---
title: "GetActivityReservationAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetActivityReservationAPIV2-zh-CN"
---

获取指定直播间的预约信息。

&nbsp;

<span id="Requirements"></span>
## 要求

配额：每个账号每分钟最多可查询 120 次

<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityReservationAPIV2` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |`1779187158280` |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|Page |Integer |否 |`1` |返回的页码。默认值：`1`。 |
|PageSize |Integer |否 |`10` |每页返回的结果数量。默认值：`10`。取值范围：[1,500]。 |
|Channel |String |否 |`123` |返回指定渠道标识的渠道数据。默认情况下，返回所有渠道的数据。你可以在直播间的**营销工具包** \> **渠道**页面的[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)获取渠道标识。 |
|TelReserve |String |否 |`182****5709` |用于预约直播流的手机号。 |
|NickName |String |否 |`Viewer A` |预约直播流的观众昵称。支持模糊搜索。 |
|ExternalId |String |否 |`1234` |观众在第三方平台上的唯一标识。支持模糊搜索。<br><br>该 ID 根据观众进入直播间的登录方式而变化。更多信息请参见[观众行为数据](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。你可以使用该 ID 在你的组织内识别观众身份，实现用户洞察和数据分析。 |


<span id="Response parameters"></span>
## 返回调用结果参数


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityId |Long |`1779187158280` |直播间的活动 ID。 |
|Total |Integer |`1` |返回结果总数。 |
|Page |Integer |`1` |返回页码。 |
|Items |[Items](https://docs.byteplus.com/en/docs/11/113516#items) 数组 |`-` |观众预约信息列表。 |


<span id="items"></span>
### Items


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|NickName |String |`Viewer A` |观众昵称。 |
|TelReserve |String |`182****5709` |用于预约直播流的手机号。 |
|Ip |String |`192.168.0.1` |观众的 IP 地址。 |
|IpAddress |String |`北京` |IP 地址所属地区。 |
|SubmitTime |Integer |`1697080167` |观众预约直播流的时间，Unix 时间戳格式。单位：秒。 |
|UserDevice |String |`Windows 10` |观众进入直播间所使用的设备类型。 |
|ExternalId |String |`31210506554471` |观众在第三方平台上的唯一标识。你可以使用该 ID 在你的组织内识别观众身份，实现用户洞察和数据分析。 |
|Extra |String |`abc` |你的额外参数。 |
|Channel |String |`123` |渠道标识。 |
|UserId |Long |`1744663139363934` |用户 ID，即观众在 BytePlus Live 内的唯一标识。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
GET https://livesaas.byteplusapi.com/?Action=GetActivityReservationAPIV2&Version=2020-06-01&ActivityId=1779****58280&Page=1&PageSize=10&Channel=123&TelReserve=182****5709
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetActivityReservationAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697080180
    },
    "Result": {
        "ActivityId": 1779****58280,
        "Total": 1,
        "Page": 1,
        "Items": [
            {
                "NickName": "Viewer A",
                "UserId": 174466****363934,
                "Channel": "123",
                "Extra": "abc",
                "ExternalId": "31210****54471",
                "UserDevice": "Windows 10",
                "SubmitTime": 1697080167,
                "IpAddress": "Beijing",
                "Ip": "192.*.*.1",
                "TelReserve": "182****5709"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

常见错误码列表请参见[常见错误及状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。
