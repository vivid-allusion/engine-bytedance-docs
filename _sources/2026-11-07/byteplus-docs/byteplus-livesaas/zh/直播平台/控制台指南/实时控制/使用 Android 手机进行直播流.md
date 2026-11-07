---
title: "使用 Android 手机进行直播流"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-live-streaming-from-an-android-phone-zh-CN"
---

本主题介绍如何在手机上使用 BytePlus Live 应用，实现随时随地、户外或移动中开播。该应用提供美颜、商品和组件等功能，并支持与观众实时互动。广泛应用于电商直播流和在线课堂等场景。

<span id="prerequisite"></span>
## 前提条件

请确保您的手机 Android 版本为 6.0 或更高。

<span id="download-and-installation"></span>
## 下载与安装

在 Google Play 商店搜索 **BytePlus Live**，下载并安装该应用。BytePlus Live 应用在以下国家或地区可用并受支持：


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


1. 您可以通过以下任意方式登录 BytePlus Live 应用：

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28370f31337749b29e091c36b167b6b6~tplv-goo7wpa0wc-image.image) </span>

   * 通过活动 ID：输入活动 ID 和开播密钥，进入指定直播间。

      登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，获取直播间的活动 ID 和开播密钥。可参考下方截图。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb83748cb7b84bcaa3a3e5c3c28b79c7~tplv-goo7wpa0wc-image.image) </span>

   * 通过二维码：点击应用右上角的扫描图标，然后扫描包含直播流信息的二维码，进入指定直播间。

      登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，获取直播间的二维码。可参考下方截图。

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0765853e9b9d44c7b2afaa594d2888c2~tplv-goo7wpa0wc-image.image) </span>

