---
title: "使用 iframe 嵌入主控台"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/shi-yong-iframe-qian-ru-zhu-kong-tai-zh-TW"
---

若要將 BytePlus Live 主控台功能直接整合到你自己的網站中，你可以使用 iframe 嵌入如直播間管理、站點建立等功能模組。本指南將說明如何構建嵌入連結並使用各種參數自訂體驗，讓你能在自己的頁面中提供無縫的管理能力，同時降低開發成本。

<span id="2a8bf87a"></span>
## 限制

此方法僅支援 PC 平台，H5 頁面不適用。

<span id="a087634b"></span>
## 前置條件


* 為確保可存取嵌入的功能頁面，請確保你的頁面使用 HTTPS 網域。

* 請使用 BytePlus 帳號或具備超級管理員角色的 IAM 使用者呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)。


<span id="924ba3eb"></span>
## 功能

目前，你可以使用 iframe 將下列功能模組嵌入到自己的頁面中。

<span id="a5416915"></span>
### 直播間


|功能 ||頁面截圖 |
|---|---|---|
|嵌入整頁 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345b1d741a5b43ee8c7f1b690a49b707~tplv-goo7wpa0wc-image.image) </span> |
|直播控制 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca9fc7076e2a4da5b65e59559d179267~tplv-goo7wpa0wc-image.image) </span> |
|直播控制 |互動聊天選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e376c8b7a4747d5a0804770bc5299fa~tplv-goo7wpa0wc-image.image) </span> |
||互動工具選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe88530c1a754c4985d121f924cbeef8~tplv-goo7wpa0wc-image.image) </span> |
||商品卡片選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a5548b6ad143dcb9f399df595a51f4~tplv-goo7wpa0wc-image.image) </span> |
||問答選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84447cee7b514b8d9f0ded8d939cf89f~tplv-goo7wpa0wc-image.image) </span> |
|製作人 |基本資訊 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4becad3111ee42ee9ae75d8c42322f1b~tplv-goo7wpa0wc-image.image) </span> |
||外觀 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d9400fefb264134bda66bad834ff1f0~tplv-goo7wpa0wc-image.image) </span> |
||選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f838a5a082b6416aa8d214ac99ce88f0~tplv-goo7wpa0wc-image.image) </span> |
||觀看限制 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d991c9f0f9a4f6e84f2730bea4e9bd2~tplv-goo7wpa0wc-image.image) </span> |
||安全控制 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4cc2281fd404f0eb5d44b7cb1bc1f0a~tplv-goo7wpa0wc-image.image) </span> |
||敏感詞 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62547c7a72014dae9c1f725f0f0fb624~tplv-goo7wpa0wc-image.image) </span> |
|行銷工具包 |分享 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9be0543c231e452684e8f7dd80f2990f~tplv-goo7wpa0wc-image.image) </span> |
||問卷 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071c2b7d09d64108b57e29ba30777b5a~tplv-goo7wpa0wc-image.image) </span> |
||多平台串流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/341810a9fc8f4198a95d8866b7ee73e3~tplv-goo7wpa0wc-image.image) </span> |
||抽獎 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b839dfa3d2f24b358f3b7e327b8dcff4~tplv-goo7wpa0wc-image.image) </span> |
||禮物獎勵 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd87c0bcb6604a87a032433700497f8f~tplv-goo7wpa0wc-image.image) </span> |
||推廣 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/369f207ca21a4bf0997a8889ee16445d~tplv-goo7wpa0wc-image.image) </span> |
|回放 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd62f7a1998948ecb82a95797b68ec2d~tplv-goo7wpa0wc-image.image) </span> |
|洞察 |基礎數據 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a572a8836b91409dba0802a5c070e37f~tplv-goo7wpa0wc-image.image) </span> |
||觀眾行為數據 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f14caeaebe1646149d1f65a14a1406dd~tplv-goo7wpa0wc-image.image) </span> |


