---
title: "ListActivityDetailAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-CN"
---

调用此 API，可获取指定时间范围内特定直播间的关键指标，如总直播时长、平均观看时长、独立观众（UV）和峰值同时在线人数（PCU）。

<span id="0d7f64af"></span>
## 要求


* 配额：每个账号每分钟最多查询 100 次

* 数据延迟：5 分钟


<span id="f713d23f"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01`

* 方法：GET


<span id="3442b2a9"></span>
## 请求参数

以下表格未包含所有通用请求参数。完整参数列表请参见 [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="0a89855a"></span>
### Query


|Name |Data Type |是否必填 |Sample Value |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`ListActivityDetailAPI` |API 操作。 |
|Version |String |是 |`2020-06-01` |此 API 操作的版本。当前版本：`2020-06-01`。 |


<span id="0aee7785"></span>
### Body


|Name |Data Type |是否必填 |Sample Value |接口行为 |
|---|---|---|---|---|
|PageNumber |Integer |否 |`1` |返回的页码。<br><br>默认值：`1`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该 API 操作最多支持返回 10,000 条结果，即 <code>PageNumber</code> × <code>PageSize</code> 必须小于或等于 10,000。</div><br> |
|PageSize |Integer |否 |`10` |每页返回的结果数量。<br><br>默认值：`10`。<br><br>取值范围：[1,100]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该 API 操作最多支持返回 10,000 条结果，即 <code>PageNumber</code> × <code>PageSize</code> 必须小于或等于 10,000。</div><br> |
|SortMode |String |否 |`desc` |排序方式。<br><br>默认值：`desc`。<br><br>有效值：<br><br><br>* `asc`：升序。<br><br>* `desc`：降序。 |
|SortField |String |否 |`LiveTime` |指定用于数据排序的维度。<br><br>默认值：`LiveTime`。<br><br>有效值：<br><br><br>* `LiveTime`：直播间的直播流时间，可能不是直播实际开始时间。<br><br>* `LiveDuration`：直播间的总直播时长。<br><br>* `PCU`：直播间的峰值同时在线人数。<br><br>* `UV`：直播间的独立观众或访客数量。<br><br>* `PV`：直播间的总观看次数或访问次数。<br><br>* `CommentCount`：直播间的评论数。<br><br>* `WatchDurationPerPeople`：直播间的平均观看或访问时长。 |
|ActivityName |String |否 |`直播间A` |用于筛选名称包含该值的直播间。 |
|StartLiveTime |Long |是 |`1692339016` |时间范围的起始时间，Unix 时间戳格式。单位：秒。<br><br>将返回该时间范围内的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">时间范围不能超过 365 天（31,536,000 秒）。</div><br> |
|EndLiveTime |Long |是 |`1700115016` |时间范围的结束时间，Unix 时间戳格式。单位：秒。<br><br>将返回该时间范围内的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">时间范围不能超过 365 天（31,536,000 秒）。</div><br> |
|PlayStatus |Integer |是 |`11` |指定要返回哪些数据。有效值：<br><br><br>* `1`：返回直播间处于“直播”状态时产生的数据。<br><br>* `2`：返回直播间处于“预告”状态时产生的数据，即使观看页未播放预告。<br><br>* `3`：返回直播间处于“回放”状态时产生的数据，即使观看页未播放回放。<br><br>* `10`：当直播间处于**直播**、**预告**、**回放**或**结束**状态时产生的数据均会返回，即使观看页未播放预告或回放。<br><br>* `11`：当直播间处于**直播**、**预告**或**回放**状态时产生的数据均会返回，即使观看页未播放预告或回放。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果值为 <code>1</code>、 <code>2</code>、 <code>3</code> 或 <code>11</code>，则返回总浏览量、独立观众数、平均观看时长和总观看时长。如果值为 <code>10</code>，则返回总访问量、独立访客数、平均访问时长和总访问时长。</div><br> |


<span id="c24c437f"></span>
## 返回调用结果参数


|Name |Data Type |Sample Value |接口行为 |
|---|---|---|---|
|PageNumber |Integer |`1` |返回的页码。 |
|PageSize |Integer |`10` |每页返回的结果数量。 |
|TotalCount |Integer |`1` |找到的匹配结果总数。 |
|Activities |Array of[Activities](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi-zh-CN#305f7323) |`-` |返回的直播间数据。 |


<span id="305f7323"></span>
### Activities


|Name |Data Type |Sample Value |接口行为 |
|---|---|---|---|
|ActivityId |Long |`17218346****` |直播间的活动 ID。 |
|ActivityName |String |`直播间A` |直播间名称。 |
|LiveTime |Long |`1692559016` |直播流计划开始时间，Unix 时间戳格式。单位：秒。<br><br>该时间可能与实际开始时间不同。 |
|LiveDuration |Long |`899` |直播总时长。单位：秒。 |
|PV |Long |`412` |总浏览量或访问量。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果观众或访客刷新一次观看页，浏览量或访问量会增加 1。</div><br> |
|UV |Long |`286` |独立观众或访客数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">设备 ID 相同的设备视为同一设备，使用同一设备的观众或访客计为一人。</div><br> |
|PCU |Long |`47` |峰值同时在线访客数。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">设备 ID 相同的设备视为同一设备，使用同一设备的访客计为一人。</div><br> |
|CommentCount |Long |`403` |直播间内由主播、观众和嘉宾发送的评论数量，包括已删除评论和审核中的评论。 |
|WatchDurationPerPeople |Long |`476` |平均观看或访问时长。单位：分钟。 |
|ViewDurationTotal |Long |`800` |总观看或访问时长。单位：分钟。 |


<span id="c97117a2"></span>
## 示例

<span id="38c2a2ea"></span>
### 请求示例

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01&StartLiveTime=1692339016&EndLiveTime=1700115016
```


<span id="ae83324e"></span>
### 返回示例

```JSON
{
    "ResponseMetadata": {
        "Action": "ListActivityDetailAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "Activities": [
          {
            "ActivityId": 17218346****,
            "ActivityName": "Live room A",
            "LiveTime": 1692559016,
            "LiveDuration": 899,
            "PV": 412,
            "UV": 286,
            "PCU": 47,
            "WatchDurationPerPeople": 476,
            "ViewDurationTotal": 800,
            "CommentCount": 403
          }
        ],
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1
  }
}
```


<span id="fa56be7f"></span>
## 错误码

有关通用错误码列表，请参见 [常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。
