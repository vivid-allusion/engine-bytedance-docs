---
title: "BytePlus MediaLive 入门"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getting-started-zh-CN"
---

要使用 BytePlus MediaLive 开始直播您的内容，本主题将为您提供完整的初始设置流程。您将学习如何激活服务、添加并配置推流域名和拉流域名、生成流地址，并开启您的首个直播流。

<span id="6cf2b444"></span>
## 前提条件


* 一个 BytePlus 账号。

* 如果这是您首次登录 [BytePlus 控制台](https://console.byteplus.com)，请完成身份认证。

* 如果您没有自己的推流域名和拉流域名，可以使用 MediaLive 提供的测试域名。

* 若您希望使用自己的域名，必须至少添加两个：一个用于推流，一个用于拉流。推流域名和拉流域名必须处于同一域名空间。


<span id="b3bed337"></span>
## 操作流程

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a390beb258b4fb589a233096aa071f3~tplv-goo7wpa0wc-image.image) </span>

<span id="da5a6a63"></span>
### 激活 MediaLive 服务


1. 登录 [BytePlus 控制台](https://console.byteplus.com/)。

2. 在 **产品**部分，点击 **BytePlus MediaLive**。

3. 如页面提示，请按照屏幕上的指引填写您的计费情况。否则，请进入下一步。

4. 点击 **立即激活**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718efbc829a14a5c939be63e0b4f3dbf~tplv-goo7wpa0wc-image.image) </span>

5. 根据屏幕指引填写您的信息，然后点击 **申请激活**。

6. 激活完成后，登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live)。


<span id="fc8ae6de"></span>
### 添加域名

要使用 BytePlus MediaLive，您必须至少添加两个域名，一个用于推流，另一个用于拉流。

MediaLive 使用域名空间来关联推流域名和拉流域名。用于同一业务线的推流域名和拉流域名需处于同一域名空间。请参阅 [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost)，了解推流域名和拉流域名之间的详细关联说明。


1. 在左侧导航栏，点击 **域名**。

2. 在出现的 **域名**页面，点击 **添加域名**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ec6554b63b6491d81155cd2a980b6c5~tplv-goo7wpa0wc-image.image) </span>

3. 完成以下配置：

   * **添加域名**：

      1. 选择 **推流**作为域名类型。域名添加后无法更改域名类型。

      2. 输入推流域名。您不能添加泛域名。建议您使用二级域名，例如 `example.live.com`。每个账号最多可添加 10 个域名。

      3. 若需使用 [实时媒体（RTM）](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction)协议，必须为您的域名配置 SSL 证书。

   * **关联域名空间**：

      * 建议使用第一个添加的域名作为域名空间名称。

      * 请输入以“.com”结尾的小写字母域名。

      * 输入二级域名或子域名。

      * 域名与域名空间相关联。默认可添加 10 个域名空间。如需添加更多，请联系 [BytePlus 技术支持](https://console.byteplus.com/workorder/create)。

   * **加速区域：**  选择您希望加速内容分发的区域。直播服务费用会因加速区域而异。请参阅 [直播服务费用](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-streaming-service-fees)，获取详细价格信息。

      :::提示

      如果你选择**全球加速**或**中国大陆**，则必须为域名办理互联网内容提供商（ICP）许可证。你可以在[ICP/IP 地址/域名信息备案管理系统](https://beian.miit.gov.cn/#/Integrated/index)上完成验证流程。

      :::

   * **项目**：为域名空间选择一个项目。域名空间与项目关联后，你可以按项目管理资源使用情况和计费情况。有关项目的更多信息，请参见[关于项目](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects)。

4. 点击**下一步**以保存设置。

5. 重复步骤 2 至 4，添加拉流域名。请确保将**拉流**选择为域名类型。


已添加的域名会显示在域名列表中。

<span id="f55c33b3"></span>
### 配置 CNAME 记录

为域名添加 CNAME 记录，将其指向自动分配的对应 BytePlus MediaLive 域名。这样，所有访问你的域名的流量都会被定向到 BytePlus MediaLive 域名。


1. 在域名列表中，找到你要配置的域名，然后复制**CNAME**列中的对应 BytePlus MediaLive 域名。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5facfd095c54e19b6fb629e262ad6df~tplv-goo7wpa0wc-image.image) </span>

2. 登录你的域名服务商的 DNS 平台。为该域名添加 CNAME 记录，指向 BytePlus MediaLive 域名。

3. 运行`ping`或`dig`命令，检查 CNAME 记录是否生效。如果输出结果显示 BytePlus MediaLive 域名为 CNAME，则配置成功，域名可以正常使用。你也可以通过确认 BytePlus MediaLive 域名旁边的图标变为绿色对勾来验证配置。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8f1391c173444ff8a74ca5db24385da~tplv-goo7wpa0wc-image.image) </span>


