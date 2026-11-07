---
title: "Type definitions"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions"
---

<span id="5ed875e7"></span>
## BdlActivityConfig

```Dart
class BdlActivityConfig {
    final int activityId;
    final String token;
    final BdlViewerAuthMode authMode;
    final bool isPortrait;
}
```


The information required to join a live room.

**Input parameters**


|Name |Type |Description |
|---|---|---|
|activityId |Integer |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|token |String |The authorization token required to join the live room. You can get the token by calling [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi). |
|authMode |BdlViewerAuthMode |The authentication mode of the live room. For more information, see [BdlViewerAuthMode](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#415010a6). |
|isPortrait |Boolean |Whether the live room is in portrait mode.<br><br><br>* `true`: In portrait mode.<br><br>* `false`: In landscape mode. |


<span id="0c2adc1a"></span>
## BdlViewerOpenUrlType

```Dart
enum BdlViewerOpenUrlType {
    pageHeaderAd,
    pageAd,
    floatingAd,
    cardAd,
}
```


The type of content to which the embedded link belongs.

**Enumerated value**


|Type |Value |Description |
|---|---|---|
|pageHeaderAd |0 |Header ads. |
|pageAd |1 |In\-page ads. |
|floatingAd |2 |Floating ads. |
|cardAd |3 |Product cards, including those displayed under the menu and floating product cards. |


<span id="415010a6"></span>
## BdlViewerAuthMode

```Dart
enum BdlViewerAuthMode {
    public,
    custom,
}
```


The authentication mode of a live room.

**Enumerated value**


|Type |Value |Description |
|---|---|---|
|public |0 |Public mode. Viewers join the live room as guests. They must enter a nickname to register before performing actions that require user information, such as commenting or liking comments. |
|custom |1 |Custom mode. Viewers join the live room using their user information from your app, allowing them to directly comment and like comments. |


<span id="4b59aa3f"></span>
## BdLiveViewerConfig

```Dart
class BdLiveViewerConfig {
  BdLivePlayerConfig playerConfig = BdLivePlayerConfig();
}
```


Configuration of the viewing page.

**Input parameters**


|Name |Type |Description |
|---|---|---|
|playerConfig |BdLivePlayerConfig |The player configuration. For more information, see [BdLivePlayerConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-flutter-type-definitions#b4ff383c). |


<span id="b4ff383c"></span>
## BdLivePlayerConfig

```Dart
class BdLivePlayerConfig {
  bool liveAutoPlay = true;
  bool replayAutoPlay = true;
  bool previewAutoPlay = true;
  bool enablePIP = true;
  bool enablePIPWhenExit = true;
}
```


The player configuration.

**Input parameters**


|Name |Type |Description |
|---|---|---|
|liveAutoPlay |Boolean |Whether to automatically play the live video if the live room is in the **Live** status. Default value: `true`. Valid values:<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |
|replayAutoPlay |Boolean |Whether to automatically play the playback if the live room is in the **Playback** status. Default value: `true`. Valid values:<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |
|previewAutoPlay |Boolean |Whether to automatically play the preview if the live room is in the **Preview** status and a preview is available. Default value: `true`. Valid values:<br><br><br>* `true`: Automatically play.<br><br>* `false`: Do not automatically play. |
|enablePIP |Boolean |Whether to enable the PiP feature when viewers leave the live room, open a new page by tapping a URL (including URLs embedded in product cards and ads), or move the app to the background. Default value: `true`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
|enablePIPWhenExit |Boolean |Whether to enable the PiP feature only when viewers leave the live room. Default value: `true`. Valid values:<br><br><br>* `true`: Enable.<br><br>* `false`: Disable. |
