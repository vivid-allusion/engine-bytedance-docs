---
title: "PlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/playerview-zh-CN"
---

PlayerView 是在直播间中实现视频播放的核心 UI 组件。本文档概述了 PlayerView 类，包括如何构建其实例，以及如何使用其主要方法（如 play() 和 pause()）来管理视频码流。

```java
public class com.bytedance.live.sdk.player.view.PlayerView extends FrameLayout
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需了解在集成完整播放器时如何使用<code>PlayerView</code>实例，请参见<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#4b8efe3c">完整播放器</a>。</div>


<span id="a4a89053"></span>
## 成员函数

<span id="c6fff5e6"></span>
### PlayerView

创建一个`PlayerView`实例。

```java
public PlayerView(Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |用于展示直播间的 Activity 的 Context。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>PlayerView</code>实例会在<code>onDetachedFromWindow</code>回调中自动释放资源，因此无需手动释放。</div>


**返回值**

新的`PlayerView`实例。

<span id="8d4ad319"></span>
### play

播放视频。

```Java
public void play()
```


<span id="41fc784c"></span>
### pause

暂停视频。

```Java
public void pause()
```
