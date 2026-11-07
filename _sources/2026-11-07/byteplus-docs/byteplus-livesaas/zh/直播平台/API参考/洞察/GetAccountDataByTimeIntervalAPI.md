---
title: "GetAccountDataByTimeIntervalAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi-zh-CN"
---

调用此 API，可在指定时间区间内获取你 BytePlus 账号下所有直播间的汇总数据。返回的数据包含关键指标，如直播间总数、累计观看次数、独立观众数和总观看时长。

<span id="aa541d6f"></span>
## 需求


* 配额：每个账号每分钟最多查询 20 次

* 数据延迟：1\-3 小时


<span id="a564cbb1"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01`

* 方法：GET


<span id="8865ec2a"></span>
## 请求参数

下表未包含所有通用请求参数。完整参数列表请参见[通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。

<span id="8578a4ac"></span>
### **查询**


|**名称** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetAccountDataByTimeIntervalAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |该 API 操作的版本。当前版本：`2020-06-01`。 |
|BeginTime |Long |是 |`1692339016` |时间区间的起始时间，Unix 时间戳格式。单位：秒。<br><br>将返回该时间区间的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">时间区间不能超过 365 天（31,536,000 秒）。</div><br> |
|EndTime |Long |是 |`1700115016` |时间区间的结束时间，Unix 时间戳格式。单位：秒。<br><br>将返回该时间区间的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">时间区间不能超过 365 天（31,536,000 秒）。</div><br> |


<span id="124cd05e"></span>
## **返回调用结果参数**


|**名称** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|EventTimes |Integer |`55` |在所选时间区间内，你 BytePlus 账号下创建的直播间总数。 |
|ViewTime |Integer |`390` |在所选时间区间内，你 BytePlus 账号下所有直播间的累计观看次数。<br><br>若观众刷新一次观看页，观看次数会增加 1。 |
|ViewPeople |Integer |`200` |在所选时间区间内，你 BytePlus 账号下所有直播间的累计独立观众数。使用同一设备的观众会被计为同一观众。 |
|ViewDuration |Integer |`6000` |在所选时间区间内，你 BytePlus 账号下所有直播间的累计观看时长。单位：分钟。 |
|ViewEventTimesPerPeople |Double |`2` |在所选时间区间内，每位观众平均观看的直播间数量。该值通过将所有直播间的独立观众总和除以累计独立观众数计算得出。<br><br>分子（所有直播间的独立观众总和）会为观众加入的每个直播间计数一次。分母（累计独立观众数）无论观众加入多少直播间，只计一次。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">具有相同设备 ID 的设备会被视为同一设备。</div><br> |
|ViewDurationPerPeople |Double |`30` |在所选时间区间内，每位观众的平均观看时长。该值通过累计观看时长除以累计独立观众数计算得出。单位：分钟。 |
|ViewTimesPerPeople |Double |`1.95` |在所选时间区间内，你 BytePlus 账号下每位观众的平均观看次数，计算方式为累计观看次数除以累计独立观众数。 |


<span id="02d94806"></span>
## 示例

<span id="43bb91f0"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01&BeginTime=1692339016&EndTime=1700115016
```


<span id="74b36b31"></span>
### **返回示例**

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAccountDataByTimeIntervalAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "EventTimes": 55,
        "ViewTime ": 390,
        "ViewPeople": 200,
        "ViewDuration": 6000,
        "ViewEventTimesPerPeople": 2,
        "ViewDurationPerPeople": 30,
        "ViewTimesPerPeople": 1.95
  }
}
```


<span id="6fa7036e"></span>
## 错误码

通用错误码列表请参见[通用错误码及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
