---
title: "AI 配音"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation-zh-TW"
---

AI 配音功能整合豆包同聲傳譯模型、多語字幕、聲音複製和唇形同步等進階技術。此功能可將直播音訊中的人聲處理為多語內容，有效提升觀眾在嘈雜、靜音或跨語言情境下的觀看體驗，並協助您的內容觸及更廣泛的全球受眾。本主題說明如何透過 BytePlus MediaLive 主控台使用 AI 配音功能。

## 架構

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90b1efb646914de0a42c64fd86b75a19~tplv-goo7wpa0wc-topic.webp)

此架構圖展示推流情境中 AI 配音的整體處理流程，主要包含下列階段：

1. **音訊來源分離**：從直播串流中擷取人聲和背景聲，為後續處理提供乾淨音訊。

2. **語音辨識與翻譯**：使用豆包同聲傳譯模型辨識人聲內容，並產生多語字幕。

3. **聲音複製**：配音音訊會保留原始音色、最佳化音量，並執行降噪。

4. **唇形同步**：即時調整說話者的唇部動作，並與配音音訊同步，達到高度逼真的效果。

5. **音訊融合**：將複製的人聲與背景聲自然混合，以提升整體音訊品質。

6. **音訊和視訊合成**：結合處理後的音訊和字幕，產生最終輸出，達到自然的多語直播效果。

## 亮點

* **沉浸式體驗**：結合聲音複製和唇形同步技術，提供逼真的配音和臉部動作，顯著提升影片自然度。

* **低延遲**：適配直播情境，提供端對端低延遲體驗。

* **彈性使用方式**：根據您的情境選取適合的功能。

   |情境 |建議功能 |模式選擇 |說明 |
   |---|---|---|---|
   |為直播提供基本字幕，方便在靜音或嘈雜環境中觀看。 |原文 ASR 字幕 |**原文 (ASR) 字幕** |使用語音辨識在影片上疊加來源字幕。 |
   |啟用跨語言文字溝通，以觸及全球受眾。 |字幕翻譯 |**AI 配音**或**即時口譯** |使用語音辨識在影片上疊加翻譯字幕，同時保留原聲。 |
   |提供配音式翻譯體驗，類似觀看配音電影。 |配音音訊 |**AI 配音**或**即時口譯** |提供配音音訊並取代原聲。在**即時口譯**模式中，您可以選擇將配音音訊疊加到原聲上，或直接取代原聲。 |
   |提供沉浸式真人口譯員體驗，以提升專業感。 |配音音訊 + 唇形同步 |**AI 配音** |以配音音訊為基礎，AI 技術會將說話者的唇部動作與配音音訊同步，創造高度逼真的效果。 |

## 情境

* **無障礙觀看**

   為聽力障礙人士產生來源字幕，支援在辦公室和圖書館等安靜環境，以及地鐵和商場等嘈雜環境中的無障礙觀看體驗。

* **跨境商務與全球溝通**

   適用於跨境電商直播、產品發表會、國際會議、教育訓練和非母語人士演講等多種情境，促進跨語言溝通與市場拓展。

* **娛樂與體育**

   支援海外賽事轉播和國內賽事國際化，滿足即時串流需求，並促進賽事內容全球發行。

## 計費

