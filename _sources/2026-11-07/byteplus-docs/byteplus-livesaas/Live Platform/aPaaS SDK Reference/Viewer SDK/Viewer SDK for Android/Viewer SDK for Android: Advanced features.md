---
title: "Viewer SDK for Android: Advanced features"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features"
---

To create a unique and deeply integrated live viewing experience in your Android app, you can use the advanced features of the Viewer SDK. This guide provides step\-by\-step instructions and code examples for implementing custom login flows, overriding default redirection and exit behaviors, and extensively customizing the UI for both portrait and landscape modes.

<span id="bcd7a14a"></span>
## Prerequisites


* Complete the first 5 steps in [Integrating the Viewer SDK for Android](https://docs.byteplus.com/docs/byteplus-livesaas/docs-integrating-the-viewer-sdk-for-android).

* The following integrations are required.

   * Integrate basic features to customize the video scaling mode. For more information, see [Viewer SDK for Android: Basic features](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features).

   * Integrate the full\-featured live room to implement other advanced features as described in this topic. For more information, see [Full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-basic-features#d27888d9).


<span id="77b0428c"></span>
## Features

This topic describes how to integrate the following features.


* [Custom login](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e54b3982)

* [Custom redirection logic](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#69a798ec)

* [Custom exit behavior of the full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#0dc820f5)

* [UI customization for a live room in landscape mode](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#31413a88)

* [UI customization for a live room in portrait mode](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#3657f7b5)

* [Frequently used UI customization features](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#92cb972c)

   * [Video scaling mode](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#1d02978f)

   * [Icon to close the full-featured live room](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#5b9de944)

   * [Floating interaction tools](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#b68426af)

   * [Height of the menu for product cards](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e52a2874)


<span id="e54b3982"></span>
## Custom login

If you need viewers to log in to your app first and then watch the live stream, participate in comments and interactions, and more, you can choose the custom login method. This allows viewers to join the live room using their existing app account.

You can configure when viewers are prompted to log in.


* Viewers log in to your app first, and then join the live room.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ca690e7373748d4a3f86cdd0b3c0b1e~tplv-goo7wpa0wc-image.image) </span>

   1. After viewers log in to the app and join the live room, you need to call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `2` to get the authorization token.

   2. After getting the token, call the SDK's [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1) method to join the live room.

   The sample code is as follows.

   ```Java
   long activityId = 1721010849258****;  // The activity ID of the live room.
   String token = "ak3T%2FdaGJDL5zSFD7%2F1GPGP****wx0zaTfQ1M4Dahp8%3D";  //  The authorization token when the value of Mode is 2.
   TVULiveRoom.TVURoomAuthMode roomAuthMode = TVULiveRoom.TVURoomAuthMode.CUSTOM; // Custom mode.
   boolean isPortrait = true; // Live room in portrait mode. 
   TVULiveRoom.joinLiveRoom(context, new JoinRoomConfig(activityId,token,roomAuthMode,isPortrait));
   ```
   

* Viewers first join the live room to watch the live stream, view comments, and more. The login process is triggered when they perform operations such as participating in comments and interactions, and then the authentication mode changes from public to custom.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4ae17f6d5f425ab21012288dc119a9~tplv-goo7wpa0wc-image.image) </span>

   1. Viewers first join the live room in public mode.

   2. You need to implement the method of getting the authorization token in public mode. Then, call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `1` to get the token.

   3. Call the [setCustomLoginListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#ad65c19c) method to set the listener for logging in to your own account system in public mode.

   4. Call the SDK's [joinLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/docs-tvuliveroom#b20db0d1) method to join the live room.

   5. When viewers perform the following operations that require user information, the custom login process of the app is triggered:

      * Tap the comment text box under the menu for chat interaction

      * Like a comment

      * Reward hosts with gifts

      * Tap the book button to book the live stream

      * Quizzes

      * Votes

      * Lucky draws

      * Non\-Anonymous questionnaires

   6. The SDK triggers the [onCustomLoginStart](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#d3799085) callback to notify your app that viewers need to perform custom login. You need to implement the method of getting the authorization token in custom mode. After viewers complete the custom login, call [GetSDKTokenAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getsdktokenapi) and set the value of `Mode` to `2` to get the token.

   7. The [onLoginFinished](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cb937422) callback is triggered when the custom login of viewers is successful, fails, or is cancelled, informing the SDK of the viewers' login results.

      * If the login is successful, pass the custom mode token to the SDK.

      * If the login fails or is canceled, pass a null value to the SDK.

   8. The SDK requests viewer information from BytePlus Live by using the token.

   9. After verifying that the token is valid, BytePlus Live passes the viewer information to the SDK. If the token verification fails or the token is empty, BytePlus Live passes the error message to the SDK.

   The sample code is as follows.

   ```Java
   // Set the listener for logging in to your own account system in public mode.
   CustomSettings settings = CustomSettings.Holder.mSettings;
   settings.setCustomLoginListener((context, activityId, callBack) -> {
       //  After triggering the onCustomLoginStart callback, execute the custom login logic of the app. Here, display a custom login dialog box as an example. You can redirect viewers to a specific custom login page as needed.
       new AlertDialog.Builder(context)
               .setTitle("Custom login")
               .setView(editText)
               .setCancelable(false)
               .setPositiveButton(android.R.string.yes, (dialog, which) -> {
                   // In this example, viewers need to enter a token. The onLoginFinished callback, which is triggered when the custom login of viewers is successful, passes the token in custom mode to the SDK. Call the URLDecoder.decode method to decode the token before passing it to the SDK.
                   String token = editText.getText().toString().trim();
                   callBack.onLoginFinished(URLDecoder.decode(token));
               })
               // The onLoginFinished callback, which is triggered when the custom login of viewers fails or is cancelled, passes the null value to the SDK.
               .setNegativeButton(android.R.string.no, ((dialog, which) -> callBack.onLoginFinished(null)))
               .setIcon(android.R.drawable.ic_dialog_alert)
               .show();
   });       
   ```
   


<span id="69a798ec"></span>
## Custom redirection logic

The SDK executes the default redirection behavior when viewers tap the following items in the live room:


* Product card displayed under the menu

* Floating product card

* Header ad

* In\-page ad

* Floating ad

* Host account

* URL in a comment


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information on how to configure the product card, header ad, in\-page ad, floating ad, and host account on the BytePlus Live console, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream">Managing product cards</a>, <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-logo-and-ads">Adding ads</a>, and <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-a-brand-account">Associating a host account to a live room</a>.</div>


After calling the [setRedirectPageListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#be1306ce) method to set the listener for link tap events in the live room, the SDK triggers the [redirectPage](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#381d7dca) callback when viewers tap these items. You can use the return value to decide whether to intercept the default redirection behavior when executing the custom redirection logic.


* Return `true`: Intercept the default redirection behavior.

* Return `false`: Do not intercept the default redirection behavior.


The following sample code only executes the custom redirection logic when viewers tap floating ads, product cards under the menu, and floating product cards, and executes both the custom redirection logic and the default redirection behavior when viewers tap header ads, in\-page ads, host accounts, and URLs in comments.

```Java
// Set the listener for link tap events in the live room.
CustomSettings.Holder.mSettings.setRedirectPageListener(new RedirectPageListener() {
    /**
     *
     * @param liveActivity The Activity where the live room is located.
     * @param redirectInfo Information required to implement the custom redirection logic.
     * @return Whether to intercept the SDK's default redirection behavior. true: Intercept the default redirection behavior. false: Do not intercept the default redirection behavior.
     */
    @Override
    public boolean redirectPage(Activity liveActivity, RedirectInfo redirectInfo) {
        // Use the entrance field to check the entry of the tap event.
        String entrance = redirectInfo.getEntrance();
        switch (redirectInfo.getContentType()) {
            case RedirectInfo.CONTENT_TYPE_URL:
                // When the content type is URL, get the urlRedirectInfo field.
                UrlRedirectInfo urlRedirectInfo = redirectInfo.getUrlRedirectInfo();
                // When viewers tap a floating ad
                if (entrance.equals(Entrance.FLOATING_ADVERTISEMENT.value)) {
                    //  Execute the custom redirection logic. Here, display an internal WebViewDialog of the SDK as an example. You can also use a custom Dialog. 
                    new CommonWebViewDialog(liveActivity, urlRedirectInfo.getUrl(),
                            com.bytedance.live.sdk.R.style.TvuLiveBottomDialog).show();
                    // Execute the custom redirection logic but do not execute the default redirection behavior.
                    return true;
                }
                // When viewers tap a product card under the menu or a floating product card
                if (entrance.equals(Entrance.FLOATING_SHOPPING_CARD.value)) {
                    String productUrl = urlRedirectInfo.getUrl();
                    ToastUtil.displayToast("click : " + productUrl);
                    // Execute the custom redirection logic. Here, redirect viewers to the product detail Activity as an example. 
                    startActivities(new Intent[]{new Intent(MainActivity.this, ProductActivity.class)});
                    // Execute the custom redirection logic but do not execute the default redirection behavior.
                    return true;
                }
        }
        // Execute both the custom redirection logic and the default redirection behavior.
        return false;
    }
});                
```


The features for custom redirection logic, `entrance` field values, and positions on the viewing page are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In this topic, take the positions on the viewing page of mobile devices in portrait mode as an example. For the positions on the viewing page of PCs or mobile devices in landscape mode, see the corresponding documentation.</div>


&nbsp;


|Feature |`entrance` field value |Position on the viewing page |
|---|---|---|
|Product card displayed under the menu |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8abeef62ca8446bb8ff5168977d96bc2~tplv-goo7wpa0wc-image.image) </span> |
|Floating product card |`FLOATING_SHOPPING_CARD` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/55f44ed1cf794259b21ad471927464c5~tplv-goo7wpa0wc-image.image) </span> |
|Header ad |`HEADER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efe65ff843f54cf1a8c28ea8e075cc70~tplv-goo7wpa0wc-image.image) </span> |
|In\-page ad |`BANNER_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1467ed744c9c411baf7b0a94bf6e9d5b~tplv-goo7wpa0wc-image.image) </span> |
|Floating ad |`FLOATING_ADVERTISEMENT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1932e1f10c8445d0941c623d9852f091~tplv-goo7wpa0wc-image.image) </span> |
|Avatar or name of the host account |`BUSINESS_ACCOUNT` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3433b3a664104b0aa1bf92d12d540e90~tplv-goo7wpa0wc-image.image) </span> |
|URL in a comment |`COMMENT_LINK` |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8a1b2f7c4564b9986a132206c72562f~tplv-goo7wpa0wc-image.image) </span> |


By default, only URLs in the host's comments are tappable. You can use the [setAudienceCommentLinkClickable](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#4d6e871a) method to set URLs in viewers' comments as tappable.

The sample code is as follows.

```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setAudienceCommentLinkClickable(true);
```


<span id="0dc820f5"></span>
## Custom exit behavior of the full\-featured live room

By default, viewers exit the full\-featured live room when they tap the exit button or the physical back button in the full\-featured live room. If a live or Video On Demand (VOD) video is playing and viewers enable the floating window permission on their mobile devices, the default behavior is to exit the full\-featured live room and display the floating window, namely picture\-in\-picture (PiP).

After calling the [setLiveRoomActionListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#59235a7d) method to set the listener for exit events of the full\-featured live room, the SDK triggers the [onClickExitLiveRoom](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#f195449a) callback when viewers tap the exit button or the physical back button to exit the full\-featured live room. You can use the return value to decide whether to intercept this default behavior and execute your own custom exit logic.


* Return `true`: Intercept the default tap behavior.

* Return `false`: Do not intercept the default tap behavior.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from version 1.33.0 of the Viewer SDK for Android, the <a href="https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#f195449a">onClickExitLiveRoom</a> callback supports deciding whether to intercept the default tap behavior based on the return value. If the specified SDK version is not integrated, the default tap behavior is always intercepted.</div>


The following sample code only executes the custom exit behavior of the full\-featured live room, but does not execute the default tap behavior.

```Java
// Set the listener for exit events of the full-featured live room.
CustomSettings settings = CustomSettings.Holder.mSettings;
settings.setLiveRoomActionListener(context -> {
    ToastUtil.displayToast("Custom exit behavior of the full-featured live room");
    TVULiveRoom.leaveLiveRoom(MainActivity.this); // Execute the custom exit behavior of the full-featured live room.    
    return true; // Supported only for version 1.33.0 and above of the Viewer SDK for Android.
});
```


<span id="31413a88"></span>
## UI customization for a live room in landscape mode

After integrating a full\-featured live room, you can customize the UI for a live room in landscape mode.

<span id="0a538de3"></span>
### Step 1: Get the `TvuLivePlayerLayoutBinding` instance

After the SDK triggers the [onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cfe9163a) callback, you can customize the UI for a live room in landscape mode by using the obtained `ViewBinding` instance.

The sample code is as follows.

```Java
public interface LiveRoomStatusListener {
    ...
    default void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


The UI structure of the obtained `ViewBinding` instance is as follows.

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



* The `contentContainer` (content container) includes four containers: the `head` (`headContainer`), player (`livePlayerContainer`), `mid` (`midContainer`), and `bottomMenu` (`bottomTvuMenuContainer`).

* The `floatingContainer` (floating container) layer is above the `contentContainer.`


<span id="d1c7cc6f"></span>
#### Replacing the UI component

You can replace the UI components for a live room in landscape mode by hiding the default components and adding custom UI components.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">To avoid a null pointer exception, do not remove unnecessary default UI components.</div>


The following sample code replaces the `head` container for a live room in landscape mode and modifies the player size.

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
    // Set the player size as 16:9.
    binding.livePlayerCardView.setResizeMode(TVUAspectRatioFrameLayout.RESIZE_MODE_FIXED_WIDTH);
    binding.livePlayerCardView.setWidthRatio(16);
    binding.livePlayerCardView.setHeightRatio(9);
    // Remove the player's rounded corners.
    binding.livePlayerCardView.setRadius(0);
}
```


<span id="98e137b2"></span>
#### Adding the custom floating view component

The `floatingContainer` is used to store the live room's floating view component and provides the [addChildViewInFrameLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#580ab639) and [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#d396dffc) methods to add the custom floating view component.

The following sample code uses the [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8d1bd70f) method, the [onLandLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cfe9163a) callback, and the [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#d396dffc) method to add the custom floating view component to the `floatingContainer` for a live room in landscape mode.

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onLandLiveRoomBindingAvailable(TvuLivePlayerLayoutBinding binding, LanguageManager languageManager) {
    // Find the floatingContainer using the findViewById method. The view ID of the floatingContainer in Activity is R.id.tvu_floating_views_container. 
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // Add the TextView component to the floatingContainer.
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false, new CustomSize(20, 20));
}
// ...
```


<span id="580ab639"></span>
##### **addChildViewInFrameLayout**

Add the custom floating view component to the `floatingContainer`. This view component is not linked to the position of the SDK's default view component in the `floatingContainer`. The display position is determined only by the configuration of the view component.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the SDK's default view component includes a complete set of interaction tool icons, floating product card, and floating ad.</div>


```Java
public void addChildViewInFrameLayout(View childView, SimpleLayoutParams layoutParams)
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|childView |View |The view component to be added. |
|layoutParams |[SimpleLayoutParams](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#e4a2c940) |The position of the view component to be added. |


<span id="d396dffc"></span>
##### **addChildViewInLinearLayout**

Add the custom floating view component to the `floatingContainer`. This view component is linked to the position of the SDK's default view component in the `floatingContainer`, meaning it participates in the reordering of the view component display sequence.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Currently, the SDK's default view component includes a complete set of interaction tool icons, floating product card, and floating ad.</div>


```Java
public void addChildViewInLinearLayout(View childView, int location, boolean isLastChild, CustomSize customSize)
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|childView |View |The view component to be added. |
|location |Integer |The display position of the view component to be added in the live room. Valid values:<br><br><br>* `0`: Displayed in the upper\-left corner of the live room, and linked to the position of the complete set of interaction tool icons for a live room in portrait mode.<br><br>* `1`: Displayed in the upper\-right corner of the live room, and linked to the position of the header ad and in\-page ad for a live room in portrait mode.<br><br>* `2`: Displayed in the lower\-right corner of the live room, and linked to the position of the complete set of interaction tool icons for a live room in landscape mode, the floating product card, and the floating ad.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">In a live room in portrait mode, the content displayed in the upper\-right corner (the custom floating view component, header ad, and in\-page ad) is top\-aligned with the content displayed in the upper\-left corner (the custom floating view component and the complete set of interaction tool icons).</div><br> |
|isLastChild |Boolean |The display order of the view component to be added relative to other view components:<br><br><br>* `true`: Displayed at the bottom of all view components.<br><br>* `false`: Displayed on top of all view components. |
|customSize |[CustomSize](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#38b050a5) |The size of the view component to be added. |


<span id="effcf64c"></span>
### (Optional) Step 2: Configure multiple languages

After detecting a language change on the viewing page by using the `LanguageManager.LanguageManagerListener`, switch to the corresponding language for custom components.

The sample code is as follows.

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
// Add the listener. 
LanguageManager.getInstance().addListener(listener);
// Remove the listener. 
LanguageManager.getInstance().removeListener(listener);
```


<span id="3657f7b5"></span>
## UI customization for a live room in portrait mode

After integrating a full\-featured live room, you can customize the UI for a live room in portrait mode.

<span id="e0a074b4"></span>
### Step 1: Get the `TvuPortraitLiveRoomLayoutBinding` instance

After the SDK triggers the [onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cc008fd8) callback, you can customize the UI for a live room in portrait mode by using the obtained `ViewBinding` instance.

The sample code is as follows.

```Java
public interface LiveRoomStatusListener {
    ...default void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    }
    ...
}
```


The UI structure of the obtained `ViewBinding` instance is as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c16d2945e1d142ab9ec5e86a0797b670~tplv-goo7wpa0wc-image.image) </span>

```Plain
rootLayout(FrameLayout)
|-- portraitCommentListArea(LinearLayout)
|-- portraitLiveRoomBottomBarLayout(PortraitLiveRoomBottomBarLayout)         
|-- floatingContainer(FloatingContainer)
```


The `floatingContainer` (floating container) layer is above the `portraitCommentListArea` (comment area) and the `portraitLiveRoomBottomBarLayout` (bottom icon area).

<span id="16d3245a"></span>
#### Replacing tap events for icons at the bottom of a live room

The `portraitLiveRoomBottomBarLayout` is used to store the icons at the bottom of a live room in portrait mode, and provides the [setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e6e6879a) method to replace tap events for specific icons with custom tap events. This method replaces the default tap event for a specific bottom bar icon with a custom listener, allowing you to execute custom logic when a viewer taps the icon.

The following sample code uses the [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8d1bd70f) method, the [onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cc008fd8) callback, and the [setBottomOnClickListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#e6e6879a) method to replace the tap event for the image\-text icon at the bottom of the portrait mode live room and customize the tap behavior after a tap event is triggered.

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // Find the portraitLiveRoomBottomBarLayout using the findViewById method. The view ID of portraitLiveRoomBottomBarLayout in the Activity is R.id.portrait_bottom_bar.
    PortraitLiveRoomBottomBarLayout portraitLiveRoomBottomBarLayout = findViewById(com.bytedance.live.sdk.R.id.portrait_bottom_bar);
    // Replace tap events for icons at the bottom of a live room in portrait mode with your custom tap events. In this example, replace the tap event for the icon of graphics menu.
portraitLiveRoomBottomBarLayout.setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar.IMAGE_TEXT_ICON, new View.OnClickListener() {
        @Override
        public void onClick(View view) {
            // After triggering the tap event for the icon of graphics menu, execute the custom tap behavior. 
            ToastUtil.displayToast("Tapped the icon of graphics menu");
        }
    });
}
```


<span id="e6e6879a"></span>
##### **setBottomOnClickListener**

This method replaces the default tap event for a specific bottom bar icon with a custom listener, allowing you to execute custom logic when a viewer taps the icon.

```Java
public void setBottomOnClickListener(PortraitLiveRoomBottomBarLayout.BottomBar bottomBar, View.OnClickListener listener)
```


**Parameters**


|Name |Type |Description |
|---|---|---|
|bottomBar |[PortraitLiveRoomBottomBarLayout.BottomBar](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#d9f238b6) |The icons at the bottom of the live room in portrait mode. |
|listener |[View.OnClickListener](https://developer.android.com/reference/android/view/View.OnClickListener) |Used to customize the tap behaviors of icons. |


<span id="cc374f87"></span>
#### Adding the custom floating view component

The following sample code uses the [setLiveRoomStatusListener](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#8d1bd70f) method, the [onPortraitLiveRoomBindingAvailable](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#cc008fd8) callback, and the [addChildViewInLinearLayout](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-advanced-features#d396dffc) method to add the custom floating view component to the `floatingContainer` for a live room in portrait mode.

```Java
// CustomSettings.Holder.mSettings.setLiveRoomStatusListener
// ...
@Override
public void onPortraitLiveRoomBindingAvailable(TvuPortraitLiveRoomLayoutBinding binding, LanguageManager languageManager) {
    // Find the floatingContainer using the findViewById method. The view ID of the floatingContainer in Activity is R.id.tvu_floating_views_container.
    FloatingContainer floatingContainer = binding.getRoot().findViewById(com.bytedance.live.sdk.R.id.tvu_floating_views_container);
    // Add the TextView component to the floatingContainer.
    TextView textView = new TextView(binding.getRoot().getContext());
    textView.setText("Hello World");
    floatingContainer.addChildViewInLinearLayout(textView, true, false,
            new CustomSize(20, 20));
}
// ...
```


<span id="8df7019b"></span>
### (Optional) Step 2: Configure multiple languages

After detecting a language change on the viewing page by using the `LanguageManager.LanguageManagerListener`, switch to the corresponding language for custom components.

The sample code is as follows.

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
// Add the listener. 
LanguageManager.getInstance().addListener(listener);
// Remove the listener. 
LanguageManager.getInstance().removeListener(listener);
```


<span id="7b1d80cb"></span>
## Updating live room UI and interaction behaviors dynamically

To dynamically update the live room UI and interaction behaviors after viewers join the live room, you can use `DynamicCustomSettings`.

In a full\-featured live room, do the following to get the [DynamicCustomSettings](https://docs.byteplus.com/docs/byteplus-livesaas/dynamiccustomsettings) instance.


1. Call the [setLiveRoomStatusListener](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-msettings#setliveroomstatuslistener) method to set the listener for live room status.

2. After the `TVULiveRoomServer` instance is successfully created, the SDK triggers the [onRoomServerCreated](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#38dde242) callback. You can get the [TVULiveRoomServer](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver) instance through the callback.

3. Call the [getDynamicSettings](https://docs.byteplus.com/docs/byteplus-livesaas/tvuliveroomserver#2323d292) method of the `TVULiveRoomServer` instance to get the `DynamicCustomSettings` instance.

4. Use `DynamicCustomSettings` to complete the UI customization as needed.

5. When the live room's Activity is destroyed, set the instance to null to avoid memory leaks.


The sample code is as follows.

```Java
// Declare a DynamicCustomSettings reference.
DynamicCustomSettings dynamicCustomSettings;

// Set the listener for live room status.
CustomSettings.Holder.mSettings.setLiveRoomStatusListener(new LiveRoomStatusListener() {
    
    // Get the TVULiveRoomServer instance through the onRoomServerCreated callback. Call the getDynamicSettings method of the TVULiveRoomServer instance to get the DynamicCustomSettings instance.
    @Override
    public void onRoomServerCreated(Activity activity, long activityId, TVULiveRoomServer roomServer) {
         dynamicCustomSettings = roomServer.getDynamicSettings();
         // Use DynamicCustomSettings to complete the UI customization as needed. Here, set the button text when the host is not followed as an example.
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
## Frequently used UI customization features

You can customize the UI on the viewing page.

In this topic, take the frequently used UI customization features in e\-commerce scenarios as an example. For more information about the methods and callbacks used to customize the UI, see [mSettings](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings) and [Viewer SDK for Android: Callbacks](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks).

<span id="1d02978f"></span>
### Video scaling mode

By default, the video in a portrait mode live room is scaled to fill the player while maintaining its aspect ratio (equivalent to `ScaleType.CENTER_CROP`). You can customize the video scaling mode. For more information, see [setPortraitPlayerLayoutMode](https://docs.byteplus.com/docs/byteplus-livesaas/docs-msettings#bcd1844b).

The following sample code changes the scaling mode to fit the video within the player's bounds while maintaining its aspect ratio. This ensures the entire video is visible without cropping, which may result in letterboxing or pillarboxing.


<Tabs>
<Tab zoneid="cetagjkWpV" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d656ba6bb054b11a0f5af80444f1a5f~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="oNs9plGTuf" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fae9ce9f8a046ce85be7dd0cb5bb275~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the video scaling mode as ImageAspectFit. 
settings.setPortraitPlayerLayoutMode(0); 
```


<span id="5b9de944"></span>
### Icon to close the full\-featured live room

By default, the icon for closing the full\-featured live room in portrait mode is an "X". You can customize the icon display style.

The following sample code replaces the default icon with the `tvu_nav_icon_back_melon` drawable.


<Tabs>
<Tab zoneid="XrwX8HnMAU" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1ccce4dc4a3946719c3277e06fdd025b~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="nTdFsMwDfP" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d3aed731a33f45bdb4dfa05e3a8f9169~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
//  Customize the icon as the image named tvu_nav_icon_back_melon.
settings.setExitRoomIcon(ContextCompat.getDrawable(this, R.mipmap.tvu_nav_icon_back_melon));
```


<span id="b68426af"></span>
### Floating interaction tools

Floating interaction tools contain the icons for lucky draws, quizzes, votes, questionnaires, and announcements. For a live room in portrait mode, floating interaction tools are displayed in the upper\-left corner of the live room by default. You can customize the default position of floating interaction tools.

The following sample code moves the default position of floating interaction tools from the upper\-left corner to the lower\-left corner, 80 dp from the bottom.


<Tabs>
<Tab zoneid="T5hzatDLZU" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/00b839ef77fa4a96bfdb62ce646d9f0d~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="m1Oe2HHYdI" title="After customization">
<TabTitle>After customization</TabTitle>

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
### Height of the menu for product cards

By default, the height of the menu for product cards is 0.73 times the screen height. You can customize the height of the menu.

The following sample code sets the height of the menu for product cards to 700 dp.


<Tabs>
<Tab zoneid="wEZfTRp7c7" title="Before customization">
<TabTitle>Before customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bd87ad61aa047edaec8826192b46a27~tplv-goo7wpa0wc-image.image) </span>


</Tab>
<Tab zoneid="Kq2aEJ2Xnz" title="After customization">
<TabTitle>After customization</TabTitle>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abd6011cd92d4cb388ccb9ae7eb4b314~tplv-goo7wpa0wc-image.image) </span>


</Tab>
</Tabs>


```Java
CustomSettings settings = CustomSettings.Holder.mSettings;
// Set the height of the menu for product cards to 700 dp.
settings.setShoppingCardDialogHeight(700);
```
