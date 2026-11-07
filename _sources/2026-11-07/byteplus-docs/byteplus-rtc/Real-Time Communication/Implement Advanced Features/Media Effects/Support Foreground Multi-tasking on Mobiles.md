---
title: "Support Foreground Multi-tasking on Mobiles"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1178325"
---

To enable users to watch video from your app in a small floating window while multitasking on their mobile devices, you can implement a foreground multitasking or Picture\-in\-Picture (PiP) feature. This guide provides detailed steps and code examples for building this functionality on both Android (using a floating window) and iOS (using the native PiP controller).

> To implement an in\-app floating window, set the canvas size and position using setLocalVideoCanvas and setRemoteVideoCanvas. For example, in a one\-on\-one video call, the remote video stream is displayed full\-screen, with the local video stream appearing in a corner.


<span id="prerequisites"></span>
## Prerequisites


* You have already integrated RTC SDK and are able to implement basic audio and video calls.

* You have implemented a custom video renderer on your iOS device.

* Device requirements:

   * iOS 16 and above

   * Android 8.0 or newer, API level 26


<span id="to-support-foreground-multitasking-on-android"></span>
## To support foreground multitasking on Android

You can implement foreground multitasking on Android by building a floating window. The floating window can be used for video playback, audio\-only playback, or both.

> You can also enable foreground multitasking using Android's picture\-in\-picture feature.


1. Check whether you have permission to display the floating window. If you do not have permission, go to the Settings app to enable it.

   ```java
   private void requestFloatingWindowPermission() {
       if (Build.VERSION.SDK_INT  >= Build.VERSION_CODES.M  && !Settings.canDrawOverlays(this)) {
           Intent intent = new Intent(Settings.ACTION_MANAGE_OVERLAY_PERMISSION, Uri.parse("package:" + getPackageName()));
           startActivityForResult(intent, REQUEST_CODE_FLOATING_WINDOW);
       } else {
           addFloatingWindow();
       }
   }
   
   @Override
   protected void onActivityResult(int requestCode, int resultCode, Intent data) {
       super.onActivityResult(requestCode, resultCode, data);
       if (requestCode == REQUEST_CODE_FLOATING_WINDOW) {
           if (Build.VERSION.SDK_INT  >= Build.VERSION_CODES.M  && Settings.canDrawOverlays(this)) {
               addFloatingWindow();
           } else {
               ToastUtil.showAlert(this, "Floating window permission not granted, unable to add floating window");
           }
       }
   }
   
   @Override
   public void onRequestPermissionsResult(int requestCode, @NonNull String[] permissions, @NonNull int[] grantResults) {
       super.onRequestPermissionsResult(requestCode, permissions, grantResults);
       if (requestCode == REQUEST_CODE_FLOATING_WINDOW) {
           if (grantResults.length > 0 && grantResults[0] == PackageManager.PERMISSION_GRANTED) {
               addFloatingWindow();
           } else {
               ToastUtil.showAlert(this, "Floating window permission not granted, unable to add floating window");
           }
       }
   }
   ```
   

2. Build the UI for the floating window in `layout_float_window`.

   ```java
   private View createFloatWindowView(Context context, @LayoutRes int floatWindowLayoutResId) {
       return LayoutInflater.from(mContext).inflate(R.layout.layout_float_window, null);
   }
   ```
   

3. Create the Window for the floating view.

   ```java
   public FloatWindowManager(Context context, TextureView mainTextureView) {
       this.context = context;
       this.mainTextureView = mainTextureView;
       windowManager = (WindowManager) context.getSystemService(Context.WINDOW_SERVICE);
       DisplayMetrics displayMetrics = new DisplayMetrics();
       windowManager.getDefaultDisplay().getMetrics(displayMetrics);
       int windowSizeInPixel = convertDpToPixel(windowSizeInDp, displayMetrics.density);
       windowParams = new WindowManager.LayoutParams(
               windowSizeInPixel,
               windowSizeInPixel,
               Build.VERSION.SDK_INT  >= Build.VERSION_CODES.O  ? WindowManager.LayoutParams.TYPE_APPLICATION_OVERLAY  : WindowManager.LayoutParams.TYPE_PHONE,
               WindowManager.LayoutParams.FLAG_NOT_FOCUSABLE,
               PixelFormat.TRANSLUCENT
       );
       windowParams.gravity = Gravity.TOP  | Gravity.START;
       
       floatView = new FrameLayout(context);
       closeButton = new Button(context);
       closeButton.setText("Close");
       floatView.addView(closeButton, new FrameLayout.LayoutParams(
               FrameLayout.LayoutParams.WRAP_CONTENT,
               FrameLayout.LayoutParams.WRAP_CONTENT,
               Gravity.BOTTOM  | Gravity.CENTER_HORIZONTAL
       ));
       floatView.setBackgroundResource(R.color.grey);
       isWindowOpen = false;
   
       floatView.setOnTouchListener(new View.OnTouchListener() {
           @Override
           public boolean onTouch(View v, MotionEvent event) {
               switch (event.getAction()) {
                   case MotionEvent.ACTION_DOWN:
                       initialTouchX = event.getRawX();
                       initialTouchY = event.getRawY();
                       initialWindowX = windowParams.x;
                       initialWindowY = windowParams.y;
                       return true;
                   case MotionEvent.ACTION_MOVE:
                       float dx = event.getRawX() - initialTouchX;
                       float dy = event.getRawY() - initialTouchY;
                       windowParams.x = (int) (initialWindowX + dx);
                       windowParams.y = (int) (initialWindowY + dy);
                       windowManager.updateViewLayout(floatView, windowParams);
                       return true;
               }
               return false;
           }
       });
   }
   ```
   

