---
title: "Pages + Trae Work 实操指南：6 个场景，把你的想法变成可分享的网页"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/pages-trae_zh-cn"
---

这份指南教你在 Trae Work 里，用大白话描述需求，就能生成一个完整网页（报告、小游戏、原型、手册……），再把它部署到公网、拿到一个谁都能打开的分享链接。全程不用懂代码、不用配服务器。

下面 6 个场景都给了**可以直接复制的提示词**（代码块里的内容）。挑一个和你需求接近的，复制提示词、按需改改，就能上手。

<span id="先认识一下-pages"></span>
## 先认识一下 Pages

你在本指南里生成的网页，最终都托管在 **BytePlus Pages** 上。Pages 是 BytePlus 提供的一站式静态站点与 Web 应用托管服务，把代码托管、自动构建、全球 CDN 加速和轻量动态能力整合到一个控制台里。简单说，它帮你把一个网页变成「谁都能用浏览器打开」的线上站点，全程不用自己买服务器、配环境。

它能托管的内容很广，常见的有：


* 静态网站（HTML / CSS / JavaScript）

* 单页应用（SPA）、文档站、博客

* 基于 Git 持续部署的前端项目

* 用模板快速起步的项目


因为站点资源是通过 BytePlus 的全球边缘节点分发的，所以无论你的同事、客户在哪儿打开，加载都很快。

想了解 Pages 的完整能力和控制台操作，可以查阅 [Pages 官方文档](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/host_static_pages_console)。

<span id="pages-和-trae-work-是如何协作的"></span>
## Pages 和 Trae Work 是如何协作的

一句话：\*\*Trae Work 负责「把网页做出来」，Pages 负责「把网页发出去」。\*\*两者在本指南里是配合使用的——你只跟 Trae Work 对话，部署这一步它会自动调用 Pages，你基本不用单独打开 Pages 控制台。

具体到使用上：


* **做页面：**  你在 Trae Work 里用大白话描述需求，它生成完整网页并在预览窗口里给你看效果。

* **发页面：**  满意后，你发一句「部署该页面并获取分享链接」，Trae Work 会通过 `byted-bp-cdn-pagesdeploy` 这个 Skill 把页面打包上传到 Pages，自动完成部署，并把分享链接回给你。

* **想精细管理：**  如果你想查看部署记录、回滚到历史版本、绑定一个稳定的自定义域名，再去 [Pages 控制台](https://console.byteplus.com/cdn/cdn-bp/synthopages/list) 操作即可。日常分享其实用不到这一步。

> 📌 小提示：Trae Work 部署后给你的是一个临时预览地址，便于快速验证，但这个地址会定期重置（约每 3 小时）。要长期对外分享，建议在 Pages 控制台为项目绑定一个自定义域名。


<span id="整个流程就三步"></span>
## 整个流程就三步


|步骤 |你要做的 |
|---|---|
|1. 描述需求 |把想要什么效果，用大白话讲给 Trae Work（如果有素材文件，先作为附件上传给它） |
|2. 等它生成 |Trae Work 自动分析、画图、找图、写内容，几分钟生成一个网页，在预览窗口看效果，不满意就接着聊着改 |
|3. 部署分享 |部署该页面并获取分享链接，复制就能发给任何人 |


>  **⚠️ 全局提醒｜留意 Trae Work 会话的「Waiting」状态**

> 使用过程中请随时关注侧边任务列表里的会话状态。一旦某个会话出现 **Waiting（等待中）**  标记，说明它**需要你介入**才能继续，常见情形：

> * **确认高风险操作**：执行删除、覆盖、拷贝等命令前会弹确认框，需要你点「允许」。

> * **提供凭证**：部署或调用外部服务时，可能需要你提供 AK/SK 或完成授权。

> * **补充信息 / 做选择**：路径含空格、缺少入口文件等情况，会暂停征询你的意见。

> 看到 Waiting 别干等——点开会话按提示处理，任务就会继续往下跑。

> <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/010e19fdcb604240b33abb2437f3dd87~tplv-goo7wpa0wc-topic.png) </span>


