---
title: "通过 RTMP 在 TikTok 上进行直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN"
---

你可以通过 RTMP 将 BytePlus AI Live 的直播推送到 TikTok，让观众在 TikTok 上观看你的 AI 数字人。本指南介绍如何在 AI Live 中将 TikTok 配置为直播目的地，并通过 TikTok 应用或 TikTok LIVE Center 获取服务器 URL 和推流密钥。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b107d695409a419c88170e89cfbb29b6~tplv-goo7wpa0wc-image.image)

## 前提条件

* 你已搭建 AI 数字人直播间，并准备开始直播。如需了解更多信息，请参见 [启动 AI 直播](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN)。

* 你拥有在 TikTok 上直播的权限。如需了解更多信息，请参见 [TikTok 上谁可以使用 LIVE](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

## 操作流程

在 AI Live 中，于 **直播平台**对话框配置 TikTok 的 RTMP 推流设置。

1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)并打开你的 AI 直播间。

2. 在顶部导航栏，点击 **直播平台**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

3. 在 **直播平台**对话框中，配置以下设置，然后点击 **保存**。

   |**配置** |**说明** |
   |---|---|
   |直播平台设置 |选择 **TikTok 作为** 流目的地。 |
   |推流方式 |当你选择 **TikTok** 作为直播平台时，请选择 **RTMP** 作为推流方式。关于 **Virtual Camera**，请参见 [通过 OBS 虚拟摄像头在 TikTok 直播](https://docs.byteplus.com/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS-zh-CN)。 |
   |TikTok ID |如下所示，在你的 TikTok 应用中获取 ID。<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10ac18d800e74e5dbc8c28146e8b1580~tplv-goo7wpa0wc-image.image) |
   |URL 服务器 |输入当前 TikTok 直播的推流地址（RTMP 服务器地址）。操作说明请参见 [获取服务器 URL 和推流密钥](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |流密钥 |输入与上述服务器地址关联的 TikTok 流密钥。操作说明请参见 [获取服务器 URL 和推流密钥](https://docs.byteplus.com/docs/byteplus-livesaas/Synchronizing_a_live_stream_from_AI_Live_to_third-party_platforms-zh-CN#how-to-synchronize-a-live-stream-to-major-live-streaming-platforms)。 |
   |推流 |启用此选项，将你的 AI 直播推送到 TikTok。 |

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9269d0affec041ab96bc5e24801eb065~tplv-goo7wpa0wc-image.image)

4. 启动你的 AI Live。详情请参见 [启动 AI 直播](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN)。

### 获取服务器 URL 和推流密钥

本节介绍如何通过 TikTok 应用或 TikTok LIVE Center 获取服务器 URL 和推流密钥。随着 TikTok 政策的更新，方法和直播权限要求可能会发生变化。

1. 在 TikTok 上查找并复制服务器 URL 和推流密钥。

   > **说明**

   > 每次在 TikTok 开播时，必须复制服务器地址和流密钥。

   **TikTok 应用**

在 TikTok 应用中查找并复制服务器地址和流密钥。

      1. 打开你的 TikTok 应用。

      2. 进入底部导航栏，点击加号“+”按钮。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75eece96c4641228a643f1cd42f32c8~tplv-goo7wpa0wc-image.image)

      3. 选择 **Stream key** 选项，然后点击 **Go LIVE**。

         > **说明**

         > 如果未显示此选项，说明你的账号没有直播权限。更多信息，请参见[谁可以在 TikTok 上使用 LIVE](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9d3e968f9536438288b68d3c759612d6~tplv-goo7wpa0wc-image.image)

      4. 根据需要选择你的直播主题。此时即可看到服务器地址和流密钥。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a414115857ec46c18bdac55cb92dcf15~tplv-goo7wpa0wc-image.image)

   **TikTok LIVE Center**

在 TikTok LIVE Center 查找并复制服务器地址和流密钥。

      1. 进入 [TikTok LIVE Center](https://livecenter.tiktok.com/producer)。

      2. 在左侧导航栏点击 **Go LIVE**。

         > **说明**

         > 如果未显示此选项，说明你的账号没有直播权限。更多信息，请参见[谁可以在 TikTok 上使用 LIVE](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d076bd36c2974227b8d36c5643953aca~tplv-goo7wpa0wc-image.image)

      3. 输入你的直播详情，如有需要上传 LIVE 封面。

      4. 点击 **Save & Go LIVE**。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/80d6e9c8b8f84967b36611d3ebd26a51~tplv-goo7wpa0wc-image.image)

         这还不会启动你的直播。这会生成你的服务器 URL 和推流密钥，你需要将其添加到 BytePlus，以便启动你的直播。服务器 URL 和推流密钥将保持有效 5 分钟，因此你需要在该时间内完成下一部分操作。

         ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85bdf73e46c1475e8592a9ffd3fce217~tplv-goo7wpa0wc-image.image)