有关配置 CNAME 记录的详细说明，请参见[添加 CNAME 记录](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record)。

<span id="4f17ce32"></span>
### （可选）HTTPS 及其他域名设置

你可以根据实际需求配置其他域名设置，例如配置 SSL 证书或 referer blocklist。请参见以下主题，获取完成设置的详细说明。


* [添加 SSL 证书](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)

* [Referer](https://docs.byteplus.com/docs/byteplus-media-live/docs-referer)

* [URL 鉴权](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication)

* [IP 限制](https://docs.byteplus.com/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist)


本主题以 SSL 证书配置为例进行说明。如需为域名配置 SSL 证书，请完成以下步骤：

<span id="7a4f3332"></span>
#### 添加 SSL 证书


1. 在左侧导航栏，点击**证书**。

2. 在**证书**页面，点击**添加证书**，打开**添加 HTTPS 证书**对话框。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9223e729e0c74fc2a6075fbaed9b4043~tplv-goo7wpa0wc-image.image) </span>

3. 输入证书名称、证书内容和私钥。当前仅支持添加 PEM 格式的证书。

4. 点击**确认**以保存 SSL 证书。


<span id="67853b4d"></span>
#### 启用 HTTPS


1. 在左侧导航栏，点击**域名**。

2. 在出现的**域名**页面，找到待配置的域名，在**操作**列点击**设置**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86933bf66e50428889bd16253b570a0e~tplv-goo7wpa0wc-image.image) </span>

3. 在打开的域名页面，点击**HTTPS**标签页。

4. 在**HTTPS**开关右侧点击**编辑**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10c428c6e1f14e32b86461545b03bf08~tplv-goo7wpa0wc-image.image) </span>

5. 在弹出的**编辑 HTTPS 信息**对话框中，**HTTPS**会自动开启。选择要使用的 SSL 证书，点击**确认**。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">要在 <strong>证书</strong> 列表中显示，你的 SSL 证书必须在其 <strong>Subject Alternative Name</strong> 字段中包含你的域名。</div>


* <div data-tips="true" data-tips-type="tip">HTTPS 加密大约需要 10 分钟生效。如果配置未生效，请联系你的技术支持人员协助。</div>



<span id="fc6a3cf4"></span>
### （可选）转码及其他功能设置

BytePlus MediaLive 还为你提供多种增值服务，例如转码和录制。有关如何使用这些服务的详细说明，请参见以下主题：


* [配置转码任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)

* [配置录制任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings)

* [配置截图任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-screenshot-capturing)

* [配置回源拉流任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings)

* [配置时移任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting)

* [配置水印任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks)

* [配置回调任务](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task)


<span id="f4551ba7"></span>
### 生成流地址

你可以通过 [地址生成器](https://console.byteplus.com/live/main/locationGenerate) 生成推流和拉流地址，或通过一组拼接规则手动构造。详情请参见 [生成直播流地址](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses)。

<span id="Starting the live stream"></span>
### 开始直播

你可以通过以下任一方式开始直播：


* 使用 [Web 推流](https://console.byteplus.com/live/main/WebPushStream) 和 [Web 拉流](https://console.byteplus.com/live/main/webPullStream/play)，这是 BytePlus MediaLive 控制台内提供的 Web 工具，可直接通过浏览器进行推流和拉流。有关如何使用这些工具的说明，请参见以下主题：

   * [通过控制台推流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-push)

   * [通过控制台拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull)

* 使用第三方推流工具（如 Open Broadcaster Software（OBS））和视频播放器（如 VLC）进行推流和拉流。

* 将 BytePlus MediaLive 推流 SDK 和 BytePlus MediaLive 拉流 SDK 集成到你的应用中，实现推流和拉流：

   * Android 和 iOS：[SDK 简介](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)

   * Web：[Web 端拉流 SDK：SDK 概览](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web) 和 [Web 端推流 SDK：SDK 概览](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web)


<span id="1f2fd5c3"></span>
### （可选）使用 OpenAPI

除了使用 BytePlus MediaLive 控制台外，你还可以通过 OpenAPI 访问 MediaLive 服务。请参见

[BytePlus MediaLive OpenAPI 简介](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-with-your-api)，了解如何开始使用 MediaLive OpenAPI。

此外，BytePlus MediaLive 还提供服务端 SDK，包含 Java、Python、Go 和 PHP 的 API 请求示例。详情请参见 [服务端 SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk)。
