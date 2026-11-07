---
title: "管理 DRM 许可证"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-managing-drm-licenses-zh-CN"
---

要通过加密保护您的视频流，您需要将 DRM 密钥和 FairPlay 证书上传至 BytePlus MediaLive。本主题为这两项操作提供了分步说明。

<span id="8aa0da77"></span>
## 上传 DRM 密钥

<span id="24fcd147"></span>
### 前提条件

您必须首先从[Intertrust](https://portal.expressplay.com/)获取 DRM 密钥。有关获取密钥的详细说明，请参见[获取 DRM 密钥](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-drm-key)。

<span id="bf440097"></span>
### 操作步骤


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**加密**。

3. 点击**DRM**标签页。

4. 在**API 密钥信息**配置区域，点击**编辑**。将弹出一个对话框。

5. 输入密钥。

6. 点击**确认**以保存设置。


<span id="28aa3894"></span>
## 上传 FairPlay 证书

要在 Apple 设备上启用加密，您还需要上传 FairPlay 证书。

<span id="c7f3874e"></span>
### 前提条件

您必须拥有 FairPlay 证书。有关获取证书及其他相关信息的说明，请参见[获取 FairPlay 证书](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-acquiring-a-fairplay-certificate)。

<span id="ad2418f7"></span>
### 操作步骤


1. 登录[BytePlus MediaLive 控制台](https://console.byteplus.com/live)。

2. 在左侧导航栏，点击**加密**。

3. 点击**DRM**标签页。

4. 在**证书**配置区域，点击**编辑**。将弹出一个对话框。

5. 配置相关设置。

   
   |**参数** |**接口行为** |
   |---|---|
   |证书名称 |您的 FairPlay 证书名称。 |
   |证书文件 |上传 .cer 文件。 |
   |私钥文件 |上传 .pem 文件。 |
   |私钥 |用于解密私钥文件的密码。 |
   |ASK |申请证书时 Apple 提供的 Application Secret Key（ASK） |
   

6. 点击**确认**以保存设置。


<span id="54d8c93d"></span>
## 后续操作

在 BytePlus MediaLive 控制台中，配置需要加密的域名和 AppName。您可以参考[管理加密配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task)获取详细说明。
