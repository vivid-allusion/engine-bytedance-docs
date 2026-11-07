---
title: "从 iOS 手机进行直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-live-streaming-from-an-ios-phone-zh-CN"
---

要随时随地从你的 iOS 手机开播，可以使用 BytePlus Live 应用。本指南将带你完整了解整个流程，包括登录、设置直播间，以及使用美颜、商品和小组件等互动功能。你将学习如何针对电商、在线课堂等场景管理你的直播流，实现与观众的实时互动。

<span id="prerequisites"></span>
## 前提条件


* 请确保你的手机 iOS 版本为 12.0 或更高。

* 通过邮箱登录应用时，请确保你拥有以下权限的 IAM 用户，或是 BytePlus 账户的 root 用户。关于如何添加 IAM 用户的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

   * **Live control** \> **Edit** 权限：开播所需权限。

   * **Producer** \> **Edit** 权限：更换封面图或直播间名称所需权限。


<span id="download-and-installation"></span>
## 下载与安装

在 App Store 搜索 **BytePlus Live**，下载并安装应用。BytePlus Live 应用在以下国家或地区可用：


* 中国香港

* 中国台湾

* 中国澳门

* 日本

* 韩国

* 印度尼西亚

* 新加坡

* 马来西亚

* 菲律宾

* 泰国

* 越南

* 阿拉伯联合酋长国

* 科威特

* 沙特阿拉伯

* 土耳其

* 卡塔尔


<span id="procedure"></span>
## 操作流程


1. 你可以通过以下任意方式登录 BytePlus Live 应用：

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0694699de85c4e1e8971639c62847115~tplv-goo7wpa0wc-image.image) </span>

   * **ActivityID 登录**：输入活动 ID 和 start key，加入指定直播间。登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，获取直播间的活动 ID 和 start key。可参考下方截图。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb83748cb7b84bcaa3a3e5c3c28b79c7~tplv-goo7wpa0wc-image.image) </span>

   * **账号登录**：输入 IAM 用户的邮箱和密码，以及创建该 IAM 用户的 BytePlus 账户的 root 用户的邮箱和密码。

   * **扫码登录**：点击应用右上角的扫描图标，然后扫描包含直播流信息的二维码，进入指定直播间。

      登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，获取直播间的二维码。可参考下方截图。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a9196456b7ad4df49f201c5a0786886f~tplv-goo7wpa0wc-image.image) </span>

