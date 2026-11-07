---
title: "通过 OBS 虚拟摄像头在 TikTok 直播"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/Going_live_on_TikTok_via_Digital_Human_and_OBS-zh-CN"
---

要将你的BytePlus AI形象推流到TikTok，本指南提供了使用OBS Studio和TikTok Live Studio的完整设置流程。你将学习如何配置所有必需的软件，在应用之间传递音频和视频信号，并排查常见问题，以确保直播顺利进行。

## 系统要求

在开始之前，请确保你的电脑满足系统要求，并安装下方列出的必需软件。

* **内存：** 至少16 GB（低于此配置可能导致流卡顿或崩溃）

* **显卡：** GTX 1080 / RTX 2070 / RTX 3060或更高

* **处理器：** Intel i9、Intel i7\-9700K或AMD Ryzen 5 3600X及以上

## 前置条件

* 拥有BytePlus账号，或具备**营销工具包** \> **编辑**权限的IAM用户。如需了解如何添加IAM用户，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。

* 拥有在TikTok上开启直播的权限。如需了解更多信息，请参见[谁可以在TikTok使用LIVE](https://www.tiktok.com/support/faq_detail?id=7543604790438451768&category=web_account#2)。

* 你已下载以下软件：

|**软件名称** |**下载链接** |**用途** |
|---|---|---|
|Google Chrome |[下载 Google Chrome](https://www.google.com/chrome/) |BytePlus AI 数字人平台所需。仅支持 Chrome。 |
|OBS Studio |[下载 OBS Studio](https://obsproject.com/download)（使用默认选项安装） |视频采集与推流软件。 |
|VB\-Audio Virtual Cable |请联系销售获取下载链接 |虚拟音频设备，用于将 OBS 音频路由到 TikTok。 |
|TikTok Live Studio |[下载 TikTok Live Studio](https://www.tiktok.com/studio/download) |TikTok 官方推流助手。 |

## 操作步骤

### Step 1: 配置Google Chrome浏览器

1. 在你的电脑上打开**Google Chrome**。

2. 点击浏览器窗口顶部的地址栏，并准确粘贴以下URL：

```Plain
chrome://settings/content/popups
```

3. 在键盘上按下**Enter**键。

4. 启用“网站可以发送弹窗并使用重定向”。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15fa2a981c43491d8ec1d9d8598f587c~tplv-goo7wpa0wc-image.image)

### Step 2: 配置VB\-Audio Virtual Cable

1. 联系销售获取VB\-Audio Virtual Cable的下载链接。

2. 解压ZIP文件。

3. 在VB\-Cable文件夹内，右键点击`VBCABLE_Setup_x64.exe`，选择“以管理员身份运行”。

4. 安装程序打开后，点击**Install Driver**按钮。如存在旧版本，先点击“Remove Driver”，然后重新安装。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a683c1ad239b44a1afc7c75a21d3e316~tplv-goo7wpa0wc-image.image)

### **Step 3: 配置声音设置**

1. 按下**Win + I**打开**Windows 设置**。

2. 进入**系统** \> **声音**。

3. 在**输入**下，将**CABLE Output (VB\-Audio Virtual Cable)** 设置为默认输入设备。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image)

4. 如有需要，点击**所有声音设备**查看完整设备列表，并确认两个虚拟音频线设备均可用：

   * **CABLE Input**应显示在**输出设备**下

   * **CABLE Output**应显示在**输入设备**下

5. 禁用你不打算使用的录音设备，使虚拟音频线成为活动输入路径。

### **步骤 4：** 开启 AI 直播

参考 [启动 AI Live](https://docs.byteplus.com/docs/byteplus-livesaas/start-a-digital-human-livestream-zh-CN) 完成开播流程，并确保流成功启动。当流处于直播状态时，屏幕上会显示视频预告。

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/621856507af14628a00986a367b92c3c~tplv-goo7wpa0wc-image.image)

### **Step 5: 获取拉流地址**

1. 在顶部导航栏，点击**直播平台**按钮。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6b082de70e24ddc8aa86c4726e151de~tplv-goo7wpa0wc-image.image)

