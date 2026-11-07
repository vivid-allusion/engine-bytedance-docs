---
title: "AI 直播分析"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/AI-Live-analysis-zh-CN"
---

AI 直播分析支持对 BytePlus Live 媒体库中已有的视频内容进行智能分段，并为主播和运营提供 AI 优化建议。

<span id="e3ef9248"></span>
## 适用场景

AI 直播分析适用于电商直播等需要复盘直播内容的场景。系统会基于直播语音转写内容进行话题分段，为每个片段展示主题、正文和分析标签，并支持按需生成片段级 AI 分析建议。

通过 AI 直播分析，您可以快速判断不同直播片段的内容表达，沉淀优秀话术，发现需要优化的直播环节，为下一场直播制定更明确的改进方向。

<span id="09cc439f"></span>
## 前提条件


* **开通服务**：AI 分析功能当前为邀测功能。如需开通，请联系 BytePlus Sales。

* 您已拥有 BytePlus 账号，或拥有具备 **Video library** \> **View** 权限的 IAM 用户账号。有关如何添加 IAM 用户的更多信息，请参见[管理用户、组织和角色](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles-zh-CN)。


<span id="7bb6ed7f"></span>
## 注意事项


* AI 直播分析结果由系统基于视频内容和语音转写自动生成，仅供直播运营复盘参考。实际优化策略请结合您的业务目标、主播风格和商品特点综合判断。

* 如果视频缺少有效语音、直播内容异常、语音转写质量较低或相关数据不足，分析结果可能不完整。


<span id="830ec89b"></span>
## 操作步骤

按照以下步骤在 BytePlus Live 中复盘直播视频并生成 AI 分析建议。

<span id="6dd0ef3f"></span>
### 步骤一：进入 AI 直播分析页面


1. 登录 [BytePlus Live 控制台](https://console.byteplus.com/livesaas/liveManagement/)。

2. 在 BytePlus Live 的菜单栏中，点击 **Media library**。

3. 在左侧导航栏中，点击 **Videos** \> **Video library** 或 **Temporary storage**。

4. 在目标视频右侧的 **Actions** 列中点击 **AI analysis**。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/817cdab1ca8646cb94114a0bab59dac2~tplv-goo7wpa0wc-image.image) </span>

   将打开 AI 直播分析页面。

5. 点击“开始生成”以启动分析。视频分析需要一定时间。请耐心等待。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/03e20d7e022e421580a5a078daffa78e~tplv-goo7wpa0wc-image.image) </span>


<span id="10620291"></span>
### 步骤二：分析直播内容

AI 分析页面会展示视频数据和内容分析。您可以参考下方实际场景示例来解读自己的直播内容。

<span id="1b64f9c1"></span>
## 内容分析结果解读

<span id="7d60531f"></span>
### 注意


* AI 分析建议按片段生成。默认不会提前生成建议。您需在目标片段中点击 **AI Analysis** 以获取结果。

* AI 分析建议按片段生成。默认不会提前生成建议，您需要在目标片段中手动单击 **AI Analysis** 后获取结果。


<span id="e3893808"></span>
### 直播指标

在直播指标部分，您可以查看视频的时长、语速和平均句长，以帮助评估主播的语速和内容连贯性。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3be2a858368743c38991687b2142c217~tplv-goo7wpa0wc-image.image) </span>

<span id="75535080"></span>
### **内容分析**

在内容分析模块，您可以：


* 使用页面顶部的页签，根据**时间范围**、**关键词**或**是否已进行 AI 分析**，快速查找感兴趣的直播片段。

* 点击任意片段右侧的 **AI Analysis** 按钮，生成基于 AI 的摘要和优化建议。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ea695a259ba41bc948d58ee754ae3a3~tplv-goo7wpa0wc-image.image) </span>

<span id="c182588c"></span>
### 常见问题

<span id="fb38ceed"></span>
#### 为什么无法看到 AI 直播分析入口？

请确认您的账号已开通 AI 直播分析功能，并且当前账号拥有访问媒体库、直播回放或直播暂存视频的权限。如仍无法看到入口，请联系 BytePlus Live 技术支持。

<span id="43916130"></span>
#### 为什么某个片段没有 AI 分析结果？

片段级 AI 分析默认按需生成。您需要在目标片段中单击**AI Analysis**后，系统才会生成并展示分析建议。

<span id="027b720d"></span>
#### 为什么搜索不到目标内容？

请检查关键词是否与语音转写内容一致。若直播语音不清晰或转写质量较低，可能会影响搜索结果。
