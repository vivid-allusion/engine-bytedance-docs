---
title: "PlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/playerview"
---

The player component of a live room.

```java
public class com.bytedance.live.sdk.player.view.PlayerView extends FrameLayout
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to use the <code>PlayerView</code> instance when integrating the default player, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#4b8efe3c">Default player</a>.</div>


<span id="a4a89053"></span>
## Member Functions

<span id="c6fff5e6"></span>
### PlayerView

Creates a `PlayerView` instance.

```java
public PlayerView(Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>PlayerView</code> instance automatically releases resources in the <code>onDetachedFromWindow</code> callback, so manual release is not required.</div>


**Return Value**

The `PlayerView` instance.

<span id="8d4ad319"></span>
### play

Plays the video.

```Java
public void play()
```


<span id="41fc784c"></span>
### pause

Pauses the video.

```Java
public void pause()
```