### 从 BytePlus Live 获取拉流地址

若第三方平台支持从外部 URL 拉取直播流，你可以获取 BytePlus Live 直播间的拉流地址，并在该平台使用。

1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)并打开直播间。

2. 在左侧导航栏，点击 **营销工具包** \> **多平台直播**。

3. 点击 **获取拉流地址**，并复制弹出对话框中的地址。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4672bbd0f94f018254c6526b42a7cf~tplv-goo7wpa0wc-image.image)

> **说明**

> 每个直播间仅有一个拉流地址。

### 获取其他平台的推流地址

本节介绍如何在其他主流直播平台获取服务器 URL 和推流密钥，或等效的推流地址。随着各平台政策的更新，方法和直播权限要求可能会发生变化。

#### YouTube Live

1. 登录 [YouTube Live](https://www.youtube.com/)。

2. 在页面右上角，点击 **创建**图标并选择 **直播**。

若首次启用直播功能，最多可能需要 24 小时才能获得直播权限。

3. 在 **STREAM SETTINGS**标签页，将流 URL 与推流密钥拼接。确保流 URL 在前，推流密钥在后。

4. 使用拼接后的字符串作为推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image)

#### MetaLive

1. 登录 [Facebook](https://www.facebook.com/live/create)。

2. 在 **直播**板块点击 **直播**。

3. 选择 **流媒体软件**作为视频来源。

4. 如需让推流密钥永久有效，请开启 **持久推流密钥**开关。否则，直播结束后推流密钥将无法再次使用。

5. 用斜杠（/）将服务器 URL 与推流密钥拼接。确保服务器 URL 在前，推流密钥在后。

6. 使用拼接后的字符串作为推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image)

#### LinkedIn Live

LinkedIn Live 仅对已获批准的用户开放。要检查你是否符合条件，请了解 [LinkedIn Live](https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other) 的访问标准。

1. 登录 [LinkedIn Live](https://www.linkedin.com/video/golive/now/)。

2. 在页面左上角的 **New stream** 下选择 **Go live now**。

3. 在 **Stream settings** 标签页中，选择你的地区，然后点击 **Get URL**。

4. 将流地址（stream URL）和流密钥（stream key）拼接。确保流地址在前，流密钥在后。

5. 将拼接后的字符串作为推流地址使用。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image)

#### Twitch TV

1. 登录 [Twitch TV](https://www.twitch.tv/)。

2. 点击你的头像，在下拉列表中选择 **Settings**。

3. 点击 **Channel and Videos** 标签。

4. 在左侧导航栏，点击 **Stream** \> **Settings**。

5. 用斜杠（/）将服务器地址（server URL）和流密钥（stream key）拼接。确保服务器地址在前，流密钥在后。Twitch TV 的 RTMP 服务器地址始终为 `rtmp:// live.twitch.tv/app`。

6. 将拼接后的字符串作为推流地址使用。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image)

#### Instagram

1. 启用专业账户。

   1. 登录 [Instagram](https://www.instagram.com/)。

   2. 在左侧导航栏选择 **More** \> **Settings**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image)

   3. 在 **For professionals** 下点击 **Account type and tools**，然后点击 **Switch to professional account**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image)

   4. 根据需要选择 **Creator** 或 **Business**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image)

2. 获取流地址和流密钥。

   1. 在 [Instagram](https://www.instagram.com/accounts/edit/) 左侧导航栏选择 **Create** \> **Live video**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image)

   2. 在弹出的对话框中，为你的直播输入标题并选择观众。本示例中，选择 **Public**。然后点击 **Next**。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image)

   3. 获取流地址和流密钥。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image)

每次 Instagram 直播都会生成新的流密钥。

3. 将流地址和流密钥拼接。确保流地址在前，流密钥在后。

4. 将拼接后的字符串作为推流地址使用。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image)
