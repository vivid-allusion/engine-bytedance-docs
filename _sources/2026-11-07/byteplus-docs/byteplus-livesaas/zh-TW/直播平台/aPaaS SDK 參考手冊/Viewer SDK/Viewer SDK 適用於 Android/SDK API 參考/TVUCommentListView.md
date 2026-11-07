---
title: "TVUCommentListView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvucommentlistview-zh-TW"
---

直播間的聊天組件，用於整合到您自己的頁面中。必須與[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW)一起使用。

```Java
public class TVUCommentListView extends FrameLayout
```


<span id="671c236e"></span>
## 成員函數

<span id="f1bc0bc7"></span>
### TVUCommentListView

建立`TVUCommentListView`實例。

```Java
public TVUCommentListView(@NonNull Context context)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|context |Context |直播間頁面的上下文。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">當<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW">TVULiveRoomServer</a>被銷毀時，<code>TVUCommentListView</code>實例會自動釋放資源，因此無需手動清理。</div>


**返回值**

`TVUCommentListView`實例。

<span id="838c8d63"></span>
### attachRoomServer

將`TVUCommentListView`實例綁定到[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW)實例。綁定後，`TVUCommentListView`實例會自動初始化。

```Java
public void attachRoomServer(TVULiveRoomServer server)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|server |TVULiveRoomServer |要綁定的[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW)實例。 |


<span id="990aafd5"></span>
### setShowCommentBottomBar

設定是否顯示底部評論文字框。

```Java
public void setShowCommentBottomBar(boolean showCommentBottomBar)
```


**輸入參數**


|名稱 |類型 |描述 |
|---|---|---|
|showCommentBottomBar |Boolean |是否顯示底部評論文字框。預設值：`true`。<br><br><br>* `true`：顯示。<br><br>* `false`：不顯示。 |