2. 根据需要完成以下配置，然后点击 **开始直播**，根据配置开播。您也可以点击页面左上角的退出图标，退出当前页面。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be1bf3ccc07647d9bbf7e3874ce8d529~tplv-goo7wpa0wc-image.image) </span>

   
   |功能 |接口行为 |
   |---|---|
   |更改基本信息 |更改直播间的基本信息。<br><br><br>* 点击**Change**更换封面图。<br><br>* 点击编辑图标更改直播间名称。<br><br>* 点击**Basic information**更改以下基本信息：<br><br>* 直播间名称。<br><br>* 直播间描述。你可以选择是否在直播间显示描述。<br><br>* 主播账号头像。你可以上传不超过 2 MB 的 JPG 或 PNG 文件。<br><br>* 主播账号名称。<br><br>* 封面图。你可以上传不超过 2 MB 的 JPG 或 PNG 文件。<br><br>* 品牌标签。此处仅可选择标签。如需添加标签，请前往[BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)添加分类标签。如需了解更多信息，请参见[为直播间添加标签](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tagging-live-streams-zh-CN)。<br><br><br>为使不同观看页语言的观众能够以其对应语言查看直播间名称、直播间描述和主播账号名称，请按照以下步骤操作：<br><br><br>1. 在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，开启**语言**开关，并在直播间的**制作端** \> **基本信息**页面选择所需语言。<br><br>2. 按照指引顺序，在不同语言下编辑直播间名称、直播间描述或主播账号名称，并用竖线（\|）分隔。例如，若在上一步选择了英语和简体中文，编辑直播间名称时请输入`Live room A\\|直播间 A`。观看页语言设置为英语的观众将看到直播间名称为`Live room A`，而观看页语言设置为简体中文的观众将看到直播间名称为`直播间 A`。<br><br>* 在竖屏模式下可查看和更换竖屏封面，在横屏模式下可查看和更换横屏封面。<br><br>* 若需更改账号头像和名称，请确保[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)已开启主播账号功能。如需了解更多信息，请参见[将主播账号关联到直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN)。 |
   |切换前后摄像头 |点击**Flip**切换摄像头。默认设置为前置摄像头。 |
   |使用美颜 |点击**Beauty AR**，使用美颜和滤镜功能。<br><br><br>* 美颜：通过美颜技术让你更具吸引力。<br><br>* 滤镜：可选择多种滤镜，为画面增添风格和氛围。 |
   |管理商品 |轻触**商品**以管理商品。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c39078e905354963b5ed2d6f85a291da~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 此功能仅在竖屏模式下可用。<br><br>* 请确保已在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播间中添加商品卡片菜单。欲了解更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。<br><br>* 若直播间有多个商品卡片菜单，可根据需要轻触菜单名称，对该菜单下的商品进行操作。<br><br>* 可手动添加商品或从商品库添加。每个商品卡片菜单下最多可添加 500 个商品。<br><br>* 手动添加商品：轻触**手动添加**。配置商品信息后，轻触**提交**。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48955b1109ad4b8296e2606b00a29240~tplv-goo7wpa0wc-image.image) </span><br><br>   观众在观看页点击商品后，将跳转至商品链接。<br><br>   上传不超过 2 MB 的 JPG 或 PNG 文件作为商品图片。<br><br><br>为使不同观看页语言的观众能够看到商品名称、现价和原价，并访问其特定语言的商品链接，请按以下步骤操作：<br><br><br>1. 在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)，开启**多语言**开关，并在**Producer** \> **基本信息**页面选择所需语言。<br><br>2. 按照指示顺序，在不同语言中配置商品名称、现价、原价或商品 URL，并用竖线（\|）分隔。例如，如果你在上一步选择了英文和简体中文，在配置商品名称时输入`Product A\\|商品 A`。将观看页语言设置为英文的观众会看到商品名称为`Product A`，而将观看页语言设置为简体中文的观众会看到商品名称为`商品 A`。<br><br>* 从商品库添加商品：点击**Add from library**，可从已在[BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)添加的商品库中添加商品。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/36298e485a454b959d7dda63ac93d907~tplv-goo7wpa0wc-image.image) </span><br><br>* 上架或下架商品：点击**List**或**Unlist**，可在观看页展示或隐藏商品。<br><br>* 搜索商品：点击**Search**，可根据商品名称在所有商品卡片菜单中搜索商品。支持模糊搜索。<br><br>* 根据商品分类筛选商品。<br><br>   仅当在[BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/)配置了商品分类时，该功能可用。更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。<br><br>* 删除商品：可一次删除一个或多个商品。<br><br>* 单次删除一个商品：点击商品右侧的更多（...）图标，然后点击**Delete**。<br><br>* 单次删除多个商品：点击**More**并选择**Batch manage**。选择多个商品并点击**Delete**。<br><br>* 调整顺序：点击**More**并选择**Reorder**。按住并拖动商品以更改其顺序，然后点击**Save**。<br><br>* 编辑商品：点击商品右侧的更多（...）图标，然后点击**Edit**。<br><br>* 置顶商品：点击商品右侧的更多（...）图标，然后点击**Pin**。商品将被置顶到商品卡片菜单，并在观看页以悬浮窗形式展示。你也可以点击**Unpin**取消商品置顶。 |
   |管理组件 |轻触**组件**。在弹出的对话框中，您可以：<br><br><br>* 轻触**上传图片**以上传本地图片。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6173b86aa3d94e4dacc2ff3c5f4220ac~tplv-goo7wpa0wc-image.image) </span><br><br>* 上传不超过 10 MB 的 PNG 或 GIF 格式图片。<br><br>* 在同一设备上添加的组件可在不同直播间间共享。<br><br>* 轻触组件右下角的删除图标以删除该组件。<br><br>* 轻触组件可将其添加到当前页面。<br><br>* 一个组件可多次添加到当前页面。<br><br>* 当前页面最多可添加 10 个 GIF 格式的组件。<br><br>* 添加到当前页面的每个组件都属于一个图层。<br><br><br>轻触当前页面上的组件后，您可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/899f7c2ed93d490993376145f323fbb8~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 轻触组件右上角的删除图标，将其从当前页面删除。<br><br>* 拖动组件右下角的缩放图标或使用双指等比例缩放组件。<br><br>* 拖动以移动组件。<br><br><br>若您使用同一设备再次进入直播间，组件配置可与您离开直播间时保持一致。 |
   |管理图层 |点击**图层**。在弹出的对话框中，你可以：<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df179fa35f584c8383ae6d93ea0c2e67~tplv-goo7wpa0wc-image.image) </span><br><br><br>* 按住并拖动图层，或点击图层上的**上移**或**下移**，调整图层顺序。若组件之间发生重叠，上层的组件会遮挡下层的组件。<br><br>* 点击**隐藏**或**显示**，隐藏或显示图层。该图层上的组件也将在当前页面上被隐藏或显示。<br><br>* 轻触**删除**以删除图层。该图层上的组件也将从当前页面中被删除。<br><br>* 轻触**清除组件**以删除当前页面上的所有组件。<br><br>* 最多支持 20 个图层。<br><br>* 若您使用同一设备再次进入直播间，图层配置可与您离开直播间时保持一致。 |
   |切换横屏和竖屏模式 |点击**横屏**或**竖屏**以切换横屏和竖屏模式。默认设置为竖屏模式。 |
   |选择直播视频分辨率 |点击**分辨率**以修改直播视频的分辨率。供参考，默认设置为720p。 |
   |清屏 |双击屏幕以清屏，当前页面除组件外的所有内容将被隐藏。<br><br>撤销此操作，可点击撤销图标或再次双击屏幕。<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/545b67f198434ef199ca9904a8455008~tplv-goo7wpa0wc-image.image) </span> |
   

