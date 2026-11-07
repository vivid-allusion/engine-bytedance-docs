---
title: "Using an iframe to embed the AI Live console"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console"
---

To integrate AI Live console features directly into your own website, you can embed AI Live pages such as live room lists and model training pages using an iframe. This guide shows you how to construct the embed link, allowing you to provide seamless management capabilities within your own page while reducing development costs.

## Notes

* This approach supports PC platforms only and is not available on H5 pages.

* Pop\-ups can only be centered within the embedded functional page but cannot be centered on your own page.

## Prerequisites

* To ensure the embedded pages can be accessed, make sure your own page uses an HTTPS domain.

* Use the BytePlus account or an IAM user with the super administrator role to call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts).

## Supported pages

Currently, you can use iframe to embed the following pages into your own page. The minimum width is 1000 px and the minimum height is 500 px.

|Pages ||Page screenshot |Example links |
|---|---|---|---|
|AI Live control ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4df3dafa05274d24b174cb6066e91d5b~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/185304025******?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|AI Live room list ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70e5cd96b39246bba2b2e87e431cb7ca~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveRoom&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|Model training |Avatar |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/788ce1a99b11417582561a716cc81a88~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveAvatarTraining&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
||Voice |![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/afba3dda9fff406ba6f40d20e7dd559f~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveVoiceTraining&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|Product Library ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64e59a2efda549158e822484dff69476~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveProducts&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|Material Library ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f487c4f1b874f5ea1e9478c2bff0962~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveMaterials&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|Knowledge base ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f62095fd5474bd6bf38002dd2284bae~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveKnowledgeBase&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|Service center ||![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31b900cd923349edb83e1b4933fdd766~tplv-goo7wpa0wc-image.image)<br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63083c31f2d24c11b0c91b3d0f73c0ee~tplv-goo7wpa0wc-image.image) |```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveServiceCenter&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br><br><br>> **注意**<br><br><br>> The **Service center** page for AI Live is available only to the main account. Subaccounts do not have access to the **Service center** page.<br> |

## Process

To embed the AI Live console, follow these steps:

1. **Add a super administrator IAM user**: Create an IAM user for BytePlus Live and grant it the super administrator role.

2. **Get the AK and SK**: Get the AccessKey (AK) and SecretKey (SK) of the IAM user. Alternatively, get the AK and SK of the BytePlus account. Either option works.

3. **Call GetLoginLivesaasSts to get temporary credentials**: Use the AK/SK to call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to obtain the temporary AK, SK, and session token, as well as the BytePlus Live token.

4. **Build the embed link**: Build the embed link for the target functional page using the temporary credentials.

![](data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI3OTVweCIgaGVpZ2h0PSIxODVweCIgdmlld0JveD0iLTAuNSAtMC41IDc5NSAxODUiPjxkZWZzLz48Zz48cGF0aCBkPSJNIDEyMiAzMiBMIDE5NS42MyAzMiIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDIwMC44OCAzMiBMIDE5My44OCAzNS41IEwgMTk1LjYzIDMyIEwgMTkzLjg4IDI4LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyIiB5PSIyIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMycHg7IG1hcmdpbi1sZWZ0OiAzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFkZCBhIEJ5dGVQbHVzIExpdmUgSUFNIHVzZXIgd2l0aCB0aGUgc3VwZXIgYWRtaW5pc3RyYXRvcnMgcm9sZTxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMzIgTCAzNjIgMzIgTCAzNjIgODIgTCAzOTUuNjMgODEuOTciIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0MDAuODggODEuOTYgTCAzOTMuODkgODUuNDcgTCAzOTUuNjMgODEuOTcgTCAzOTMuODggNzguNDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjIiIHdpZHRoPSIxMjAiIGhlaWdodD0iNjAiIHJ4PSI5IiByeT0iOSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIElBTSB1c2VyPC9kaXY+PC9kaXY+PHNwYW4+PC9zcGFuPjxkaXY+PGRpdj48L2Rpdj48L2Rpdj48c3Bhbj48L3NwYW4+PGRpdj48ZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSAzMjIgMTUyIEwgMzYyIDE1MiBMIDM2MiA4NyBMIDM5NS42MyA4NyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQwMC44OCA4NyBMIDM5My44OCA5MC41IEwgMzk1LjYzIDg3IEwgMzkzLjg4IDgzLjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cmVjdCB4PSIyMDIiIHk9IjEyMiIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI2MCIgcng9IjkiIHJ5PSI5IiBmaWxsPSIjZmZmZmZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNTJweDsgbWFyZ2luLWxlZnQ6IDIwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+R2V0IHRoZSBBSyBhbmQgU0sgb2YgdGhlIEJ5dGVQbHVzIGFjY291bnQ8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNTcyIDg3IEwgNjQ1LjYzIDg3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjUwLjg4IDg3IEwgNjQzLjg4IDkwLjUgTCA2NDUuNjMgODcgTCA2NDMuODggODMuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxyZWN0IHg9IjQwMiIgeT0iNDIiIHdpZHRoPSIxNzAiIGhlaWdodD0iOTAiIHJ4PSIxMy41IiByeT0iMTMuNSIgZmlsbD0iI2ZmZmZmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTY4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogODdweDsgbWFyZ2luLWxlZnQ6IDQwM3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj48ZGl2PjxkaXY+Q2FsbCBHZXRMb2dpbkxpdmVzYWFzU3RzIHRvIGdldCB0aGUgdGVtcG9yYXJ5IEFLLCBTSywgdG9rZW4gcmVxdWlyZWQgd2hlbiB1c2luZyB0ZW1wb3JhcnkgY3JlZGVudGlhbHMsIGFuZCBCeXRlUGx1cyBMaXZlIHRva2VuPC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTIiIHk9IjYyIiB3aWR0aD0iMTQwIiBoZWlnaHQ9IjYwIiByeD0iOSIgcnk9IjkiIGZpbGw9IiNmZmZmZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDEzOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDkycHg7IG1hcmdpbi1sZWZ0OiA2NTNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxMnB4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgd2hpdGUtc3BhY2U6IG5vcm1hbDsgd29yZC13cmFwOiBub3JtYWw7ICI+PGRpdj48ZGl2PkNvbmNhdGVuYXRlIHRoZSBlbWJlZCBsaW5rIGFzIG5lZWRlZDwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==)

## **Link parameters**

```Plain
https://live.byteplus.com/livesaas/embeded/178179896233****?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN
```

|Link/Parameter |Location |Description |
|---|---|---|
|https://live.byteplus.com/livesaas/embeded/ |URL |The base URL for the embed link. |
|178179896233\*\*\*\* |URL |The activity ID of the live room, which only needs to be configured when embedding the AI Live control page. You can get the activity ID by calling [ListActivityAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi). For example, to embed the AI Live control page, the link is as follows:<br><br>```Plain```<br>```https://live.byteplus.com/livesaas/embeded/185304025******?AppId=AILive&type=AILiveStudio&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br> |
|AppId |Query |The unique identifier for embedding AI Live pages. Fixed value: `AILive`. |
|type |Query |Specifies the functional page to embed. For example links, see [Supported pages](https://docs.byteplus.com/docs/byteplus-livesaas/using-iframe-to-embed-the-ai-live-console#924ba3eb).<br><br>For example, the parameter value \*\*`AILiveRoom` \*\*refers to the **AI Live room list** page. The link is as follows:<br><br>```Plain```<br>```https://live.byteplus.com/livesaas/embeded/?AppId=AILive&type=AILiveRoom&AccessKeyId=ACCESS_KEY_ID&SecretAccessKey=SECRET_ACCESS_KEY&SessionToken=SESSION_TOKEN&LoginLivesaasToken=LIVESAAS_TOKEN```<br><br><br>Valid values:<br><br><br>* **AILiveRoom**: The AI Live room list page.<br><br>* **AILiveAvatarTraining**: The Model training \> Avatar page.<br><br>* **AILiveVoiceTraining**: The Model training \> Voice page.<br><br>* **AILiveProducts**: The Product Library page.<br><br>* **AILiveMaterials**: The Material Library page.<br><br>* **AILiveKnowledgeBase**: The Knowledge base page.<br><br>* **AILiveServiceCenter**: The Service center page.<br><br>* **AILiveStudio**: The AI Live control page. When embedding the AI Live control page, you need to add the activity ID of the live room as well. |
|AccessKeyId |Query |The temporary AccessKey ID (AK).<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the AK and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|SecretAccessKey |Query |The temporary Secret Access Key (SK).<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the SK and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|SessionToken |Query |The token required when using temporary credentials.<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the token and URL\-encode the value according to [RFC3986](https://datatracker.ietf.org/doc/html/rfc3986). |
|LoginLivesaasToken |Query |The BytePlus Live token.<br><br>Call [GetLoginLivesaasSts](https://docs.byteplus.com/en/docs/byteplus-livesaas/getloginlivesaassts) to get the token. The token returned by the `GetLoginLivesaasSts` call is already URL\-encoded, so no further encoding is necessary. |

## Sample code

The following sample code uses JavaScript. If you generate the embed link using another language, adapt the code accordingly.

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
          // The page to embed. Replace with the target page's value,
          // e.g. AILiveRoom, AILiveAvatarTraining, AILiveVoiceTraining,
          // AILiveProducts, AILiveMaterials, AILiveKnowledgeBase.
          Type: 'AILiveStudio',
          AppId: 'AILive', // The unique identifier for embedding AI Live pages. Fixed value: AILive.
        } 
        // Note: /${activityId} applies only to the AI Live control page. For other pages, use: https://live.byteplus.com/livesaas/embeded/?${...}
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