2. 创建直播间或进入已有直播间。

   如需创建直播间，请按以下步骤操作。

   1. 点击页面底部的 + 图标。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3317d242e1c4ad792b0562b3b8f3921~tplv-goo7wpa0wc-image.image) </span>

   2. 配置直播间名称和直播流时间，并选择是否在直播结束后自动将回放发布到观看页。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3de712c5465421888200a5fdd369449~tplv-goo7wpa0wc-image.image) </span>

   3. 点击 **Create**。

   * 通过活动 ID 或二维码登录后，将直接进入已有直播间。

   * 使用 IAM 用户登录时，只能查看可见范围内的直播间。关于如何配置可见范围的更多信息，请参见 [管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

3. 根据需要完成以下配置，然后点击 **Start live**，根据配置开播。你也可以点击页面左上角的退出图标，退出当前页面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4edd9ce17c78426ab852b705e359ba1c~tplv-goo7wpa0wc-image.image) </span>

   
   |功能 |接口行为 |
   |---|---|
   |更改基本信息 |更改直播间的基本信息。<br><br><br>* 点击**更换**以更换封面图。<br><br>* 点击编辑图标以更改直播间名称。<br><br>* 点击**基本信息**以更改以下基本信息：<br><br>* 直播间名称。<br><br>* 直播间描述。你可以选择是否在直播间显示描述。<br><br>* 主播账号头像。你可以上传不超过 2 MB 的 JPG 或 PNG 文件。<br><br>* 主播账号名称。<br><br>* 封面图。你可以上传不超过 2 MB 的 JPG 或 PNG 文件。<br><br>* 品牌标签。你只能在此处选择标签。如需添加标签，请前往[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)添加分类标签。更多信息，请参见[为直播间添加标签](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tagging-live-streams-zh-CN)。<br><br><br>为使不同观看页语言的观众能够以其特定语言查看直播间名称、直播间描述和主播账号名称，请按以下步骤操作：<br><br><br>1. 在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，开启**语言**开关，并在直播间的**制作人** \> **基本信息**页面选择所需语言。<br><br>2. 按指示顺序编辑直播间名称、直播间描述或主播账号名称，并用竖线（\|）分隔不同语言。例如，若在上一步选择了英文和简体中文，编辑直播间名称时输入`Live room A\\|直播间 A`。观看页语言设置为英文的观众将看到直播间名称为`Live room A`，而观看页语言设置为简体中文的观众将看到直播间名称为`直播间 A`。<br><br>* 在竖屏模式下可查看和更换竖屏封面图，在横屏模式下可查看和更换横屏封面图。<br><br>* 如需更改账号头像和名称，请确保已在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)启用主播账号功能。更多信息，请参见[将主播账号关联到直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN)。 |
   |切换前后摄像头 |点击**翻转**以切换摄像头。默认设置为前置摄像头。 |
   |使用美颜 |点击**美颜**以使用美颜和滤镜。<br><br><br>* 美颜：使用美颜技术提升你的外观。<br><br>* 滤镜：从多种滤镜中选择，为你的视觉效果增添风格和氛围。 |
   |管理商品 |点击**商品**以管理商品。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd473929c718478887a72e64443711c1~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 此功能仅在竖屏模式下可用。<br><br>* 请确保已在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播间中添加商品卡片菜单。更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。<br><br>* 若直播间有多个商品卡片菜单，点击菜单名称以管理该菜单下的商品。<br><br>* 可手动添加商品或从商品库添加商品。每个商品卡片菜单下最多可添加 500 个商品。<br><br>* 手动添加商品：点击**手动添加**。配置商品信息后，点击**提交**。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48955b1109ad4b8296e2606b00a29240~tplv-goo7wpa0wc-image.image) </span><br><br>   观众在观看页点击商品后，将跳转至商品链接。<br><br>   上传不超过 2 MB 的 JPG 或 PNG 文件作为商品图片。<br><br><br>为使不同观看页语言的观众能够看到商品名称、现价和原价，并访问各自语言的商品链接，请按以下步骤操作：<br><br><br>1. 在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，开启**Languages**开关，并在直播间的**Producer** \> **基本信息**页面选择所需语言。<br><br>2. 按指引顺序配置不同语言的商品名称、现价、原价或商品链接，并用竖线（\|）分隔。例如，若上一步选择了英文和简体中文，配置商品名称时输入`Product A\\|商品 A`。观看页语言为英文的观众将看到商品名称为`Product A`，观看页语言为简体中文的观众将看到商品名称为`商品 A`。<br><br>* 从商品库添加商品：点击**从库添加**，可添加已在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)中添加的商品库商品。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b5599aab720340d299099e911b31d41e~tplv-goo7wpa0wc-image.image) </span><br><br>* 上架或下架商品：点击**上架**或**下架**，在观看页显示或隐藏商品。<br><br>* 搜索商品：点击**搜索**，可根据商品名称在所有商品卡片菜单中搜索商品。支持模糊搜索。<br><br>* 按商品分类筛选商品。<br><br>   仅在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)配置商品分类后可用此功能。更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。<br><br>* 删除商品：可一次删除一个或多个商品。<br><br>* 单次删除一个商品：点击商品右侧的更多（...）图标，然后点击**删除**。<br><br>* 单次删除多个商品：点击**更多**并选择**批量管理**。选择多个商品后点击**删除**。<br><br>* 调整顺序：点击**更多**并选择**重新排序**。长按并拖动商品以更改顺序，然后点击**保存**。<br><br>* 编辑商品：点击商品右侧的更多（...）图标，然后点击**编辑**。<br><br>* 置顶商品：点击商品右侧的更多（...）图标，然后点击**置顶**。该商品将被固定在商品卡片菜单，并在观看页以悬浮窗形式展示。你也可以点击**取消固定**来取消商品的固定。 |
   |管理商品 |点击**组件**。在弹出的对话框中，您可以：<br><br><br>* 点击**上传图片**以上传本地图片。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11c1292af62c4f8b80957f26c5742262~tplv-goo7wpa0wc-image.image) </span><br><br>* 上传 PNG、HEIC 或 GIF 格式且不超过 10 MB 的图片。<br><br>* 同一设备添加的组件可在不同直播间间共享。<br><br>* 点击组件右下角的删除图标以删除该组件。<br><br>* 点击组件以将其添加到当前页面。<br><br>* 一个组件可多次添加到当前页面。<br><br>* 当前页面最多可添加 10 个 GIF 格式的组件。<br><br>* 每个添加到当前页面的组件均属于一个图层。<br><br><br>点击当前页面上的组件后，您可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ed30e1d28544470a0122e2e67b438d0~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 点击组件右上角的删除图标以将其从当前页面删除。<br><br>* 拖动组件右下角的缩放图标或使用双指按比例缩放组件。<br><br>* 拖动以移动组件。<br><br><br>若使用同一设备再次进入直播间，组件配置可与离开直播间时保持一致。 |
   |管理图层 |点击**图层**。在弹出的对话框中，您可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99e1a33a164b4246be9711e1a1c128bf~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 按住并拖动图层，或点击图层上的**上移**或**下移**以调整图层顺序。若组件重叠，位于较高图层的组件会显示在较低图层组件之上。<br><br>* 点击**隐藏**或**显示**以隐藏或显示图层。该图层上的组件也会在当前页面被隐藏或显示。<br><br>* 点击**删除**以删除图层。该图层上的组件也会从当前页面被删除。<br><br>* 点击**清除组件**以删除所有组件。<br><br>* 最多支持 20 个图层。<br><br>* 若使用同一设备再次进入直播间，图层配置可与离开直播间时保持一致。 |
   |切换横屏和竖屏模式 |点击**横屏**或**竖屏**以切换横屏和竖屏模式。默认设置为竖屏模式。 |
   |选择直播视频的分辨率 |点击**分辨率**以修改直播视频的分辨率。供参考，默认设置为 720p。 |
   |清屏 |双击屏幕以清屏，当前页面除组件外的所有内容将被隐藏。<br><br>如需撤销此操作，可点击撤销图标或再次双击屏幕。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1835de52e8f1459bbb6ca1f669937a2a~tplv-goo7wpa0wc-image.image) </span> |
   