2. 在**直播平台**对话框中，选择**TikTok** 作为直播平台，并选择**虚拟摄像头**作为推流方式。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56b641374be9477ead9cbde9d6097879~tplv-goo7wpa0wc-image.image)

3. 如图所示，在你的 TikTok 应用中获取 ID。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a0e3fc1adba4f5fb470be530312ebb4~tplv-goo7wpa0wc-image.image)

4. 点击**复制**按钮。地址以“rtmp://pull\-rtmp\-...”开头。

### **Step 6:**  通过媒体源将流拉入OBS

1. 打开OBS Studio。

2. 在**源**面板，点击\*\*+**按钮并选择**媒体\*\*。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0fb4b58c328b41ef95646c2bdf7ec532~tplv-goo7wpa0wc-image.image)

3. 在**创建/选择源**对话框中，确认名称并点击**确定**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61355af960bb4352b8d8c1203b86fa04~tplv-goo7wpa0wc-image.image)

4. 在\*\*“媒体”属性**对话框中，取消勾选“本地文件”，将第5步获取的直播流URL粘贴到输入框，设置**输入格式**为flv，然后点击**确定\*\*。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/237cf3914e2045d78e42bcd8328382fa~tplv-goo7wpa0wc-image.image)

### Step 7: 将OBS音频路由到虚拟麦克风

1. 在OBS中，点击音频混音器面板右下角的齿轮图标，打开音频属性对话框。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9a038fa968a4dbf94ce4f51553e58bc~tplv-goo7wpa0wc-image.image)

2. 在 **Media** Source 行，将音频监听设置为“**Monitor and Output**”。这样可以将流的音频路由到 VB\-Cable 虚拟麦克风，以便 TikTok Live Studio 能够捕获音频。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b6107940fa304cc4ab9b5bb35ccc7bc0~tplv-goo7wpa0wc-image.image)

3. 然后在OBS中点击**Start Virtual Camera**，在**Controls**面板启用虚拟摄像头。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5466bb9d7b1e41c68cf793061baf9f65~tplv-goo7wpa0wc-image.image)

### Step 8: 在TikTok Live Studio中添加摄像头并开始直播

1. 打开TikTok LIVE Studio。

2. 在Sources面板中，点击**Add Source**。

3. 在**Add Source**对话框中，选择**Camera**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4fa84fc27d94c5c9bcf4193f386c84b~tplv-goo7wpa0wc-image.image)

4. 在**Camera**下拉菜单中，选择**OBS Virtual Camera**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29f01a49481b41ffac345d2747025c46~tplv-goo7wpa0wc-image.image)

5. 确认预告显示你的OBS场景。如果图像倒置，点击**Rotate**或**Flip**进行调整。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24e186f9e96d4c508e39180ca237b51a~tplv-goo7wpa0wc-image.image)

6. 点击底部工具栏的音频混音器图标，然后点击\*\*+ Add\*\*。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3a436b5a3274a1cb12acd9461a8e595~tplv-goo7wpa0wc-image.image)

7. 选择**CABLE Output (VB\-Audio Virtual Cable)** ，然后点击**Add**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c1cb4dc32038413f9fd90f9568e8158f~tplv-goo7wpa0wc-image.image)

8. 静音其他麦克风。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image)

9. 确认你能看到流的视频，并且麦克风电平指示器在移动。当一切正常时，点击右下角的**Start Live**。

## 故障排查

音频问题是此设置中最常见的问题。以下是用户最常报告的症状，以及每种情况的具体解决方法。

### 流中出现回声（观众听到你的音频重复）

**可能原因：**

* OBS音频监听在一个同时被麦克风采集的源上设置为“Monitor and Output”（如桌面扬声器和麦克风）。

* 桌面音频和Media Source都被发送到虚拟音频线，因此TikTok会捕获同一声音两次。

* Windows的“Listen to this device”在CABLE Output上已开启，导致音频回流到扬声器。

**解决方法：**

