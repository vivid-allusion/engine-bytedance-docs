---
title: "集成 Web 端推流 SDK"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-integrating-the-broadcast-sdk-for-web-zh-CN"
---

要实现基于 Web 的直播流，可以使用 Web 端推流 SDK。本主题提供从安装 SDK 到推送你的流的端到端操作指南。内容涵盖摄像头设置、示例代码及常见问题解答，帮助你在几分钟内开始推流。

<span id="be143904"></span>
## 前提条件

在集成**BytePlus MediaLive Broadcast SDK**之前，请确保以下事项：


* **环境要求**：

   * **推流地址**：登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/locationGenerate)，并使用地址生成器获取 RTM 推流地址。

* **硬件设置**：

   * 请确认你的设备（如摄像头、麦克风）已正确连接。

   * 授予浏览器访问摄像头、麦克风和屏幕共享的权限。

* **所需工具**：如通过**NPM**使用 SDK，请确保已安装**Node.js**及包管理器。


<span id="e912e634"></span>
## 操作流程

<span id="0fb66f1b"></span>
### Step 1: 导入 SDK

你可以**通过 NPM**导入 SDK


<Tabs>
<Tab zoneid="A1kWmGoFaW" title="通过 NPM">
<TabTitle>通过 NPM</TabTitle>

1. 安装 SDK：


```Bash
npm install @byteplus/vepusher@2.0.1 --save
```



2. 导入 SDK：


```JavaScript
import LivePusher from '@byteplus/vepusher';
```



</Tab>
</Tabs>


<span id="7c3aca7c"></span>
### Step 2: 启动直播流


1. 初始化 SDK：


```JavaScript
const livePusher = new LivePusher();
```



2. 在 HTML 中创建本地预告容器：


```HTML
<div id="preview"></div>
```



3. 绑定预告容器并开始渲染：


```JavaScript
livePusher.setRenderView('preview');
livePusher.startPreview();
```



4. 可选：在采集前设置视频/音频转码档位：


```JavaScript
livePusher.setVideoQuality('720p-1'); // Default video quality
livePusher.setAudioQuality('STANDARD'); // Default audio quality
```



5. 采集媒体源。SDK 支持摄像头、麦克风、屏幕共享等多种媒体源。采集完成后，预告会自动更新：


```JavaScript
livePusher.startCamera();       // Capture camera
livePusher.startMicrophone();   // Capture microphone
```



6. 开始推流。使用 BytePlus MediaLive 控制台中的推流地址：


```JavaScript
livePusher.startPush('https://{{domain}}/{{appName}}/{{streamName}}.sdp');
```


<span id="5bd75e48"></span>
### Step 3: 结束直播流


1. 停止推流：


```JavaScript
livePusher.stopPush();
```



2. 释放媒体设备（摄像头/麦克风）：


```JavaScript
livePusher.stopCamera();
livePusher.stopMicrophone();
```


<span id="3304c6ec"></span>
## 常见问题

<span id="75db841d"></span>
### 为什么推流失败？


* 请确保推流地址有效。

* 请确保有视频轨道；当前暂不支持纯音频推流。

* 请确认你的网络带宽能够支持推流。


<span id="bbe22907"></span>
### 为什么视频卡顿？


* 请检查你的网络是否有足够且稳定的上行带宽。

* 降低转码档位（例如从`720p-1`降至`360p`）。
