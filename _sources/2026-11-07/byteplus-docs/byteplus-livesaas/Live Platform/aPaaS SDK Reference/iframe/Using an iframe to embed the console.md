---
title: "Using an iframe to embed the console"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-console"
---

This topic describes how to use an iframe to embed functional modules of the BytePlus Live console into your own page. This allows you to manage live rooms, create sites, and more directly from your own page. By embedding the console via an iframe, you can integrate these features more conveniently and quickly, effectively reducing development costs.

<span id="2a8bf87a"></span>
## Limitation

This approach supports PC platforms only and is not available on H5 pages.

<span id="a087634b"></span>
## Prerequisites


* To ensure the embedded functional pages can be accessed, make sure your own page uses an HTTPS domain.

* Use the BytePlus account or an IAM user with the super administrators role to call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts).


<span id="924ba3eb"></span>
## Features

Currently, you can use an iframe to embed the following functional modules into your own page.

<span id="a5416915"></span>
### Live rooms


|Feature ||Page screenshot |
|---|---|---|
|Embedding a full page ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/345b1d741a5b43ee8c7f1b690a49b707~tplv-goo7wpa0wc-image.image) </span> |
|Live control ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca9fc7076e2a4da5b65e59559d179267~tplv-goo7wpa0wc-image.image) </span> |
|Live control |Menu for chat interaction |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e376c8b7a4747d5a0804770bc5299fa~tplv-goo7wpa0wc-image.image) </span> |
||Menu for interaction tools |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fe88530c1a754c4985d121f924cbeef8~tplv-goo7wpa0wc-image.image) </span> |
||Menu for product cards |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83a5548b6ad143dcb9f399df595a51f4~tplv-goo7wpa0wc-image.image) </span> |
||Menu for Q&A |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/84447cee7b514b8d9f0ded8d939cf89f~tplv-goo7wpa0wc-image.image) </span> |
|Producer |Basic information |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4becad3111ee42ee9ae75d8c42322f1b~tplv-goo7wpa0wc-image.image) </span> |
||Appearance |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d9400fefb264134bda66bad834ff1f0~tplv-goo7wpa0wc-image.image) </span> |
||Menus |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f838a5a082b6416aa8d214ac99ce88f0~tplv-goo7wpa0wc-image.image) </span> |
||Viewing restrictions |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d991c9f0f9a4f6e84f2730bea4e9bd2~tplv-goo7wpa0wc-image.image) </span> |
||Security control |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4cc2281fd404f0eb5d44b7cb1bc1f0a~tplv-goo7wpa0wc-image.image) </span> |
||Sensitive words |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62547c7a72014dae9c1f725f0f0fb624~tplv-goo7wpa0wc-image.image) </span> |
|Marketing toolkits |Sharing |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9be0543c231e452684e8f7dd80f2990f~tplv-goo7wpa0wc-image.image) </span> |
||Questionnaires |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/071c2b7d09d64108b57e29ba30777b5a~tplv-goo7wpa0wc-image.image) </span> |
||Multi\-platform streaming |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/341810a9fc8f4198a95d8866b7ee73e3~tplv-goo7wpa0wc-image.image) </span> |
||Lucky draws |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b839dfa3d2f24b358f3b7e327b8dcff4~tplv-goo7wpa0wc-image.image) </span> |
||Gift rewards |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd87c0bcb6604a87a032433700497f8f~tplv-goo7wpa0wc-image.image) </span> |
||Promotion |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/369f207ca21a4bf0997a8889ee16445d~tplv-goo7wpa0wc-image.image) </span> |
|Playbacks ||<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd62f7a1998948ecb82a95797b68ec2d~tplv-goo7wpa0wc-image.image) </span> |
|Insights |Basic data |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a572a8836b91409dba0802a5c070e37f~tplv-goo7wpa0wc-image.image) </span> |
||Viewer behavior data |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f14caeaebe1646149d1f65a14a1406dd~tplv-goo7wpa0wc-image.image) </span> |


<span id="90a96a50"></span>
### Sites


|Feature ||Page screenshot |
|---|---|---|
|Embedding a full page |Site list |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/48c1275bf3f540f0aa43be83ddd1a1bf~tplv-goo7wpa0wc-image.image) </span> |
||New site |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7658739f55ab445e8ca2ca4ccd68d1d5~tplv-goo7wpa0wc-image.image) </span> |
||Site information |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/279b0008b094434bbff911f274330b90~tplv-goo7wpa0wc-image.image) </span> |
||Page configuration |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/350199a0237f4c5c8a93ef424ea299a5~tplv-goo7wpa0wc-image.image) </span> |


<span id="31aff156"></span>
## **Notes**


* Pop\-ups can only be centered within the embedded functional page but cannot be centered on your own page.