* 在OBS → 高级音频属性中：只有Media Source（BytePlus拉流）应设置为“Monitor and Output”。将其他所有源——桌面音频、Mic/Aux、浏览器源等——设置为“Monitor Off”。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image)

* 如果不需要分享电脑声音，请在OBS混音器中静音桌面音频。

* 打开Windows声音 → 录音 → CABLE Output → 属性 → 监听标签页，取消勾选“Listen to this device”。

* 测试时请使用耳机而非扬声器——扬声器输出被物理麦克风拾取是回声的常见来源。

### 双重音频输入（音频被重复）

**可能原因：**

* 你的物理麦克风和VB\-Cable虚拟麦克风都作为输入在TikTok LIVE Studio中已开启。

* OBS同时将音频发送到虚拟音频线和TikTok的直接采集（桌面音频监听）。

* 在 OBS 中意外添加了两个 Media Source，均拉取了同一个 BytePlus 流。

* VB\-Cable被安装了两次，生成了CABLE\-A和CABLE\-B，音频被同时路由到两者。

**解决方法：**

* 在TikTok LIVE Studio音频设置中，只设置一个主麦克风——CABLE Output (VB\-Audio Virtual Cable)。在下拉菜单中禁用其他麦克风。

* 在Windows声音 → 录音中，右键点击所有非CABLE Output的输入并选择禁用。只保留CABLE Output已开启。

* 在 OBS 中，检查 Sources 列表，确保 BytePlus 拉流只存在一个 Media Source。删除所有重复项。

* 在 OBS 音频混音器中，静音 Mic/Aux，除非你确实需要将自己的声音叠加到数字主播上。

* 在 Windows 中打开“程序和功能”；如果 VB\-Audio Virtual Cable 出现两次，请卸载两项，重启电脑，然后仅重新安装一次。

### 没有音频传输到 TikTok LIVE Studio

* 确认 OBS 正在播放 Media Source（你应能看到该行的绿色 VU 表在跳动）。

* 在 OBS → 高级音频属性中，将 Media Source 行设置为“Monitor and Output”（不要仅选“Monitor Off”或“Monitor Only”）。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e520771d8754e33a649d5a3f3dcc976~tplv-goo7wpa0wc-image.image)

* 在 Windows 声音 → 播放中，确保 CABLE Input（VB\-Audio Virtual Cable）已开启。如果未开启，OBS 无法将音频路由到该设备。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2eb0ed44a0f94955a3a97258cef953f7~tplv-goo7wpa0wc-image.image)

* 在 TikTok LIVE Studio 中，确认主麦克风为 CABLE Output，并点击**Test** 以查看音量表是否有反应。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0cbd2c8c73f14b2e82ddde59739a71e4~tplv-goo7wpa0wc-image.image)

* 更改音频路由后请重启 OBS——部分更改仅在重新启动后生效。

### 音频出现爆音、机械音或失真

* 在 Windows 声音 → 录制 → CABLE Output → 属性 → 高级中，将采样率设置为 48 000 Hz，16 位（DVD 质量）。

* 在 Windows 声音 → 播放 → CABLE Input → 属性 → 高级中，设置为相同的采样率（48 000 Hz，16 位）。虚拟音频线两端的采样率必须一致。

* 在 OBS → 设置 → 音频中，将采样率设置为 48 kHz，声道设置为立体声。

* 若 CPU 负载较高，请降低 OBS 输出分辨率或视频码率，以释放 CPU 资源用于音频处理。

### 推流卡顿、冻结或掉线

* 确认内存 ≥ 16 GB，且未运行其他大型应用（如游戏、多标签浏览器、视频编辑器）。

* 在 OBS → 设置 → 输出中，将视频码率降低至 4 000–6 000 kbps，并将编码器设置为 NVENC（NVIDIA）或 QuickSync（Intel），不要使用 x264。

* 请使用有线以太网连接，不要使用 Wi\-Fi。

* 如果 Media Source 卡死，在 OBS 中右键点击该源 → 重启，或直接移除并用相同 flv URL 重新添加该源。