<span id="90a96a50"></span>
### 站點


|功能 ||頁面截圖 |
|---|---|---|
|嵌入整頁 |站點列表 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48c1275bf3f540f0aa43be83ddd1a1bf~tplv-goo7wpa0wc-image.image) </span> |
||新建站點 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7658739f55ab445e8ca2ca4ccd68d1d5~tplv-goo7wpa0wc-image.image) </span> |
||站點資訊 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279b0008b094434bbff911f274330b90~tplv-goo7wpa0wc-image.image) </span> |
||頁面配置 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350199a0237f4c5c8a93ef424ea299a5~tplv-goo7wpa0wc-image.image) </span> |


<span id="31aff156"></span>
## **注意**


* 彈窗僅能在嵌入的功能頁面中置中，無法在你的頁面中置中。

* 嵌入的功能頁面版本與你通過 iframe 嵌入時所使用的主控台版本相同。若需升級功能頁面的版本，請聯繫 BytePlus Live 技術支援。


<span id="f7a5587c"></span>
## 嵌入說明

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSIxODVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSAxODUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZCBhIEJ5dGVQbHVzIExpdmUgSUFNIHVzZXIgd2l0aCB0aGUgc3VwZXIgYWRtaW5pc3RyYXRvcnMgcm9sZTxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzNjIgMzIgTCAzNjIgODIgTCAzOTUuNjMgODEuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggODEuOTYgTCAzOTMuODkgODUuNDcgTCAzOTUuNjMgODEuOTcgTCAzOTMuODggNzguNDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIElBTSB1c2VyPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMTUyIEwgMzYyIDE1MiBMIDM2MiA4NyBMIDM5NS42MyA4NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQwMC44OCA4NyBMIDM5My44OCA5MC41IEwgMzk1LjYzIDg3IEwgMzkzLjg4IDgzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjEyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIEJ5dGVQbHVzIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTcyIDg3IEwgNjQ1LjYzIDg3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjUwLjg4IDg3IEwgNjQzLjg4IDkwLjUgTCA2NDUuNjMgODcgTCA2NDMuODggODMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQwMiIgeT0iNDIiIHdpZHRoPSIxNzAiIGhlaWdodD0iOTAiIHJ4PSIxMy41IiByeT0iMTMuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODdweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbCBHZXRMb2dpbkxpdmVzYWFzU3RzIHRvIGdldCB0aGUgdGVtcG9yYXJ5IEFLLCBTSywgdG9rZW4gcmVxdWlyZWQgd2hlbiB1c2luZyB0ZW1wb3JhcnkgY3JlZGVudGlhbHMsIGFuZCBCeXRlUGx1cyBMaXZlIHRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjYyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiA2NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNvbmNhdGVuYXRlIHRoZSBlbWJlZCBsaW5rIGFzIG5lZWRlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