* The version of the embedded functional page is the same as the console version you use when embedding via an iframe. If you need to upgrade the version of the functional page, contact BytePlus Live technical support.


<span id="f7a5587c"></span>
## Embedding instructions

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSIxODVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSAxODUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZCBhIEJ5dGVQbHVzIExpdmUgSUFNIHVzZXIgd2l0aCB0aGUgc3VwZXIgYWRtaW5pc3RyYXRvcnMgcm9sZTxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzNjIgMzIgTCAzNjIgODIgTCAzOTUuNjMgODEuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggODEuOTYgTCAzOTMuODkgODUuNDcgTCAzOTUuNjMgODEuOTcgTCAzOTMuODggNzguNDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIElBTSB1c2VyPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMTUyIEwgMzYyIDE1MiBMIDM2MiA4NyBMIDM5NS42MyA4NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQwMC44OCA4NyBMIDM5My44OCA5MC41IEwgMzk1LjYzIDg3IEwgMzkzLjg4IDgzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjEyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIEJ5dGVQbHVzIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTcyIDg3IEwgNjQ1LjYzIDg3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjUwLjg4IDg3IEwgNjQzLjg4IDkwLjUgTCA2NDUuNjMgODcgTCA2NDMuODggODMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQwMiIgeT0iNDIiIHdpZHRoPSIxNzAiIGhlaWdodD0iOTAiIHJ4PSIxMy41IiByeT0iMTMuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODdweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbCBHZXRMb2dpbkxpdmVzYWFzU3RzIHRvIGdldCB0aGUgdGVtcG9yYXJ5IEFLLCBTSywgdG9rZW4gcmVxdWlyZWQgd2hlbiB1c2luZyB0ZW1wb3JhcnkgY3JlZGVudGlhbHMsIGFuZCBCeXRlUGx1cyBMaXZlIHRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjYyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiA2NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNvbmNhdGVuYXRlIHRoZSBlbWJlZCBsaW5rIGFzIG5lZWRlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

<span id="4f495113"></span>
### **Embed link**

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&bgColorPage=COLOR&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN
```



|Link/Parameter |Location |Description |
|---|---|---|
|https://live.byteplus.com/livesaas/embeded |URL |Public route of the embed link. |
|178179896233\*\*\*\* |URL |The activity ID of the live room, which only needs to be configured when embedding live room\-related functional pages. You can get the activity ID by calling [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi). |
|type |Query |Functional page. For embed link examples and minimum width and height requirements for each functional page, see [Embedding features](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-console#d17178a5).<br><br>For example, the parameter value `LiveControl` refers to the **Live control** page.<br><br>Valid values:<br><br><br>* `LiveControlMenu`: Menus for chat interaction, interaction tools, product cards, and Q&A on the **Live control** page.<br><br>* `LiveControl`: The **Live control** page.<br><br>* `LivePageSettingInfo`: The **Producer** \> **Basic information** page.<br><br>* `LivePageSettingAppearance`: The **Producer** \> **Appearance** page.<br><br>* `MenuBar`: The **Producer** \> **Menus** page.<br><br>* `WatchLimit`: The **Producer** \> **Viewing restrictions** page.<br><br>* `LivePageSettingSecurityControl`: The **Producer** \> **Security control** page.<br><br>* `Antidirt`: The **Producer** \> **Sensitive words** page.<br><br>* `SharePoster`: The **Marketing toolkits** \> **Sharing** page.<br><br>* `Questionnaire`: The **Marketing toolkits** \> **Questionnaires** page.<br><br>* `BindUser`: The **Marketing toolkits** \> **Multi\-platform streaming** page.<br><br>* `LotteryGame`: The **Marketing toolkits** \> **Lucky draws** page.<br><br>* `GiftReward`: The **Marketing toolkits** \> **Gift rewards** page.<br><br>* `MarketingAd`: The **Marketing toolkits** \> **Promotion** page.<br><br>* `ReplayManagement`: The **Playbacks** page.<br><br>* `StatisticsBasicData`: The **Insights** \> **Basic data** page.<br><br>* `StatisticsUserBehaviourData`: The **Insights** \> **Viewer behavior data** page.<br><br>* `LiveSite`: The site\-related pages.<br><br><br>To hide specific features in the embedded page, you can append specific parameters to the embed link. For more information, see [Hiding specific features in embedded pages](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-console#0ad911a5). |
|bgColorPage |Query |The background color of the embedded page. If this parameter is not passed, the background color of your own page will be used by default.<br><br>Follow these steps to get the parameter value:<br><br><br>1. Use any of the following methods to represent the color value:<br><br>   * Color name, such as `red`, `blue`, and `green`.<br><br>   * Hexadecimal color code, such as `#FF0000`, `#0000FF`, and `#00FF00`.<br><br>   * RGB color value, such as `rgb(255, 0, 0)`, `rgb(0, 0, 255)`, and `rgb(0, 255, 0)`.<br><br>2. URL\-encode the color value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986).<br><br><br>For example, to set the background color of the embedded page to blue using the hexadecimal color code, URL\-encode `#0000FF` according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986), resulting in a parameter value of `%230000FF`. |
|appid |Query |Your unique identifier. Contact BytePlus Live technical support to get it. |
|AccessKeyId |Query |Temporary AccessKey ID (AK).<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the AK and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|SecretAccessKey |Query |Temporary Secret Access Key (SK).<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the SK and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|SessionToken |Query |Token required when using temporary credentials.<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the token and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|LoginLivesaasToken |Query |BytePlus Live token.<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the token. Since the token is URL\-encoded in `GetLoginLivesaasSts`, no further encoding is required. |


