---
title: "Android 观播 SDK：高级功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN"
---

要在你的 Android 应用中打造独特且深度集成的直播观看体验，可以使用 Android 观播 SDK 的高级功能。本指南提供了逐步操作说明和代码示例，帮助你实现自定义登录流程、覆盖默认重定向和退出行为，并对 UI 在竖屏和横屏模式下进行深度定制。

<span id="bcd7a14a"></span>
## 前提条件


* 完成 [集成 Android 观播 SDK](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android-zh-CN) 中的前 5 步。

* 需要集成以下内容。

   * 集成基础功能以自定义视频缩放模式。更多信息，请参见 [Android 观播 SDK：基础功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN)。

   * 集成完整直播间，以实现本主题描述的其他高级功能。更多信息，请参见 [完整直播间](https://docs.byteplus.com/docs/byteplus-livesaas/docs-basic-for-viewer-sdk-for-android-zh-CN#d27888d9)。


<span id="77b0428c"></span>
## 功能

本主题介绍如何集成以下功能。


* [自定义登录](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e54b3982)

* [自定义跳转逻辑](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#69a798ec)

* [完整直播间的自定义退出行为](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#0dc820f5)

* [横屏模式直播间的 UI 自定义](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#31413a88)

* [竖屏模式直播间UI自定义](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#3657f7b5)

* [常用 UI 个性化功能](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#92cb972c)

   * [视频缩放模式](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#1d02978f)

   * [关闭完整直播间的图标](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#5b9de944)

   * [悬浮互动工具](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#b68426af)

   * [商品卡片菜单高度](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e52a2874)


<span id="e54b3982"></span>
## 自定义登录

如需让观众先登录你的应用，再观看直播流、参与评论和互动等，可以选择自定义登录方式。此方式允许观众使用已有的应用账号加入直播间。

你可以配置观众何时被提示登录。


* 观众先登录你的应用，然后加入直播间。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca690e7373748d4a3f86cdd0b3c0b1e~tplv-goo7wpa0wc-image.image) </span>

   1. 观众登录应用并加入直播间后，你需要调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `2`，以获取授权 token。

   2. 获取 token 后，调用 SDK 的 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1) 方法加入直播间。

   示例代码如下。

   ```Java
   long activityId = 1721010849258****;  // 直播间的活动 ID。
   String token = "ak3T%2FdaGJDL5zSFD7%2F1GPGP****wx0zaTfQ1M4Dahp8%3D";  //  当 Mode 的值为 2 时的授权令牌。
   TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.CUSTOM; // 自定义模式。
   boolean isPortrait = true; // 竖屏模式下的直播间。
   TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
   ```
   

* 观众先加入直播间，观看直播流、查看评论等。当观众进行评论和互动等操作时，将触发登录流程，认证模式由公开模式切换为自定义模式。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4ae17f6d5f425ab21012288dc119a9~tplv-goo7wpa0wc-image.image) </span>

   1. 观众首先以公开模式加入直播间。

   2. 你需要实现公开模式下获取授权 token 的方法。然后，调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `1`，以获取 token。

   3. 调用 [setCustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#ad65c19c) 方法，在公开模式下设置登录你自有账号系统的监听器。

   4. 调用 SDK 的 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-CN#b20db0d1) 方法加入直播间。

   5. 当观众执行以下需要用户信息的操作时，将触发应用的自定义登录流程：

      * 点击菜单下聊天互动的评论输入框

      * 点赞评论

      * 为主播送礼

      * 点击预约按钮预约直播流

      * 答题

      * 投票

      * 抽奖

      * 非匿名问卷

   6. SDK 会触发 [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#d3799085) 回调，通知你的应用观众需要进行自定义登录。你需要实现自定义模式下获取授权 token 的方法。观众完成自定义登录后，调用 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-CN)，并将 `Mode` 的值设置为 `2`，以获取 token。

   7. 当观众自定义登录成功、失败或取消时，会触发 [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cb937422) 回调，通知 SDK 观众的登录结果。

      * 登录成功时，将自定义模式 token 传递给 SDK。

      * 登录失败或取消时，将 null 值传递给 SDK。

   8. SDK 使用 token 向 BytePlus Live 请求观众信息。

   9. 在验证 token 有效后，BytePlus Live 会将观众信息传递给 SDK。如果 token 验证失败或 token 为空，BytePlus Live 会将错误信息传递给 SDK。

   示例代码如下。

   ```Java
   // 设置公有模式下登录自有账号系统的监听器。
   CustomSettings settings = CustomSettings.Holder.mSettings;
   settings.setCustomLoginListener((context, activityId, callBack) -> {
       //  触发 onCustomLoginStart 回调后，执行应用的自定义登录逻辑。此处以展示自定义登录对话框为例。你可以根据需要将观众重定向到指定的自定义登录页面。
       new AlertDialog.Builder(context)
               .setTitle("Custom login")
               .setView(editText)
               .setCancelable(false)
               .setPositiveButton(android.R.string.yes, (dialog, which) -> {
                   // 在本示例中，观众需要输入令牌。onLoginFinished 回调在观众自定义登录成功时触发，并将自定义模式下的令牌传递给 SDK。在传递令牌给 SDK 前，调用 URLDecoder.decode 方法对令牌进行解码。
                   String token = editText.getText().toString().trim();
                   callBack.onLoginFinished(URLDecoder.decode(token));
               })
               // onLoginFinished 回调在观众自定义登录失败或取消时触发，并将 null 值传递给 SDK。
               .setNegativeButton(android.R.string.no, ((dialog, which) -> callBack.onLoginFinished(null)))
               .setIcon(android.R.drawable.ic_dialog_alert)
               .show();
   });       
   ```
   


<span id="69a798ec"></span>
## 自定义跳转逻辑

当观众在直播间点击以下项目时，SDK 会执行默认跳转行为：


* 菜单下显示的商品卡片

* 商品浮窗

* 页头广告

* 页中广告

* 浮标广告

* 主播账号

* 评论中的 URL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">关于如何在 BytePlus Live 控制台配置商品卡片、页头广告、页中广告、浮标广告和主播账号的更多信息，请参见 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream-zh-CN">管理商品卡片</a>、<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-logo-and-ads-zh-CN">添加广告</a> 和 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account-zh-CN">将主播账号关联到直播间</a>。</div>


调用 [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#be1306ce) 方法设置直播间链接点击事件监听器后，观众点击这些项目时，SDK 会触发 [redirectPage](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#381d7dca) 回调。你可以通过返回值决定在执行自定义跳转逻辑时是否拦截默认跳转行为。


* 返回 `true`：拦截默认跳转行为。

* 返回 `false`：不拦截默认跳转行为。


以下示例代码仅在观众点击浮标广告、菜单下的商品卡片和商品浮窗时执行自定义跳转逻辑；当观众点击页头广告、页中广告、主播账号和评论中的 URL 时，同时执行自定义跳转逻辑和默认跳转行为。

```Java
// Set the listener for link tap events in the live room.
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /**
*
*@paramliveActivity 直播间所在的 Activity。
*@paramredirectInfo 实现自定义跳转逻辑所需的信息。
*@return 是否拦截 SDK 的默认跳转行为。true: 拦截默认跳转行为。false: 不拦截默认跳转行为。*/
    @Override
    public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo) {
        // 通过 entrance 字段判断点击事件的入口。
        String entrance = redirectInfo.getEntrance();
        switch (redirectInfo.getContentType()) {
            case RedirectInfo.CONTENT_TYPE_URL:
                // 当内容类型为 URL 时，获取 urlRedirectInfo 字段。
                UrlRedirectInfo urlRedirectInfo = redirectInfo.getUrlRedirectInfo();
                // 当观众点击浮标广告时
                if (entrance.equals(Entrance.FLOATING_ADVERTISEMENT.value)) {
                    //  执行自定义跳转逻辑。此处以展示 SDK 内部的 WebViewDialog 为例。你也可以使用自定义的 Dialog。
                    new CommonWebViewDialog(liveActivity, urlRedirectInfo.getUrl(),
                            com.bytedance.live.sdk.R.style.TvuLiveBottomDialog).show();
                    // 执行自定义跳转逻辑，但不执行默认跳转行为。
                    return true;
                }
                // 当观众点击菜单下的商品卡片或商品浮窗时
                if (entrance.equals(Entrance.FLOATING_SHOPPING_CARD.value)) {
                    String productUrl = urlRedirectInfo.getUrl();
                    ToastUtil.displayToast("click : " + productUrl);
                    // 执行自定义跳转逻辑。此处以跳转到商品详情 Activity 为例。
                    startActivities(new Intent[]{new Intent(MainActivity.this, ProductActivity.class)});
                    // 执行自定义跳转逻辑，但不执行默认跳转行为。
                    return true;
                }
        }
        // 同时执行自定义跳转逻辑和默认跳转行为。
        return false;
    }
});                
```


自定义跳转逻辑的功能、`entrance` 字段值以及观看页上的位置如下表所示。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本主题以竖屏模式下移动设备观看页的位置为例。关于 PC 或移动设备横屏模式下观看页的位置，请参见对应文档。</div>


&nbsp;


|功能 |`entrance` 字段值 |观看页的位置 |
|---|---|---|
|菜单下展示的商品卡片 |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8abeef62ca8446bb8ff5168977d96bc2~tplv-goo7wpa0wc-image.image) </span> |
|商品浮窗 |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55f44ed1cf794259b21ad471927464c5~tplv-goo7wpa0wc-image.image) </span> |
|页头广告 |`HEADER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe65ff843f54cf1a8c28ea8e075cc70~tplv-goo7wpa0wc-image.image) </span> |
|页中广告 |`BANNER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1467ed744c9c411baf7b0a94bf6e9d5b~tplv-goo7wpa0wc-image.image) </span> |
|浮标广告 |`FLOATING_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1932e1f10c8445d0941c623d9852f091~tplv-goo7wpa0wc-image.image) </span> |
|主播账号头像或名称 |`BUSINESS_ACCOUNT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3433b3a664104b0aa1bf92d12d540e90~tplv-goo7wpa0wc-image.image) </span> |
|评论中的 URL |`COMMENT_LINK` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a1b2f7c4564b9986a132206c72562f~tplv-goo7wpa0wc-image.image) </span> |


默认情况下，只有主播评论中的 URL 可点击。你可以通过 [setAudienceCommentLinkClickable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#4d6e871a) 方法设置观众评论中的 URL 可点击。

示例代码如下。

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setAudienceCommentLinkClickable(true);
```


<span id="0dc820f5"></span>
## 完整直播间的自定义退出行为

默认情况下，观众在完整直播间点击退出按钮或物理返回键时会退出完整直播间。如果正在播放直播或点播视频，且观众在移动设备上开启了悬浮窗权限，默认行为是退出完整直播间并显示悬浮窗，即画中画（PiP）。

调用 [setLiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#59235a7d) 方法设置完整直播间退出事件监听器后，观众点击退出按钮或物理返回键退出完整直播间时，SDK 会触发 [onClickExitLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#f195449a) 回调。你可以通过返回值决定是否拦截此默认行为并执行自定义退出逻辑。


* 返回 `true`：拦截默认点击行为。

* 返回 `false`：不拦截默认点击行为。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">从 Android 观播 SDK 1.33.0 版本开始，<a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#f195449a">onClickExitLiveRoom</a> 回调支持根据返回值决定是否拦截默认点击行为。若未集成指定 SDK 版本，则默认点击行为始终被拦截。</div>


以下示例代码仅执行完整直播间的自定义退出行为，不执行默认点击行为。

```Java
// Set the listener for exit events of the full-featured live room.
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setLiveRoomActionListener(context -> {
    ToastUtil.displayToast("Custom exit behavior of the full-featured live room");
    TVULiveRoom.leaveLiveRoom(MainActivity.this); // Execute the custom exit behavior of the full-featured live room.
    return true; // 仅支持 Android 观播 SDK 1.33.0 及以上版本。
});
```


<span id="31413a88"></span>
## 横屏模式直播间的 UI 自定义

集成完整直播间后，你可以自定义横屏模式直播间的 UI。

<span id="0a538de3"></span>
### Step 1: 获取 `TvuLivePlayerLayoutBinding` 实例

SDK触发[onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cfe9163a)回调后，可以使用获取到的`ViewBinding`实例自定义横屏模式直播间的UI。

示例代码如下。

```Java
public interface LiveRoomStatusListener {
    ...
    default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


获取到的`ViewBinding`实例的UI结构如下。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c407244d106c4cbfa06d6464424899e1~tplv-goo7wpa0wc-image.image) </span>

```Plain
rootContainer(FrameLayout)
|-- contentContainer(LinearLayout)
    |-- headContainer(LinearLayout)
        |-- headTvuContainer
    |-- livePlayerContainer(FrameLayout)
        |-- livePlayerCardView(TVUAspectRatioCardView)
            |-- tvu_player_view(PlayerView)
    |-- midContainer(LinearLayout)
        |-- midTvuContainer     
    |-- bottomTvuMenuContainer        
|-- floatingContainer(FrameLayout)
    |-- tvuFloatingViewsContainer
```



* `contentContainer`（内容容器）包含四个容器：`head`（`headContainer`）、播放器（`livePlayerContainer`）、`mid`（`midContainer`）和`bottomMenu`（`bottomTvuMenuContainer`）。

* `floatingContainer`（悬浮容器）层位于`contentContainer`之上。


<span id="d1c7cc6f"></span>
#### 替换UI组件

可以通过隐藏默认组件并添加自定义UI组件，替换横屏模式直播间的UI组件。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">为避免空指针异常，请勿移除默认 UI 组件。</div>


以下示例代码替换了横屏模式直播间的`head`容器，并修改了播放器尺寸。

```Java
public void custom(TvuLivePlayerLayoutBinding binding) {
    // Hide the default head component for a live room in landscape mode.
    binding.headTvuContainer.setVisibility(View.GONE);
    // Inflate the custom head component.
    View customHeadView = LayoutInflater.from(context).inflate(R.layout.include_custom_header, binding.headContainer, false);
    customHeadView.findViewById(R.id.back_btn).setOnClickListener(v -> {
        TVULiveRoom.manualClickLiveRoomExitBtn(context);
    });
    customHeadView.findViewById(R.id.share_btn).setOnClickListener(v -> {
        ToastUtil.displayToast("Tapped to share");
    });
    // Add the custom head component.
    binding.headContainer.addView(customHeadView);
    ViewGroup.MarginLayoutParams params = (ViewGroup.MarginLayoutParams) binding.livePlayerContainer.getLayoutParams();
    // Remove the left and right margins as well as the padding on all sides of the player.
    params.leftMargin = params.rightMargin = 0;
    binding.livePlayerContainer.setLayoutParams(params);
    binding.livePlayerContainer.setPadding(0, 0, 0, 0);
    // 设置播放器尺寸为 16:9。
    binding.livePlayerCardView.setResizeMode(TVUAspectRatioFrameLayout.RESIZE_MODE_FIXED_WIDTH);
    binding.livePlayerCardView.setWidthRatio(16);
    binding.livePlayerCardView.setHeightRatio(9);
    // 移除播放器的圆角。
    binding.livePlayerCardView.setRadius(0);
}
```


<span id="98e137b2"></span>
#### 添加自定义悬浮视图组件

`floatingContainer`用于存储直播间的悬浮视图组件，并提供[addChildViewInFrameLayout](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#580ab639)和[addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#d396dffc)方法用于添加自定义悬浮视图组件。

以下示例代码通过[setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#8d1bd70f)方法、[onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cfe9163a)回调和[addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#d396dffc)方法，将自定义悬浮视图组件添加到横屏模式直播间的`floatingContainer`中。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法查找 floatingContainer。Activity 中 floatingContainer 的视图 ID 为 R.id.tvu_floating_views_container。
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // 将 TextView 组件添加到 floatingContainer。
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false, new CustomSize(20, 20));
}
// ...
```


<span id="580ab639"></span>
##### **addChildViewInFrameLayout**

将自定义悬浮视图组件添加到`floatingContainer`。该视图组件与SDK默认视图组件在`floatingContainer`中的位置无关联。显示位置仅由视图组件的配置决定。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">当前 SDK 的默认视图组件包含完整的互动工具图标集、商品浮窗和浮标广告。</div>


```Java
public void addChildViewInFrameLayout(View childView, SimpleLayoutParams layoutParams)
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|childView |View |待添加的视图组件。 |
|layoutParams |[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#e4a2c940) |待添加视图组件的位置。 |


<span id="d396dffc"></span>
##### **addChildViewInLinearLayout**

将自定义悬浮视图组件添加到`floatingContainer`。该视图组件与SDK默认视图组件在`floatingContainer`中的位置有关联，即会参与视图组件显示顺序的重新排序。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">当前 SDK 的默认视图组件包含完整的互动工具图标集、商品浮窗和浮标广告。</div>


```Java
public void addChildViewInLinearLayout(View childView, int location, boolean isLastChild, CustomSize customSize)
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|childView |View |待添加的视图组件。 |
|location |Integer |待添加视图组件在直播间中的显示位置。有效值：<br><br><br>* `0`：显示在直播间左上角，并关联竖屏模式下直播间完整互动工具图标集的位置。<br><br>* `1`：显示在直播间右上角，并关联竖屏模式下直播间页头广告和页中广告的位置。<br><br>* `2`：显示在直播间右下角，并关联横屏模式下直播间完整互动工具图标集、商品浮窗和浮标广告的位置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在竖屏模式的直播间中，右上角显示的内容（自定义浮动视图组件、页头广告和页中广告）与左上角显示的内容（自定义浮动视图组件和完整的互动工具图标组）顶部对齐。</div><br> |
|isLastChild |Boolean |待添加视图组件相对于其他视图组件的显示顺序：<br><br><br>* `true`：显示在所有视图组件的底部。<br><br>* `false`：显示在所有视图组件的顶部。 |
|customSize |[CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#38b050a5) |待添加视图组件的尺寸。 |


<span id="effcf64c"></span>
### （可选）Step 2: 配置多语言

通过`LanguageManager.LanguageManagerListener`监听观看页语言变化后，为自定义组件切换到对应语言。

示例代码如下。

```Java
LanguageManager.LanguageManagerListener listener = new LanguageManager.LanguageManagerListener() {
    @Override
    public void onLanguageChanged(LanguageManager.LANGUAGE language, int languageIdx, Properties properties) {
        // 检测到观看页语言切换后，切换自定义组件至对应语言。
        switch (language) {
            case ZH_HANS:
                break;
            case EN:
                break;
            default:
        }
    }
};
// 添加监听器。
LanguageManager.getInstance().addListener(listener);
// 移除监听器。
LanguageManager.getInstance().removeListener(listener);
```


<span id="3657f7b5"></span>
## 竖屏模式直播间UI自定义

集成完整直播间后，可以自定义竖屏模式直播间的UI。

<span id="e0a074b4"></span>
### Step 1: 获取`TvuPortraitLiveRoomLayoutBinding`实例

SDK触发[onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cc008fd8)回调后，可以使用获取到的`ViewBinding`实例自定义竖屏模式直播间的UI。

示例代码如下。

```Java
public interface LiveRoomStatusListener {
    ...default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


获取到的`ViewBinding`实例的UI结构如下。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c16d2945e1d142ab9ec5e86a0797b670~tplv-goo7wpa0wc-image.image) </span>

```Plain
rootLayout(FrameLayout)
|-- portraitCommentListArea(LinearLayout)
|-- portraitLiveRoomBottomBarLayout(PortraitLiveRoomBottomBarLayout)         
|-- floatingContainer(FloatingContainer)
```


`floatingContainer`（悬浮容器）层位于`portraitCommentListArea`（评论区）和`portraitLiveRoomBottomBarLayout`（底部图标区）之上。

<span id="16d3245a"></span>
#### 替换直播间底部图标的点击事件

`portraitLiveRoomBottomBarLayout`用于存储竖屏模式直播间底部图标，并提供[setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e6e6879a)方法用于将特定图标的点击事件替换为自定义点击事件。该方法将特定底部栏图标的默认点击事件替换为自定义监听器，使你可以在观众点击图标时执行自定义逻辑。

以下示例代码通过[setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#8d1bd70f)方法、[onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cc008fd8)回调和[setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#e6e6879a)方法，替换竖屏模式直播间底部图文图标的点击事件，并自定义点击事件触发后的行为。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法查找 portraitLiveRoomBottomBarLayout。Activity 中 portraitLiveRoomBottomBarLayout 的视图 ID 为 R.id.portrait_bottom_bar。
    PortraitLiveRoomBottomBarLayout portraitLiveRoomBottomBarLayout = findViewById(com.bytedance.live.sdk.R.id.portrait_bottom_bar);
    // 将竖屏模式下直播间底部图标的点击事件替换为自定义点击事件。本示例将替换图形菜单图标的点击事件。
portraitLiveRoomBottomBarLayout.setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar.IMAGE_TEXT_ICON, new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            // 触发图形菜单图标点击事件后，执行自定义点击行为。
            ToastUtil.displayToast("Tapped the icon of graphics menu");
        }
    });
}
```


<span id="e6e6879a"></span>
##### **setBottomOnClickListener**

此方法将特定底部栏图标的默认点击事件替换为自定义监听器，使你能够在观众点击该图标时执行自定义逻辑。

```Java
public void setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar bottomBar, View.OnClickListener listener)
```


**参数**


|名称 |类型 |接口行为 |
|---|---|---|
|bottomBar |[PortraitLiveRoomBottomBarLayout.BottomBar](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#d9f238b6) |竖屏模式下直播间底部的图标。 |
|监听器 |[View.OnClickListener](https://developer.android.com/reference/android/view/View.OnClickListener) |用于自定义图标的点击行为。 |


<span id="cc374f87"></span>
#### 添加自定义悬浮视图组件

以下示例代码通过 [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#8d1bd70f) 方法、[onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#cc008fd8) 回调和 [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/docs-advanced-for-the-viewer-sdk-for-android-zh-CN#d396dffc) 方法，将自定义悬浮视图组件添加到竖屏模式直播间的 `floatingContainer` 中。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法查找 floatingContainer。Activity 中 floatingContainer 的视图 ID 为 R.id.tvu_floating_views_container。
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // 将 TextView 组件添加到 floatingContainer。
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false,
            new CustomSize(20, 20));
}
// ...
```


<span id="8df7019b"></span>
### （可选）Step 2: 配置多语言

通过使用 `LanguageManager.LanguageManagerListener` 检测观看页上的语言变化后，为自定义组件切换到对应语言。

示例代码如下。

```Java
LanguageManager.LanguageManagerListener listener = new LanguageManager.LanguageManagerListener() {
    @Override
    public void onLanguageChanged(LanguageManager.LANGUAGE language, int languageIdx, Properties properties) {
        // After detecting a language change on the viewing page, switch to the corresponding language for custom components.
        switch (language) {
            case ZH_HANS:
                break;
            case EN:
                break;
            default:
        }
    }
};
// 添加监听器。
LanguageManager.getInstance().addListener(listener);
// 移除监听器。
LanguageManager.getInstance().removeListener(listener);
```


<span id="7b1d80cb"></span>
## 动态更新直播间 UI 和交互行为

要在观众加入直播间后动态更新直播间的 UI 和交互行为，可以使用 `DynamicCustomSettings`。

在完整直播间中，按如下方式获取 [动态自定义设置](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-CN) 实例。


1. 调用 [setLiveRoomStatusListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setliveroomstatuslistener) 方法设置直播间状态监听器。

2. 当 `TVULiveRoomServer` 实例创建成功后，SDK 会触发 [onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#38dde242) 回调。你可以通过该回调获取 [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN) 实例。

3. 调用 `TVULiveRoomServer` 实例的 [getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-CN#2323d292) 方法，获取 `DynamicCustomSettings` 实例。

4. 使用 `DynamicCustomSettings` 按需完成 UI 个性化定制。

5. 当直播间的 Activity 被销毁时，将该实例设置为 null，以避免内存泄漏。


示例代码如下。

```Java
// Declare a DynamicCustomSettings reference.
DynamicCustomSettings dynamicCustomSettings;

// Set the listener for live room status.
CustomSettings.Holder.mSettings.setLiveRoomStatusListener(new LiveRoomStatusListener() {
    
    // Get the TVULiveRoomServer instance through the onRoomServerCreated callback.调用 TVULiveRoomServer 实例的 getDynamicSettings 方法获取 DynamicCustomSettings 实例。
    @Override
    public void onRoomServerCreated(Activity activity, long activityId, TVULiveRoomServer roomServer) {
         dynamicCustomSettings = roomServer.getDynamicSettings();
         // Use DynamicCustomSettings to complete the UI customization as needed.此处以设置未关注主播时按钮文本为例。
         dynamicCustomSettings.setFollowText("Follow me");
    }
    
    @Override
    public void onLiveRoomActivityDestroy(Activity activity) {
        // When the Activity of the live room is destroyed, set to null to avoid memory leaks.
        dynamicCustomSettings = null;
    }
    

}
```


<span id="92cb972c"></span>
## 常用 UI 个性化功能

你可以在观看页上定制 UI。

本主题以电商场景下常用的 UI 个性化功能为例。关于用于定制 UI 的方法和回调的更多信息，请参见 [mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN) 和 [Android 观播 SDK：回调](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN)。

<span id="1d02978f"></span>
### 视频缩放模式

默认情况下，竖屏模式直播间中的视频会缩放填满播放器，同时保持视频长宽比（等同于 `ScaleType.CENTER_CROP`）。你可以自定义视频缩放模式。更多信息请参见 [setPortraitPlayerLayoutMode](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-CN#bcd1844b)。

以下示例代码将缩放模式更改为在保持视频长宽比的前提下，使视频适配到播放器边界内。这样可以确保完整视频内容可见且不会被裁剪，但可能会出现黑边或竖边。


<Tabs>
<Tab zoneid="TPhkWiJZYT" title="定制前">
<TabTitle>定制前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d656ba6bb054b11a0f5af80444f1a5f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="lm8spOp8Sa" title="定制后">
<TabTitle>定制后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fae9ce9f8a046ce85be7dd0cb5bb275~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the video scaling mode as ImageAspectFit.
settings.setPortraitPlayerLayoutMode(0); 
```


<span id="5b9de944"></span>
### 关闭完整直播间的图标

默认情况下，竖屏模式下关闭完整直播间的图标为“X”。你可以自定义图标显示样式。

以下示例代码将默认图标替换为 `tvu_nav_icon_back_melon` 可绘制资源。


<Tabs>
<Tab zoneid="YXpcHXCJ7W" title="定制前">
<TabTitle>定制前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ccce4dc4a3946719c3277e06fdd025b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="FokgfzTpZY" title="定制后">
<TabTitle>定制后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3aed731a33f45bdb4dfa05e3a8f9169~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
//  Customize the icon as the image named tvu_nav_icon_back_melon.
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.mipmap.tvu_nav_icon_back_melon));
```


<span id="b68426af"></span>
### 悬浮互动工具

悬浮互动工具包含抽奖、答题、投票、问卷和公告的图标。在竖屏模式直播间中，悬浮互动工具默认显示在直播间左上角。你可以自定义悬浮互动工具的默认位置。

以下示例代码将悬浮互动工具的默认位置从左上角移动到左下角，距离底部 80 dp。


<Tabs>
<Tab zoneid="hoz3pHgWiA" title="定制前">
<TabTitle>定制前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b839ef77fa4a96bfdb62ce646d9f0d~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="FwBbAto6eh" title="定制后">
<TabTitle>定制后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/264f75de88554414ad7ae12aa9938ed1~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Move the default position of floating interaction tools to the lower-left corner, 80 dp from the bottom.
SimpleLayoutParams simpleLayoutParams = new SimpleLayoutParams(Gravity.START | Gravity.BOTTOM, 0, 0, 0, 80);
settings.setFloatInteractToolLayoutParams(simpleLayoutParams);
```


<span id="e52a2874"></span>
### 商品卡片菜单高度

默认情况下，商品卡片菜单的高度为屏幕高度的 0.73 倍。你可以自定义菜单高度。

以下示例代码将商品卡片菜单的高度设置为 700 dp。


<Tabs>
<Tab zoneid="PtsBZiyssy" title="定制前">
<TabTitle>定制前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bd87ad61aa047edaec8826192b46a27~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="EE7goUkpKF" title="定制后">
<TabTitle>定制后</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd6011cd92d4cb388ccb9ae7eb4b314~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the height of the menu for product cards to 700 dp.
settings.setShoppingCardDialogHeight(700);
```