<span id="4f495113"></span>
### **嵌入連結**

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&bgColorPage=COLOR&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN
```



|連結/參數 |位置 |說明 |
|---|---|---|
|https://live.byteplus.com/livesaas/embeded |URL |嵌入連結的基礎 URL。 |
|178179896233\*\*\*\* |URL |直播間的活動 ID，僅在嵌入直播間功能頁面時需配置。你可以通過呼叫 [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi) 取得活動 ID。 |
|type |查詢 |功能頁面。有關嵌入連結範例及各功能頁面的最小寬高，請參見 [嵌入功能](https://docs.byteplus.com/docs/byteplus-livesaas/shi-yong-iframe-qian-ru-zhu-kong-tai-zh-TW#d17178a5)。<br><br>例如，參數值 `LiveControl` 代表 **直播控制** 頁面。<br><br>有效值：<br><br><br>* `LiveControlMenu`：**Live control** 頁面上的聊天互動、互動工具、商品卡片及問答選單。<br><br>* `LiveControl`：**Live control** 頁面。<br><br>* `LivePageSettingInfo`：**Producer** \> **Basic information** 頁面。<br><br>* `LivePageSettingAppearance`：**Producer** \> **Appearance** 頁面。<br><br>* `MenuBar`：**Producer** \> **Menus** 頁面。<br><br>* `WatchLimit`：**Producer** \> **Viewing restrictions** 頁面。<br><br>* `LivePageSettingSecurityControl`：**Producer** \> **Security control** 頁面。<br><br>* `Antidirt`：**Producer** \> **Sensitive words** 頁面。<br><br>* `SharePoster`：**Marketing toolkits** \> **Sharing** 頁面。<br><br>* `Questionnaire`：**Marketing toolkits** \> **Questionnaires** 頁面。<br><br>* `BindUser`：**Marketing toolkits** \> **Multi\-platform streaming** 頁面。<br><br>* `LotteryGame`：**Marketing toolkits** \> **Lucky draws** 頁面。<br><br>* `GiftReward`：**Marketing toolkits** \> **Gift rewards** 頁面。<br><br>* `MarketingAd`：**Marketing toolkits** \> **Promotion** 頁面。<br><br>* `ReplayManagement`：**Playbacks** 頁面。<br><br>* `StatisticsBasicData`：**Insights** \> **Basic data** 頁面。<br><br>* `StatisticsUserBehaviourData`：**Insights** \> **Viewer behavior data** 頁面。<br><br>* `LiveSite`：與網站相關的頁面。<br><br><br>若要隱藏嵌入頁面中的特定功能，可在嵌入連結後加上特定參數。如需更多資訊，請參閱[隱藏嵌入頁面的特定功能](https://docs.byteplus.com/docs/byteplus-livesaas/shi-yong-iframe-qian-ru-zhu-kong-tai-zh-TW#0ad911a5)。 |
|bgColorPage |查詢參數 |嵌入頁面的背景顏色。若省略此參數，嵌入頁面將預設使用您的主頁面背景顏色。<br><br>請依下列步驟設定參數值格式：<br><br><br>1. 可使用以下任一方式表示顏色值：<br><br>   * 顏色名稱，例如 `red`、`blue` 及 `green`。<br><br>   * 十六進位色碼，例如 `#FF0000`、`#0000FF` 及 `#00FF00`。<br><br>   * RGB 顏色值，例如 `rgb(255, 0, 0)`、`rgb(0, 0, 255)` 及 `rgb(0, 255, 0)`。<br><br>2. 請依 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 規範將顏色值進行 URL 編碼。<br><br><br>例如，若要以十六進位色碼設定嵌入頁面的背景顏色為藍色，請依 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 規範將 `#0000FF` 進行 URL 編碼，參數值即為 `%230000FF`。 |
|appid |查詢參數 |您的唯一識別碼。請聯絡 BytePlus Live 技術支援以取得。 |
|AccessKeyId |查詢參數 |臨時 AccessKey ID（AK）。<br><br>請呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) 以取得 AK，並依 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 規範將值進行 URL 編碼。 |
|SecretAccessKey |查詢參數 |臨時 Secret Access Key（SK）。<br><br>請呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) 以取得 SK，並依 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 規範將值進行 URL 編碼。 |
|SessionToken |查詢參數 |使用臨時憑證時所需的 Token。<br><br>請呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) 以取得 Token，並依 [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986) 規範將值進行 URL 編碼。 |
|LoginLivesaasToken |查詢參數 |BytePlus Live Token。<br><br>請呼叫 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) 以取得 Token。由 `GetLoginLivesaasSts` 呼叫返回的 Token 已經過 URL 編碼，無需再次編碼。 |


<span id="d17178a5"></span>
### 嵌入功能

<span id="7fea9f55"></span>
#### 嵌入整頁


* 直播間

   
   |範例 |說明 |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1350px<br><br>最小高度：900px |
   

   你可以嵌入直播間的所有功能。