<span id="d17178a5"></span>
### Embedding features

<span id="7fea9f55"></span>
#### Embedding a full page


* Live room

   
   |Example |Description |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1350 px<br><br>Minimum height: 900 px |
   

   You can embed all the features of a live room.

* Site

   
   |Example |Description |
   |---|---|
   |`https://live.byteplus.com/livesaas/embeded?type=LiveSite&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1000 px<br><br>Minimum height: 500 px |
   |||
   |||
   |||
   

   You can embed the following pages:

   * Site list

   * New site

   * Site information

   * Page configuration


<span id="2e2e42c9"></span>
#### Embedding a single module


|Functional page ||Example |Description |
|---|---|---|---|
|Live control ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 950 px<br><br>Minimum height: 625 px |
|Live control |Menu for chat interaction |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControlMenu&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1100 px<br><br>Minimum height: 500 px |
||Menu for interaction tools |||
||Menu for product cards |||
||Menu for Q&A |||
|Producer |Basic information |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingInfo&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 600 px<br><br>Minimum height: 650 px |
||Appearance |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingAppearance&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 600 px<br><br>Minimum height: 650 px |
||Menus |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MenuBar&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 900 px<br><br>Minimum height: 630 px |
||Viewing restrictions |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=WatchLimit&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1000 px<br><br>Minimum height: 500 px |
||Security control |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LivePageSettingSecurityControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 500 px<br><br>Minimum height: 650 px |
||Sensitive words |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Antidirt&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 800 px<br><br>Minimum height: 500 px |
|Marketing toolkits |Sharing |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=SharePoster&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 500 px<br><br>Minimum height: 650 px |
||Questionnaires |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=Questionnaire&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1000 px<br><br>Minimum height: 500 px |
||Multi\-platform streaming |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=BindUser&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 880 px<br><br>Minimum height: 650 px |
||Lucky draws |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=LotteryGame&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 500 px<br><br>Minimum height: 650 px |
||Gift rewards |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=GiftReward&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 800 px<br><br>Minimum height: 500 px |
||Promotion |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=MarketingAd&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 400 px<br><br>Minimum height: 650 px |
|Playbacks ||`https://live.byteplus.com/livesaas/embeded/178179896233****?type=ReplayManagement&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1400 px<br><br>Minimum height: 650 px |
|Insights |Basic data |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsBasicData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1120 px<br><br>Minimum height: 650 px |
||Viewer behavior data |`https://live.byteplus.com/livesaas/embeded/178179896233****?type=StatisticsUserBehaviourData&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN` |Minimum width: 1300 px<br><br>Minimum height: 650 px |


<span id="0ad911a5"></span>
### Hiding specific features in embedded pages

To hide the left navigation bar in the embedded live room full page, you can append `hideLiveManagementSideMenu=true` to the embed link. A complete embed link is as follows.

```Bash
https://live.byteplus.com/livesaas/embeded/liveManagement/178179896233****?appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveManagementSideMenu=true
```