<span id="准备工作（只需一次）"></span>
## 准备工作（只需一次）

<span id="第一步：下载安装-trae-work"></span>
### 第一步：下载安装 Trae Work

还没装 Trae Work 的，先到 https://www.trae.cn/ide/download 下载并安装。

<span id="第二步：开通-byteplus-服务"></span>
### 第二步：开通 BytePlus 服务

Pages 是 BytePlus CDN 旗下的一个服务，部署会用到 BytePlus 的 CDN 能力，所以第一次使用前先完成下面两件事：


1. **注册 BytePlus 账号**：访问 [https://console.byteplus.com/auth/signup](https://console.byteplus.com/auth/signup)注册并登录——仅需邮箱即可注册，无需手机号。

2. **创建 AK/SK（Access Key / Secret Key）** ：访问 [https://console.byteplus.com/iam/keymanage](https://console.byteplus.com/iam/keymanage) 创建一组 AK/SK 并妥善保存——部署时会用它来完成授权。


<span id="第三步：安装部署-skill"></span>
### 第三步：安装部署 Skill

在 Trae Work 的**技能市场**里找到 `byted-bp-cdn-pagesdeploy` Skill 并安装。装好之后，每当你要部署页面，它会自动调用，无需手动触发；之后所有项目都能直接用。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/51af7e760c5040eca0fc48b986e97ae8~tplv-goo7wpa0wc-topic.png) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>关于效果截图</strong>：下文每个场景展示的最终网页截图都只是<strong>大致效果示意</strong>。由于页面是大模型每次现场生成的，你自己运行得到的结果在排版、配色、文案等细节上一定会与截图不同——<strong>请以你实际运行的结果为准</strong>。</div>


<span id="场景一：把一堆-csv-变成会讲故事的数据周报"></span>
## 场景一：把一堆 CSV 变成会讲故事的数据周报

**适合谁**：产品运营、增长、数据分析、需要定期向团队汇报的人。

**能做出什么**：把几个枯燥的 CSV，变成一份带交互图表、自带核心结论的在线周报，链接发群里同事手机就能看。

 **▶ 先看效果**：[打开数据周报 Demo](https://p-2e9jg043qh8u9lai.synthopages.bytepluses.com/?_token=20a80ebe7823eab1ab9e9d27c9fccf8c4ff44c632738bbc9adc3544b3c414b37aacf8698b2aeb69dff3e980796a7a99122effca806fbfadaf3a696ae43b1a65f27c10d219ec8f87d2b808acae078d1b536bc2f7b28251cd422e9e9e696f4)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：把你这周的数据 CSV 打包作为附件上传给 Trae Work。

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6aa6d785524e1a511ac832988aa997b4.zip" name="SnapVibe测试数据.zip">SnapVibe测试数据.zip</Attachment>


&nbsp;

**第 2 步**：复制下面这段提示词给 Trae Work，按你的实际情况改改想要的图表。

```Plain Text
这周的用户数据在附件中，一共六个表。帮我做一份本周用户数据周报网页：最上面用几张大卡片放核心指标（日活、新增、留存），下面要有这两周的趋势折线图、转化漏斗图、还有不同用户分层的对比雷达图。风格用深色、专业一点，最好图表能用鼠标点点看看细节。
```


**第 3 步**：几分钟后预览窗口出现深色周报，看效果。不满意就继续说，比如「漏斗图颜色再深一点」「把雷达图换成柱状图」，它会即时改。

**第 4 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ad01b7bc1d2d41ad8559e4ae3cd65d19~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 顶部指标卡，一眼看到大盘走势（如 DAU 环比 +9.6%）

* 趋势折线图，鼠标悬停就能看到每天的精确数值

* 转化漏斗，清晰标出每层流失、最弱环节

* 用户分层雷达图叠加对比

* 底部「核心发现」和「下周行动建议」——结论由 AI 读完数据写好，直接能用

> **想先试试？**  本场景第 1 步已附上测试数据 SnapVibe测试数据.zip，内含 6 份自洽的 CSV（每日指标 / 漏斗 / 用户分层 / AB 实验 / 渠道 / 功能模块），直接下载下来上传给 Trae Work，就能复现本场景。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/050bab81cc414c8682af2ed8a0e1e7ed~tplv-goo7wpa0wc-topic.png) </span>

<span id="场景二：做一份图文并茂的旅行手册"></span>
## 场景二：做一份图文并茂的旅行手册

**适合谁**：要出门玩、又懒得在十几个 App 之间反复比价排行程的人。

**能做出什么**：描述你想去哪、喜欢什么，AI 帮你排好行程、联网配上真实图片和真实地图动线，最后一个链接发给同行的人。

 **▶ 先看效果**：[打开越南会安岘港 4 天 3 晚行程 Demo](https://p-2e9gwucjmdudi52n.synthopages.bytepluses.com/?_token=28706c94c967e4dcd916af7014285590e6f6241a892ccd63db94c2b17563bdc04beaad2b0a758dd209bce0a913f0fbb726de0c64185a11d4678362737cf6069b6a17a84ae225a82f6807223983ebeed07723caa0542949e3a44a91ec6dcc)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：把你的旅行想法（目的地、天数、偏好、预算等）一股脑讲给 Trae Work，先让它出个初步方案。

```Plain Text
设计一个越南会安、岘港 4 天 3 晚的行程。希望：能深度体验当地文化、住得舒服点、最好直飞、每天行程别排太满、计划 6—8 月出行、安排一两顿米其林餐厅。先给我备选出发城市和几家备选酒店。
```


**第 2 步**：从它给的方案里挑定酒店、敲定细节，让它把行程细化到时间轴。比如回一句「就定四季酒店，把每天行程细化到时间轴，精确到小时」。

**第 3 步**：让它升级成完整手册——这一步要**把「我要真实照片、真实地图」一开始就说清楚**，否则默认可能给你示意图或随手贴的网图。

```Plain Text
在这个网页基础上，帮我做成一份完整的旅行手册。图片别用占位图了，上网找些真实的照片换上去，比如酒店、餐厅、景点的实景图。还有每天的地图 —— 我要的是那种能看出真实街道和海岸线的地图，上面按先后顺序标好每天去的地点和走的路线，别用那种随便画几个圈连根直线的示意图。最后再补上四天的详细时间安排和预订提示。
```


**第 4 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dba0820b6fa045f8accb107398f0dbd4~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 每日动线地图：真实地图底图上按顺序标出当天停靠点，机场→酒店→古城关系一目了然

* 逐日时间轴，精确到小时

* 每个景点配真实图片和说明，像一本随手翻的电子手册，没网也能存图看

> **避坑提示**：要地图、要配图时，第一句话就把「我要真实的照片 / 真实的地图」说清楚。至于图片怎么存进网页、部署后会不会丢图，这些技术细节不用你操心，AI 会自动处理好。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3ee683fb8ed4386a92e2d819a578d0b~tplv-goo7wpa0wc-topic.png) </span>

<span id="场景三：做一个让朋友停不下来的冷知识闯关"></span>
## 场景三：做一个让朋友停不下来的冷知识闯关

**适合谁**：想做点好玩东西、给团队团建、给社群涨活跃、或单纯想在群里整个活的人。

**能做出什么**：一句话让 AI 一次性出一大批冷知识题、做成能闯关的网页，发到群里，朋友一个接一个来挑战。

 **▶ 先看效果**：[打开冷知识闯关 Demo](https://p-2e9j1bmf4641yp82.synthopages.bytepluses.com/?_token=470a527c521a6cd19691bf9c00f03fe776d83d0ada7bccf3fab4b95e11ec8175c34a86dd7d5599dd7fba89f0129e93103d42b5d2c1ea1d0990ea32de40d66e823d0b441855d5aef5814bdddbdec35855f7833ab45192a35f2351c8067bed)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：把玩法讲清楚，复制下面这段提示词给 Trae Work。

```Plain Text
帮我做一个网页版的「冷知识闯关」小游戏。先一次性想 200 道有趣的冷知识选择题，每道四个选项，配上正确答案和一句话讲解，都放进这个网页里。玩法是：每关随机抽一道题，答对了进下一关，答错就结束，每答完一题就告诉我对不对、为什么。界面活泼点，要有进度条、连续答对的连击得分，最后结束的时候显示「你超过了百分之多少的人」，再来个「再玩一次」的按钮。
```


**第 2 步**：几分钟后就有一个能玩的网页。AI 在生成阶段就把这 200 道题写进网页里，每次玩都从题库随机抽题、打乱选项，连玩几局也不容易重样。预览里自己先玩一遍。

**第 3 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3af9607e7d80439fad0e577aec21a7d5~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 带进度条、连击得分的闯关界面

* 答对/答错都有即时反馈和一句话讲解

* 结束页显示「你超过了 X% 的人」+「再玩一次」按钮，天然适合群里裂变

> **小贴士**：题目越多越耐玩，想加量直接说「再多来点，出 300 道」，想精简就说「留 50 道精华就行」。换个主题（行业黑话、城市冷知识、电影台词……）让 AI 重新出一批题，同一套玩法就是一个新游戏。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df0be98f6cc4465683afebd69b3aff3c~tplv-goo7wpa0wc-topic.png) </span>

> **下面两个场景围绕同一个产品需求**，看「收藏夹」功能从产品原型到代码评审怎么用 Trae Work。

> **需求背景**：SnapVibe App 要新增「收藏夹」功能——用户可以把喜欢的视频点「收藏」，之后在「我的\-收藏夹」里集中查看、还能新建分组（如「美食」「旅行」）归类。产品经理先出可点击原型，工程师再评审实现代码。


<span id="场景四：产品经理一句话出可点击的原型"></span>
## 场景四：产品经理一句话出可点击的原型

**适合谁**：产品经理、交互设计、任何要把想法快速变成「能点的样子」给人看的人。

**能做出什么**：不用学 Axure、不用等设计排期，把功能讲清楚，几分钟就有一版能点、能演示、能发给别人提意见的高保真原型。

 **▶ 先看效果**：[打开收藏夹高保真原型 Demo](https://p-2e9helwetzhaisgw.synthopages.bytepluses.com?_token=3eeec136420d69f1f8d913ca9d6ec989e56275eab8d01fa03a31ad10cbc18bf03de8c9d17f9f1f02b6660d155b46c9319c464bb42092a9c79fa71db616a2ce27d199235b2337aff69b71f4e3745c01d7e65f3f3e25bf8d2a591ef39a12cc)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：把要哪几个页面、每个页面长什么样、点了会怎样，讲清楚。复制下面这段提示词给 Trae Work。

```Plain Text
帮我做一套手机 App 的「收藏夹」功能高保真原型，做成能点击跳转的网页。要这么几个页面：①视频播放页，右侧有个「收藏」的爱心按钮，点一下变红、弹出「已收藏到默认分组」；②「我的 - 收藏夹」列表页，用网格展示收藏过的视频缩略图，顶部能切换不同分组；③新建分组的弹窗，能输入分组名字、点确定。页面之间的按钮要能真的点击跳转，串成一个能演示的完整流程。整体按主流短视频 App 的风格来，清爽现代一点。
```


**第 2 步**：预览窗口里就是一个能用鼠标点的真原型（点爱心变红、点「我的」跳列表、点「新建分组」弹窗）。不满意接着聊着改，比如「分组的标签选中时加个下划线、颜色重一点」。

**第 3 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b42af6208d4a4cdea8232483403cfd1f~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 一版能真实点击跳转的高保真原型，不是静态截图

* 一个公网链接，谁都能在手机上亲手点着体验，开会前先发，大家带着体验来开会

* 定稿链接还能直接附在需求文档里，给工程师当交付标准


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/856e34e6ac2d414fa85935b0c1237920~tplv-goo7wpa0wc-topic.png) </span>

<span id="场景五：工程师把一份代码评审做得明明白白"></span>
## 场景五：工程师把一份代码评审做得明明白白

**适合谁**：研发工程师、技术 Leader、需要做 Code Review 或给别人讲清楚一段代码的人。

**能做出什么**：把一段不好读的代码，变成一份带高亮、带讲解、问题分级标注的评审网页，发给同事一起看，省掉一场冗长的当面讲解。

 **▶ 先看效果**：[打开收藏夹功能代码评审 Demo](https://p-2e9in3t7n5x1md7n.synthopages.bytepluses.com/?_token=1fa5050559bf6291c2daae3e64eea6993c0a4f23ed7c5a618d4b717be0b678349629aa6760c3c88805836f2f0956af945c426793b5d5a202df80b63ef4e5d437791591f5144b7782fef85651b4516c9146e98ec79e4fd964ae33065613e4)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：把要评审的代码文件作为附件上传给 Trae Work，复制下面这段提示词，把你的评审要求讲清楚。

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_83d09ef38f971000fc240f1555404d12.js" name="favorites_demo.js">favorites_demo.js</Attachment>


```Plain Text
这是同事写的「收藏夹」功能代码（favorites_demo.js），帮我做一份代码评审网页方便大家一起看。要求：
1. 把完整代码贴出来，带行号和语法高亮；
2. 逐段加上中文讲解，说明每块代码在干嘛；
3. 把你发现的问题按严重程度标出来——可能有 bug 的标红、性能或可维护性问题标黄、写得好的地方标绿，每条都写清楚为什么、建议怎么改；
4. 最上面放一个小结：总共几个问题、最该优先改哪个；
5. 对其中影响最大的问题，再给一段「修改前 / 修改后」的对比代码。

排版清爽一点，方便对着屏幕一起过。
```


**第 2 步**：预览窗口里就是一份评审报告网页：带高亮的代码 + 逐段讲解 + 红黄绿分级问题标注 + 顶部小结。需要补充就接着说，比如「把那个同步拉缩略图的性能问题，再给一段修改前后的对比代码」。

**第 3 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92faa94497ee488bb87acf962e797c87~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 带语法高亮、行号的完整代码

* 逐段中文讲解 + 红黄绿三色问题分级（红=可能 bug，黄=性能/可维护性，绿=写得好）

* 顶部问题小结（几个问题、优先改哪个）+ 重点问题的修改前后对比代码

* 一份可存档的评审记录，回头追溯一目了然

> **想先试试？**  本场景第 1 步已附上示例代码 favorites_demo.js（一份「收藏夹」功能代码），直接下载下来上传给 Trae Work，就能复现本场景的代码评审。


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a727de01bdf47ab9b564cfed8f8589b~tplv-goo7wpa0wc-topic.png) </span>

<span id="这份示例代码里预埋了哪些问题"></span>
### 这份示例代码里预埋了哪些问题

为了让你直观看到「红黄绿分级」的效果，`favorites_demo.js` 故意埋了一批典型问题，覆盖三个严重等级。上传给 Trae Work 后，可以对照下表看它是否都识别出来了：


|等级 |所在函数 |问题 |为什么是问题 |
|---|---|---|---|
|🔴 红（可能 bug） |`loadFavorites()` |直接 `JSON.parse(raw)` 读缓存，没有任何异常兜底 |本地缓存一旦损坏或格式非法，parse 会抛异常，导致整个收藏功能崩溃 |
|🔴 红（性能） |`renderFavoriteList()` |在 for 循环里逐个调用 `fetchThumbnailSync()` 同步拉缩略图 |同步请求会阻塞主线程，收藏越多界面卡得越久，是典型的性能与体验杀手 |
|🟡 黄（可维护性 / 健壮性） |`addFavorite()` |判断是否已收藏时全量遍历，且用 `==` 弱比较 |每次新增都全量遍历效率低；`==` 会发生隐式类型转换，埋下难查的判等隐患 |
|🟡 黄（健壮性） |`removeFavorite()` 等 |用 `!=` 弱比较，且未对入参做校验 |同样的弱比较风险；缺少参数校验，传入异常值时行为不可控 |
|🟢 绿（写得好） |`createGroup()` / `showToast()` |职责单一、命名清晰、逻辑直白 |作为「正面示例」，让评审网页也能标出值得保留的好写法 |


> **小贴士**：这招也适合「给自己的代码写讲解」——把一段复杂逻辑做成带讲解的网页发给新同事，比口头讲一遍省事，他还能反复看。


<span id="场景六：做一个能动手拖着玩的小工具"></span>
## 场景六：做一个能动手拖着玩的小工具

**适合谁**：想算笔账、又懒得开 Excel 套公式的人——算房贷月供、估算存款利息、换算卡路里、做个番茄钟，都行。

**能做出什么**：一个能动手拖滑块、填数字的网页小工具，参数一调，结果实时就变。部署成链接后，谁打开都能自己拖着算，不用你每次帮人代算。

 **▶ 先看效果**：[打开卡路里计算器 Demo](https://p-2e9ib1643dnj4mth.synthopages.bytepluses.com?_token=73447f7f29b8db152beca50dd4b07cf761457379263cb64ef2d87bf3cda9230955c31fd5a586dc0ea905dbe7e1e6d346c27d7bcd37f18098ffc5b812fd6af01abaa5f6f0431faeb84e007bf7fcca46164ed9c3edf1183cdfcb5fb3962d48)

<span id="操作步骤"></span>
### 操作步骤

**第 1 步**：复制下面这段提示词，发给 Trae Work 直接开搞。想算别的就照着改改要算的内容。

```Plain Text
帮我做一个卡路里计算器网页。上面放几个可以拖动的滑块：性别、年龄、身高、体重，再选一个每天的活动量（久坐 / 偶尔运动 / 经常运动）。我一边调，下面就实时显示我每天大概需要多少卡路里（基础代谢和总消耗分开列）。如果想减重，再给出一个建议的每日摄入区间。配一张图直观展示。整体做得简洁好看一点，数字要大、看得清，手机上也能正常拖动。
```


**第 2 步**：几分钟后预览窗口出现计算器，拖几下滑块试试。不满意就继续说，比如「再加一个『目标体重』的输入」「把饼图换成柱状图」，它会即时改。

**第 3 步**：复制下面这句提示词发给 Trae Work，它会自动部署页面并给你一个分享链接。

```Plain Text
部署该页面并获取分享链接
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48cbee58974e451b97432516c9aa7ecd~tplv-goo7wpa0wc-topic.png) </span>

<span id="你会得到什么"></span>
### 你会得到什么


* 几个可以直接拖动的滑块，拖到哪、结果就算到哪

* 每日基础代谢、总消耗等关键数字实时更新，数字醒目好读

* 想减重时，给出建议的每日摄入区间

* 手机上也能流畅拖动，链接发给谁，谁就能自己算


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb33fad7aa164fe19abc3d8706dccecb~tplv-goo7wpa0wc-topic.png) </span>

<span id="几点小提示"></span>
## 几点小提示


* **部署出去的是纯静态网页**：所有数据、图片、内容都在生成阶段内嵌进页面里。需要数据分析、联网找图、批量出题这类活，交给 Trae Work 在生成阶段完成即可。

* **技术细节交给它**：像「网页要有个入口页」「图片要打包进网页、不能丢」这类要求，你不用在提示词里特意交代，部署时会自动处理好。你只管把「想要什么效果」「想分享给谁」说清楚。

* **大文件可能部署失败**：网页里塞了特别多高清大图、视频，体积可能过大。遇到这种情况，说一句「帮我把图片压缩一下再部署」即可。

* **预览链接有时效**：部署后会先给一个临时预览地址，便于快速验证；这个地址会定期重置。如果要长期对外分享，建议绑定一个稳定的自定义域名。

* **留意 Waiting 状态**：再次提醒（见文首），会话出现 Waiting 表示需要你介入（确认高风险操作、提供 AK/SK、补充信息），及时处理任务才会继续。