* 站點

   
   |範例 |說明 |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded?type=LiveSite&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1000 px<br><br>最小高度：500 px |
   |||
   |||
   |||
   

   你可以嵌入以下頁面：

   * 站點列表

   * 新建站點

   * 站點資訊

   * 頁面配置


<span id="2e2e42c9"></span>
#### 嵌入單一模組


|功能頁面 ||範例 |說明 |
|---|---|---|---|
|Live control ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：950px<br><br>最小高度：625px |
|Live control |聊天互動選單 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControlMenu&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1100px<br><br>最小高度：500px |
||互動工具選單 |||
||商品卡片選單 |||
||問答選單 |||
|Producer |基本資訊 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingInfo&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：600px<br><br>最小高度：650px |
||外觀 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingAppearance&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：600px<br><br>最小高度：650px |
||選單 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MenuBar&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：900px<br><br>最小高度：630px |
||觀看限制 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=WatchLimit&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1000px<br><br>最小高度：500px |
||安全控制 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingSecurityControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：500px<br><br>最小高度：650px |
||敏感詞 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Antidirt&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：800px<br><br>最小高度：500px |
|行銷工具包 |分享 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=SharePoster&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：500px<br><br>最小高度：650px |
||問卷 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Questionnaire&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1000px<br><br>最小高度：500px |
||多平台串流 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=BindUser&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：880px<br><br>最小高度：650px |
||抽獎 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LotteryGame&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：500px<br><br>最小高度：650px |
||禮品獎勵 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=GiftReward&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：800px<br><br>最小高度：500px |
||推廣 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MarketingAd&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：400px<br><br>最小高度：650px |
|回放 ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=ReplayManagement&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1400px<br><br>最小高度：650px |
|分析 |基本資料 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsBasicData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1120px<br><br>最小高度：650px |
||觀眾行為資料 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsUserBehaviourData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小寬度：1300px<br><br>最小高度：650px |


<span id="0ad911a5"></span>
### 隱藏嵌入頁面的特定功能

若要在嵌入的整個直播間頁面中隱藏左側導覽列，可在嵌入連結後加上 `hideLiveManagementSideMenu=true`。完整的嵌入連結如下。

```Bash
https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveManagementSideMenu=true
```


