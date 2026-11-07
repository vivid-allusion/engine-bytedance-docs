---
title: "GetAccountQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-CN"
---

调用此 API 可获取指定时间范围内，您 BytePlus 账号下所有直播间的直播流质量数据。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">请注意，目前仅支持获取集成了 iOS/Android Viewer SDK 的应用数据。</div>


<span id="a5fecde7"></span>
## 要求


* 配额：每个账号每分钟最多 120 次查询

* 前提条件：拥有 BytePlus 账号或具备超级管理员角色的 IAM 用户。更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="57b1847f"></span>
## HTTP 请求


* URL：`https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01`

* 方法：GET


<span id="0659ac9b"></span>
## 请求参数

下表未包含所有通用请求参数。完整列表请参见[Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters-zh-CN#f1706967)。

<span id="21812e6d"></span>
### 查询


|名称 |数据类型 |是否必填 |示例值 |接口行为 |
|---|---|---|---|---|
|Action |String |是 |`GetAccountQualityDataAPI` |API 操作。 |
|Version |String |是 |`2023-08-01` |此 API 操作的版本。当前版本：`2023-08-01`。 |
|BeginTime |Long |是 |`1702263015` |查询时间范围的起始时间，Unix 时间戳格式。单位：秒。 |
|EndTime |Long |是 |`1702264015` |查询时间范围的结束时间，Unix 时间戳格式。单位：秒。 |


<span id="154a269b"></span>
## 返回调用结果参数


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|AccountData |Object of[AccountData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi-zh-CN#638706eb) |`-` |指定时间范围内，您 BytePlus 账号下所有直播间的直播流质量数据。 |


<span id="638706eb"></span>
### AccountData


|名称 |数据类型 |示例值 |接口行为 |
|---|---|---|---|
|PullSuccessRate |Double |`100` |拉流成功率。该指标表示观众设备上直播流播放成功的百分比。该指标衡量观众成功拉取流的概率。<br><br>计算方式：拉流成功率 =（所有直播间的播放成功总次数 / 所有直播间的播放尝试总次数）\* 100% |
|StallTimePer100Sec |Double |`0` |每 100 秒卡顿时长。该指标表示每 100 秒直播流回放时长内的视频卡顿时长。单位：秒。<br><br>该指标衡量回放过程中视频卡顿的严重程度。<br><br>计算方式：每 100 秒卡顿时长 =（所有直播间的卡顿总时长 / 所有直播间的回放总时长）\* 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当渲染的视频帧与上一帧之间的时间间隔超过 200 毫秒时，该间隔会计入视频卡顿的时长。持续监控和优化该指标可以提升视频播放的流畅性并改善用户体验。</div><br> |
|FirstFrameTime |Double |`0` |您 BytePlus 账号下每位观众的平均首帧时间，即直播流中从播放器启动到屏幕显示首帧视频画面的时间。单位：毫秒。<br><br>该指标衡量观众等待直播视频开始播放所需的时间。<br><br>计算方法：<br><br><br>* 观众首帧时间 = 首帧显示时间戳 \- 播放器启动时间戳<br><br>* 平均首帧时间 = 您 BytePlus 账号下所有直播间所有观众的首帧时间总和 / 您 BytePlus 账号下所有直播间的观众总数 |


<span id="276bff99"></span>
## 示例

<span id="0c1dde7c"></span>
### 请求示例

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015
```


<span id="7238a117"></span>
### 返回示例

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetAccountQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
   "Result": {
        "AccountData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="63ff57ff"></span>
## 错误码

通用错误码列表请参见[常见错误和状态码](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes-zh-CN)。


|名称 |消息 |解决方案 |
|---|---|---|
|100000 |内部错误。 |请联系技术支持。 |
|100005 |指定的参数 BeginTime 无效。 |请更改`BeginTime`值。 |
|100005 |EndTime 不能等于或早于 BeginTime。 |请更改`EndTime`值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能小于 1 分钟。 |请检查并更改`BeginTime`和`EndTime`值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能超过 365 天。 |请检查并修改 `BeginTime` 和 `EndTime` 的数值。 |
|100005 |BeginTime 与 EndTime 之间的时间间隔不能设置为距今超过 365 天。 |请检查并修改 `BeginTime` 和 `EndTime` 的数值。 |
