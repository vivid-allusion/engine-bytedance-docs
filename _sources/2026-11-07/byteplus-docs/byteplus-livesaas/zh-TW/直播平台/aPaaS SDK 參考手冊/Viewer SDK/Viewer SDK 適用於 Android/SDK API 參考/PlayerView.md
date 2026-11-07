---
title: "PlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/playerview-zh-TW"
---

PlayerView 是在直播間內實現視頻播放的核心 UI 元件。本文檔將概述 PlayerView 類別，包括如何建立實例，以及如何使用其主要方法（如 play() 和 pause()）來管理視頻流。

```java
public class com.bytedance.live.sdk.player.view.PlayerView extends FrameLayout
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需了解在集成預設播放器時如何使用 <code>PlayerView</code> 實例，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#4b8efe3c">預設播放器</a>。</div>


<span id="a4a89053"></span>
## 成員函數

<span id="c6fff5e6"></span>
### PlayerView

建立一個 `PlayerView` 實例。

```java
public PlayerView(Context context)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|context |Context |用於顯示直播間的 Activity 的 Context。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>PlayerView</code> 實例會在 <code>onDetachedFromWindow</code> 回調中自動釋放資源，因此無需手動釋放。</div>


**返回值**

新的 `PlayerView` 實例。

<span id="8d4ad319"></span>
### play

播放視頻。

```Java
public void play()
```


<span id="41fc784c"></span>
### pause

暫停視頻。

```Java
public void pause()
```
