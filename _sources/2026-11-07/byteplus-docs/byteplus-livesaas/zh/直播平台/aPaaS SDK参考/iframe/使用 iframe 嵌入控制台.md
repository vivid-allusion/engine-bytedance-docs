---
title: "使用 iframe 嵌入控制台"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-using-iframe-to-embed-the-console-zh-CN"
---

要将 BytePlus Live 控制台功能直接集成到您的网站中，可以通过 iframe 嵌入如直播间管理、站点创建等功能模块。本指南将介绍如何构建嵌入链接并使用各种参数自定义体验，使您能够在自己的页面内提供无缝管理能力，同时降低开发成本。

<span id="2a8bf87a"></span>
## 限制

此方法仅支持 PC 平台，不适用于 H5 页面。

<span id="a087634b"></span>
## 前提条件


* 为确保嵌入的功能页面可访问，请确保您的页面使用 HTTPS 域名。

* 使用 BytePlus 账号或具有超级管理员角色的 IAM 用户调用 [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)。


<span id="924ba3eb"></span>
## 功能

目前，您可以通过 iframe 将以下功能模块嵌入到您的页面中。

<span id="a5416915"></span>
### 直播间


|功能 ||页面截图 |
|---|---|---|
|嵌入整页 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345b1d741a5b43ee8c7f1b690a49b707~tplv-goo7wpa0wc-image.image) </span> |
|直播控制 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca9fc7076e2a4da5b65e59559d179267~tplv-goo7wpa0wc-image.image) </span> |
|直播控制 |聊天互动菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e376c8b7a4747d5a0804770bc5299fa~tplv-goo7wpa0wc-image.image) </span> |
||互动工具菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe88530c1a754c4985d121f924cbeef8~tplv-goo7wpa0wc-image.image) </span> |
||商品卡片菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a5548b6ad143dcb9f399df595a51f4~tplv-goo7wpa0wc-image.image) </span> |
||问答菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84447cee7b514b8d9f0ded8d939cf89f~tplv-goo7wpa0wc-image.image) </span> |
|制作人 |基本信息 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4becad3111ee42ee9ae75d8c42322f1b~tplv-goo7wpa0wc-image.image) </span> |
||外观 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d9400fefb264134bda66bad834ff1f0~tplv-goo7wpa0wc-image.image) </span> |
||菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f838a5a082b6416aa8d214ac99ce88f0~tplv-goo7wpa0wc-image.image) </span> |
||观看限制 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d991c9f0f9a4f6e84f2730bea4e9bd2~tplv-goo7wpa0wc-image.image) </span> |
||安全控制 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4cc2281fd404f0eb5d44b7cb1bc1f0a~tplv-goo7wpa0wc-image.image) </span> |
||敏感词 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62547c7a72014dae9c1f725f0f0fb624~tplv-goo7wpa0wc-image.image) </span> |
|营销工具包 |分享 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9be0543c231e452684e8f7dd80f2990f~tplv-goo7wpa0wc-image.image) </span> |
||问卷 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071c2b7d09d64108b57e29ba30777b5a~tplv-goo7wpa0wc-image.image) </span> |
||多平台推流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/341810a9fc8f4198a95d8866b7ee73e3~tplv-goo7wpa0wc-image.image) </span> |
||抽奖 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b839dfa3d2f24b358f3b7e327b8dcff4~tplv-goo7wpa0wc-image.image) </span> |
||礼物奖励 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd87c0bcb6604a87a032433700497f8f~tplv-goo7wpa0wc-image.image) </span> |
||推广 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/369f207ca21a4bf0997a8889ee16445d~tplv-goo7wpa0wc-image.image) </span> |
|回放 ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd62f7a1998948ecb82a95797b68ec2d~tplv-goo7wpa0wc-image.image) </span> |
|洞察 |基础数据 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a572a8836b91409dba0802a5c070e37f~tplv-goo7wpa0wc-image.image) </span> |
||观众行为数据 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f14caeaebe1646149d1f65a14a1406dd~tplv-goo7wpa0wc-image.image) </span> |


<span id="90a96a50"></span>
### 站点


|功能 ||页面截图 |
|---|---|---|
|嵌入整页 |站点列表 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48c1275bf3f540f0aa43be83ddd1a1bf~tplv-goo7wpa0wc-image.image) </span> |
||新建站点 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7658739f55ab445e8ca2ca4ccd68d1d5~tplv-goo7wpa0wc-image.image) </span> |
||站点信息 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279b0008b094434bbff911f274330b90~tplv-goo7wpa0wc-image.image) </span> |
||页面配置 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350199a0237f4c5c8a93ef424ea299a5~tplv-goo7wpa0wc-image.image) </span> |


<span id="31aff156"></span>
## **注意**


