---
title: "将 BytePlus Live 的直播流同步到第三方平台"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-synchronizing-a-live-stream-from-byteplus-live-to-third-party-platforms-zh-CN"
---

您可以使用多平台推流功能，将 BytePlus Live 的直播流同步到第三方平台，使观众能够在不同平台同时观看同一直播流，扩展您的直播内容的覆盖范围。

<span id="prerequisite"></span>
## 前提条件


* 需要拥有 BytePlus 账号或具备 **营销工具包** \> **编辑**权限的 IAM 用户。如需了解如何添加 IAM 用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-managing-iam-users-and-roles)。

* 同步直播流时，您必须拥有目标平台的开播权限。


<span id="procedure"></span>
## 操作步骤


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在直播间列表中，点击打开一个直播间。

3. 在左侧导航栏，点击 **营销工具包** \> **多平台推流**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f6f1411fec524fed9624f4d489f54cb5~tplv-goo7wpa0wc-image.image) </span>

4. 您可以添加第三方平台或获取该直播间的拉流地址。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">如果直播间有多个直播源，只有第一个直播源的直播流可以同步到已添加的第三方平台。关于多个直播源的更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-setting-multi-source-live-streaming">管理直播源</a>。如需同步其他直播源的直播流，请联系销售代表进行自定义设置。如果您没有销售代表，请点击<a href="https://www.byteplus.com/en/contact">此处</a>填写此表单，我们的销售团队会与您联系。   </div>
   

   * 添加第三方平台：点击 **添加平台**。在 **添加平台**对话框中，选择您要同步直播流的平台。然后，输入平台名称和推流地址。**推流**开关默认已开启。关于如何获取推流地址的更多信息，请参见下一节。

      启用**推流**开关后，直播活动开始时，流会自动同步到该平台，观众可同时在 BytePlus Live 和第三方平台观看。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/032aa5707a0c4a1cbe5163059bee305a~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">仅支持 RTMP 格式的推流地址。      </div>
      

   * 获取拉流地址：点击**获取拉流地址**，然后复制弹出对话框中的地址。您可以在第三方平台使用该地址，将该直播间的直播流同步到平台。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c4672bbd0f94f018254c6526b42a7cf~tplv-goo7wpa0wc-image.image) </span>

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">每个直播间仅有一个拉流地址。      </div>
      

5. 使用除预录视频外的播出方式开播。

6. （可选）添加第三方平台后，您可以执行以下操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2df6c1cbf4c4d91a0b2c178330dfd63~tplv-goo7wpa0wc-image.image) </span>

   * 查看推流状态。

   * 编辑或删除平台信息。

   * 开启或关闭**推流**开关，以同步或停止同步直播流到指定平台。


<span id="how-to-synchronize-a-live-stream-to-major-live-streaming-platforms"></span>
## 如何将直播流同步到主流直播平台

本节介绍如何在以下主流直播平台获取服务器 URL 和流密钥：TikTok、YouTube Live、MetaLive（Facebook）、LinkedIn Live、Twitch 和 Instagram。

由于平台政策变动，以下平台获取推流地址的方法及开播要求可能会发生变化。请参考各平台的最新要求。

<span id="tiktok"></span>
### TikTok

以下步骤说明如何在 TikTok 查找您的服务器 URL 和流密钥，并将其添加到 BytePlus Live 控制台。


1. 在 TikTok 查找并复制服务器 URL 和流密钥。

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">每次在 TikTok 开播时，您都必须复制服务器 URL 和流密钥。   </div>
   

   
   <Tabs>
   <Tab zoneid="crtXC8YkGQ" title="TikTok 应用">
   <TabTitle>TikTok 应用</TabTitle>
   
   在 TikTok 应用中查找并复制服务器 URL 和流密钥。
   
   
      1. 打开您的 TikTok 应用。
   
      2. 进入底部导航栏，点击加号“ **+** ”按钮。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f75eece96c4641228a643f1cd42f32c8~tplv-goo7wpa0wc-image.image) </span>
   
      3. 选择**在 PC/Mac 上投屏**选项，然后点击**Go LIVE**。
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">如果未显示此选项，您的账户没有开播权限。更多信息，请参见<a href="https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2">谁可以在 TikTok 使用 LIVE</a>。      </div>
         
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46afb30216844bde9f52f0791d2ed725~tplv-goo7wpa0wc-image.image) </span>
   
         随后即可看到服务器 URL 和流密钥。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e09dd69817149a0a826d34c55b31e2d~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   <Tab zoneid="v6PO3GIq6v" title="TikTok LIVE Center">
   <TabTitle>TikTok LIVE Center</TabTitle>
   
   在 TikTok LIVE Center 查找并复制服务器 URL 和流密钥。
   
   
      1. 进入[TikTok LIVE Center](https://livecenter.tiktok.com/producer)。
   
      2. 在左侧导航栏，点击**Go LIVE**。
   
         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
         
   
         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">如果未显示此选项，您的账户没有开播权限。更多信息，请参见<a href="https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2">谁可以在 TikTok 使用 LIVE</a>。      </div>
         
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43e2a98aa8e040b985d5f3fe581f3569~tplv-goo7wpa0wc-image.image) </span>
   
      3. 输入您的流详情，并根据需要上传 LIVE 封面。
   
      4. 点击**Save & Go LIVE**。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16680a4d7a344d429a78a4db60fa45df~tplv-goo7wpa0wc-image.image) </span>
   
         此操作尚未开始您的直播流。此操作会生成您的服务器 URL 和流密钥，您需要将其添加到 BytePlus 以启动您的流。服务器 URL 和流密钥将保持有效 5 分钟，因此您需在该时间内完成下一部分操作。
   
         <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/127823a7435147b9ba289b32d03c8e41~tplv-goo7wpa0wc-image.image) </span>
   
   
   </Tab>
   </Tabs>
   

