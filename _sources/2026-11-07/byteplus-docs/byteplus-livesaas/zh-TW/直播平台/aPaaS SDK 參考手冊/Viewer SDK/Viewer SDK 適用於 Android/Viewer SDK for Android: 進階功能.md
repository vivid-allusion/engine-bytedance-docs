---
title: "Viewer SDK for Android: 進階功能"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW"
---

要在您的 Android 應用程式中打造獨特且深度整合的直播觀看體驗，您可以使用 Viewer SDK 的進階功能。本指南提供逐步操作說明與程式碼範例，協助您實現自訂登入流程、覆寫預設的重定向與退出行為，以及針對直式與橫式模式進行 UI 深度自訂。

<span id="bcd7a14a"></span>
## 先決條件


* 請完成 [整合 Android Viewer SDK](https://docs.byteplus.com/docs/byteplus-livesaas/zheng-he-android-viewer-sdk-zh-TW) 的前五個步驟。

* 以下整合是必要的。

   * 整合基本功能以自訂影片縮放模式。如需詳細資訊，請參閱 [Android 版 Viewer SDK：基本功能](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW)。

   * 整合全功能直播間，以實現本主題所述的其他進階功能。如需詳細資訊，請參閱 [全功能直播間](https://docs.byteplus.com/docs/byteplus-livesaas/android-ban-viewer-sdk-ji-ben-gong-neng-zh-TW#d27888d9)。


<span id="77b0428c"></span>
## 功能

本主題說明如何整合以下功能。


* [自訂登入](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e54b3982)

* [自訂導向邏輯](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#69a798ec)

* [全功能直播間的自訂退出行為](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#0dc820f5)

* [橫屏直播間的 UI 客製化](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#31413a88)

* [直式直播間 UI 自訂](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#3657f7b5)

* [常用 UI 客製化功能](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#92cb972c)

   * [影片縮放模式](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#1d02978f)

   * [關閉全功能直播間的圖示](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#5b9de944)

   * [浮動互動工具](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#b68426af)

   * [商品卡片選單高度](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e52a2874)


<span id="e54b3982"></span>
## 自訂登入

若您希望觀眾先登入您的應用程式，再觀看直播、參與留言互動等，您可以選擇自訂登入方式。此方式可讓觀眾使用現有的應用程式帳號加入直播間。

您可以設定觀眾何時需要登入。


* 觀眾先登入您的應用程式，然後加入直播間。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca690e7373748d4a3f86cdd0b3c0b1e~tplv-goo7wpa0wc-image.image) </span>

   1. 觀眾登入應用程式並加入直播間後，您需呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `2`，以取得授權憑證。

   2. 取得憑證後，呼叫 SDK 的 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1) 方法加入直播間。

   範例程式碼如下。

   ```Java
   long activityId = 1721010849258****;  // 直播間的活動 ID。
   String token = "ak3T%2FdaGJDL5zSFD7%2F1GPGP****wx0zaTfQ1M4Dahp8%3D";  // 當 Mode 的值為 2 時的授權 token。
   TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.CUSTOM; // 自定義模式。
   boolean isPortrait = true; // 直立模式下的直播間。
   TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
   ```
   

* 觀眾先加入直播間觀看直播、瀏覽留言等。當觀眾執行參與留言互動等操作時，會觸發登入流程，並將驗證模式從公開切換為自訂。

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4ae17f6d5f425ab21012288dc119a9~tplv-goo7wpa0wc-image.image) </span>

   1. 觀眾先以公開模式加入直播間。

   2. 您需實作公開模式下取得授權憑證的方法。然後呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `1`，以取得憑證。

   3. 呼叫 [setCustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#ad65c19c) 方法，設定公開模式下登入自有帳號系統的監聽器。

   4. 呼叫 SDK 的 [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom-zh-TW#b20db0d1) 方法加入直播間。

   5. 當觀眾執行以下需要用戶資訊的操作時，會觸發應用程式的自訂登入流程：

      * 點選聊天互動選單下的留言文字框

      * 對留言按讚

      * 送禮物給主播

      * 點選預約按鈕預約直播

      * 答題

      * 投票

      * 抽獎

      * 非匿名問卷

   6. SDK 會觸發 [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#d3799085) 回呼，通知您的應用程式觀眾需要執行自訂登入。您需實作自訂模式下取得授權憑證的方法。觀眾完成自訂登入後，呼叫 [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi-zh-TW)，並將 `Mode` 的值設為 `2`，以取得憑證。

   7. 當觀眾自訂登入成功、失敗或取消時，會觸發 [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cb937422) 回呼，通知 SDK 觀眾的登入結果。

      * 若登入成功，請將自訂模式憑證傳給 SDK。

      * 若登入失敗或取消，請傳送 null 值給 SDK。

   8. SDK 會使用 token 向 BytePlus Live 請求觀眾資訊。

   9. 在驗證 token 有效後，BytePlus Live 會將觀眾資訊傳遞給 SDK。若 token 驗證失敗或 token 為空，BytePlus Live 會將錯誤訊息傳遞給 SDK。

   範例程式碼如下。

   ```Java
   // 設置公有模式下登入自有帳號系統的監聽器。
   CustomSettings settings = CustomSettings.Holder.mSettings;
   settings.setCustomLoginListener((context, activityId, callBack) -> {
       //  觸發 onCustomLoginStart 回調後，執行 App 的自定義登入邏輯。此處以顯示自定義登入對話框為例。可根據需求將觀眾導向特定的自定義登入頁面。
       new AlertDialog.Builder(context)
               .setTitle("Custom login")
               .setView(editText)
               .setCancelable(false)
               .setPositiveButton(android.R.string.yes, (dialog, which) -> {
                   // 本範例中，觀眾需輸入 token。當觀眾自定義登入成功時，onLoginFinished 回調會將自定義模式下的 token 傳遞給 SDK。在傳遞給 SDK 前，需呼叫 URLDecoder.decode 方法解碼 token。
                   String token = editText.getText().toString().trim();
                   callBack.onLoginFinished(URLDecoder.decode(token));
               })
               // 當觀眾自定義登入失敗或取消時，onLoginFinished 回調會將 null 傳遞給 SDK。
               .setNegativeButton(android.R.string.no, ((dialog, which) -> callBack.onLoginFinished(null)))
               .setIcon(android.R.drawable.ic_dialog_alert)
               .show();
   });       
   ```
   


<span id="69a798ec"></span>
## 自訂導向邏輯

當觀眾在直播間點擊下列項目時，SDK 會執行預設導向行為：


* 選單下方顯示的商品卡片

* 浮動商品卡片

* 頁首廣告

* 頁面內廣告

* 浮動廣告

* 主播帳號

* 評論中的 URL


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如需瞭解如何在 BytePlus Live 控制台配置商品卡片、頭部廣告、頁內廣告、浮動廣告及主播帳號，請參閱 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/guan-li-chan-pin-ka-pian-zh-TW">管理商品卡片</a>、<a href="https://docs.byteplus.com/docs/byteplus-livesaas/xin-zeng-guang-gao-zh-TW">新增廣告</a> 和 <a href="https://docs.byteplus.com/docs/byteplus-livesaas/jiang-zhu-ban-ren-zhang-hu-guan-lian-zhi-zhi-bo-ji-zh-TW">將主辦人帳戶關聯至直播間</a>。</div>


呼叫 [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#be1306ce) 方法設定直播間連結點擊事件的監聽器後，當觀眾點擊這些項目時，SDK 會觸發 [redirectPage](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#381d7dca) 回呼。您可以根據回傳值決定在執行自訂導向邏輯時，是否攔截預設導向行為。


* 回傳 `true`：攔截預設導向行為。

* 回傳 `false`：不攔截預設導向行為。


下方範例程式碼僅於觀眾點擊浮動廣告、選單下方商品卡片及浮動商品卡片時執行自訂導向邏輯；當觀眾點擊頁首廣告、頁面內廣告、主播帳號及評論中的 URL 時，則同時執行自訂導向邏輯與預設導向行為。

```Java
// Set the listener for link tap events in the live room.
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /**
*
*@paramliveActivity 直播間所在的 Activity。
*@paramredirectInfo 實現自定義跳轉邏輯所需的資訊。
*@return 是否攔截 SDK 的預設跳轉行為。true: 攔截預設跳轉行為。false: 不攔截預設跳轉行為。*/
    @Override
    public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo) {
        // 使用 entrance 欄位判斷點擊事件的入口。
        String entrance = redirectInfo.getEntrance();
        switch (redirectInfo.getContentType()) {
            case RedirectInfo.CONTENT_TYPE_URL:
                // 當內容類型為 URL 時，取得 urlRedirectInfo 欄位。
                UrlRedirectInfo urlRedirectInfo = redirectInfo.getUrlRedirectInfo();
                // 當觀眾點擊浮動廣告
                if (entrance.equals(Entrance.FLOATING_ADVERTISEMENT.value)) {
                    //  執行自定義跳轉邏輯。此處以顯示 SDK 內部 WebViewDialog 為例。也可使用自定義 Dialog。
                    new CommonWebViewDialog(liveActivity, urlRedirectInfo.getUrl(),
                            com.bytedance.live.sdk.R.style.TvuLiveBottomDialog).show();
                    // 執行自定義跳轉邏輯，但不執行預設跳轉行為。
                    return true;
                }
                // 當觀眾點擊菜單下的商品卡片或浮動商品卡片
                if (entrance.equals(Entrance.FLOATING_SHOPPING_CARD.value)) {
                    String productUrl = urlRedirectInfo.getUrl();
                    ToastUtil.displayToast("click : " + productUrl);
                    // 執行自定義跳轉邏輯。此處以將觀眾導向商品詳情 Activity 為例。
                    startActivities(new Intent[]{new Intent(MainActivity.this, ProductActivity.class)});
                    // 執行自定義跳轉邏輯，但不執行預設跳轉行為。
                    return true;
                }
        }
        // 同時執行自定義跳轉邏輯及預設跳轉行為。
        return false;
    }
});                
```


下表顯示自訂導向邏輯的功能、`entrance` 欄位值及觀看頁面上的位置。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">本主題以直立模式下行動裝置觀看頁面的各位置為例。如需瞭解 PC 或橫向模式行動裝置觀看頁面的各位置，請參閱相關文件。</div>


&nbsp;


|功能 |`entrance` 欄位值 |觀看頁面位置 |
|---|---|---|
|菜單下顯示的商品卡片 |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8abeef62ca8446bb8ff5168977d96bc2~tplv-goo7wpa0wc-image.image) </span> |
|浮動商品卡片 |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55f44ed1cf794259b21ad471927464c5~tplv-goo7wpa0wc-image.image) </span> |
|頭部廣告 |`HEADER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe65ff843f54cf1a8c28ea8e075cc70~tplv-goo7wpa0wc-image.image) </span> |
|頁內廣告 |`BANNER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1467ed744c9c411baf7b0a94bf6e9d5b~tplv-goo7wpa0wc-image.image) </span> |
|浮動廣告 |`FLOATING_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1932e1f10c8445d0941c623d9852f091~tplv-goo7wpa0wc-image.image) </span> |
|主播帳號頭像或名稱 |`BUSINESS_ACCOUNT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3433b3a664104b0aa1bf92d12d540e90~tplv-goo7wpa0wc-image.image) </span> |
|評論中的 URL |`COMMENT_LINK` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a1b2f7c4564b9986a132206c72562f~tplv-goo7wpa0wc-image.image) </span> |


預設情況下，僅主播評論中的 URL 可被點擊。您可以使用 [setAudienceCommentLinkClickable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#4d6e871a) 方法設定觀眾評論中的 URL 可被點擊。

範例程式碼如下。

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setAudienceCommentLinkClickable(true);
```


<span id="0dc820f5"></span>
## 全功能直播間的自訂退出行為

預設情況下，觀眾在全功能直播間點擊退出按鈕或實體返回鍵時，會退出全功能直播間。若正在播放直播或隨選視訊（VOD），且觀眾於行動裝置開啟浮動視窗權限，預設行為為退出全功能直播間並顯示浮動視窗（即子母畫面，PiP）。

呼叫 [setLiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#59235a7d) 方法設定全功能直播間退出事件的監聽器後，當觀眾點擊退出按鈕或實體返回鍵以退出全功能直播間時，SDK 會觸發 [onClickExitLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#f195449a) 回呼。您可以根據回傳值決定是否攔截此預設行為並執行自訂退出邏輯。


* 回傳 `true`：攔截預設點擊行為。

* 回傳 `false`：不攔截預設點擊行為。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">自 Android Viewer SDK 1.33.0 版本起，<a href="https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#f195449a">onClickExitLiveRoom</a> 回調支援根據回傳值決定是否攔截預設點擊行為。若未集成指定 SDK 版本，預設點擊行為將始終被攔截。</div>


下方範例程式碼僅執行全功能直播間的自訂退出行為，不執行預設點擊行為。

```Java
// Set the listener for exit events of the full-featured live room.
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setLiveRoomActionListener(context -> {
    ToastUtil.displayToast("Custom exit behavior of the full-featured live room");
    TVULiveRoom.leaveLiveRoom(MainActivity.this); // Execute the custom exit behavior of the full-featured live room.
    return true; // 僅支援 Android Viewer SDK 1.33.0 及以上版本。
});
```


<span id="31413a88"></span>
## 橫屏直播間的 UI 客製化

整合全功能直播間後，您可以自訂橫屏直播間的 UI。

<span id="0a538de3"></span>
### Step 1: 取得 `TvuLivePlayerLayoutBinding` 實例

當 SDK 觸發 [onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cfe9163a) 回調後，你可以使用獲取到的 `ViewBinding` 實例來自訂橫屏直播間的 UI。

範例程式碼如下。

```Java
public interface LiveRoomStatusListener {
    ...
    default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


獲取到的 `ViewBinding` 實例的 UI 結構如下。

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



* `contentContainer`（內容容器）包含四個容器：`head`（`headContainer`）、播放器（`livePlayerContainer`）、`mid`（`midContainer`）以及 `bottomMenu`（`bottomTvuMenuContainer`）。

* `floatingContainer`（浮動容器）層位於 `contentContainer` 之上。


<span id="d1c7cc6f"></span>
#### 替換 UI 元件

你可以通過隱藏預設元件並新增自訂 UI 元件，來替換橫屏直播間的 UI 元件。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">為避免空指標異常，請勿移除不必要的預設 UI 元件。</div>


以下範例程式碼替換了橫屏直播間的 `head` 容器，並修改了播放器尺寸。

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
    // 設定播放器尺寸為 16:9。
    binding.livePlayerCardView.setResizeMode(TVUAspectRatioFrameLayout.RESIZE_MODE_FIXED_WIDTH);
    binding.livePlayerCardView.setWidthRatio(16);
    binding.livePlayerCardView.setHeightRatio(9);
    // 移除播放器的圓角。
    binding.livePlayerCardView.setRadius(0);
}
```


<span id="98e137b2"></span>
#### 新增自訂浮動視圖元件

`floatingContainer` 用於存放直播間的浮動視圖元件，並提供 [addChildViewInFrameLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#580ab639) 和 [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#d396dffc) 方法以新增自訂浮動視圖元件。

以下範例程式碼使用 [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#8d1bd70f) 方法、[onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cfe9163a) 回調以及 [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#d396dffc) 方法，將自訂浮動視圖元件新增至橫屏直播間的 `floatingContainer`。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法尋找 floatingContainer。Activity 中 floatingContainer 的視圖 ID 為 R.id.tvu_floating_views_container。
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // 將 TextView 元件新增至 floatingContainer。
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false, new CustomSize(20, 20));
}
// ...
```


<span id="580ab639"></span>
##### **addChildViewInFrameLayout**

將自訂浮動視圖元件新增至 `floatingContainer`。此視圖元件不會與 `floatingContainer` 中 SDK 預設視圖元件的位置產生關聯。顯示位置僅由視圖元件的配置決定。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">目前，SDK 的預設視圖元件包含完整互動工具圖示組、浮動商品卡片及浮動廣告。</div>


```Java
public void addChildViewInFrameLayout(View childView, SimpleLayoutParams layoutParams)
```


**參數**


|名稱 |型別 |描述 |
|---|---|---|
|childView |View |要新增的視圖元件。 |
|layoutParams |[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#e4a2c940) |要新增的視圖元件的位置。 |


<span id="d396dffc"></span>
##### **addChildViewInLinearLayout**

將自訂浮動視圖元件新增至 `floatingContainer`。此視圖元件會與 `floatingContainer` 中 SDK 預設視圖元件的位置產生關聯，亦即會參與視圖元件顯示順序的重新排序。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">目前，SDK 的預設視圖元件包含完整互動工具圖示組、浮動商品卡片及浮動廣告。</div>


```Java
public void addChildViewInLinearLayout(View childView, int location, boolean isLastChild, CustomSize customSize)
```


**參數**


|名稱 |型別 |描述 |
|---|---|---|
|childView |View |要新增的視圖元件。 |
|location |Integer |要新增的視圖元件在直播間中的顯示位置。有效值：<br><br><br>* `0`：顯示於直播間左上角，並與直屏直播間完整互動工具圖示組的位置連動。<br><br>* `1`：顯示於直播間右上角，並與直屏直播間頭部廣告及頁內廣告的位置連動。<br><br>* `2`：顯示於直播間右下角，並與橫屏直播間完整互動工具圖示組、浮動商品卡片及浮動廣告的位置連動。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在直式直播間中，右上角顯示的內容（自訂浮動視圖元件、標頭廣告與頁內廣告）與左上角顯示的內容（自訂浮動視圖元件及完整互動工具圖示組）頂端對齊。</div><br> |
|isLastChild |Boolean |要新增的視圖元件相對於其他視圖元件的顯示順序：<br><br><br>* `true`：顯示於所有視圖元件的底部。<br><br>* `false`：顯示於所有視圖元件的頂部。 |
|customSize |[CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#38b050a5) |要新增的視圖元件的尺寸。 |


<span id="effcf64c"></span>
### （選填）Step 2: 設定多語言

當使用 `LanguageManager.LanguageManagerListener` 偵測到觀看頁面語言變更後，切換自訂元件至對應語言。

範例程式碼如下。

```Java
LanguageManager.LanguageManagerListener listener = new LanguageManager.LanguageManagerListener() {
    @Override
    public void onLanguageChanged(LanguageManager.LANGUAGE language, int languageIdx, Properties properties) {
        // 偵測到觀看頁語言變更後，切換自訂元件至對應語言。
        switch (language) {
            case ZH_HANS:
                break;
            case EN:
                break;
            default:
        }
    }
};
// 新增監聽器。
LanguageManager.getInstance().addListener(listener);
// 移除監聽器。
LanguageManager.getInstance().removeListener(listener);
```


<span id="3657f7b5"></span>
## 直式直播間 UI 自訂

整合全功能直播間後，你可以自訂直式直播間的 UI。

<span id="e0a074b4"></span>
### Step 1: 取得 `TvuPortraitLiveRoomLayoutBinding` 實例

當 SDK 觸發 [onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cc008fd8) 回調後，你可以使用獲取到的 `ViewBinding` 實例來自訂直式直播間的 UI。

範例程式碼如下。

```Java
public interface LiveRoomStatusListener {
    ...default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


獲取到的 `ViewBinding` 實例的 UI 結構如下。

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c16d2945e1d142ab9ec5e86a0797b670~tplv-goo7wpa0wc-image.image) </span>

```Plain
rootLayout(FrameLayout)
|-- portraitCommentListArea(LinearLayout)
|-- portraitLiveRoomBottomBarLayout(PortraitLiveRoomBottomBarLayout)         
|-- floatingContainer(FloatingContainer)
```


`floatingContainer`（浮動容器）層位於 `portraitCommentListArea`（留言區）及 `portraitLiveRoomBottomBarLayout`（底部圖示區）之上。

<span id="16d3245a"></span>
#### 替換直播間底部圖示的點擊事件

`portraitLiveRoomBottomBarLayout` 用於存放直式直播間底部圖示，並提供 [setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e6e6879a) 方法以將特定圖示的點擊事件替換為自訂點擊事件。此方法會將特定底部欄圖示的預設點擊事件替換為自訂監聽器，讓你能在觀眾點擊圖示時執行自訂邏輯。

以下範例程式碼使用 [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#8d1bd70f) 方法、[onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cc008fd8) 回調以及 [setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#e6e6879a) 方法，替換直式直播間底部圖文圖示的點擊事件，並自訂點擊事件觸發後的行為。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法尋找 portraitLiveRoomBottomBarLayout。Activity 中 portraitLiveRoomBottomBarLayout 的視圖 ID 為 R.id.portrait_bottom_bar。
    PortraitLiveRoomBottomBarLayout portraitLiveRoomBottomBarLayout = findViewById(com.bytedance.live.sdk.R.id.portrait_bottom_bar);
    // 將直屏直播間底部圖示的點擊事件替換為自訂點擊事件。本範例中，替換圖形選單圖示的點擊事件。
portraitLiveRoomBottomBarLayout.setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar.IMAGE_TEXT_ICON, new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            // 觸發圖形選單圖示的點擊事件後，執行自訂點擊行為。
            ToastUtil.displayToast("Tapped the icon of graphics menu");
        }
    });
}
```


<span id="e6e6879a"></span>
##### **setBottomOnClickListener**

此方法會將特定底部欄圖示的預設點擊事件替換為自訂監聽器，讓你能在觀眾點擊該圖示時執行自訂邏輯。

```Java
public void setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar bottomBar, View.OnClickListener listener)
```


**參數**


|名稱 |型別 |描述 |
|---|---|---|
|bottomBar |[PortraitLiveRoomBottomBarLayout.BottomBar](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#d9f238b6) |直屏直播間底部的圖示。 |
|listener |[View.OnClickListener](https://developer.android.com/reference/android/view/View.OnClickListener) |用於自訂圖示的點擊行為。 |


<span id="cc374f87"></span>
#### 新增自訂浮動檢視元件

以下範例程式碼使用[setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#8d1bd70f)方法、[onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#cc008fd8)回呼，以及[addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-jin-jie-gong-neng-zh-TW#d396dffc)方法，將自訂浮動檢視元件新增至`floatingContainer`，用於直式模式的直播間。

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // 使用 findViewById 方法尋找 floatingContainer。Activity 中 floatingContainer 的視圖 ID 為 R.id.tvu_floating_views_container。
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // 將 TextView 元件加入 floatingContainer。
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false,
            new CustomSize(20, 20));
}
// ...
```


<span id="8df7019b"></span>
### （選用）Step 2: 設定多語言

在觀看頁面中透過`LanguageManager.LanguageManagerListener`偵測語言變更後，切換自訂元件的對應語言。

範例程式碼如下。

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
// 新增監聽器。
LanguageManager.getInstance().addListener(listener);
// 移除監聽器。
LanguageManager.getInstance().removeListener(listener);
```


<span id="7b1d80cb"></span>
## 動態更新直播間 UI 與互動行為

若要在觀眾進入直播間後動態更新直播間的 UI 與互動行為，可使用`DynamicCustomSettings`。

在全功能直播間中，請依下列步驟取得[DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings-zh-TW)實例。


1. 呼叫[setLiveRoomStatusListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setliveroomstatuslistener)方法以設定直播間狀態的監聽器。

2. 當`TVULiveRoomServer`實例建立成功後，SDK 會觸發[onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#38dde242)回呼。你可以透過該回呼取得[TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW)實例。

3. 呼叫`TVULiveRoomServer`實例的[getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver-zh-TW#2323d292)方法以取得`DynamicCustomSettings`實例。

4. 使用`DynamicCustomSettings`，依需求完成 UI 客製化。

5. 當直播間的 Activity 被銷毀時，請將該實例設為 null 以避免記憶體洩漏。


範例程式碼如下。

```Java
// Declare a DynamicCustomSettings reference.
DynamicCustomSettings dynamicCustomSettings;

// Set the listener for live room status.
CustomSettings.Holder.mSettings.setLiveRoomStatusListener(new LiveRoomStatusListener() {
    
    // Get the TVULiveRoomServer instance through the onRoomServerCreated callback.呼叫 TVULiveRoomServer 實例的 getDynamicSettings 方法以取得 DynamicCustomSettings 實例。
    @Override
    public void onRoomServerCreated(Activity activity, long activityId, TVULiveRoomServer roomServer) {
         dynamicCustomSettings = roomServer.getDynamicSettings();
         // Use DynamicCustomSettings to complete the UI customization as needed.此處以設定未關注主播時的按鈕文字為例。
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
## 常用 UI 客製化功能

你可以在觀看頁面自訂 UI。

本主題以電商場景下常用的 UI 客製化功能為例。如需更多自訂 UI 所用方法與回呼的資訊，請參閱[mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW)與[Android Viewer SDK：回呼](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW)。

<span id="1d02978f"></span>
### 影片縮放模式

預設情況下，直式模式直播間中的影片會等比例縮放填滿播放器（等同於 `ScaleType.CENTER_CROP`）。你可以自訂影片縮放模式。如需更多資訊，請參閱[setPortraitPlayerLayoutMode](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings-zh-TW#bcd1844b)。

以下範例程式碼將縮放模式更改為在維持影片比例的同時，將影片完整顯示於播放器範圍內。這可確保影片完整顯示不被裁切，但可能會出現黑邊或側邊黑條。


<Tabs>
<Tab zoneid="GYhC0TJf6x" title="客製化前">
<TabTitle>客製化前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d656ba6bb054b11a0f5af80444f1a5f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="briejqJu52" title="客製化後">
<TabTitle>客製化後</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fae9ce9f8a046ce85be7dd0cb5bb275~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the video scaling mode as ImageAspectFit.
settings.setPortraitPlayerLayoutMode(0); 
```


<span id="5b9de944"></span>
### 關閉全功能直播間的圖示

預設情況下，直式模式全功能直播間的關閉圖示為「X」。你可以自訂圖示的顯示樣式。

以下範例程式碼將預設圖示替換為 `tvu_nav_icon_back_melon` drawable 資源。


<Tabs>
<Tab zoneid="bI4mEeSke9" title="客製化前">
<TabTitle>客製化前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ccce4dc4a3946719c3277e06fdd025b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="AUFNgLGOg4" title="客製化後">
<TabTitle>客製化後</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3aed731a33f45bdb4dfa05e3a8f9169~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
//  Customize the icon as the image named tvu_nav_icon_back_melon.
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.mipmap.tvu_nav_icon_back_melon));
```


<span id="b68426af"></span>
### 浮動互動工具

浮動互動工具包含抽獎、答題、投票、問卷及公告等圖示。在直式模式的直播間中，浮動互動工具預設顯示於直播間左上角。你可以自訂浮動互動工具的預設位置。

以下範例程式碼將浮動互動工具的預設位置由左上角移至左下角，距底部 80 dp。


<Tabs>
<Tab zoneid="cQopKy4moX" title="客製化前">
<TabTitle>客製化前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b839ef77fa4a96bfdb62ce646d9f0d~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="rJeBhB7fEK" title="客製化後">
<TabTitle>客製化後</TabTitle>

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
### 商品卡片選單高度

預設情況下，商品卡片選單的高度為螢幕高度的 0.73 倍。你可以自訂選單高度。

以下範例程式碼將商品卡片選單高度設為 700 dp。


<Tabs>
<Tab zoneid="t9P9onbb08" title="客製化前">
<TabTitle>客製化前</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bd87ad61aa047edaec8826192b46a27~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="EeIpD4heZn" title="客製化後">
<TabTitle>客製化後</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd6011cd92d4cb388ccb9ae7eb4b314~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the height of the menu for product cards to 700 dp.
settings.setShoppingCardDialogHeight(700);
```