* 弹窗只能在嵌入的功能页面内居中，无法在您的页面上居中。

* 嵌入的功能页面版本与您通过 iframe 嵌入时使用的控制台版本一致。如需升级功能页面版本，请联系 BytePlus Live 技术支持。


<span id="f7a5587c"></span>
## 嵌入说明

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSIxODVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSAxODUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZCBhIEJ5dGVQbHVzIExpdmUgSUFNIHVzZXIgd2l0aCB0aGUgc3VwZXIgYWRtaW5pc3RyYXRvcnMgcm9sZTxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzNjIgMzIgTCAzNjIgODIgTCAzOTUuNjMgODEuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggODEuOTYgTCAzOTMuODkgODUuNDcgTCAzOTUuNjMgODEuOTcgTCAzOTMuODggNzguNDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIElBTSB1c2VyPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMTUyIEwgMzYyIDE1MiBMIDM2MiA4NyBMIDM5NS42MyA4NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQwMC44OCA4NyBMIDM5My44OCA5MC41IEwgMzk1LjYzIDg3IEwgMzkzLjg4IDgzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjEyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIEJ5dGVQbHVzIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTcyIDg3IEwgNjQ1LjYzIDg3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjUwLjg4IDg3IEwgNjQzLjg4IDkwLjUgTCA2NDUuNjMgODcgTCA2NDMuODggODMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQwMiIgeT0iNDIiIHdpZHRoPSIxNzAiIGhlaWdodD0iOTAiIHJ4PSIxMy41IiByeT0iMTMuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODdweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbCBHZXRMb2dpbkxpdmVzYWFzU3RzIHRvIGdldCB0aGUgdGVtcG9yYXJ5IEFLLCBTSywgdG9rZW4gcmVxdWlyZWQgd2hlbiB1c2luZyB0ZW1wb3JhcnkgY3JlZGVudGlhbHMsIGFuZCBCeXRlUGx1cyBMaXZlIHRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjYyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiA2NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNvbmNhdGVuYXRlIHRoZSBlbWJlZCBsaW5rIGFzIG5lZWRlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

