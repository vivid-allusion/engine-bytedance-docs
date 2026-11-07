---
title: "使用 iframe 嵌入 AI Live 控制台"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
section: "繁體中文"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console-zh-TW"
---

若要將 AI Live 控制台功能直接整合至您自己的網站，您可以使用 iframe 嵌入 AI Live 頁面，例如直播間列表與模型訓練頁面。本指南將說明如何構建嵌入連結，讓您能在自己的頁面中無縫提供管理能力，同時降低開發成本。

## 注意

* 此方法僅支援 PC 平台，H5 頁面暫不支援。

* 彈窗僅能在嵌入的功能頁面內置中顯示，無法在您自己的頁面置中顯示。

## 前置條件

* 為確保嵌入頁面可被存取，請確保您的頁面使用 HTTPS 網域。

* 請使用 BytePlus 帳號或具備超級管理員角色的 IAM 使用者來調用[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW)。

## 支援的頁面

目前，您可以使用 iframe 將下列頁面嵌入至您的頁面中。最小寬度為 1000 px，最小高度為 500 px。

|頁面 ||頁面截圖 |範例連結 |
|---|---|---|---|
|AI Live 控制頁面 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4df3dafa05274d24b174cb6066e91d5b~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/185304025******?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|AI Live 直播間列表 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70e5cd96b39246bba2b2e87e431cb7ca~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveRoom&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|模型訓練 |虛擬形象 |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/788ce1a99b11417582561a716cc81a88~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveAvatarTraining&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
||語音 |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afba3dda9fff406ba6f40d20e7dd559f~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveVoiceTraining&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|產品庫 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64e59a2efda549158e822484dff69476~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveProducts&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|素材庫 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f487c4f1b874f5ea1e9478c2bff0962~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveMaterials&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|知識庫 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f62095fd5474bd6bf38002dd2284bae~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveKnowledgeBase&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|服務中心 ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b900cd923349edb83e1b4933fdd766~tplv-goo7wpa0wc-image.image)<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63083c31f2d24c11b0c91b3d0f73c0ee~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveServiceCenter&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br><br><br>> **注意**<br><br><br>> AI Live 的**服務中心**頁面僅限主帳號使用，子帳戶無法存取該頁面。<br> |

## 流程

若要嵌入 AI Live 控制台，請依照以下步驟操作：

1. **新增超級管理員 IAM 使用者**：為 BytePlus Live 建立一個 IAM 使用者，並賦予其超級管理員角色。

2. **取得 AK 與 SK**：取得該 IAM 使用者的 AccessKey（AK）與 SecretKey（SK）。或者，取得 BytePlus 帳號的 AK 與 SK。兩種方式皆可。

3. **調用 GetLoginLivesaasSts 取得臨時憑證**：使用 AK/SK 調用 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW)，取得臨時 AK、SK、工作階段權杖以及 BytePlus Live 權杖。

4. **構建嵌入連結**：使用臨時憑證為目標功能頁面構建嵌入連結。

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSIxODVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSAxODUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZCBhIEJ5dGVQbHVzIExpdmUgSUFNIHVzZXIgd2l0aCB0aGUgc3VwZXIgYWRtaW5pc3RyYXRvcnMgcm9sZTxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzNjIgMzIgTCAzNjIgODIgTCAzOTUuNjMgODEuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggODEuOTYgTCAzOTMuODkgODUuNDcgTCAzOTUuNjMgODEuOTcgTCAzOTMuODggNzguNDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIElBTSB1c2VyPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMTUyIEwgMzYyIDE1MiBMIDM2MiA4NyBMIDM5NS42MyA4NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQwMC44OCA4NyBMIDM5My44OCA5MC41IEwgMzk1LjYzIDg3IEwgMzkzLjg4IDgzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjEyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIEJ5dGVQbHVzIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTcyIDg3IEwgNjQ1LjYzIDg3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjUwLjg4IDg3IEwgNjQzLjg4IDkwLjUgTCA2NDUuNjMgODcgTCA2NDMuODggODMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQwMiIgeT0iNDIiIHdpZHRoPSIxNzAiIGhlaWdodD0iOTAiIHJ4PSIxMy41IiByeT0iMTMuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODdweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbCBHZXRMb2dpbkxpdmVzYWFzU3RzIHRvIGdldCB0aGUgdGVtcG9yYXJ5IEFLLCBTSywgdG9rZW4gcmVxdWlyZWQgd2hlbiB1c2luZyB0ZW1wb3JhcnkgY3JlZGVudGlhbHMsIGFuZCBCeXRlUGx1cyBMaXZlIHRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjYyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiA2NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNvbmNhdGVuYXRlIHRoZSBlbWJlZCBsaW5rIGFzIG5lZWRlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

