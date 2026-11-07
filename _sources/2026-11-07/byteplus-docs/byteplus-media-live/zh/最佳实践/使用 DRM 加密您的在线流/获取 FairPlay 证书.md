---
title: "获取 FairPlay 证书"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate-zh-CN"
---

要在您的在线流中实施 FairPlay 加密，您首先需要从 Apple 获取 FairPlay 流媒体证书。本主题提供了获取证书并准备上传至 BytePlus MediaLive 和 Intertrust 的详细步骤说明。

<span id="9aa7496a"></span>
## 前提条件

一个[Apple Developer account](https://developer.apple.com/)。

<span id="cd56ff31"></span>
## 操作流程

<span id="79283f56"></span>
### 获取 PEM 文件


1. 访问 Apple 的[FairPlay Streaming](https://developer.apple.com/streaming/fps/)概览页面，并使用您的 Apple 开发者账号登录。

2. 导航至页面底部，点击[Request FPS Deployment Package](https://developer.apple.com/contact/fps/)。

3. 按照页面上的说明下载 FPS 部署包并解压。

4. 根据包内说明，创建 .pem 格式的私钥文件和 .csr 格式的证书签名请求文件。记录用于生成私钥文件的私钥。


<span id="c164d382"></span>
### 获取 ASK 和证书文件


1. 在[Apple Developer Portal](https://developer.apple.com/)中，点击左侧导航栏的**Certificates, ID & Profiles**。

2. 点击 + 按钮。

3. 选择**FairPlay Streaming Certificate**，然后点击**Continue**。

4. 上传您在上一步获得的 CSR 文件。上传成功后，您将获得 Application Secret Key (ASK)。

5. 按照屏幕上的指示生成 FairPlay 证书。

6. 证书签发后，下载 FairPlay 流媒体证书。


<span id="1d180a9f"></span>
## 后续操作

获取 FairPlay 流媒体证书后，您需要将证书上传至 BytePlus MediaLive 和 Intertrust。

有关上传的详细说明，请参阅[Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses)和[Uploading a FairPlay certificate to Intertrust](https://docs.byteplus.com/docs/byteplus-media-live/docs-uploading-a-fairplay-certificate-to-intertrust)。
