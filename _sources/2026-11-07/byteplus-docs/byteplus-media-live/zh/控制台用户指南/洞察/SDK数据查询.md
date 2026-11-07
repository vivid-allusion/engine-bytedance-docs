---
title: "SDK数据查询"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-clientdata-zh-CN"
---

要监控你的直播内容的质量表现，可以在BytePlus MediaLive控制台使用SDK数据查询功能。本主题介绍如何查看和筛选推流和拉流的指标数据，并详细说明关键质量指标，包括回放成功率、首帧延迟和视频卡顿。

<span id="cbfcf895"></span>
## 操作流程


1. 登录[BytePlus MediaLive控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，选择**洞察** ＞ **SDK数据查询**，默认进入**全部推流**标签页的**SDK数据查询**页面。

3. 切换标签页，在指定时间范围内查看**全部推流**、**单个推流**、**全部拉流**和**单个拉流**的数据。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">在SDK数据查询页面，你可以使用以下功能细化查询结果。</div>



* <div data-tips="true" data-tips-type="tip">指定应用类型：目前仅支持查看客户端SDK数据。</div>


* <div data-tips="true" data-tips-type="tip">指定应用：查看指定应用或全部应用的SDK指标数据。默认显示全部应用。</div>


* <div data-tips="true" data-tips-type="tip">指定时间：可快速选择查询时间或手动指定时间区间。</div>


* <div data-tips="true" data-tips-type="tip">数据拆分：将展示的数据按最多三种维度进行拆分。默认不进行数据拆分。</div>


* <div data-tips="true" data-tips-type="tip">数据聚合：选择数据聚合的时间颗粒度。</div>


* <div data-tips="true" data-tips-type="tip">指定指标：查看指定指标或全部指标的数据。</div>


* <div data-tips="true" data-tips-type="tip">条件筛选：根据具体数值（如等于或不等于某值）筛选数据。</div>



<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">当SDK版本不是最新时，某项数据可能会丢失，导致数据看板出现异常值。如遇此情况，可尝试更新SDK版本。</div>


<span id="d37e31f2"></span>
## 接口行为

<span id="de270f9e"></span>
### SDK日志上报时机

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57854bdc6ecc499b8969dc6cf8f31983~tplv-goo7wpa0wc-image.image) </span>


* 首次设置URL并调用播放方法视为一次播放事件。在此过程中，每次播放仅记录并上报一条事件跟踪日志。

* 回放成功日志会在用户停止播放（调用停止方法）时于启动阶段和播放阶段均进行上报。


<span id="bedcc3ec"></span>
### 关键质量指标


|流类型 |指标 |接口行为 |
|---|---|---|
|推流 |平均码率 |展示全部推流（或单个推流）在数据聚合时间颗粒度下的平均码率趋势图，以及查询时间内的平均码率。 |
||平均帧率 |展示全部推流（或单个推流）在数据聚合时间颗粒度下的平均帧率趋势图，以及查询时间内的平均帧率。 |
|拉流 |回放成功率 |在观众设备上成功接收并回放的在线流占比。该指标衡量观众成功拉流的概率。<br><br>**计算方法**：回放成功率 =（成功回放次数 / 总回放次数）× 100%。 |
||平均首帧延迟 |用户点击播放按钮到屏幕上出现首个视频帧的时间。该指标衡量观众等待视频开始的时间。<br><br>**计算方法**：首帧延迟 = 首帧回放时间戳 \- 用户点击播放按钮时间戳。 |
||每100秒视频卡顿时长 |直播流回放过程中，每100秒视频渲染卡顿的总时长。该指标衡量回放过程中卡顿的严重程度。<br><br>**计算方法**：每100秒视频卡顿时长＝回放期间视频卡顿时长 / 回放时长 x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">视频卡顿定义：若连续两帧视频渲染间隔大于200ms，则计为一次卡顿。该时间随后会计入总卡顿时长。持续监控并优化该指标可提升回放流畅度和用户体验。</div><br> |
||平均码率 |展示所有拉流（或单个拉流）在数据聚合颗粒度下的平均码率趋势图，以及查询时间范围内的平均码率。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">为减少启动阶段码率波动的影响，拉流码率的统计范围不包含回放开始后的前5秒。</div><br> |
||端到端延迟 |服务器编码完成后推流到观众屏幕上渲染首帧视频的时间。该指标衡量观众开始观看流所需的等待时间。<br><br>**计算方法**：端到端延迟＝AVG（首帧完成渲染时间戳 \- 编码完成后实际推流时间戳） |
||平均播放时长 |展示所有拉流（或单个拉流）在数据聚合颗粒度下的平均播放时长趋势图，以及查询时间范围内的平均播放时长。 |