## **連結參數**

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN
```

|連結/參數 |位置 |說明 |
|---|---|---|
|https://live.byteplus.com/livesaas/embeded/ |URL |嵌入連結的基礎 URL。 |
|178179896233\*\*\*\* |URL |直播間的活動 ID，僅在嵌入 AI Live 控制頁面時需配置。您可以透過調用 [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi) 取得活動 ID。例如，若要嵌入 AI Live 控制頁面，連結如下：<br><br>```Plain```<br>```https://live.byteplus.com/livesaas/embeded/185304025******?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|AppId |Query |嵌入 AI Live 頁面的唯一識別碼。固定值：`AILive`。 |
|type |Query |指定要嵌入的功能頁面。範例連結請參見[支援的頁面](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console-zh-TW#924ba3eb)。<br><br>例如，參數值 **`AILiveRoom`** 對應 **AI Live 直播間列表**頁面。連結如下：<br><br>```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveRoom&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br><br><br>有效值：<br><br><br>* **AILiveRoom**：AI Live 直播間列表頁面。<br><br>* **AILiveAvatarTraining**：模型訓練 \> 虛擬形象頁面。<br><br>* **AILiveVoiceTraining**：模型訓練 \> 語音頁面。<br><br>* **AILiveProducts**：產品庫頁面。<br><br>* **AILiveMaterials**：素材庫頁面。<br><br>* **AILiveKnowledgeBase**：知識庫頁面。<br><br>* **AILiveServiceCenter**：服務中心頁面。<br><br>* **AILiveStudio**：AI Live 控制頁面。嵌入 AI Live 控制頁面時，還需添加直播間的活動 ID。 |
|AccessKeyId |Query |臨時 AccessKey ID（AK）。<br><br>請調用 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW) 取得 AK，並根據 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 對該值進行 URL 編碼。 |
|SecretAccessKey |Query |臨時 Secret Access Key（SK）。<br><br>呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW) 以取得 SK，並根據 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 對該值進行 URL 編碼。 |
|SessionToken |Query |使用臨時憑證時所需的權杖。<br><br>呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW) 以取得權杖，並根據 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 對該值進行 URL 編碼。 |
|LoginLivesaasToken |Query |BytePlus Live 權杖。<br><br>呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/GetLoginLivesaasSts-zh-TW) 以取得權杖。`GetLoginLivesaasSts` 呼叫返回的權杖已經過 URL 編碼，因此無需再次編碼。 |

## 範例程式碼

以下範例程式碼採用 JavaScript。若您使用其他語言生成嵌入連結，請相應調整程式碼。

```HTML
<html>
  <header>
    <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
  </header>
  <body style='margin: 0; background-color: rgba(0,0,0,0.1);'>
    <div id='root' style='height: 100%; width: 100%; display: flex;'>
    </div>
    <script>
      async function initIframe() {
        // Call GetLoginLivesaasSts to get temporary STS credentials.
        var result = await GetLoginLivesaasSts();
        var activities = await listActivityAPI();
        var activityId = activities[0].ID;
        var params = {
          AccessKeyId: result.StsMsg.AccessKeyId,
          SecretAccessKey : result.StsMsg.SecretAccessKey,
          SessionToken: result.StsMsg.SessionToken,
          // 要嵌入的頁面。請替換為目標頁面的值。
          // 例如 AILiveRoom、AILiveAvatarTraining、AILiveVoiceTraining，
          // AILiveProducts、AILiveMaterials、AILiveKnowledgeBase。
          Type: 'AILiveStudio',
          AppId: 'AILive', // 嵌入 AI Live 頁面的唯一識別碼。固定值：AILive。
        }
        // 注意：/${activityId} 僅適用於 AI Live 控制頁面。其他頁面請使用：https://live.byteplus.com/livesaas/embeded/?${...}
        var iframeUrl = `https://live.byteplus.com/livesaas/embeded/${activityId}?${new URLSearchParams(params).toString()}&LoginLivesaasToken=${result.LoginLivesaasToken}`;
        createIframe(iframeUrl);
      }

      function createIframe(url) {
        var dom = document.createElement('iframe');
        dom.setAttribute('width', '1000px');
        dom.setAttribute('height', '800px');
        dom.setAttribute('frameborder', 0);
        dom.setAttribute('src', url);
        dom.setAttribute('id', 'embededIframe');
        document.getElementById('root').appendChild(dom);
      }
    </script>
  </body>
</html>
```
