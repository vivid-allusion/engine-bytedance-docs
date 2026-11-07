---
title: "Preventing screen recording"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/docs-anti-screen-recording"
---

To safeguard your video content on platforms like live streaming or video\-on\-demand from unauthorized recording, you can implement anti\-screen recording and screenshot protection. This guide provides instructions and code examples for implementing this security feature on both Android and iOS, ensuring that any recorded videos or screenshots of your app's player will display a black screen.

This article offers instructions on how to implement anti\-screen recording and screenshot protection in your app. By following these guidelines, you can reinforce the security of your video content and provide a safer viewing experience for your users.

<span id="b557bb9a"></span>
# Demonstration

After anti\-screen recording functionality is integrated and enabled, app users can still watch videos normally during the screen recording process. However, after the recording is completed, the recorded screen video or screenshots will show a black screen in the area where the application's video playback window is displayed.

The image below shows the result on iOS:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10e035830e614c1aa9ffe80c3b82b4b7~tplv-goo7wpa0wc-image.image) </span>

<span id="954acb5a"></span>
# Approach

<span id="cf0446e5"></span>
## Android

We provide two methods for preventing screen recording on Android. This flexibility allows developers to implement a customized anti\-screen recording solution that best suits their application's needs.

<span id="d0119721"></span>
### Window Anti\-Screen Recording/Anti\-Screenshot

VideoOne utilizes the [Window.addFlags(int)](https://developer.android.com/reference/android/view/Window#addFlags(int)) method provided by the Android system to implement window protection. This approach focuses on protecting the content displayed within the entire window of the application. By adding the [WindowManager.LayoutParams.FLAG_SECURE](https://developer.android.com/reference/android/view/WindowManager.LayoutParams#FLAG_SECURE) flag to the window, all the content within the window, including any views or surfaces, will be protected.


* Protect the window content by adding the `WindowManager.LayoutParams.FLAG_SECURE` flag using `Window.addFlags(int)`.

   ```Java
   Window window = getWindow();
   window.addFlags(WindowManager.LayoutParams.FLAG_SECURE);
   ```
   

* Remove the content protection by clearing the `WindowManager.LayoutParams.FLAG_SECURE` flag using `Window.clearFlags(int)`.

   ```Java
   Window window = getWindow();
   window.clearFlags(WindowManager.LayoutParams.FLAG_SECURE);
   ```
   


<span id="cc4a38fb"></span>
### SurfaceView Anti\-Screen Recording/Anti\-Screenshot

This approach specifically targets the protection of content displayed within a SurfaceView. By setting the [SurfaceView.setSecure(boolean)](https://developer.android.com/reference/android/view/SurfaceView#setSecure(boolean)) flag on the SurfaceView, the content rendered within that SurfaceView will be protected. This is particularly useful when you have specific areas or elements in your application that require protection.


* Protect the SurfaceView content by setting the secure flag to true.

   ```Java
   surfaceView.setSecure(true);  
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This must be set before the window containing the SurfaceView is attached to the window manager.   </div>
   

* Remove the content protection by setting the secure flag to false.

   ```Java
   surfaceView.setSecure(false);  
   ```
   


<span id="03f9a0a0"></span>
## iOS

On iOS, VideoOne uses a workaround that leverages the [isSecureTextEntry](https://developer.apple.com/documentation/uikit/uitextinputtraits/1624427-issecuretextentry) property of [UITextField](https://developer.apple.com/documentation/uikit/uitextfield). While this property is designed to obscure text in password fields, it has the side effect of preventing the view's contents from being captured in screenshots or screen recordings.

```objectivec
UITextField *textField = [[UITextField alloc] init];
textField.secureTextEntry = YES;
self.textField = textField;

// Add the player view to the text field's content view.
UIView *contentView = textField.subviews.firstObject;
contentView.userInteractionEnabled = YES;
[contentView addSubview:playerView];

// Add contentView to your UI layout as needed.
```


<span id="a5fd9f84"></span>
# Implementation

Refer to the open\-source code to integrate this feature into your app:

Android: [PreventRecordingFragment.java](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/vod/vod-function/src/main/java/com/videoone/vod/function/fragment/PreventRecordingFragment.java)

iOS: [VEPlayerContainer.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/ToolKit/VodPlayer/VEPlayerUIModule/Classes/UI/PlayerContainer/VEPlayerContainer.m)

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Use these reference implementations to understand best practices and customize the code for your application.</div>