<span id="4f495113"></span>
### **嵌入链接**

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&bgColorPage=COLOR&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN
```



|链接/参数 |位置 |接口行为 |
|---|---|---|
|https://live.byteplus.com/livesaas/embeded |URL |嵌入链接的基础 URL。 |
|178179896233\*\*\*\* |URL |直播间的活动 ID，仅在嵌入直播间功能页面时需要配置。您可以通过调用 [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi) 获取活动 ID。 |
|type |查询 |功能页面。有关嵌入链接示例及各功能页面的最小宽高，请参见 [嵌入功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-iframe-to-embed-the-console-zh-CN#d17178a5)。<br><br>例如，参数值 `LiveControl` 表示 **直播控制** 页面。<br><br>有效值：<br><br><br>* `LiveControlMenu`：**Live control**页面上的聊天互动、互动工具、商品卡片和问答菜单。<br><br>* `LiveControl`：**Live control**页面。<br><br>* `LivePageSettingInfo`：**Producer** \> **Basic information**页面。<br><br>* `LivePageSettingAppearance`：**Producer** \> **Appearance**页面。<br><br>* `MenuBar`：**Producer** \> **Menus**页面。<br><br>* `WatchLimit`：**Producer** \> **Viewing restrictions**页面。<br><br>* `LivePageSettingSecurityControl`：**Producer** \> **Security control**页面。<br><br>* `Antidirt`：**Producer** \> **Sensitive words**页面。<br><br>* `SharePoster`：**Marketing toolkits** \> **Sharing**页面。<br><br>* `Questionnaire`：**Marketing toolkits** \> **Questionnaires**页面。<br><br>* `BindUser`：**Marketing toolkits** \> **Multi\-platform streaming**页面。<br><br>* `LotteryGame`：**Marketing toolkits** \> **Lucky draws**页面。<br><br>* `GiftReward`：**Marketing toolkits** \> **Gift rewards**页面。<br><br>* `MarketingAd`：**Marketing toolkits** \> **Promotion**页面。<br><br>* `ReplayManagement`：**Playbacks**页面。<br><br>* `StatisticsBasicData`：**Insights** \> **Basic data**页面。<br><br>* `StatisticsUserBehaviourData`：**Insights** \> **Viewer behavior data**页面。<br><br>* `LiveSite`：与站点相关的页面。<br><br><br>要隐藏嵌入页面中的特定功能，可以在嵌入链接后添加特定参数。更多信息，请参见[在嵌入页面中隐藏特定功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-using-iframe-to-embed-the-console-zh-CN#0ad911a5)。 |
|bgColorPage |Query |嵌入页面的背景颜色。如果省略此参数，嵌入页面默认使用你的主播页面的背景颜色。<br><br>请按照以下步骤格式化参数值：<br><br><br>1. 可使用以下任意方法表示颜色值：<br><br>   * 颜色名称，例如`red`、`blue`和`green`。<br><br>   * 十六进制颜色代码，例如`#FF0000`、`#0000FF`和`#00FF00`。<br><br>   * RGB颜色值，例如`rgb(255, 0, 0)`、`rgb(0, 0, 255)`和`rgb(0, 255, 0)`。<br><br>2. 根据[RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)对颜色值进行URL编码。<br><br><br>例如，若要使用十六进制颜色代码将嵌入页面的背景色设置为蓝色，需根据[RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)对`#0000FF`进行URL编码，参数值为`%230000FF`。 |
|appid |Query |你的唯一标识符。请联系BytePlus Live技术支持获取。 |
|AccessKeyId |Query |临时AccessKey ID（AK）。<br><br>调用[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)获取AK，并根据[RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)对值进行URL编码。 |
|SecretAccessKey |Query |临时Secret Access Key（SK）。<br><br>调用[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)获取SK，并根据[RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)对值进行URL编码。 |
|SessionToken |Query |使用临时凭证时所需的令牌。<br><br>调用[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)获取令牌，并根据[RFC3986](https://datatracker.ietf.org/doc/html/rfc3986)对值进行URL编码。 |
|LoginLivesaasToken |Query |BytePlus Live令牌。<br><br>调用[GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts)获取令牌。`GetLoginLivesaasSts`调用返回的令牌已进行URL编码，无需再次编码。 |


<span id="d17178a5"></span>
### 嵌入功能

<span id="7fea9f55"></span>
#### 嵌入整页


* 直播间

   
   |示例 |接口行为 |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1350px<br><br>最小高度：900px |
   

   您可以嵌入直播间的全部功能。

* 站点

   
   |示例 |接口行为 |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded?type=LiveSite&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1000 px<br><br>最小高度：500 px |
   |||
   |||
   |||
   

   您可以嵌入以下页面：

   * 站点列表

   * 新建站点

   * 站点信息

   * 页面配置


<span id="2e2e42c9"></span>
#### 嵌入单一模块


|功能页面 ||示例 |接口行为 |
|---|---|---|---|
|Live control ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：950px<br><br>最小高度：625px |
|Live control |聊天互动菜单 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControlMenu&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1100px<br><br>最小高度：500px |
||互动工具菜单 |||
||商品卡片菜单 |||
||问答菜单 |||
|Producer |Basic information |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingInfo&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：600px<br><br>最小高度：650px |
||Appearance |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingAppearance&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：600px<br><br>最小高度：650px |
||Menus |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MenuBar&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：900px<br><br>最小高度：630px |
||Viewing restrictions |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=WatchLimit&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1000px<br><br>最小高度：500px |
||Security control |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingSecurityControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：500px<br><br>最小高度：650px |
||Sensitive words |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Antidirt&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：800px<br><br>最小高度：500px |
|Marketing toolkits |Sharing |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=SharePoster&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：500px<br><br>最小高度：650px |
||Questionnaires |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Questionnaire&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1000px<br><br>最小高度：500px |
||Multi\-platform streaming |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=BindUser&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：880px<br><br>最小高度：650px |
||抽奖 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LotteryGame&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：500px<br><br>最小高度：650px |
||礼品奖励 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=GiftReward&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：800px<br><br>最小高度：500px |
||推广 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MarketingAd&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：400px<br><br>最小高度：650px |
|回放 ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=ReplayManagement&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1400px<br><br>最小高度：650px |
|洞察 |基础数据 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsBasicData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1120px<br><br>最小高度：650px |
||观众行为数据 |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsUserBehaviourData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |最小宽度：1300px<br><br>最小高度：650px |


<span id="0ad911a5"></span>
### 在嵌入页面中隐藏特定功能

要在嵌入的完整直播间页面中隐藏左侧导航栏，可以在嵌入链接后追加 `hideLiveManagementSideMenu=true`。完整的嵌入链接如下。

```Bash
https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveManagementSideMenu=true
```


要在嵌入的单一模块页面中隐藏特定功能，可以在嵌入链接后追加特定参数。例如，嵌入 **Live control** 页面后需要隐藏播放器时，可以在嵌入链接后添加 `hideLiveControlPlayer=true`。完整的嵌入链接如下。

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveControlPlayer=true
```


下表列出了支持隐藏的功能及其对应参数。


|嵌入页面 |参数 |功能 |页面截图 |
|---|---|---|---|
|直播控制（`type=LiveControl`） |`hideLiveControlPlayer=true` |播放器 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cca3a5efdb0466fb0932b10d02ca32d~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerPopularity=true` |人气 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf31337bd2d49d492a4e85b04b64d20~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerLikes=true` |直播间点赞 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a5e0f97ac454358988cda9af2164032~tplv-goo7wpa0wc-image.image) </span> |
||`hideAudienceList=true` |观众列表 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de9b859cf3b541af9c72897add4afd0b~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlChat=true` |菜单 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fa6761bca2f49aeb24d7feb29346159~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlTab=true` |播放器下方区域 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/640a4ee9c0604db1898a4e15d4cf41c5~tplv-goo7wpa0wc-image.image) </span> |
||`hideWebPush=true` |网页浏览器 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7c521be3ef0437ea304025efea5617c~tplv-goo7wpa0wc-image.image) </span> |
||`hidePullStream=true` |拉流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd744ff8a47499d8abf60b43ad5b480~tplv-goo7wpa0wc-image.image) </span> |
||`hideLoopVideo=true` |预录制视频 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/161686b58e004ef0be1eb6d1570c2737~tplv-goo7wpa0wc-image.image) </span> |
||`hidePushStream=true` |推流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b117873b4d44df9f5ba9cfe3f76204~tplv-goo7wpa0wc-image.image) </span> |
||`hidePopularity=true` |互动人气 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21110daf8c6145998571143b8ed6ddd3~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveScreenData=true` |数据看板 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b391d8c2048643a8b673f79fc8fe910c~tplv-goo7wpa0wc-image.image) </span> |
||`hideVideoEdit=true` |剪辑直播流 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edaba5f530084510af1cda766e250f0f~tplv-goo7wpa0wc-image.image) </span> |
|制作人 \> 基本信息（`type=LivePageSettingInfo`） |`hideSettingBasic=true` |基础设置 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9bccd4d9652451b8902795cee587b9e~tplv-goo7wpa0wc-image.image) </span> |
||`hideSettingAdvanced=true` |高级设置 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7daef71e9a22426283b5e8e47b365cca~tplv-goo7wpa0wc-image.image) </span> |
|制作人 \> 安全控制（`type=LivePageSettingSecurityControl`） |`hideSecurityControlBasic=true` |基础设置 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3780cf6efd144d37855427f8cdd4f20b~tplv-goo7wpa0wc-image.image) </span> |
||`hideSecurityControlWatermark=true` |全屏水印 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dc669a1726b4d0d9f797a3e2e18de01~tplv-goo7wpa0wc-image.image) </span> |
|营销工具包 \> 抽奖（`type=LotteryGame`） |`hideRealtimeLottery=true` |实时抽奖 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae073f2829144cd886c59e02a9dde0b9~tplv-goo7wpa0wc-image.image) </span> |
||`hideTaskAward=true` |基于观看时长的抽奖 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/450b51850da743eda1028cad973624cc~tplv-goo7wpa0wc-image.image) </span> |
||`hideLotteryLib=true` |奖品库 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1ec96e6f99140dfbb117654d34d57d3~tplv-goo7wpa0wc-image.image) </span> |
|营销工具包 \> 推广（`type=MarketingAd`） |`hideAdBrand=true` |主播/品牌账号 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92128f5fac3745e9ab4761b529fc2704~tplv-goo7wpa0wc-image.image) </span> |
||`hideGuide=true` |引导页 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50694e3566ab4214acf8002937e6600e~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageHeadAd=true` |页头广告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0fd7446c3a34f2a886d409355026df3~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageMiddleAd=true` |页中广告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/198e04d004ef4f28a92ed5bdf7f153a5~tplv-goo7wpa0wc-image.image) </span> |
||`hideFloatAd=true` |浮标广告 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/256cca86693d41e88bbcec67a08d8373~tplv-goo7wpa0wc-image.image) </span> |
|回放（`type=ReplayManagement`） |`hideUploadVideoBtn=true` |上传视频 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4caae8f28eef4d199f07dec54f9b3704~tplv-goo7wpa0wc-image.image) </span> |
||`hideImportFromVideoLib=true` |从视频库导入 |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb70168ec4b4ebf8d5b9333c425381c~tplv-goo7wpa0wc-image.image) </span> |


<span id="8c3d70c2"></span>
## 示例代码

以下示例代码使用 JavaScript。如果您使用其他语言生成嵌入链接，请相应调整代码。

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
        // 调用 GetLoginLivesaasSts 以获取临时STS凭证。
        var result = await GetLoginLivesaasSts();
        var activities = await listActivityAPI();
        var activityId = activities[0].ID;
        var params = {
          AccessKeyId: result.StsMsg.AccessKeyId,
          SecretAccessKey : result.StsMsg.SecretAccessKey,
          SessionToken: result.StsMsg.SessionToken,
          Type: 'LiveControlMenu',
          AppId: 'AppId', // 你的唯一标识符。请联系 BytePlus Live 技术支持获取。
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
