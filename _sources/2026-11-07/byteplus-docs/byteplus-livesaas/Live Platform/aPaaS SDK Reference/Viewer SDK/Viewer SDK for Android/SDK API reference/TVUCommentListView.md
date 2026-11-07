---
title: "TVUCommentListView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvucommentlistview"
---

The chat component of a live room, which is used for integrating into your own page. It must be used in conjunction with the [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver).

```Java
public class TVUCommentListView extends FrameLayout
```


<span id="671c236e"></span>
## Member Functions

<span id="f1bc0bc7"></span>
### TVUCommentListView

Creates a `TVUCommentListView` instance.

```Java
public TVUCommentListView(@NonNull Context context)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|context |Context |The context of the live room page. |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The <code>TVUCommentListView</code> instance automatically releases resources when <a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver">TVULiveRoomServer</a> is destroyed, so manual release is not required.</div>


**Return Value**

The `TVUCommentListView` instance.

<span id="838c8d63"></span>
### attachRoomServer

Binds the `TVUCommentListView` instance to the [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver) instance. When bound, the `TVUCommentListView` instance performs initialization internally.

```Java
public void attachRoomServer(TVULiveRoomServer server)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|server |TVULiveRoomServer |The [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver) instance to be bound. |


<span id="990aafd5"></span>
### setShowCommentBottomBar

Sets whether to display the comment text box at the bottom.

```Java
public void setShowCommentBottomBar(boolean showCommentBottomBar)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|showCommentBottomBar |Boolean |Whether to display the comment text box at the bottom. Default value: `true`.<br><br><br>* `true`: Display.<br><br>* `false`: Do not display. |
