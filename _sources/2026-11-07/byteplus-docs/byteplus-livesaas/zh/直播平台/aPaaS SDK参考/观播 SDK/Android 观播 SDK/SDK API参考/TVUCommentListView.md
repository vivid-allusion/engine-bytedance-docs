---
title: "TVUCommentListView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvucommentlistview-zh-CN"
---

用于集成到你自己的页面的直播间聊天组件。必须与[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN)配合使用。

```Java
public class TVUCommentListView extends FrameLayout
```


<span id="671c236e"></span>
## 成员函数

<span id="f1bc0bc7"></span>
### TVUCommentListView

创建一个`TVUCommentListView`实例。

```Java
public TVUCommentListView(@NonNull Context context)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|context |Context |直播间页面的context。 |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">当<a href="https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN">TVULiveRoomServer</a>被销毁时，<code>TVUCommentListView</code>实例会自动释放资源，无需手动清理。</div>


**返回值**

`TVUCommentListView`实例。

<span id="838c8d63"></span>
### attachRoomServer

将`TVUCommentListView`实例绑定到[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN)实例。绑定后，`TVUCommentListView`实例会自动初始化。

```Java
public void attachRoomServer(TVULiveRoomServer server)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|server |TVULiveRoomServer |要绑定的[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN)实例。 |


<span id="990aafd5"></span>
### setShowCommentBottomBar

设置是否显示底部评论输入框。

```Java
public void setShowCommentBottomBar(boolean showCommentBottomBar)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|showCommentBottomBar |Boolean |是否显示底部评论输入框。默认值：`true`。<br><br><br>* `true`：显示。<br><br>* `false`：不显示。 |