4. Display the floating window using the WindowManager.

> Add the View (TextureView or SurfaceView) that the RTC SDK uses for rendering remote video to the Window.


```java
public void openWindow() {
    if (!isWindowOpen) {
        floatView.addView(mainTextureView);
        windowManager.addView(floatView, windowParams);
        isWindowOpen = true;
    }
}
```


5. Render the video. The following example shows how to render a remote video stream.

   ```java
   private void setRemoteRenderView(String streamId) {
       if (textureView.getParent() == null) {
           remoteViewContainer.removeAllViews();
           remoteViewContainer.addView(textureView);
       }
       VideoCanvas videoCanvas = new VideoCanvas();
       videoCanvas.renderView = textureView;
       videoCanvas.renderMode = VideoCanvas.RENDER_MODE_HIDDEN;
   
       rtcEngine.setRemoteVideoCanvas(streamId, videoCanvas);
   }
   ```
   

6. Close the floating window.

   ```java
   private void closeFloatingWindow() {
       floatWindowManager.closeWindow();
       if (textureView.getParent() != null) {
           remoteViewContainer.addView(textureView);
       }
   }
   
   public void closeWindow() {
       if (isWindowOpen) {
           floatView.removeView(mainTextureView);
           windowManager.removeView(floatView);
           isWindowOpen = false;
       }
   }
   ```
   


<span id="to-enable-pip-on-ios"></span>
## To enable PIP on iOS


1. Configure the project to enable the picture\-in\-picture option.


<span>![图片](https://tosv.byted.org/obj/social-friends-dev/docc/img/C0GEdfzcMoVhYlxxgs2cGrlDnbb/FYzBbm0Cio1jxIxRUK8ck0a2nvc) </span>


1. Create the picture\-in\-picture controller.

   ```swift
   func setupPipController(with sourceView: UIView) {
       
       if #available(iOS 16, *) {
           let callViewController = AVPictureInPictureVideoCallViewController()
           callViewController.preferredContentSize = CGSize(width: 360, height: 640)
           callViewController.view.backgroundColor = UIColor.clear
           
           let source = AVPictureInPictureController.ContentSource(activeVideoCallSourceView: sourceView, contentViewController: callViewController)
           
           let pipVC = AVPictureInPictureController(contentSource: source)
           pipVC.canStartPictureInPictureAutomaticallyFromInline = true
           pipVC.delegate = self
           self.pipVC = pipVC
       } else {
           ToastComponents.shared.show(withMessage: "Not supported on the current system.")
       }
   }
   ```
   

2. Use the system API to enable the picture\-in\-picture function.

   ```swift
   @objc func startPip()  {
       if self.pipVC!.isPictureInPictureActive {
           self.pipVC!.stopPictureInPicture() 
       } else {
           self.pipVC!.startPictureInPicture()
       }
   }
   ```
   

3. Enable the picture\-in\-picture function and add the canvas view to the PiP controller's view.

   ```swift
   func pictureInPictureControllerDidStartPictureInPicture(_ pictureInPictureController: AVPictureInPictureController) {
       
       ToastComponents.shared.show(withMessage: "pictureInPictureControllerDidStart")
       
       if #available(iOS 16.0, *) {
           if let vc = pictureInPictureController.contentSource?.activeVideoCallContentViewController {
               vc.view.addSubview(self.customRenderView)
               self.customRenderView.snp.remakeConstraints() { make in
                   make.edges.equalTo(vc.view)
               }
           }
       }
   }
   ```
   

4. Enable external rendering. Using internal rendering will cause a black screen.

   ```swift
   func bindRemoteRenderView(view: CustomVideoRenderView, streamId: String) {
        self.rtcEngine?.setRemoteVideoSink(streamId, withSink: self.customRenderView, withPixelFormat: .original)
   }
   ```
   


<span id="sample-projects"></span>
## Sample projects


* [Android](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/Android/solutions/rtc-api-example/rtc-api-example/src/main/java/com/vertc/api/example/examples/video/pip/PictureInPictureActivity.java)

* [iOS](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/RTCAPIExample/RTCAPIExample/VideoManager/PictureInPicture/PipViewController.swift)


<span id="api-reference"></span>
## **API reference**


|Platform |Android |iOS |
|---|---|---|
|Set the view for the local stream. |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setlocalvideocanvas) |[setLocalVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70092#setlocalvideocanvas) |
|Set the view for remote streams. |[setRemoteVideoCanvas](https://docs.byteplus.com/en/docs/12/docs-70080#setremotevideocanvas) |[setRemoteVideoCanvas:withCanvas:](https://docs.byteplus.com/en/docs/12/docs-70092#ByteRTCEngine-setremotevideocanvas-withcanvas) |
