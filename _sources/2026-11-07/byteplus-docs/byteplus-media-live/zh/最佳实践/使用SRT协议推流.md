---
title: "使用SRT协议推流"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/PushWithSRT-zh-CN"
---

要实现低延迟推送在线视频流，可以在MediaLive中使用安全可靠传输（SRT）协议。本主题介绍SRT协议的定义、限制，并提供获取推流地址及配置推流软件（如OBS）的分步操作说明。

<span id="5f710556"></span>
## Context

SRT协议是一种开源的低延迟视频传输协议。它支持在不可预测的网络类型（如互联网）上优化流媒体性能，并实现安全、可靠的高清视频传输与分发。

SRT协议基于UDT协议（基于UDP的传输协议），并保留了UDT的核心思想和机制。它提供了强大的丢包重传能力。SRT支持自动重传请求（ARQ）和前向纠错（FEC），以帮助数据恢复。

<span id="458950f1"></span>
## Restrictions


* MediaLive支持两种SRT协议推流方式：RTMP over SRT和TS over SRT。

   * TS over SRT功能使用UDP端口9000；

   * RTMP over SRT功能使用UDP端口1999。

* MediaLive支持使用H.264或H.265视频编码推送在线流，以及使用AAC编码和单音轨的纯音频流。

* 使用SRT协议推流后，支持以RTMP、FLV和RTM格式拉流和播放。目前不支持使用SRT协议拉流。

* MediaLive默认支持使用SRT协议推流。使用SRT协议推流产生的流量按**Standard**计费档位计费。


<span id="9bf6edca"></span>
## Procedure

<span id="30d88731"></span>
### 获取SRT推流地址

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">建议使用<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-address-generator">地址生成器</a>快速生成SRT推流地址。</div>


你也可以根据SRT推流地址规则手动构建推流地址。规则如下。


* TS over SRT

   ```Plain
   srt://push.example.com:9000?streamid=#!::h=push.example.com,r=AppName/StreamName,m=publish,volcTime=1648717***,volcSecret=xxx
   ```
   

   格式说明见下表。

   
   |参数 |接口行为 |
   |---|---|
   |`streamid` |需以`#!::`开头，并遵循YAML语法。 |
   |`h` |值为推流域名。 |
   |`r` |值为`{AppName}/{StreamName}`。 |
   |`m` |值为`publish`，表示推流操作。 |
   

* RTMP over SRT

   ```Plain
   rtmp://push.example.com:1999/AppName/StreamName?volcTime=1648717***&volcSecret=***
   ```
   


<span id="98c74f75"></span>
### 使用SRT协议推流

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本节示例使用最新版本的OBS进行推流演示。你可以使用任何支持SRT协议的推流软件进行直播。</div>



1. 打开OBS推流软件。

2. 在**Controls**区域点击**Settings**。

3. 在左侧导航栏选择**Stream**。在**Service**项选择**Custom**。在**Server**字段输入SRT推流地址，然后点击**OK**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cacc6f1015b34b968ec5ceadecc166cb~tplv-goo7wpa0wc-image.image) </span>

4. 在**Controls**区域点击**Start Streaming**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ebe665e26154792bbfb8d1ba089e011~tplv-goo7wpa0wc-image.image) </span>