4. 直播过程中，你可以执行以下操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4782645545534474a802c23170216201~tplv-goo7wpa0wc-image.image) </span>

   
   |编号 |功能 |接口行为 |
   |---|---|---|
   |1 |直播间信息 |你可以执行以下操作：<br><br><br>* 若主播账号功能已开启，可查看账号头像和名称。关于如何开启该功能的更多信息，请参见[将主播账号关联到直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN)。<br><br>* 实时查看在线人数。<br><br>* 若已开启直播流结束时间功能，可查看直播流结束倒计时。如需了解如何启用该功能，请参见[自动结束直播流](https://docs.byteplus.com/docs/byteplus-livesaas/automatically-ending-a-live-stream-zh-CN)。<br><br>* 点击右上角的结束图标以结束直播流。<br><br>* 查看直播间的人气。<br><br>* 查看当前网络状态。<br><br>* 查看本次直播流的时长。 |
   |2 |聊天区域 |阅读并发送评论。<br><br>为确保不同观看页语言的观众能以其对应语言看到主播的评论，请按以下步骤操作：<br><br><br>1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。<br><br>2. 在直播间列表中，点击打开一个直播间。<br><br>3. 在左侧导航栏，点击**Producer** \> **Basic information**。开启**Languages**开关，并选择所需语言。<br><br>4. 在左侧导航栏，点击**Producer** \> **Menus**。在聊天互动菜单下，开启**Comment translation**开关。观看页聊天区域的评论会自动翻译为对应语言。<br><br>5. 为提升主播评论在不同语言下的准确性，主播可按照指示顺序在聊天区域编辑不同语言的评论，并用竖线（\|）分隔。例如，若在 Step 3 选择了英语和简体中文，主播在聊天区域发送`Hello\\|你好`，则观看页语言设置为英语的观众会在聊天区域看到`Hello`，而观看页语言设置为简体中文的观众会在聊天区域看到`你好`。 |
   |3 |Products |点击商品图标管理商品。更多信息，请参见 Step 3。<br><br><br>* 此功能仅在竖屏模式下可用。<br><br>* 请确保在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播间中添加了商品卡片菜单。更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。 |
   |4 |Settings |点击右下角的设置图标，然后：<br><br><br>* 选择**Flip**，切换前后摄像头。<br><br>* 选择**Beauty AR**，使用美颜和滤镜。<br><br>* 美颜：通过美颜技术提升你的外观。<br><br>* 滤镜：从多种滤镜中选择，为你的画面增添风格和氛围。<br><br>* 选择**Widgets**，管理组件。更多信息，请参见 Step 3。<br><br>* 选择**Layers**，管理图层。更多信息，请参见 Step 3。<br><br>* 选择**Mirror**，将直播流画面水平翻转。<br><br>* 选择**Flash**，激活手机的闪光灯功能。<br><br>* 选择**Mute**，静音麦克风，使观众无法听到你的声音。<br><br>* 选择**Clear screen**，隐藏除组件外的所有内容，便于专注于你的内容。<br><br>   你也可以双击屏幕清除屏幕内容。<br><br>   如需撤销此操作，可点击撤销图标或再次双击屏幕。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/305fe5a96b13480fb6529c71ead99b3f~tplv-goo7wpa0wc-image.image) </span><br><br>* 选择**Clear comments**，清除直播间的评论。 |
   

5. 直播流结束后，你可以查看直播间的以下数据。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95740480cab841ec8669bd9b90f754fd~tplv-goo7wpa0wc-image.image) </span>

   如果你在同一个直播间多次直播，所有场次的数据会被汇总。
