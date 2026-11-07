---
title: "AI 配音"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation-zh-CN"
---

AI 配音功能集成了豆包同传模型、多语言字幕、声音克隆和唇形同步等先进技术。该功能可将直播流音频中的人声处理为多语言内容，有效提升观众在嘈杂、静音或跨语言场景下的观看体验，帮助您的内容触达更广泛的全球受众。本文介绍如何通过 BytePlus MediaLive 控制台使用 AI 配音功能。

## 架构

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b1efb646914de0a42c64fd86b75a19~tplv-goo7wpa0wc-topic.webp)

此架构图展示了推流场景中 AI 配音的整体处理流程，主要包括以下阶段：

1. **音频源分离**：从直播流中提取人声和背景声，为后续处理提供干净的音频。

2. **语音识别和翻译**：使用豆包同传模型识别人声内容并生成多语言字幕。

3. **声音克隆**：配音音频保留原始声音音色，优化音量并进行降噪。

4. **唇形同步**：实时调整说话人的唇部动作，并与配音音频同步，实现高度逼真的效果。

5. **音频融合**：将克隆的人声与背景声自然混合，提升整体音频质量。

6. **音视频合成**：将处理后的音频和字幕合成最终输出，实现自然的多语言直播效果。

## 功能亮点

* **沉浸式体验**：结合声音克隆和唇形同步技术，提供逼真的配音和面部动作，显著提升视频的自然度。

* **低延迟**：适配直播场景，提供端到端低延迟体验。

* **灵活的使用方式**：可根据您的场景选择合适功能。

   |场景 |推荐功能 |模式选择 |描述 |
   |---|---|---|---|
   |为直播流提供基础字幕，便于在静音或嘈杂环境中观看。 |原文 ASR 字幕 |**原文（ASR）字幕** |通过语音识别将源字幕叠加到视频上。 |
   |支持跨语言文本沟通，触达全球受众。 |字幕翻译 |**AI 配音**或**实时传译** |通过语音识别将翻译字幕叠加到视频上，同时保留原声。 |
   |提供配音式翻译体验，类似观看译制片。 |配音音频 |**AI 配音**或**实时传译** |提供配音音频并替换原声。在**实时传译**模式下，您可以选择将配音音频叠加到原声上，或直接替换原声。 |
   |提供沉浸式人工口译员体验，提升专业感。 |配音音频 + 唇形同步 |**AI 配音** |基于配音音频，AI 技术将说话人的唇部动作与配音音频同步，营造高度逼真的效果。 |

## 场景

* **无障碍观看**

   为听障人群生成源字幕，支持在办公室、图书馆等安静环境，以及地铁、商场等嘈杂环境中的无障碍观看体验。

* **跨境业务和全球沟通**

   适用于跨境电商直播、产品发布会、国际会议、教育培训、非母语人士演讲等多种场景，促进跨语言沟通和市场拓展。

* **娱乐和体育**

   支持海外赛事转播和国内赛事国际化，满足实时直播需求，推动赛事内容全球分发。

## 计费

