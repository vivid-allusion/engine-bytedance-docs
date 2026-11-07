---
title: "管理 HLS 密钥获取地址"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-hls-keyaddress-zh-CN"
---

要使用标准加密保护您的 HLS 在线流，您需要在 MediaLive 中配置密钥获取地址。本主题介绍 HLS 加密的实现原理，并指导您完成密钥获取地址及更新周期的配置流程。

<span id="6c918260"></span>
## 实现原理

MediaLive 的 HLS 加密功能采用 HLS 协议的通用加密方案。该方案通过 AES\-128 加密算法对每个 TS（传输流）进行加密，并在生成的播放列表文件中添加解密信息。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bc33011b5894f68b09c66dad019c0ed~tplv-goo7wpa0wc-image.image) </span>

在该方案中，MediaLive 集成了 KMS 服务，用于生成并定期轮换加密密钥。

加密与解密流程如下：


1. 客户端通过 HLS 拉流地址对加密的直播流发起拉流请求。

2. 收到请求后，MediaLive 使用自身生成的密钥对直播流进行加密，并将包含解密信息的 M3U8 文件返回给客户端。在该文件中，#EXT\-X\-KEY 标签包含加密信息，URI 是客户端向自建密钥管理服务请求密钥的地址。M3U8 文件的部分内容示例如下。

   ```Bash
   #EXTM3U
   #EXT-X-VERSION:3
   #EXT-X-MEDIA-SEQUENCE:107326
   #EXT-X-TARGETDURATION:2
   #EXT-X-PROGRAM-DATE-TIME:2024-05-07T17:59:02.927+08:00
   #EXT-X-KEY:METHOD=AES-128,URI="https://example.kms.com/get_hls_enc_key?key_id=08e765a4da*****c4028755c3c",IV=0x00000000000000000000000000000000
   #EXTINF:2.000,
   HD_1080p_1715075942927_3070957834_107326.ts?ps=11&app=live&stream=HD_1080p&vhost=push.example.com
   ```
   

3. 客户端根据 M3U8 文件中的解密信息，向自建密钥管理服务请求密钥。

4. 自建密钥管理服务向 MediaLive 请求密钥。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">自建密钥管理服务必须支持密钥缓存。这样可以让服务直接返回密钥用于后续拉流请求，无需每次都从 MediaLive 获取。   </div>
   

5. 自建密钥管理服务将从 MediaLive 获取的密钥返回给客户端，客户端再使用该密钥解密并回放 M3U8 文件。


<span id="7fb5ff63"></span>
## 前提条件

<span id="73462349"></span>
### 自建密钥管理服务

要使用 HLS 加密，您必须自建密钥管理服务以处理解密和回放。该服务需支持以下功能：


* 支持从 MediaLive 获取密钥：HLS 加密密钥由 MediaLive 提供，因此您的密钥管理服务需调用 MediaLive 提供的 GetHLSEncryptDataKey API 获取加密密钥。

* 支持缓存已获取的密钥：为避免所有拉流行为都从 MediaLive 获取密钥，您的密钥管理服务应具备缓存功能，允许客户端直接从您的服务获取密钥。


<span id="a889ced5"></span>
### 鉴权（可选）

您还可以使用 MediaLive 提供的远程鉴权功能对拉流请求进行校验。如需使用该功能，请通过[创建工单](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)联系技术支持。

<span id="8a91d8c7"></span>
## 操作流程


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**设置**\>**加密**。在出现的**加密**页面，点击**HLS 标准**标签页。

3. 点击**编辑**，弹出对话框。

4. 填写密钥获取地址和密钥更新周期。

5. 点击**确认**保存设置。


<span id="d4be5c99"></span>
## 后续操作


1. 添加 HLS 加密配置。操作说明请参见[管理加密配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration-zh-CN)。

2. 生成加密 HLS 流的拉流地址。操作说明请参见[生成流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-relay-zh-CN)。