若要在嵌入的單一模組頁面中隱藏特定功能，可在嵌入連結後加上對應參數。例如，嵌入 **Live control** 頁面後想要隱藏播放器，可在嵌入連結後加上 `hideLiveControlPlayer=true`。完整的嵌入連結如下。

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveControlPlayer=true
```


下表列出可隱藏的支援功能及其對應參數。


|嵌入頁面 |參數 |功能 |頁面截圖 |
|---|---|---|---|
|直播控制（`type=LiveControl`） |`hideLiveControlPlayer=true` |播放器 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cca3a5efdb0466fb0932b10d02ca32d~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerPopularity=true` |人氣 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf31337bd2d49d492a4e85b04b64d20~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerLikes=true` |直播間點讚 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a5e0f97ac454358988cda9af2164032~tplv-goo7wpa0wc-image.image) </span> |
||`hideAudienceList=true` |觀眾列表 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de9b859cf3b541af9c72897add4afd0b~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlChat=true` |選單 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fa6761bca2f49aeb24d7feb29346159~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlTab=true` |播放器下方區域 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/640a4ee9c0604db1898a4e15d4cf41c5~tplv-goo7wpa0wc-image.image) </span> |
||`hideWebPush=true` |網頁瀏覽器 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7c521be3ef0437ea304025efea5617c~tplv-goo7wpa0wc-image.image) </span> |
||`hidePullStream=true` |拉流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd744ff8a47499d8abf60b43ad5b480~tplv-goo7wpa0wc-image.image) </span> |
||`hideLoopVideo=true` |預錄影片 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/161686b58e004ef0be1eb6d1570c2737~tplv-goo7wpa0wc-image.image) </span> |
||`hidePushStream=true` |推流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b117873b4d44df9f5ba9cfe3f76204~tplv-goo7wpa0wc-image.image) </span> |
||`hidePopularity=true` |互動人氣 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21110daf8c6145998571143b8ed6ddd3~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveScreenData=true` |資料儀表板 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b391d8c2048643a8b673f79fc8fe910c~tplv-goo7wpa0wc-image.image) </span> |
||`hideVideoEdit=true` |直播剪輯 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edaba5f530084510af1cda766e250f0f~tplv-goo7wpa0wc-image.image) </span> |
|製作人 \> 基本資訊（`type=LivePageSettingInfo`） |`hideSettingBasic=true` |基本設定 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9bccd4d9652451b8902795cee587b9e~tplv-goo7wpa0wc-image.image) </span> |
||`hideSettingAdvanced=true` |進階設定 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7daef71e9a22426283b5e8e47b365cca~tplv-goo7wpa0wc-image.image) </span> |
|製作人 \> 安全控制（`type=LivePageSettingSecurityControl`） |`hideSecurityControlBasic=true` |基本設定 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3780cf6efd144d37855427f8cdd4f20b~tplv-goo7wpa0wc-image.image) </span> |
||`hideSecurityControlWatermark=true` |全螢幕浮水印 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dc669a1726b4d0d9f797a3e2e18de01~tplv-goo7wpa0wc-image.image) </span> |
|行銷工具包 \> 抽獎（`type=LotteryGame`） |`hideRealtimeLottery=true` |即時抽獎 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae073f2829144cd886c59e02a9dde0b9~tplv-goo7wpa0wc-image.image) </span> |
||`hideTaskAward=true` |依觀看時長抽獎 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/450b51850da743eda1028cad973624cc~tplv-goo7wpa0wc-image.image) </span> |
||`hideLotteryLib=true` |獎品庫 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1ec96e6f99140dfbb117654d34d57d3~tplv-goo7wpa0wc-image.image) </span> |
|行銷工具包 \> 推廣（`type=MarketingAd`） |`hideAdBrand=true` |主持人／品牌帳號 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92128f5fac3745e9ab4761b529fc2704~tplv-goo7wpa0wc-image.image) </span> |
||`hideGuide=true` |啟動畫面 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50694e3566ab4214acf8002937e6600e~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageHeadAd=true` |頁首廣告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0fd7446c3a34f2a886d409355026df3~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageMiddleAd=true` |頁內廣告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/198e04d004ef4f28a92ed5bdf7f153a5~tplv-goo7wpa0wc-image.image) </span> |
||`hideFloatAd=true` |浮動廣告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/256cca86693d41e88bbcec67a08d8373~tplv-goo7wpa0wc-image.image) </span> |
|回放（`type=ReplayManagement`） |`hideUploadVideoBtn=true` |上傳影片 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4caae8f28eef4d199f07dec54f9b3704~tplv-goo7wpa0wc-image.image) </span> |
||`hideImportFromVideoLib=true` |從影片庫匯入 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb70168ec4b4ebf8d5b9333c425381c~tplv-goo7wpa0wc-image.image) </span> |


<span id="8c3d70c2"></span>
## 範例程式碼

以下範例程式碼使用 JavaScript。若你使用其他語言產生嵌入連結，請相應調整程式碼。

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
        // 調用 GetLoginLivesaasSts 以獲取臨時 STS 憑證。
        var result = await GetLoginLivesaasSts();
        var activities = await listActivityAPI();
        var activityId = activities[0].ID;
        var params = {
          AccessKeyId: result.StsMsg.AccessKeyId,
          SecretAccessKey : result.StsMsg.SecretAccessKey,
          SessionToken: result.StsMsg.SessionToken,
          Type: 'LiveControlMenu',
          AppId: 'AppId', // 您的唯一識別碼。請聯繫 BytePlus Live 技術支援以獲取。
        }
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