僅收取 AI 配音費用。AI 配音依據任務的**實際推流時長**計費。如需更多資訊，請參閱 [AI 配音](https://docs.byteplus.com/docs/byteplus-media-live/ai_dubbing)。

> **警告**

> 您只能免費體驗**示範影片**。其他示範方式會產生相應費用。

## 工作流程

AI 配音的完整工作流程如下。流程涉及兩種類型的位址：

* BytePlus MediaLive 位址：指網域名稱已繫結到您目前帳戶的位址。

* 第三方平台位址：指來自其他雲端服務商或 TikTok 等直播平台的位址。

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSIxMzg1cHgiIGhlaWdodD0iMjQ1cHgiIHZpZXdCb3g9Ii0wLjUgLTAuNSAxMzg1IDI0NSI+PGRlZnMvPjxnPjxyZWN0IHg9IjIiIHk9IjIiIHdpZHRoPSIyNzUiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMzIiIHk9IjYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1bGwgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMTYyIiB3aWR0aD0iMjIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE5MnB4OyBtYXJnaW4tbGVmdDogMzNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5CeXRlUGx1cyBNZWRpYUxpdmUgcHVsbMKgc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIzMiIgeT0iMjIiIHdpZHRoPSIyMjAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIxOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2Pjxmb250IHN0eWxlPSJmb250LXNpemU6MTlweCI+UHVsbCBzdHJlYW0gYWRkcmVzczwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDQyIDEzMiBMIDI4OC4zNyAxMzIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyODMuMTIgMTMyIEwgMjkwLjEyIDEyOC41IEwgMjg4LjM3IDEzMiBMIDI5MC4xMiAxMzUuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNTcyIDEzMiBMIDY1MiAxMzIgTCA2NTIgMTMyLjYgTCA3MTkuNTQgMTMyLjU2IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzI0Ljc5IDEzMi41NiBMIDcxNy43OSAxMzYuMDYgTCA3MTkuNTQgMTMyLjU2IEwgNzE3Ljc5IDEyOS4wNiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQ0MiIgeT0iMTAyIiB3aWR0aD0iMTMwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEyOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEzMnB4OyBtYXJnaW4tbGVmdDogNDQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+VGFzazwvZm9udD48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjMyMiIgeT0iOTIiIHdpZHRoPSI3MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogNjhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDMyM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1bGw8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDEwMjIgMTIyIEwgMTIwNS42MyAxMjIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAxMjEwLjg4IDEyMiBMIDEyMDMuODggMTI1LjUgTCAxMjA1LjYzIDEyMiBMIDEyMDMuODggMTE4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSI3MzIiIHk9IjIiIHdpZHRoPSIyOTAiIGhlaWdodD0iMjQwIiByeD0iMzYiIHJ5PSIzNiIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHJlY3QgeD0iMTIxMiIgeT0iMiIgd2lkdGg9IjE3MCIgaGVpZ2h0PSIyNDAiIHJ4PSIyNS41IiByeT0iMjUuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTIycHg7IG1hcmdpbi1sZWZ0OiAxMjEzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MjBweCI+TGl2ZSBwbGF5ZXI8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iNzIiIHdpZHRoPSIyMjcuNSIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAyMjZweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxMDJweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlRoaXJkLXBhcnR5IHBsYXRmb3JtIHB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMTUyIiB3aWR0aD0iMjI1IiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDIyM3B4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDE4MnB4OyBtYXJnaW4tbGVmdDogNzY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MjBweCI+Qnl0ZVBsdXMgTWVkaWFMaXZlIHB1c2ggc3RyZWFtIGFkZHJlc3M8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI3NjQuNSIgeT0iMjIiIHdpZHRoPSIxOTcuNSIgaGVpZ2h0PSIzMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTk2cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzdweDsgbWFyZ2luLWxlZnQ6IDc2NnB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPlB1c2ggc3RyZWFtIGFkZHJlc3M8L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MTIiIHk9IjkyIiB3aWR0aD0iODAiIGhlaWdodD0iMjAiIGZpbGw9Im5vbmUiIHN0cm9rZT0ibm9uZSIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDc4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMTAycHg7IG1hcmdpbi1sZWZ0OiA2MTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGZvbnQgc3R5bGU9ImZvbnQtc2l6ZToyMHB4Ij5QdXNoPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMTA2MiIgeT0iNzIiIHdpZHRoPSI5MCIgaGVpZ2h0PSIyMCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSJub25lIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogODhweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA4MnB4OyBtYXJnaW4tbGVmdDogMTA2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48Zm9udCBzdHlsZT0iZm9udC1zaXplOjIwcHgiPkxpdmUgc3RyZWFtaW5nPC9mb250PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

1. 拉取來源串流

   任務會根據您提供的拉流位址拉取來源串流，並執行翻譯。

   > **警告**

   > 您可以使用 BytePlus MediaLive 或其他雲端服務商的拉流位址拉取來源串流，但無法使用 TikTok 等部分直播平台的拉流位址拉取來源串流。

2. 推送串流

   任務會將新的翻譯直播串流推送到推流位址。您可以使用 BytePlus MediaLive、其他雲端服務商，或 TikTok 等直播平台的推流位址，推送新的翻譯直播串流。

3. 觀看直播

   觀眾使用播放器拉取並觀看新的翻譯直播串流。

## 前提條件

* **帳戶準備**：您可以存取 BytePlus 帳戶，並已啟用 [BytePlus MediaLive](https://console.byteplus.com/live/main/overview) 服務。如需更多資訊，請參閱[註冊 BytePlus 帳戶](https://docs.byteplus.com/en/byteplus-platform/docs/signing-up-your-account)和[啟用 MediaLive 服務](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started#da5a6a63)。

* **情境準備**：根據您的情境完成相關準備。

   * **情境 1：快速示範體驗**

      若要快速體驗此功能，請確認下列事項：

      * 您的網路連線穩定。

      * 根據您開始直播的方式準備下列內容：

         * **網頁推流**：可正常運作的攝影機和麥克風。

         * **上傳影片**：大小不超過 100 MB 的 MP4 影片檔案。

         * **線上位址**：有效的拉流位址，支援 HLS、FLV 或 RTMP 格式。您可以使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生位址。

   * **情境 2：建立 AI 配音任務**

      若要為實際直播情境建立任務，請完成下列步驟。

      1. 確認推流和拉流的網域名稱已新增到相同網域名稱空間下。如需更多資訊，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

         > **警告**

         > 只有在使用 BytePlus MediaLive 的推流和拉流位址時，才需要此步驟。

      2. 準備**拉流 URL** 和**推流 URL**。

         * **拉流 URL**：用於拉取來源串流，支援 RTMP 或 FLV 格式。

            * 若要使用 BytePlus MediaLive 的拉流位址作為**拉流 URL**，請使用相同的 `AppName` 和 `StreamName`，並使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生一組位址。此組位址包含作為**拉流 URL** 的拉流位址，以及用於推送來源串流的推流位址。

            * 若要使用其他雲端服務商的拉流位址作為**拉流 URL**，請取得有效的拉流位址。

            > **警告**

            > TikTok 等部分直播平台的拉流位址不能作為**拉流 URL**。

         * **推流 URL**：用於推送新的翻譯直播串流，支援 RTMP 格式。

            * 若要使用 BytePlus MediaLive 的推流位址作為**推流 URL**，請使用相同的 `AppName` 和 `StreamName`，並使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生一組位址。此組位址包含作為**推流 URL** 的推流位址，以及用於拉取新直播串流的拉流位址。

            * 若要使用其他雲端服務商或 TikTok 等直播平台的推流位址作為**推流 URL**，請取得有效的推流位址。若要將串流推送到 TikTok 或其他直播平台，請參閱對應官方文件，或聯絡其客服取得推流位址。

      > **注意**

      > 用於推送來源串流的推流位址，以及用於拉取新翻譯直播串流的拉流位址不受通訊協定限制。您可以根據實際需求選取適合的通訊協定。

## 體驗示範

完成下列步驟以體驗 AI 配音效果。如果效果符合預期，您可以建立任務來啟用翻譯直播。如需更多資訊，請參閱[建立 AI 配音任務](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#0946c25d)。

1. 登入 [BytePlus MediaLive 主控台](https://console.byteplus.com/live/main/si_v2)。

2. 在左側導覽列中，按一下 **AI 配音**。

3. 按一下 **AI 配音示範**。

4. 視需要選取下列任一方式開始直播。

   |開始直播的方式 |說明 |
   |---|---|
   |網頁推流 |適用於從本機裝置開始直播的情境，例如攝影機和麥克風。 |
   |上傳影片 |適用於對現有本機影片檔案進行翻譯的情境，例如錄製課程、宣傳影片等。 |
   |線上位址 |適用於從外部直播來源拉取內容並翻譯的情境，例如其他直播平台或 CDN 源站的直播串流。 |
   |示範影片 |適用於快速了解和體驗翻譯。 |

   > **警告**

   > 除**示範影片**外，所有其他用於開始直播的示範方式**均依標準費率計費**。因此，如果只是要體驗效果，建議您使用**示範影片**。

5. 根據所選的開始直播方式設定參數。

   > **注意**

   > 如果您選取**示範影片**方式，無需進一步設定即可直接進入預覽模式。

   |設定項目 |適用的開始直播方式 |說明 |設定詳情 |
   |---|---|---|---|
   |選取模式 |* **網頁推流**<br><br>* **上傳影片**<br><br>* **線上位址** |選取翻譯模式。不同模式提供不同效果和延遲。 |* **字幕 + 配音 + 唇形同步**：翻譯語音、複製聲音音色，並同步唇部動作，以提供沉浸式體驗。<br><br>* **字幕 + 配音**：翻譯語音並複製聲音音色，但不調整唇部動作。<br><br>* **僅字幕**：僅產生並顯示翻譯字幕。 |
   |設定翻譯語言 |* **網頁推流**<br><br>* **上傳影片**<br><br>* **線上位址** |選取來源語言和目標語言。<br><br>> **警告**<br><br><br><br>* > 示範體驗支援的語言少於已建立任務。<br><br><br>* > 來源語言和目標語言必須不同。<br> |* **原文**：選取來源語言。您可以選取**中文**或**英文**。<br><br>* **翻譯為**：選取翻譯目標語言。您可以選取**中文**或**英文**。 |
   |設定攝影機和麥克風 |**網頁推流** |選取音訊和視訊輸入裝置。 |* **攝影機**：從清單中選取要使用的攝影機。<br><br>* **麥克風**：從清單中選取要使用的麥克風。 |
   |上傳本機影片檔案 |**上傳影片** |上傳本機影片檔案。 |選取要上傳的影片。僅支援 MP4 格式，且檔案大小不得超過 100 MB。 |
   |直播串流位址 |**線上位址** |輸入直播串流的播放 URL。 |輸入 HLS、FLV 或 RTMP 格式的有效拉流位址。<br><br>> **注意**<br><br><br>> 位址不能直接包含多位元組字元，例如中文字元。如果需要包含這些字元，必須先對這些字元進行 URL 編碼，再輸入位址。<br> |
   |體驗時長 |* **網頁推流**<br><br>* **上傳影片**<br><br>* **線上位址** |選取體驗時長。 |選取 **10**、**60** 或 **120** 分鐘。任務會在所選時長結束時自動停止。 |

6. 完成設定後，按一下頁面底部的**開始 AI 配音**以開始翻譯。請確保直播內容包含清晰且穩定的人聲音訊。

   * **原文**區域會顯示原始輸入。

   * **輸出**區域會在翻譯完成後自動開始播放。

      播放期間，您可以按一下**暫停**或**播放**圖示，控制**原文**或**輸出**區域的播放。

      您可以隨時按一下頁面底部的**停止\*\*\*\*AI 配音**停止翻譯。

   > **警告**

   > 除**示範影片**外，所有其他用於開始直播的示範方式**均依標準費率收費**。因此，請及時**停止翻譯**，以避免不必要的費用。

## 建立 AI 配音任務

在任務時長內，當您開始推流時，任務會自動拉取直播串流進行翻譯。新的翻譯直播串流接著會推送到指定的推流位址，從而啟用翻譯直播。例如，您可以使用 OBS 開始直播。翻譯後，您可以在 TikTok 上串流翻譯內容。如需更多資訊，請參閱[串流翻譯內容是否有最佳實務？](https://docs.byteplus.com/docs/byteplus-media-live/ai-liveinterpret-simultaneous-audio-and-video-interpretation#e98319a7)。

完成下列步驟以建立任務。

1. 登入 [BytePlus MediaLive 主控台](https://console.byteplus.com/live/main/si_v2)。

2. 在左側導覽列中，按一下 **AI 配音**。

3. 按一下**新增任務**。

4. 在出現的頁面上完成下列設定，然後按一下**建立**。

   |設定項目 |說明 |
   |---|---|
   |標題 |任務標題。長度必須為 1–20 個字元。支援中文、英文大小寫字母、數字 (0–9)、底線 (_) 和連字號 (\-)。<br><br>> **警告**<br><br><br>> 此標題在所有執行中的任務中必須唯一。<br> |
   |轉推時間 |設定任務的開始和結束時間，即任務執行的時長。<br><br><br>* 在此期間，當您開始推流時，任務會自動拉取直播串流進行翻譯，並將新的翻譯直播串流推送到推流位址。<br><br>* 任務結束、來源串流中斷或拉流失敗時，任務會自動停止推送新直播串流。<br><br><br>例如，如果您將轉推時間設定為 3 天，您可以每天直播 2 小時。每次直播都會使用此任務設定進行翻譯，並根據 6 小時（3 天 × 2 小時/天）的實際推流時長計費。<br><br>> **注意**<br><br><br>> 最長轉推時間不得超過 7 天。<br> |
   |拉流 URL |任務拉取來源串流的位址。支援 RTMP 和 FLV 格式。<br><br>> **注意**<br><br><br>> 位址不能直接包含多位元組字元，例如中文字元。如果需要包含這些字元，必須先對這些字元進行 URL 編碼，再輸入位址。<br> |
   |推流 URL |推流位址，支援 RTMP 格式。任務會將新的翻譯直播串流推送到此位址。<br><br>> **注意**<br><br><br><br>* > 位址不能直接包含多位元組字元，例如中文字元。如果需要包含這些字元，必須先對這些字元進行 URL 編碼，再輸入位址。<br><br><br>* > 若要在 TikTok 或其他第三方平台播放新的翻譯直播串流，請確保使用第三方平台的推流位址（例如 TikTok 直播間的推流位址）。如需取得推流位址的資訊，請參閱第三方平台的官方文件，或聯絡其官方客服。<br> |
   |模式 |視需要從下列模式中選取。<br><br><br>* **AI 配音**：字幕、配音音訊和影片完全同步。支援唇形同步功能。適用於會議直播等需要高度同步和沉浸感的情境。此模式會引入一定延遲。<br><br>* **即時口譯**：低延遲，但影片可能無法與字幕和配音音訊同步。適用於活動直播等需要低延遲的情境。<br><br>* **原文 (ASR) 字幕**：僅需要來源字幕。不涉及翻譯。適用於在靜音或嘈雜環境中觀看。 |
   |處理延遲 |翻譯完成所需的延遲時間。<br><br>不同模式的建議值如下：<br><br><br>* **AI 配音**（取值範圍：1–60 秒）<br><br>   * 唇形同步、配音音訊和字幕：20<br><br>   * 配音音訊和字幕：12<br><br>   * 僅字幕：8<br><br>* **即時口譯**（取值範圍：0\-20 秒）：2\-3。使用此延遲時，影片、字幕和配音音訊可以更好地同步。<br><br>* **原文 (ASR) 字幕**（取值範圍：0\-20 秒）<br><br>   * 當**寫入方式**為**整句**時：15<br><br>   * 當**寫入方式**為**直播串流**時：2\-3<br><br><br>> **注意**<br><br><br>> 如果字幕早於影片或原聲出現，請視需要縮短延遲時間，使字幕與影片或原聲對齊；反之亦然。<br> |
   |翻譯語言 / 原始語言 |* 對於 **AI 配音**或**即時口譯**模式：選取來源語言和目標語言。來源語言支援中文和英文。目標語言支援中文、英文、日文、西班牙文、印尼文、葡萄牙文、法文和德文。<br><br>   > **注意**<br>   <br><br>   > 來源語言和目標語言必須不同。<br>   <br><br>* 對於**原文 (ASR) 字幕**模式<br><br>   * 當**寫入方式**為**整句**時：來源語言支援中文、英文、日文、西班牙文、印尼文、葡萄牙文、法文、德文和韓文。<br><br>   * 當**寫入方式**為**直播串流**時：來源語言支援中文和英文。 |
   |寫入 SEI |是否將字幕寫入直播串流中的 SEI 訊息。啟用後，播放器可以從 SEI 訊息接收字幕。<br><br>> **注意**<br><br><br><br>* > 此欄位會在下列任一情況下顯示：<br><br><br>   * > 已選取 **AI 配音**模式。<br><br><br>   * > 已選取**原文 (ASR) 字幕**模式，且**寫入方式**設定為**整句**。<br><br><br>* > MediaLive 將字幕寫入 SEI 訊息時，會使用 `100` 作為 SEI `type` 值。如果您的推流工具或應用程式也會將自訂 SEI 訊息寫入串流，請避免使用相同的 SEI `type` 值。否則，播放器可能會將自訂資料識別為字幕。<br> |
   |唇形同步 |是否啟用唇形同步功能。啟用後，說話者的唇部動作會與配音音訊同步，使直播更具沉浸感。<br><br>> **注意**<br><br><br>> 只有在 **AI 配音**模式中啟用配音音訊功能時，才能啟用此功能。<br> |
   |配音音訊 |是否啟用配音音訊功能。<br><br>> **注意**<br><br><br>> 此功能只能在 **AI 配音**或**即時口譯**模式中啟用。<br><br><br>啟用此功能後，請完成下列設定。<br><br><br>* **聲音設定**：目前僅支援**從來源複製**，即保留原始音色。<br><br>* **降噪**：啟用後，可有效降低配音音訊中的電流聲和環境噪音等背景噪音，提升最終輸出音訊的清晰度。<br><br>   > **警告**<br>   <br><br>   * > 您只能在 **AI 配音**模式中啟用或停用降噪，或在**即時口譯**模式中選取**僅保留翻譯音訊**時啟用或停用降噪。<br>   <br><br>   * > 啟用降噪可能會導致背景聲消失。<br>   <br><br>* **原聲設定**：選取如何處理直播串流的原聲。此設定會決定觀眾聽到混合音訊還是純配音音訊。<br><br>   * **自動疊加原聲翻譯**：在保留原聲的同時疊加配音音訊。常用於體育賽事直播等需要保留現場臨場感的情境。在此情況下，支援調整原聲音量。<br><br>   * **僅保留翻譯音訊**：完全移除原聲，僅輸出配音音訊。適用於不需要聽到原聲的情境。在此情況下，支援調整背景聲（非人聲）音量。<br><br>   > **注意**<br>   <br><br>   > 您只能在**即時口譯**模式中設定原聲。<br>   <br><br>* **音量平衡**：啟用後，系統會自動調整輸出音訊音量，以維持穩定且舒適的音量，有效避免音量突然變化或刺耳爆音，並顯著提升觀眾聆聽體驗。 |
   |字幕 |是否啟用字幕功能。啟用後，字幕會顯示在影片上。<br><br>您可以為來源字幕和翻譯字幕設定顯示行數、字幕順序（來源字幕在上方或下方）、邊距、字型大小、字型等。例如：<br><br><br>* **字幕格式**：設定顯示哪些字幕。<br><br>   * **原文 + 翻譯**：顯示雙語字幕。字幕顯示順序由**字幕排序**決定。<br><br>   * **翻譯**：僅顯示翻譯字幕。<br><br>   * **原文**：僅顯示來源字幕。<br><br>* **字幕行數**：設定每種語言字幕的最大顯示行數。<br><br>   > **注意**<br>   <br><br>   > 顯示雙語字幕時，此設定同時適用於來源字幕和翻譯字幕。例如，如果選取 **2 行**，來源字幕和翻譯字幕都最多各顯示 2 行，因此字幕總共會占用 4 行螢幕空間。<br>   <br><br>   * **1 行**：每種語言的字幕最多顯示一行。內容可能會被截斷。<br><br>   * **2 行**：每種語言的字幕最多顯示兩行。內容可能會被截斷。<br><br>   * **自動**：根據字幕字元總數和每行最大字元數自動換行，確保完整顯示內容。<br><br>* **每行最大字元數**：每行的最大字元數。當**字幕行數**設定為 **1 行**或 **2 行**，且來源字幕或翻譯字幕的字元總數超過顯示範圍時，內容會被截斷。例如，如果翻譯字幕的每行最大字元數為 10，**字幕行數**設定為 **2 行**，且翻譯字幕的字元總數超過 20，則第 20 個字元之後的任何內容都會被截斷。<br><br>   > **注意**<br>   <br><br>   * > 系統會根據您設定的**每行最大字元數**、**左右邊距**、**字型**、**字型\*\*\*\*大小**和螢幕解析度等因素，計算每行可顯示的最大字元數。<br>   <br><br>   * > 每個字元、字母、符號或數字都計為一個字元。<br>   <br><br>* **寫入方式**：來源字幕的顯示模式。<br><br>   * **整句**：字幕會一次顯示一個完整句子。系統會等到一句話結束後，一次性顯示對應該音訊片段的完整字幕。此方式確保上下文完整和閱讀連續性，提供類似觀看電影字幕的體驗。<br><br>   * **直播串流**：字幕會逐字元或逐詞顯示，不會等待句子結束。此方式優先考量即時性，讓觀眾幾乎可與音訊同步看到文字，類似手機語音輸入。<br><br>   > **注意**<br>   <br><br>   > 您只能在**原文 (ASR) 字幕**模式中設定來源字幕的顯示模式。<br>    |
   |詞彙表 |新增專有詞彙和預期翻譯，例如品牌名稱、人名、產品名稱或功能名稱。系統會將詞彙表作為翻譯模型的參考，以提升專有詞彙的翻譯準確度，**但預期翻譯不一定每次都會使用**。如果設定詞彙表後仍持續出現誤譯，請在**校正**中新增可能的誤譯及其正確翻譯，以強制校正翻譯字幕。<br><br>使用 `原文:譯文` 格式，並以英文逗號 (,) 分隔多個項目。例如，`赛事直播:sports live streaming,实时字幕:real-time subtitles`。<br><br>> **警告**<br><br><br><br>* > 您只能在 **AI 配音**或**即時口譯**模式中設定詞彙表，且詞彙表僅適用於**翻譯字幕**。<br><br><br>* > 在每個 `原文:譯文` 項目中，原文和譯文不能包含英文逗號 (,)。<br><br><br>* > **詞彙表**文字方塊中的字元總數不得超過 30,000。<br> |
   |熱詞庫 |新增熱詞，例如產品名稱或熱門詞語，作為語音辨識模型的參考，以提升辨識準確度。**熱詞不一定每次都能準確辨識**。熱詞必須與來源語言相符，並以換行分隔。<br><br>**熱詞庫**文字方塊中的字元總數不得超過 30,000。如果設定熱詞後仍持續出現辨識錯誤，請在**校正**中新增可能的辨識錯誤及其校正形式，以強制校正原文 ASR 字幕。<br><br>> **注意**<br><br><br>> 您只能在**原文 (ASR) 字幕**模式中設定熱詞。<br> |
   |校正 |設定必須強制校正的字幕文字。逐一新增可能的錯誤形式及其校正形式。每個錯誤形式或校正形式的長度必須為 1 到 50 個字元。您最多可以新增 60 個校正項。建議您根據實際結果調整。<br><br>當系統比對到錯誤形式時，會強制將錯誤形式替換為校正形式。<br><br><br>* **原文 (ASR) 字幕**：校正辨識錯誤。例如，如果 **MediaLive** 被錯誤辨識為 **media life**，您可以新增下列校正：media life（**字幕**）\> MediaLive（**校正**）。<br><br>* **翻譯字幕**：校正誤譯。**校正僅修改翻譯字幕，不會修改來源字幕或配音音訊**。例如，如果 **LiveCore** 被誤譯為**核心直播**，您可以新增下列校正：核心直播（**翻譯**）\> LiveCore（**校正**）。<br><br><br>> **警告**<br><br><br>> 校正僅比對文字，不會判斷上下文。只有在設定的文字可明確識別為錯誤時，才使用校正。校正形式不得包含對應的錯誤形式。例如，如果您設定 **stream** \> **live stream**，且字幕已正確顯示 **live stream**，系統仍會將 **stream** 替換為 **live stream**，導致 **live live stream**。<br> |
   |預覽 |根據 UI 提示在線測試字幕效果。<br><br>> **注意**<br><br><br><br>* > 此處選取的來源串流大小僅用於預覽，不會變更來源串流解析度。任務輸出串流的方向會繼承來源串流。<br><br><br>* > 此處上傳的背景圖片在大小、格式或其他屬性上沒有任何限制。<br> |
   |回呼位址 |用於接收回呼訊息的 URL。URL 必須以 `http://` 或 `https://` 開頭，可公開存取，且包含 1–100 個字元。如需 AI 配音回呼訊息的更多資訊，請參閱 [AI 配音](https://docs.byteplus.com/callback-description-1789729986264#ai-dubbing)。 |

5. 在任務的轉推時長內，使用您的推流工具（例如 OBS）開始推流。請確保直播內容包含清晰且穩定的人聲音訊。任務會自動拉取直播串流進行翻譯，並將新的翻譯直播串流推送到推流位址。

6. 如果您將新的翻譯直播串流推送到 TikTok 或其他第三方平台，觀眾可直接在第三方平台觀看直播。

   您也可以使用下列任一方式，透過與推流位址相同 `AppName` 和 `StreamName` 的拉流位址拉取翻譯內容。

   |方式 |情境 |說明 |
   |---|---|---|
   |第三方拉流工具 |沒有 SDK 開發資源。 |在第三方拉流工具中設定拉流位址以播放直播串流。如需更多資訊，請參閱對應官方文件，或諮詢官方客戶支援。 |
   |Web 播放器 SDK |在網頁瀏覽器中觀看直播。 |整合 Web 播放器 SDK，並在您的網站或 Web 應用程式上播放直播串流。如需更多資訊，請參閱[整合 Web 播放器 SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-web-1789729535065)。 |
   |用戶端 SDK |在您自己的行動應用程式中觀看直播。 |整合用戶端 SDK，並在行動應用程式中播放直播串流。如需更多資訊，請參閱：<br><br><br>* iOS：[整合 iOS 播放器 SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-ios-1789729401463)<br><br>* Android：[整合 Android 播放器 SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-android-1789729399773)<br><br>* Flutter：[整合 Flutter 播放器 SDK](https://docs.byteplus.com/docs/byteplus-media-live/integrating-the-player-sdk-for-flutter)<br><br>* React Native：[整合 React Native 播放器 SDK](https://docs.byteplus.com/integrating-the-player-sdk-for-react-native-1789729403158) |
   |BytePlus MediaLive 主控台 |用於開發或測試期間快速預覽和偵錯。 |在主控台的 [Web 拉流頁面](https://console.byteplus.com/live/main/webPullStream/play)輸入拉流位址，以快速驗證播放。如需更多資訊，請參閱[透過主控台拉流](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull)。<br><br>> **注意**<br><br><br>> 僅支援播放 FLV、HLS 和 RTM 串流。<br> |

7. （可選）在任務清單中，按一下**預覽**進入**影片預覽**頁面，並在翻譯完成後檢視影片。

   您可以隨時按一下 **EnabledSubtitle** 或 **CloseSubtitle** 來控制 AI 配音功能。此操作不會中斷推送到推流位址的串流。AI 配音仍會依據實際推流時長計費。

   * **CloseSubtitle**：停用翻譯，以推送未翻譯的原始內容。

   * **EnabledSubtitle**：啟用翻譯，以推送翻譯內容。

      例如，在面向英語人士的直播中，您可以在非英語人士發言時啟用翻譯，並在其發言結束後停用翻譯。

   > **警告**

   * > 每個帳戶最多可同時執行 2 個任務。若要同時執行更多任務，請聯絡[技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。

   * > 任務結束後無法重新啟動。您可以複製任務，以相同設定快速建立新任務，並為新任務設定新的轉推時間。

## 常見問題

### 串流翻譯內容是否有最佳實務？

以下以最常見的情境**使用 OBS 開始直播並將翻譯內容推送到 TikTok** 為例，完整流程如下。

> **注意**

> AI 配音不限制推流方式。您也可以使用手機或其他方式開始直播。此範例使用 OBS 開始直播。

1. 將推流和拉流的網域名稱新增到相同網域名稱空間下。如需更多資訊，請參閱[新增網域名稱](https://docs.byteplus.com/docs/byteplus-media-live/docs-domain)。

2. 使用[位址產生器](https://console.byteplus.com/live/main/locationGenerate)產生供 OBS 推流使用的推流位址。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d68335b38334d1db72b46564d0bd5ab~tplv-goo7wpa0wc-topic.webp)

   * 若要使用 RTMP 通訊協定推流，請取得 **OBS 推流位址**和 **OBS 串流金鑰**。

   * 若要使用 RTMPS 通訊協定推流，請取得 **OBS 推流位址**和 **OBS 串流金鑰**，並將 **OBS 推流位址**中的通訊協定標頭從 `rtmp` 修改為 `rtmps`。

   * 若要使用 SRT 通訊協定推流，請取得 **TS over SRT 位址**或 **RTMP over SRT 位址**。

3. 在 OBS 的**設定**對話方塊中，從**服務**下拉式清單選取**自訂...** ，並在**串流**索引標籤下設定**伺服器**和**串流金鑰**。

   * 若要使用 RTMP 或 RTMPS 通訊協定推流，請完成下列設定。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3858db6f3e7446f1945a8e23794e6182~tplv-goo7wpa0wc-topic.webp)

      * **伺服器**：上一步取得的 **OBS 推流位址**，例如 `rtmp://push.example.com/live/`。

         > **注意**

         > 若要使用 RTMPS 通訊協定推流，請確保 **OBS 推流位址**的通訊協定標頭已變更為 `rtmps`。

      * **串流金鑰**：上一步取得的 **OBS 串流金鑰**，例如 `test?expire=17770****6&sign=84ad24cea1fc6e186****0ceb5315bfb`。

   * 若要使用 SRT 通訊協定推流，請使用上一步取得的 **TS over SRT 位址**或 **RTMP over SRT 位址**作為**伺服器**，並將**串流金鑰**留空。

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5151957f11c04f93a37efbd642e4cc9f~tplv-goo7wpa0wc-topic.webp)

   > **注意**

   > 推流通訊協定沒有限制，但使用 OBS 推流時，目前僅支援 RTMP、RTMPS 和 SRT 通訊協定。

4. 在[位址產生器](https://console.byteplus.com/live/main/locationGenerate)頁面上，使用與步驟 2 中產生的推流位址相同的 `AppName` 和 `StreamName`，產生使用 RTMP 或 FLV 通訊協定的拉流位址。該位址將作為任務的**拉流 URL**。

5. 在 [AI 配音](https://console.byteplus.com/live/main/si_v2)頁面上建立任務。設定任務時請注意下列事項。

   * **拉流 URL**：步驟 4 中產生的拉流位址。

   * **推流 URL**：TikTok 直播間使用 RTMP 通訊協定的有效推流位址。如需取得推流位址的資訊，請參閱 TikTok 官方文件，或聯絡 TikTok 官方客服。

6. 在任務的轉推時長內，使用 OBS 開始推流。請確保直播內容包含清晰且穩定的人聲音訊。接著，任務會自動拉取直播串流進行翻譯，並將新的翻譯直播串流推送到 TikTok 的推流位址。觀眾即可在對應的 TikTok 直播間觀看翻譯內容。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7ca866bb1b9c496ab841151aea729e8e~tplv-goo7wpa0wc-topic.webp)

### 我應該選擇 AI 配音任務，還是字幕設定的 AI 配音模式？

AI 配音任務和字幕設定的 AI 配音模式使用相同的翻譯模型，並提供相同的翻譯結果。請根據您的具體情境選取適合的模式。

* 如果適用下列情境，建議您選擇 AI 配音任務：

   * **事件導向**：需要為單一或少數重要活動進行翻譯，例如產品發表會或國際會議。

   * **需要手動控制**：您想要僅在直播中的特定時段啟用翻譯，例如非母語人士發言時。

   * **需要低延遲**：對於體育賽事等對低延遲要求較高的直播情境，您可以選擇**即時口譯**模式以降低延遲。

* 如果您有大量直播間需要定期且自動啟用翻譯，建議您選擇字幕設定的 AI 配音模式。如需更多資訊，請參閱[管理字幕設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-manage-subtitle-configuration)。

### 我的直播只有字幕但沒有音訊。可以使用 AI 配音功能嗎？

不可以。AI 配音功能僅支援辨識和翻譯人聲內容，無法根據來源字幕進行翻譯。

### 我的直播面向全球受眾。如何為他們提供不同語言的字幕？

您可以建立多個任務，使用相同的**拉流 URL** 拉取來源串流，並為每個任務設定不同的目標語言和**推流 URL**。當觀眾在播放器的語言頻道之間切換時，播放器會拉取不同語言的不同直播串流。

### 我的直播涉及多種語言。例如，主持人說中文，但在直播中唱日文歌曲。這些都能翻譯成英文嗎？

不支援。目前不支援自動偵測直播串流語言。翻譯僅在任務中設定的來源語言和目標語言之間運作。在這種情況下，建議您將來源語言設定為主持人的主要語言，例如中文。在此範例中，只有中文內容會翻譯成英文，而日文歌曲會保持未翻譯。

### 可以調整配音音訊的音量嗎？

不可以。您只能在**即時口譯**模式中，透過**原聲設定**調整原聲音量或背景聲（非人聲）音量。配音音訊的音量可由觀眾調整。

### 執行翻譯時可以同時進行轉碼和其他操作嗎？

可以。翻譯完成後，任務會產生新的直播串流。只要您使用 BytePlus MediaLive 推流位址作為任務的**推流 URL**，就可以對直播串流執行任何常規處理，例如轉碼、錄製等。

以**轉碼**為例。假設推流位址為 `rtmp://push.example.com/live/test`，請依下列方式操作：

1. **新增轉碼設定**：在推流網域名稱 (`push.example.com`) 所屬的**網域名稱空間**下，使用與推流位址相同的 `AppName`（**live**）新增轉碼設定。如需更多資訊，請參閱[管理轉碼設定](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)。

2. **取得轉碼串流位址**：在[位址產生器](https://console.byteplus.com/live/main/locationGenerate)頁面上完成下列設定，以產生轉碼串流位址。

   * **選取網域名稱**：選取拉流網域名稱。此拉流網域名稱必須與您的推流網域名稱 (`push.example.com`) 屬於相同網域名稱空間。

   * **AppName** 和 **StreamName**：輸入與推流位址相同的 `AppName`（**live**）和 `StreamName`（**test**）。

3. **拉流播放**：使用取得的轉碼串流位址拉取轉碼串流，即可播放已翻譯並轉碼的直播內容。

### 為什麼無法播放翻譯直播內容，或播放一小段時間後停止？

來源串流推流不穩定可能會導致播放失敗或播放卡頓等問題。請檢查來源串流的推流狀態。

### 為什麼翻譯不成功？

請確認來源語言與來源串流音訊中的語言相符，且目標語言為觀眾所需的語言。同時，請確保直播內容包含清晰且穩定的人聲音訊。

### 可以匯出字幕檔案嗎？

不可以。BytePlus MediaLive 目前不支援匯出字幕檔案。

### 為什麼我仍然聽得到原聲？

請逐一檢查下列項目：

* **檢查是否已啟用配音音訊功能**：只有在您啟用配音音訊功能後，才會提供配音音訊。否則，僅會輸出原聲。

* **檢查即時口譯模式中的原聲設定**：如果您不想聽到原聲，可以選取**僅保留翻譯音訊**。

* **檢查任務狀態**：在 [AI 配音](https://console.byteplus.com/live/main/si_v2)頁面上，確保任務狀態為**執行中**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1074bb2673bb4e16ab54257253d4a897~tplv-goo7wpa0wc-topic.webp)

* **檢查是否已啟用翻譯**：在 [AI 配音](https://console.byteplus.com/live/main/si_v2)頁面上，按一下**預覽**。在**影片預覽**頁面上，確認已選取 **EnabledSubtitle**。

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e67e46ffaa584c3c844bc0e67952f7f0~tplv-goo7wpa0wc-topic.webp)

### 如果多個任務使用相同推流位址，會發生什麼情況？

建議您為每個任務設定獨立的推流位址，以確保直播內容的穩定性和可預測性。

如果您為不同任務設定相同推流位址，且轉推時間相近，則該推流位址上播放的內容會是最先成功推流任務的翻譯內容。

例如，任務 A 的來源串流是記者會，任務 B 的來源串流是電商直播。兩個任務都使用相同推流位址推送到 TikTok 直播間。如果任務 B 早於任務 A 完成推流，TikTok 直播間會播放電商直播。