2. 使用斜杠（/）连接服务器 URL 和流密钥。确保服务器 URL 在前，流密钥在后。

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">请确保服务器 URL 和流密钥之间仅有一个<code>/</code>。例如，最终推流 URL 应如下所示：<code>rtmps:// push-rtmp-xxx-xxxx.tiktokcdn.com:4x3/game/stream-21367xxxxxx9830?amun=true&c=PH&dsnp=1&expire=1776409004&l_region=Singapore-Central&rtcRoomId=762702085xxxxx77522&rtcStreamId=stream-213678483xxxxxx0984_rtc&rtcStreamToken=eyJhbGxxxx-ya0&rtcToken=0015dadxxxxxZs%3D&rtcUserId=7627xxxxxx23443222_8928xxx1812_0&sign=bcxxx4&th_region=sg</code>。   </div>
   

3. 在 BytePlus Live 控制台的**添加平台**对话框中，将连接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a28dd17f142344008e47081117852f4b~tplv-goo7wpa0wc-image.image) </span>


<span id="youtube-live"></span>
### YouTube Live


1. 登录[YouTube Live](https://www.youtube.com/)。

2. 在页面右上角，点击**创建**图标并选择**直播**。

   如果这是你首次启用直播流功能，最多可能需要24小时才能获得直播流访问权限。

3. 在**流设置**标签页，拼接流URL和流密钥。确保流URL在前，流密钥在后。

4. 在BytePlus Live控制台的**添加平台**对话框中，将拼接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d6887d8038a4d8c868cc4f1b6318c14~tplv-goo7wpa0wc-image.image) </span>


<span id="metalive"></span>
### MetaLive


1. 登录[Facebook](https://www.facebook.com/live/create)。

2. 在**直播**部分点击**直播**。

3. 选择**流媒体软件**作为视频源。

4. 若需让流密钥永久有效，请打开**持久流密钥**开关。否则，直播流结束后流密钥将无法再次使用。

5. 用斜杠（/）拼接服务器URL和流密钥。确保服务器URL在前，流密钥在后。

6. 在BytePlus Live控制台的**添加平台**对话框中，将拼接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/269d663243664680b93e050dd2e0f107~tplv-goo7wpa0wc-image.image) </span>


<span id="linkedin-live"></span>
### LinkedIn Live

LinkedIn Live仅对已获批准的用户开放。如需检查是否符合条件，请了解[LinkedIn Live](https://www.linkedin.com/help/linkedin/answer/a568503?src=li-other&veh=www.linkedin.com%7Cli-other)的访问标准。


1. 登录[LinkedIn Live](https://www.linkedin.com/video/golive/now/)。

2. 在页面左上角的**新流**下选择**立即直播**。

3. 在**流设置**标签页，选择你的地区，然后点击**获取URL**。

4. 拼接流URL和流密钥。确保流URL在前，流密钥在后。

5. 在BytePlus Live控制台的**添加平台**对话框中，将拼接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b20f3fd0857c41bcab188dbaa97d19d3~tplv-goo7wpa0wc-image.image) </span>


<span id="twitch-tv"></span>
### Twitch TV


1. 登录[Twitch TV](https://www.twitch.tv/)。

2. 点击你的头像，在下拉列表中选择**设置**。

3. 点击**频道和视频**标签页。

4. 在左侧导航栏点击**流** \> **设置**。

5. 用斜杠（/）拼接服务器URL和流密钥。确保服务器URL在前，流密钥在后。Twitch TV的RTMP服务器URL始终为`rtmp:// live.twitch.tv/app`。

6. 在BytePlus Live控制台的**添加平台**对话框中，将拼接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9b9fcd551f7f49a5af90766164057405~tplv-goo7wpa0wc-image.image) </span>


<span id="instagram"></span>
### Instagram


1. 启用专业账户。

   1. 登录[Instagram](https://www.instagram.com/)。

   2. 在左侧导航栏选择**更多** \> **设置**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/01cef1bc62f846f3867c45d8ebebf1ba~tplv-goo7wpa0wc-image.image) </span>

   3. 在**专业人士专用**下点击**账户类型和工具**，然后点击**切换为专业账户**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/359470824d7d4ac687621d41c153aaf1~tplv-goo7wpa0wc-image.image) </span>

   4. 根据需要选择**创作者**或**企业**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11dff9b0ecb64d0d9305c96c79ae75fa~tplv-goo7wpa0wc-image.image) </span>

2. 获取流URL和流密钥。

   1. 在[Instagram](https://www.instagram.com/accounts/edit/)左侧导航栏选择**创建** \> **直播视频**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c8e825007124527b08baa146c13eb3f~tplv-goo7wpa0wc-image.image) </span>

   2. 在弹出的对话框中，为你的直播视频输入标题并选择你的观众。本示例请选择**公开**。然后点击**下一步**。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9a18338b3834fc4b647dfa561bd9f7e~tplv-goo7wpa0wc-image.image) </span>

   3. 获取流URL和流密钥。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7eed50beb29d4b078372e9de3bdff193~tplv-goo7wpa0wc-image.image) </span>

      每次Instagram直播流都会生成新的流密钥。

3. 拼接流URL和流密钥。确保流URL在前，流密钥在后。

4. 在BytePlus Live控制台的**添加平台**对话框中，将拼接后的字符串作为推流地址输入。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24b3336dd7854c32b15237ed71fefeb5~tplv-goo7wpa0wc-image.image) </span>