3. 在直播流过程中，您可以执行以下操作。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb9976db396f4308b925864fc8d0ed98~tplv-goo7wpa0wc-image.image) </span>

   
   |编号 |功能 |接口行为 |
   |---|---|---|
   |1 |直播间信息 |你可以执行以下操作：<br><br><br>* 若已开启主播账号功能，可查看账号头像和名称。关于如何开启该功能的更多信息，请参见[将主播账号关联到直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN)。<br><br>* 实时查看在线人数。<br><br>* 若已开启直播流结束时间功能，可查看直播流结束倒计时。关于如何开启该功能的更多信息，请参见[自动结束直播流](https://docs.byteplus.com/docs/byteplus-livesaas/automatically-ending-a-live-stream-zh-CN)。<br><br>* 点击右上角的结束图标，结束直播流。<br><br>* 查看直播间热度。<br><br>* 查看当前网络类型。<br><br>* 查看本次直播流的时长。 |
   |2 |聊天区域 |阅读并发送评论。<br><br>为确保不同观看页语言的观众能够以其对应语言看到主播的评论，请按照以下步骤操作：<br><br><br>1. 登录[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。<br><br>2. 在直播间列表中，点击打开一个直播间。<br><br>3. 在左侧导航栏，点击**Producer** \> **基本信息**。打开**Languages**开关，并选择所需语言。<br><br>4. 在左侧导航栏，点击**Producer** \> **菜单**。在聊天互动菜单下，打开**评论翻译**开关。观看页聊天区域中的评论将自动翻译为对应语言。<br><br>5. 为提升主播评论在不同语言下的准确性，主播可按照指示顺序在聊天区域编辑不同语言的评论，并用竖线（\|）分隔。例如，若在第3步选择了英语和简体中文，主播在聊天区域发送`Hello\\|你好`，则观看页语言为英语的观众将在聊天区域看到`Hello`，而观看页语言为简体中文的观众将在聊天区域看到`你好`。 |
   |3 |商品 |点击商品图标，管理商品。更多信息，请参见第 3 步。<br><br><br>* 此功能仅在竖屏模式下可用。<br><br>* 请确保在[BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)的直播间中添加了商品卡片菜单。更多信息，请参见[管理商品卡片](https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN)。 |
   |4 |设置 |点击右下角的设置图标，然后：<br><br><br>* 选择 **翻转**，切换前后摄像头。<br><br>* 选择 **美颜**，使用美颜和滤镜功能。<br><br>* 美颜：通过美颜技术让您更具吸引力。<br><br>* 滤镜：可选择多种滤镜，为画面增添风格和氛围。<br><br>* 选择 **组件**，管理组件。更多信息，请参见第 2 步。<br><br>* 选择 **图层**，管理图层。更多信息，请参见第 2 步。<br><br>* 选择 **闪光灯**，开启手机闪光灯功能。<br><br>* 选择 **静音**，将麦克风静音，使观众无法听到您的声音。<br><br>* 选择 **镜像**，将直播流画面进行水平翻转。<br><br>* 选择 **清屏**，隐藏除组件外的所有元素，便于专注于内容。<br><br>   您也可以双击屏幕进行清屏操作。<br><br>   如需撤销此操作，可点击撤销图标或再次双击屏幕。<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4c94753b1de493eb863576b317c5e4e~tplv-goo7wpa0wc-image.image) </span><br><br>* 选择 **清除评论**，清除直播间内的评论。 |