To hide specific features in the embedded single module page, you can append specific parameters to the embed link. For example, if you want to hide the player after embedding the **Live control** page, you can add `hideLiveControlPlayer=true` to the embed link. A complete embed link is as follows.

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?type=LiveControl&appid=APP_ID&AccessKeyId=ACESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN&hideLiveControlPlayer=true
```


Currently, the supported features and their parameters for hiding are listed in the following table.


|Embedded page |Parameter |Feature |Page screenshot |
|---|---|---|---|
|Live control (`type=LiveControl`) |`hideLiveControlPlayer=true` |Player |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cca3a5efdb0466fb0932b10d02ca32d~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerPopularity=true` |Popularity |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2cf31337bd2d49d492a4e85b04b64d20~tplv-goo7wpa0wc-image.image) </span> |
||`hidePlayerLikes=true` |Likes for the live room |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a5e0f97ac454358988cda9af2164032~tplv-goo7wpa0wc-image.image) </span> |
||`hideAudienceList=true` |Viewer list |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de9b859cf3b541af9c72897add4afd0b~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlChat=true` |Menus |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8fa6761bca2f49aeb24d7feb29346159~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveControlTab=true` |Area under the player |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/640a4ee9c0604db1898a4e15d4cf41c5~tplv-goo7wpa0wc-image.image) </span> |
||`hideWebPush=true` |Web browser |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a7c521be3ef0437ea304025efea5617c~tplv-goo7wpa0wc-image.image) </span> |
||`hidePullStream=true` |Pull stream |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fd744ff8a47499d8abf60b43ad5b480~tplv-goo7wpa0wc-image.image) </span> |
||`hideLoopVideo=true` |Prerecorded video |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/161686b58e004ef0be1eb6d1570c2737~tplv-goo7wpa0wc-image.image) </span> |
||`hidePushStream=true` |Push stream |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a6b117873b4d44df9f5ba9cfe3f76204~tplv-goo7wpa0wc-image.image) </span> |
||`hidePopularity=true` |Interaction popularity |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21110daf8c6145998571143b8ed6ddd3~tplv-goo7wpa0wc-image.image) </span> |
||`hideLiveScreenData=true` |Data dashboard |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b391d8c2048643a8b673f79fc8fe910c~tplv-goo7wpa0wc-image.image) </span> |
||`hideVideoEdit=true` |Clip live stream |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/edaba5f530084510af1cda766e250f0f~tplv-goo7wpa0wc-image.image) </span> |
|Producer \> Basic information (`type=LivePageSettingInfo`) |`hideSettingBasic=true` |Basic settings |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9bccd4d9652451b8902795cee587b9e~tplv-goo7wpa0wc-image.image) </span> |
||`hideSettingAdvanced=true` |Advanced settings |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7daef71e9a22426283b5e8e47b365cca~tplv-goo7wpa0wc-image.image) </span> |
|Producer \> Security control (`type=LivePageSettingSecurityControl`) |`hideSecurityControlBasic=true` |Basic settings |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3780cf6efd144d37855427f8cdd4f20b~tplv-goo7wpa0wc-image.image) </span> |
||`hideSecurityControlWatermark=true` |Full\-screen watermark |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8dc669a1726b4d0d9f797a3e2e18de01~tplv-goo7wpa0wc-image.image) </span> |
|Marketing toolkits \> Lucky draws (`type=LotteryGame`) |`hideRealtimeLottery=true` |Real\-time lucky draws |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae073f2829144cd886c59e02a9dde0b9~tplv-goo7wpa0wc-image.image) </span> |
||`hideTaskAward=true` |Watch time\-based lucky draws |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/450b51850da743eda1028cad973624cc~tplv-goo7wpa0wc-image.image) </span> |
||`hideLotteryLib=true` |Prize library |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1ec96e6f99140dfbb117654d34d57d3~tplv-goo7wpa0wc-image.image) </span> |
|Marketing toolkits \> Promotion (`type=MarketingAd`) |`hideAdBrand=true` |Host/Brand account |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/92128f5fac3745e9ab4761b529fc2704~tplv-goo7wpa0wc-image.image) </span> |
||`hideGuide=true` |Splash page |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50694e3566ab4214acf8002937e6600e~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageHeadAd=true` |Header ad |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d0fd7446c3a34f2a886d409355026df3~tplv-goo7wpa0wc-image.image) </span> |
||`hidePageMiddleAd=true` |In\-page ads |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/198e04d004ef4f28a92ed5bdf7f153a5~tplv-goo7wpa0wc-image.image) </span> |
||`hideFloatAd=true` |Floating ad |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/256cca86693d41e88bbcec67a08d8373~tplv-goo7wpa0wc-image.image) </span> |
|Playbacks (`type=ReplayManagement`) |`hideUploadVideoBtn=true` |Upload video |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4caae8f28eef4d199f07dec54f9b3704~tplv-goo7wpa0wc-image.image) </span> |
||`hideImportFromVideoLib=true` |Select from video library |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3eb70168ec4b4ebf8d5b9333c425381c~tplv-goo7wpa0wc-image.image) </span> |


<span id="8c3d70c2"></span>
## Sample code

The following sample code is applicable to JavaScript. If you choose to generate the embed link using another language, rewrite it according to the specifications of that language.

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
        // Call GetLoginLivesaasSts to get the STS signature.
        var result = await GetLoginLivesaasSts();
        var activities = await listActivityAPI();
        var activityId = activities[0].ID;
        var params = {
          AccessKeyId: result.StsMsg.AccessKeyId,
          SecretAccessKey : result.StsMsg.SecretAccessKey,
          SessionToken: result.StsMsg.SessionToken,
          Type: 'LiveControlMenu',
          AppId: 'AppId', // Your unique identifier. Contact BytePlus Live technical support to get it.
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