仅收取 AI 配音费用。AI 配音按任务的**实际推流时长**计费。有关更多信息，请参见 [AI 配音](https://docs.byteplus.com/docs/byteplus-media-live/ai_dubbing)。

> **警告**

> 您只能免费体验 **Demo video**。其他演示方式将产生相应费用。

## 工作流

AI 配音的完整工作流如下。涉及两类地址：

* BytePlus MediaLive 地址：指域名已绑定到您当前账号的地址。

* 第三方平台地址：指来自其他云厂商或 TikTok 等直播平台的地址。

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMzg1cHgiIGhlaWdodD0iMjQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMzg1IDI0NSI+PGRlZnMvPjxnPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIyNzUiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIiIHk9IjYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1bGwgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMTYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5CeXRlUGx1cyBNZWRpYUxpdmUgcHVsbMKgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMjIiIHdpZHRoPSIyMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2Pjxmb250IHN0eWxlPSJmb250LXNpemU6MTlweCI+UHVsbCBzdHJlYW0gYWRkcmVzczwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDQyIDEzMiBMIDI4OC4zNyAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyODMuMTIgMTMyIEwgMjkwLjEyIDEyOC41IEwgMjg4LjM3IDEzMiBMIDI5MC4xMiAxMzUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTcyIDEzMiBMIDY1MiAxMzIgTCA2NTIgMTMyLjYgTCA3MTkuNTQgMTMyLjU2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzI0Ljc5IDEzMi41NiBMIDcxNy43OSAxMzYuMDYgTCA3MTkuNTQgMTMyLjU2IEwgNzE3Ljc5IDEyOS4wNiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMTAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+VGFzazwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyMiIgeT0iOTIiIHdpZHRoPSI3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1bGw8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEwMjIgMTIyIEwgMTIwNS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMjEwLjg4IDEyMiBMIDEyMDMuODggMTI1LjUgTCAxMjA1LjYzIDEyMiBMIDEyMDMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI3MzIiIHk9IjIiIHdpZHRoPSIyOTAiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIxMiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyNDAiIHJ4PSIyNS41IiByeT0iMjUuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+TGl2ZSBwbGF5ZXI8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iNzIiIHdpZHRoPSIyMjcuNSIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMjZweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMTUyIiB3aWR0aD0iMjI1IiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyM3B4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogNzY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MjBweCI+Qnl0ZVBsdXMgTWVkaWFMaXZlIHB1c2ggc3RyZWFtIGFkZHJlc3M8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMjIiIHdpZHRoPSIxOTcuNSIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk2cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzdweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MTIiIHk9IjkyIiB3aWR0aD0iODAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAycHg7IG1hcmdpbi1sZWZ0OiA2MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5QdXNoPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTA2MiIgeT0iNzIiIHdpZHRoPSI5MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4MnB4OyBtYXJnaW4tbGVmdDogMTA2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPkxpdmUgc3RyZWFtaW5nPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

1. 拉取源流

   任务会根据您提供的拉流地址拉取源流并进行翻译。

   > **警告**

   > 您可以使用 BytePlus MediaLive 或其他云厂商的拉流地址拉取源流，但不能使用 TikTok 等部分直播平台的拉流地址拉取源流。

2. 推流

   任务将新的已翻译直播流推送到推流地址。您可以使用 BytePlus MediaLive、其他云厂商或 TikTok 等直播平台的推流地址，推送新的已翻译直播流。

3. 观看直播流

   观众使用播放器拉取并观看新的已翻译直播流。

## 前提条件

* **账号准备**：您拥有 BytePlus 账号，并已开通 [BytePlus MediaLive](https://console.byteplus.com/live/main/overview) 服务。有关更多信息，请参见[注册 BytePlus 账号](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)和[开通 MediaLive 服务](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63)。

* **场景准备**：根据您的场景完成相关准备。

   * **场景 1：快速演示体验**

      如需快速体验功能，请确保满足以下条件：

      * 网络连接稳定。

      * 根据您发起直播的方式准备以下内容：

         * **Web 推流**：可正常工作的摄像头和麦克风。

         * **上传视频**：大小不超过 100 MB 的 MP4 视频文件。

         * **在线地址**：有效的拉流地址，支持 HLS、FLV 或 RTMP 格式。您可以使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成该地址。

   * **场景 2：创建 AI 配音任务**

      如需为实际直播场景创建任务，请完成以下步骤。

      1. 确保推流和拉流的域名已添加到同一个域名空间下。有关更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

         > **警告**

         > 仅在使用 BytePlus MediaLive 的推流和拉流地址时需要此步骤。

      2. 准备 **Pull Stream URL** 和 **Push Stream URL**。

         * **Pull Stream URL**：用于拉取源流，支持 RTMP 或 FLV 格式。

            * 如需使用 BytePlus MediaLive 的拉流地址作为 **Pull Stream URL**，请使用相同的 `AppName` 和 `StreamName`，并通过[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成一组地址。该组地址包括作为 **Pull Stream URL** 的拉流地址，以及用于推送源流的推流地址。

            * 如需使用其他云厂商的拉流地址作为 **Pull Stream URL**，请获取有效的拉流地址。

            > **警告**

            > TikTok 等部分直播平台的拉流地址不能用作 **Pull Stream URL**。

         * **Push Stream URL**：用于推送新的已翻译直播流，支持 RTMP 格式。

            * 如需使用 BytePlus MediaLive 的推流地址作为 **Push Stream URL**，请使用相同的 `AppName` 和 `StreamName`，并通过[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成一组地址。该组地址包括作为 **Push Stream URL** 的推流地址，以及用于拉取新直播流的拉流地址。

            * 如需使用其他云厂商或 TikTok 等直播平台的推流地址作为 **Push Stream URL**，请获取有效的推流地址。如需将流推送到 TikTok 或其他直播平台，请参考对应官方文档或联系其客服获取推流地址。

      > **说明**

      > 用于推送源流的推流地址和用于拉取新的已翻译直播流的拉流地址不受协议限制。您可以根据实际需求选择合适协议。

## 体验演示

完成以下步骤体验 AI 配音效果。如果效果符合预期，您可以创建任务以启用翻译直播。有关更多信息，请参见[创建 AI 配音任务](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#0946c25d)。

1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/si_v2)。

2. 在左侧导航栏中，单击 **AI 配音**。

3. 单击 **AI Dubbing Demo**。

4. 根据需要选择以下任一方式发起直播。

   |发起直播方式 |描述 |
   |---|---|
   |Web 推流 |适用于从摄像头和麦克风等本地设备发起直播的场景。 |
   |上传视频 |适用于对已有本地视频文件进行翻译的场景，如录播课程、宣传视频等。 |
   |在线地址 |适用于从外部直播源拉取内容并翻译的场景，如其他直播平台或 CDN 源站的直播流。 |
   |Demo video |适用于快速了解和体验翻译。 |

   > **警告**

   > 除 **Demo video** 外，所有其他发起直播的演示方式**均按标准费率计费**。因此，如仅需体验效果，建议您使用 **Demo video**。

5. 根据所选发起直播方式配置参数。

   > **说明**

   > 如果选择 **Demo video** 方式，无需进一步配置，可直接进入预览模式。

   |配置项 |适用的发起直播方式 |描述 |配置详情 |
   |---|---|---|---|
   |选择模式 |* **Web 推流**<br><br>* **上传视频**<br><br>* **在线地址** |选择翻译模式。不同模式提供不同的效果和延迟。 |* **字幕 + 配音 + 唇形同步**：翻译语音、克隆声音音色，并同步唇部动作，提供沉浸式体验。<br><br>* **字幕 + 配音**：翻译语音并克隆声音音色，但不调整唇部动作。<br><br>* **仅字幕**：仅生成并显示翻译字幕。 |
   |设置翻译语言 |* **Web 推流**<br><br>* **上传视频**<br><br>* **在线地址** |选择源语言和目标语言。<br><br>> **警告**<br><br><br><br>* > 演示体验支持的语言少于创建任务时支持的语言。<br><br><br>* > 源语言和目标语言必须不同。<br> |* **Original**：选择源语言。您可以选择**中文**或**英文**。<br><br>* **Translate as**：选择翻译的目标语言。您可以选择**中文**或**英文**。 |
   |设置摄像头和麦克风 |**Web 推流** |选择音视频输入设备。 |* **Camera**：从列表中选择要使用的摄像头。<br><br>* **Microphone**：从列表中选择要使用的麦克风。 |
   |上传本地视频文件 |**上传视频** |上传本地视频文件。 |选择要上传的视频。仅支持 MP4 格式，且文件大小不能超过 100 MB。 |
   |直播流地址 |**在线地址** |输入直播流的播放 URL。 |输入 HLS、FLV 或 RTMP 格式的有效拉流地址。<br><br>> **说明**<br><br><br>> 地址不能直接包含中文等多字节字符。如需包含这些字符，必须先对这些字符进行 URL 编码，再输入地址。<br> |
   |体验时长 |* **Web 推流**<br><br>* **上传视频**<br><br>* **在线地址** |选择体验时长。 |选择 **10**、**60** 或 **120** 分钟。所选时长结束后，任务将自动停止。 |

6. 完成配置后，单击页面底部的 **Start AI Dubbing** 开始翻译。请确保直播内容包含清晰稳定的人声音频。

   * **Original** 区域显示原始输入。

   * **Output** 区域会在翻译完成后自动开始播放。

      播放过程中，您可以单击**暂停**或**播放**图标，控制 **Original** 或 **Output** 区域的播放。

      您可以随时单击页面底部的 **Stop** **AI Dubbing** 停止翻译。

   > **警告**

   > 除 **Demo video** 外，所有其他发起直播的演示方式均**按标准费率收费**。因此，请及时**停止翻译**，避免产生不必要的费用。

## 创建 AI 配音任务

在任务持续期间，当您开始推流时，任务会自动拉取直播流进行翻译。新的已翻译直播流随后会被推送到指定的推流地址，从而实现翻译直播。例如，您可以使用 OBS 发起直播。翻译后，您可以在 TikTok 上推送翻译内容。有关更多信息，请参见[是否有推送翻译内容的最佳实践？](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#e98319a7)。

完成以下步骤创建任务。

1. 登录 [BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/si_v2)。

2. 在左侧导航栏中，单击 **AI 配音**。

3. 单击 **New Task**。

4. 在出现的页面中，完成以下配置并单击**创建**。

   |配置项 |描述 |
   |---|---|
   |标题 |任务标题。长度必须为 1–20 个字符。支持中文、大小写英文字母、数字（0–9）、下划线（_）和连字符（\-）。<br><br>> **警告**<br><br><br>> 该标题在所有运行中的任务中必须唯一。<br> |
   |转发时间 |设置任务的开始和结束时间，即任务运行的持续时间。<br><br><br>* 在此期间，当您开始推流时，任务会自动拉取直播流进行翻译，并将新的已翻译直播流推送到推流地址。<br><br>* 当任务结束、源流断开或拉流失败时，任务会自动停止推送新直播流。<br><br><br>例如，如果将转发时间设置为 3 天，您可以每天直播 2 小时。每次直播都会使用该任务配置进行翻译，计费将基于实际推流时长 6 小时（3 天 × 2 小时/天）。<br><br>> **说明**<br><br><br>> 最长转发时间不能超过 7 天。<br> |
   |Pull Stream URL |任务拉取源流的地址。支持 RTMP 和 FLV 格式。<br><br>> **说明**<br><br><br>> 地址不能直接包含中文等多字节字符。如需包含这些字符，必须先对这些字符进行 URL 编码，再输入地址。<br> |
   |Push Stream URL |推流地址，支持 RTMP 格式。任务会将新的已翻译直播流推送到该地址。<br><br>> **说明**<br><br><br><br>* > 地址不能直接包含中文等多字节字符。如需包含这些字符，必须先对这些字符进行 URL 编码，再输入地址。<br><br><br>* > 如需在 TikTok 或其他第三方平台播放新的已翻译直播流，请确保使用第三方平台的推流地址（例如 TikTok 直播间的推流地址）。有关如何获取推流地址，请参考第三方平台的官方文档，或联系其官方客服。<br> |
   |模式 |根据需要从以下模式中选择。<br><br><br>* **AI 配音**：字幕、配音音频和视频完全同步。支持唇形同步功能。适用于会议直播等对同步性和沉浸感要求较高的场景。该模式会引入一定延迟。<br><br>* **实时传译**：低延迟，但视频可能无法与字幕和配音音频同步。适用于赛事直播等需要低延迟的场景。<br><br>* **原文（ASR）字幕**：仅需要源字幕。不涉及翻译。适用于静音或嘈杂环境下观看。 |
   |处理延迟 |完成翻译所需的延迟时间。<br><br>不同模式的推荐值如下：<br><br><br>* **AI 配音**（取值范围：1–60 秒）<br><br>   * 唇形同步、配音音频和字幕：20<br><br>   * 配音音频和字幕：12<br><br>   * 仅字幕：8<br><br>* **实时传译**（取值范围：0\-20 秒）：2\-3。使用该延迟时，视频、字幕和配音音频可以更好地同步。<br><br>* **原文（ASR）字幕**（取值范围：0\-20 秒）<br><br>   * 当 **Writing Method** 为 **Whole Sentence** 时：15<br><br>   * 当 **Writing Method** 为 **Live Streaming** 时：2\-3<br><br><br>> **说明**<br><br><br>> 如果字幕早于视频或原声出现，请根据需要降低延迟时间，使字幕与视频或原声对齐；反之亦然。<br> |
   |翻译语言 / 原始语言 |* 对于 **AI 配音**或**实时传译**模式：选择源语言和目标语言。源语言支持中文和英文。目标语言支持中文、英文、日语、西班牙语、印度尼西亚语、葡萄牙语、法语和德语。<br><br>   > **说明**<br>   <br><br>   > 源语言和目标语言必须不同。<br>   <br><br>* 对于**原文（ASR）字幕**模式<br><br>   * 当 **Writing Method** 为 **Whole Sentence** 时：源语言支持中文、英文、日语、西班牙语、印度尼西亚语、葡萄牙语、法语、德语和韩语。<br><br>   * 当 **Writing Method** 为 **Live Streaming** 时：源语言支持中文和英文。 |
   |写入 SEI |是否将字幕写入直播流中的 SEI 消息。启用后，播放器可以从 SEI 消息中接收字幕。<br><br>> **说明**<br><br><br><br>* > 在以下任一情况下会显示该字段：<br><br><br>   * > 已选择 **AI 配音**模式。<br><br><br>   * > 已选择**原文（ASR）字幕**模式，且 **Writing Method** 设置为 **Whole Sentence**。<br><br><br>* > MediaLive 将字幕写入 SEI 消息时使用 `100` 作为 SEI `type` 值。如果您的推流工具或 App 也向流中写入自定义 SEI 消息，请避免使用相同的 SEI `type` 值。否则，播放器可能会将自定义数据识别为字幕。<br> |
   |唇形同步 |是否启用唇形同步功能。启用后，说话人的唇部动作会与配音音频同步，使直播更具沉浸感。<br><br>> **说明**<br><br><br>> 仅当在 **AI 配音**模式下启用配音音频功能时，才能启用该功能。<br> |
   |配音音频 |是否启用配音音频功能。<br><br>> **说明**<br><br><br>> 仅可在 **AI 配音**或**实时传译**模式下启用该功能。<br><br><br>启用该功能后，请完成以下配置。<br><br><br>* **声音设置**：目前仅支持**从源克隆**，即保留原始声音音色。<br><br>* **降噪**：启用后，可有效降低配音音频中的电流噪声、环境噪声等背景噪声，提升最终输出音频的清晰度。<br><br>   > **警告**<br>   <br><br>   * > 仅可在 **AI 配音**模式下，或在**实时传译**模式下选择**仅保留翻译音频**时，启用或禁用降噪。<br>   <br><br>   * > 启用降噪可能导致背景声消失。<br>   <br><br>* **原声配置**：选择如何处理直播流原声，决定观众听到的是混合音频还是纯配音音频。<br><br>   * **原声自动叠加翻译**：保留原声的同时叠加配音音频。常用于体育赛事直播等需要保留现场感的场景。在这种情况下，支持调节原声音量。<br><br>   * **仅保留翻译音频**：完全移除原声，仅输出配音音频。适用于不需要听到原声的场景。在这种情况下，支持调节背景声（非人声）音量。<br><br>   > **说明**<br>   <br><br>   > 仅可在**实时传译**模式下配置原声。<br>   <br><br>* **音量均衡**：启用后，系统会自动调整输出音频音量，保持稳定舒适的音量水平，有效避免音量突变或刺耳爆音，显著提升观众的收听体验。 |
   |字幕 |是否启用字幕功能。启用后，字幕将显示在视频上。<br><br>您可以为源字幕和翻译字幕配置显示行数、字幕顺序（源字幕在上方或下方）、边距、字号、字体等。例如，<br><br><br>* **字幕格式**：设置显示哪些字幕。<br><br>   * **原文 + 翻译**：显示双语字幕。字幕显示顺序由**字幕排序**决定。<br><br>   * **翻译**：仅显示翻译字幕。<br><br>   * **原文**：仅显示源字幕。<br><br>* **字幕行数**：设置每种语言字幕显示的最大行数。<br><br>   > **说明**<br>   <br><br>   > 显示双语字幕时，该配置同时适用于源字幕和翻译字幕。例如，如果选择 **2 行**，则源字幕和翻译字幕各最多显示 2 行，因此字幕总共会占用 4 行屏幕空间。<br>   <br><br>   * **1 行**：每种语言的字幕最多显示一行。内容可能被截断。<br><br>   * **2 行**：每种语言的字幕最多显示两行。内容可能被截断。<br><br>   * **自动**：根据字幕总字符数和每行最大字符数自动换行，确保内容完整显示。<br><br>* **每行最大字符数**：每行最大字符数。当**字幕行数**设置为 **1 行**或 **2 行**，且源字幕或翻译字幕中的总字符数超过显示范围时，内容会被截断。例如，如果翻译字幕的每行最大字符数为 10，**字幕行数**设置为 **2 行**，且翻译字幕总字符数超过 20，则第 20 个字符之后的内容会被截断。<br><br>   > **说明**<br>   <br><br>   * > 系统会根据您配置的**每行最大字符数**、**左右边距**、**字体**、**字号**和屏幕分辨率等因素，计算每行可显示的最大字符数。<br>   <br><br>   * > 每个字符、字母、符号或数字均计为一个字符。<br>   <br><br>* **Writing Method**：源字幕的显示模式。<br><br>   * **Whole Sentence**：字幕将按完整句子逐句显示。系统会等待一句话结束后，一次性显示该音频片段对应的完整字幕。该方式可确保上下文完整和阅读连续性，提供类似观看电影字幕的体验。<br><br>   * **Live Streaming**：字幕逐字或逐词显示，不等待句子结束。该方式优先保障实时性，让观众几乎与音频同步看到文本，类似手机语音输入。<br><br>   > **说明**<br>   <br><br>   > 仅可在**原文（ASR）字幕**模式下配置源字幕的显示模式。<br>    |
   |术语表 |添加专有词汇及其期望译文，如品牌名、人名、产品名或功能名。系统会将术语表作为翻译模型的参考，以提高专有词汇的翻译准确性，**但期望译文不一定每次都会被使用**。如果配置术语表后仍存在误译，请在**纠错**中添加可能的误译及其正确译文，以强制纠正翻译字幕。<br><br>使用格式 `原文:译文`，并用英文逗号（,）分隔多条记录。例如，`赛事直播:sports live streaming,实时字幕:real-time subtitles`。<br><br>> **警告**<br><br><br><br>* > 仅可在 **AI 配音**或**实时传译**模式下配置术语表，且术语表仅适用于**翻译字幕**。<br><br><br>* > 在每条 `原文:译文` 记录中，原文和译文不能包含英文逗号（,）。<br><br><br>* > **术语表**文本框中的总字符数不能超过 30,000。<br> |
   |热词库 |添加热词，如产品名或流行短语，作为语音识别模型的参考，以提高识别准确性。**热词不一定每次都能被准确识别**。热词必须与源语言匹配，并使用换行符分隔。<br><br>**热词库**文本框中的总字符数不能超过 30,000。如果配置热词后仍存在识别错误，请在**纠错**中添加可能的识别错误及其修正形式，以强制纠正原文 ASR 字幕。<br><br>> **说明**<br><br><br>> 仅可在**原文（ASR）字幕**模式下配置热词。<br> |
   |纠错 |配置必须强制纠正的字幕文本。逐条添加可能的错误形式及其修正形式。每个错误形式或修正形式的长度必须为 1 到 50 个字符。最多可添加 60 条纠错。建议您根据实际效果进行调整。<br><br>当系统匹配到错误形式时，会强制将错误形式替换为修正形式。<br><br><br>* **原文（ASR）字幕**：纠正识别错误。例如，如果 **MediaLive** 被错误识别为 **media life**，您可以添加以下纠错：media life（**字幕**）\> MediaLive（**正确**）。<br><br>* **翻译字幕**：纠正误译。**纠错仅修改翻译字幕，不会修改源字幕或配音音频**。例如，如果 **LiveCore** 被误译为**核心直播**，您可以添加以下纠错：核心直播（**翻译**）\> LiveCore（**正确**）。<br><br><br>> **警告**<br><br><br>> 纠错仅匹配文本，不判断上下文。仅当所配置文本可明确识别为错误时，才使用纠错。修正形式不得包含对应的错误形式。例如，如果配置 **stream** \> **live stream**，而字幕已正确显示 **live stream**，系统仍会将 **stream** 替换为 **live stream**，导致出现 **live live stream**。<br> |
   |预览 |根据 UI 提示在线测试字幕效果。<br><br>> **说明**<br><br><br><br>* > 此处选择的源流尺寸仅用于预览，不会改变源流分辨率。任务输出流的方向继承自源流。<br><br><br>* > 此处上传的背景图片在尺寸、格式或其他属性方面没有限制。<br> |
   |回调地址 |用于接收回调消息的 URL。该 URL 必须以 `http://` 或 `https://` 开头，可公网访问，且包含 1–100 个字符。有关 AI 配音回调消息的更多信息，请参见 [AI 配音](https://docs.byteplus.com/callback-description-1789729986264#ai-dubbing)。 |

5. 在任务的转发时长内，使用您的推流工具（如 OBS）开始推流。请确保直播内容包含清晰稳定的人声音频。任务会自动拉取直播流进行翻译，并将新的已翻译直播流推送到推流地址。

6. 如果将新的已翻译直播流推送到 TikTok 或其他第三方平台，观众可以直接在第三方平台观看直播。

   您也可以使用以下任一方式，通过与推流地址具有相同 `AppName` 和 `StreamName` 的拉流地址拉取翻译内容。

   |方法 |场景 |描述 |
   |---|---|---|
   |第三方拉流工具 |没有 SDK 开发资源。 |在第三方拉流工具中配置拉流地址以播放直播流。有关更多信息，请参考对应官方文档或咨询官方客服。 |
   |Web 端 Player SDK |在 Web 浏览器中观看直播流。 |集成 Web 端 Player SDK，并在您的网站或 Web 应用中播放直播流。有关更多信息，请参见[集成 Web 端 Player SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-web-1789729535065)。 |
   |客户端 SDK |在您自己的移动 App 中观看直播流。 |集成客户端 SDK，并在移动 App 中播放直播流。有关更多信息，请参见：<br><br><br>* iOS：[集成 iOS 端 Player SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-ios-1789729401463)<br><br>* Android：[集成 Android 端 Player SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-android-1789729399773)<br><br>* Flutter：[集成 Flutter 端 Player SDK](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* React Native：[集成 React Native 端 Player SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-react-native-1789729403158) |
   |BytePlus MediaLive 控制台 |用于开发或测试期间快速预览和调试。 |在控制台的 [Web 拉流页面](https://console.byteplus.com/live/main/webPullStream/play)输入拉流地址，以快速验证播放。有关更多信息，请参见[通过控制台拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull)。<br><br>> **说明**<br><br><br>> 仅支持播放 FLV、HLS 和 RTM 流。<br> |

7. （可选）在任务列表中，单击**预览**进入**视频预览**页面，并在翻译完成后查看视频。

   您可以随时单击 **EnabledSubtitle** 或 **CloseSubtitle** 控制 AI 配音功能。此操作不会中断推送到推流地址的流。AI 配音仍会按实际推流时长计费。

   * **CloseSubtitle**：禁用翻译，推送未翻译的原始内容。

   * **EnabledSubtitle**：启用翻译，推送已翻译内容。

      例如，在面向英语使用者的直播中，您可以在非英语使用者发言时启用翻译，并在其发言结束后禁用翻译。

   > **警告**

   * > 每个账号下最多可同时运行 2 个任务。如需同时运行更多任务，请联系[技术支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。

   * > 任务结束后无法重启。您可以复制任务，以相同配置快速创建新任务，并为新任务设置新的转发时间。

## 常见问题

### 是否有推送翻译内容的最佳实践？

以最常见的场景**使用 OBS 发起直播并将翻译内容推送到 TikTok** 为例，完整流程如下。

> **说明**

> AI 配音不限制推流方式。您也可以使用手机或其他方式发起直播。此示例使用 OBS 发起直播。

1. 将推流和拉流域名添加到同一个域名空间下。有关更多信息，请参见[添加域名](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

2. 使用[地址生成器](https://console.byteplus.com/live/main/locationGenerate)生成用于 OBS 推流的推流地址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d68335b38334d1db72b46564d0bd5ab~tplv-goo7wpa0wc-topic.webp)

   * 如需使用 RTMP 协议推流，请获取 **OBS 推流地址**和 **OBS Streaming Key**。

   * 如需使用 RTMPS 协议推流，请获取 **OBS 推流地址**和 **OBS Streaming Key**，并将 **OBS 推流地址**中的协议头从 `rtmp` 修改为 `rtmps`。

   * 如需使用 SRT 协议推流，请获取 **TS over SRT 地址**或 **RTMP over SRT 地址**。

3. 在 OBS **Settings** 对话框中，从 **Service** 下拉列表中选择 **Custom...** ，并在 **Stream** 选项卡下配置 **Server** 和 **Stream Key**。

   * 如需使用 RTMP 或 RTMPS 协议推流，请完成以下配置。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3858db6f3e7446f1945a8e23794e6182~tplv-goo7wpa0wc-topic.webp)

      * **Server**：上一步获取的 **OBS 推流地址**，例如 `rtmp://push.example.com/live/`。

         > **说明**

         > 如需使用 RTMPS 协议推流，请确保 **OBS 推流地址**的协议头已更改为 `rtmps`。

      * **Stream Key**：上一步获取的 **OBS Streaming Key**，例如 `test?expire=17770****6&sign=84ad24cea1fc6e186****0ceb5315bfb`。

   * 如需使用 SRT 协议推流，请将上一步获取的 **TS over SRT 地址**或 **RTMP over SRT 地址**用作 **Server**，并将 **Stream Key** 留空。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5151957f11c04f93a37efbd642e4cc9f~tplv-goo7wpa0wc-topic.webp)

   > **说明**

   > 对推流协议没有限制，但使用 OBS 推流时，目前仅支持 RTMP、RTMPS 和 SRT 协议。

4. 在[地址生成器](https://console.byteplus.com/live/main/locationGenerate)页面，使用与步骤 2 中生成的推流地址相同的 `AppName` 和 `StreamName`，生成 RTMP 或 FLV 协议的拉流地址，用作任务的 **Pull Stream URL**。

5. 在 [AI 配音](https://console.byteplus.com/live/main/si_v2)页面创建任务。配置任务时请注意以下内容。

   * **Pull Stream URL**：步骤 4 中生成的拉流地址。

   * **Push Stream URL**：TikTok 直播间中使用 RTMP 协议的有效推流地址。有关如何获取推流地址，请参考 TikTok 官方文档或联系 TikTok 官方客服。

6. 在任务的转发时长内，使用 OBS 开始推流。请确保直播内容包含清晰稳定的人声音频。随后，任务会自动拉取直播流进行翻译，并将新的已翻译直播流推送到 TikTok 的推流地址。观众随后可在对应的 TikTok 直播间观看翻译内容。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ca866bb1b9c496ab841151aea729e8e~tplv-goo7wpa0wc-topic.webp)

### 我应该选择 AI 配音任务，还是字幕配置的 AI 配音模式？

AI 配音任务和字幕配置的 AI 配音模式使用相同的翻译模型，翻译结果一致。请根据您的具体场景选择合适模式。

* 如果适用以下场景，建议您选择 AI 配音任务：

   * **面向活动**：需要为单个或少数重要活动提供翻译，如产品发布会或国际会议。

   * **需要手动控制**：您希望仅在直播中的特定时段启用翻译，例如非母语人士发言时。

   * **需要低延迟**：对于体育赛事等对低延迟要求较高的直播场景，您可以选择**实时传译**模式来降低延迟。

* 如果您有大量直播间需要定期自动启用翻译，建议您选择字幕配置的 AI 配音模式。有关更多信息，请参见[管理字幕配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration)。

### 我的直播流只有字幕，没有音频。可以使用 AI 配音功能吗？

不可以。AI 配音功能仅支持识别和翻译人声内容，无法基于源字幕进行翻译。

### 我的直播流面向全球观众。如何为他们提供不同语言的字幕？

您可以创建多个任务，使用相同的 **Pull Stream URL** 拉取源流，并为每个任务设置不同的目标语言和 **Push Stream URL**。当观众在播放器中切换语言频道时，播放器会拉取不同语言的不同直播流。

### 我的直播流涉及多种语言。例如，主播说中文，但在直播中演唱日语歌曲。所有这些内容都能翻译成英文吗？

不支持。目前不支持自动检测直播流语言。翻译仅在任务中配置的源语言和目标语言之间生效。在这种情况下，建议您将源语言设置为主播的主要语言，如中文。在此示例中，只有中文内容会被翻译成英文，而日语歌曲将保持未翻译。

### 可以调节配音音频的音量吗？

不可以。您只能在**实时传译**模式下通过**原声配置**调节原声音量或背景声（非人声）音量。配音音频的音量可由观众调节。

### 翻译时可以执行转码等其他操作吗？

可以。翻译完成后，任务会生成新的直播流。只要使用 BytePlus MediaLive 推流地址作为任务的 **Push Stream URL**，您就可以对直播流执行任何常规处理，如转码、录制等。

以**转码**为例。假设推流地址为 `rtmp://push.example.com/live/test`，请按以下步骤操作：

1. **添加转码配置**：在推流域名（`push.example.com`）所属的**域名空间**下，使用与推流地址相同的 `AppName`（**live**）添加转码配置。有关更多信息，请参见[管理转码配置](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

2. **获取转码流地址**：在[地址生成器](https://console.byteplus.com/live/main/locationGenerate)页面，完成以下配置以生成转码流地址。

   * **选择域名**：选择拉流域名。该拉流域名必须与您的推流域名（`push.example.com`）属于同一个域名空间。

   * **AppName** 和 **StreamName**：输入与推流地址相同的 `AppName`（**live**）和 `StreamName`（**test**）。

3. **拉流播放**：使用获取到的转码流地址拉取转码流，即可播放已翻译且已转码的直播内容。

### 为什么无法播放已翻译直播内容，或播放一段时间后停止？

源流推流不稳定可能导致播放失败或播放卡顿等问题。请检查源流的推流状态。

### 为什么翻译没有成功？

请确保源语言与源流音频中的语言一致，并确保目标语言是观众所需的语言。同时，请确保直播内容包含清晰稳定的人声音频。

### 可以导出字幕文件吗？

不可以。BytePlus MediaLive 目前不支持导出字幕文件。

### 为什么我仍然能听到原声？

请逐项检查以下内容：

* **检查是否已启用配音音频功能**：只有启用配音音频功能后，才会提供配音音频。否则，只会输出原声。

* **检查实时传译模式下的原声配置**：如果不想听到原声，可以选择**仅保留翻译音频**。

* **检查任务状态**：在 [AI 配音](https://console.byteplus.com/live/main/si_v2)页面，确保任务状态为**运行中**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1074bb2673bb4e16ab54257253d4a897~tplv-goo7wpa0wc-topic.webp)

* **检查是否已启用翻译**：在 [AI 配音](https://console.byteplus.com/live/main/si_v2)页面，单击**预览**。在**视频预览**页面，确保已选择 **EnabledSubtitle**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67e46ffaa584c3c844bc0e67952f7f0~tplv-goo7wpa0wc-topic.webp)

### 如果多个任务使用相同的推流地址，会发生什么？

建议您为每个任务配置单独的推流地址，以确保直播内容的稳定性和可预期性。

如果为转发时间相近的不同任务配置相同的推流地址，则该推流地址播放的内容将是最先成功推流的任务的翻译内容。

例如，任务 A 的源流是新闻发布会，任务 B 的源流是电商直播。两个任务都为 TikTok 直播间使用相同的推流地址。如果任务 B 早于任务 A 完成推流，则 TikTok 直播间将播放电商直播。
