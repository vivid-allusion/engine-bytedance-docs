---
title: "GetCheckInRecordStatisticsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-CN"
---

调用`GetCheckInRecordStatisticsAPI`以获取指定直播间的签到记录。

<span id="Requirements"></span>
## 要求


* 配额：每个账号每分钟最多查询 120 次。

* 前提条件：需拥有 BytePlus 账号，或具有**Insights** \> **仅查看**或**编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：GET

* Endpoint：https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020\-06\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

以下表格未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetCheckInRecordStatisticsAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |本 API 操作的版本。当前版本：`2020-06-01`。 |
|ActivityId |Long |是 |17218346\*\*\*\* |直播间的活动 ID。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|PageNo |Integer |否 |1 |返回的页码。默认值：`1`。 |
|PageItemCount |Integer |否 |`10` |每页返回的结果数量。默认值：`10`。 |
|CheckInId |String |是 |`checkIn1754478641140752` |直播间的签到 ID。可通过调用 GetCheckInListAPI 获取该 ID。 |


<span id="Response parameters"></span>
## 返回调用结果


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CheckInStatisticsList |Array of[CheckInStatisticsList](https://docs.byteplus.com/docs/byteplus-livesaas/GetCheckInRecordStatisticsAPI-zh-CN#checkinstatisticslist) |`-` |已签到观众的信息列表。 |
|PageNo |Integer |1 |返回的页码。 |
|PageItemCount |Integer |10 |每页返回的结果数量。 |
|PageTotalCount |Integer |1 |查询结果总数。 |


<span id="checkinstatisticslist"></span>
### CheckInStatisticsList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityId |Long |17218346\*\*\*\* |直播间的活动 ID。 |
|CheckInID |String |`checkIn1754478641140752` |签到 ID。 |
|UserID |Long |173868673758\*\*\*\* |观众 ID。 |
|UserName |String |`aa` |观众昵称。 |
|LoginTel |String |`158xxxx66` |观众用于登录的手机号。 |
|Email |String |zhibo@xxx.com |观众的邮箱。 |
|CheckInTime |Integer |`1673202796` |观众签到时间，Unix 时间戳（秒）。 |
|PersonInfo |String |`aa` |观众签到信息。 |
|Extra |String |abc |同步到 BytePlus Live 的额外参数，可与观众关联。例如，可以将观众的部门信息从自有账号系统同步到 BytePlus Live。 |
|UserAgent |String |Intel Mac OS X 10_15_7 |观众设备的 User Agent 字符串。 |
|Ip |String |192.0.2.1 |签到观众的 IP 地址。 |
|ExternalId |String |160575648853\*\*\*\* |观众在第三方平台的唯一标识。支持模糊搜索。<br><br>该 ID 会根据观众登录直播间的方式而变化。更多信息请参见[观众行为数据](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-data-statistics#viewer-behavior-data)。可使用该 ID 在组织内识别观众，实现用户洞察与数据分析。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetCheckInRecordStatisticsAPI&Version=2020-06-01&ActivityId=17218346****&PageNo=1&PageItemCount=10&CheckInId=checkIn1754478641140752
```


<span id="Sample response"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCheckInRecordStatisticsAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "CheckInStatisticsList": [
            {
                "ActivityId": 17218346****,
                "CheckInID": "checkIn1754478641140752",
                "UserID": 173868673758****,
                "UserName": "aa",
                "LoginTel": "158xxxx66",
                "Email": "zhibo@xxx.com",
                "CheckInTime": 1673202796,
                "PersonInfo": "aa",
                "Extra": "abc",
                "UserAgent": "Intel Mac OS X 10_15_7",
                "Ip": "192.0.2.1",
                "ExternalId": "160575648853****"
            }
        ],
        "PageNo": 1,
        "PageItemCount": 10,
        "PageTotalCount": 1
    }
}
```


<span id="Error codes"></span>
## 错误码

下表列出了本 API 操作的专用错误码。通用错误码列表请参见[通用错误码和状态码](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-shared-error-and-status-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParameter.ActivityIDInvalid |指定的参数 ActivityID 无效。 |无效的直播间 ID。请输入有效的 ID 并重试。可通过调用[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi)获取该 ID。 |
|500 |InternalError |请求因未知错误失败。 |处理请求时发生未知错误。请联系技术支持以获取帮助。 |
