---
title: "GetActivityQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-CN"
---

调用此 API 以在指定时间范围内获取某个直播间的直播质量数据。该 API 返回关键性能指标，如拉流成功率、每 100 秒卡顿时长和平均首帧时间。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请注意，当前数据仅适用于集成了 iOS 或 Android Viewer SDK 的应用。</div>


<span id="e2298f63"></span>
## 要求


* 配额：每个账号每分钟 120 次查询

* 前提条件：需拥有 BytePlus 账号，或具备 Insights \> 仅查看 或 编辑权限的 IAM 用户。更多信息，请参见 [用户、组织和角色管理](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。


<span id="7e4ac041"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01`

* 方法：GET


<span id="ff444339"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见 [通用请求参数](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。

<span id="ef12448c"></span>
### **查询**


|**名称** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GetActivityQualityDataAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |本 API 操作的版本。当前版本：`2023-08-01`。 |
|BeginTime |Long |是 |`1702263015` |查询时间范围的起始时间，Unix 时间戳格式。单位：秒。 |
|EndTime |Long |是 |`1702264015` |查询时间范围的结束时间，Unix 时间戳格式。单位：秒。 |
|ActivityId |Long |是 |`17218346****` |直播间的 ID。可通过调用 [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) 获取该 ID。 |


<span id="f6c01293"></span>
## **响应参数**


|**名称** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ActivityData |Object of[ActivityData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi-zh-CN#ActivityData) |`-` |指定时间范围内该直播间的直播质量数据。 |


<span id="2f22f87b"></span>
### ActivityData


|**名称** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PullSuccessRate |Double |`100` |拉流成功率，表示直播过程中观众设备上成功播放流的百分比。可通过该指标衡量观众成功拉取直播流的概率。<br><br>计算方法：拉流成功率 = 直播间内成功播放总次数 / 直播间内播放总次数 x 100% |
|StallTimePer100Sec |Double |`0` |每 100 秒回放的平均视频卡顿（冻结）时长。单位：秒。<br><br>可通过该指标衡量观众观看直播视频时的卡顿严重程度。<br><br>计算方法：100 秒内视频卡顿时长 = 直播间所有观众播放过程中视频卡顿总时长 / 直播间所有观众播放总时长 x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当渲染的视频帧与上一帧之间的时间间隔超过 200 毫秒时，该间隔会计入视频卡顿的时长。持续监测和优化此指标可以提升回放流畅度并改善用户体验。</div><br> |
|FirstFrameTime |Double |`0` |观众启动播放器到显示首个视频帧的平均时间。单位：毫秒。<br><br>可通过该指标衡量观众开始观看直播视频时所需等待的时长。<br><br>计算方法：<br><br><br>* 单个观众首帧时间 = 首帧显示时间戳 \- 播放器启动时间戳<br><br>* 平均首帧时间 = 直播间所有观众首帧时间总和 / 直播间观众总数 |


<span id="b6cee885"></span>
## 示例

<span id="46cbe5cf"></span>
### 请求示例

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015&ActivityId=17218346****
```


<span id="94c93aa4"></span>
### **返回示例**

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetActivityQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
    "Result": {
        "ActivityData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="34b6ffdc"></span>
## 错误码

有关通用错误码列表，请参见 [通用错误及状态码](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。


|**名称** |**消息** |**解决方案** |
|---|---|---|
|100000 |内部错误。 |请联系技术支持获取帮助。 |
|100001 |指定的参数 ActivityId 无效。 |请更改 `ActivityId` 的值。 |
|100005 |指定的参数 BeginTime 无效。 |请更改 `BeginTime` 的值。 |
|100005 |EndTime 不能等于或早于 BeginTime。 |请更改 `EndTime` 的值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能小于 1 分钟。 |请检查并更改 `BeginTime` 和 `EndTime` 的值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能超过 365 天。 |请检查并更改 `BeginTime` 和 `EndTime` 的值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能设置为早于 365 天前。 |请检查并更改 `BeginTime` 和 `EndTime` 的值。 |
