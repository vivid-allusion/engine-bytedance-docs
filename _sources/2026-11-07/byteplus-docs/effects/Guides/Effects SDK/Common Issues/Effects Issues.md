---
title: "Effects Issues"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-effects-issues"
---

<span id="1. The special effects have been set, but have not taken effect."></span>
### 1. The special effects have been set, but have not taken effect.

A: It is recommended to follow the steps below:


* Make sure the special effects handle has been initialized and licensed properly.

* Check whether the material package and the license are matched. The test version and the official version cannot be mixed.

* If the initialization was successful, check whether the file corresponding to the set face beautification material path exists. Please note that the specified materials are in a sub\-folder within the bundle.

   * Check whether the material path is set correctly.


<span id="2. Reshape has been set, but the face slimming and enlarging functions have not taken effect."></span>
### 2. Reshape has been set, but the face slimming and enlarging functions have not taken effect.

A: It is recommended to follow the steps below:


* Make sure the special effects handle has been initialized successfully.

* If the initialization is successful, check whether the file corresponding to the set shape\-changing material path exists. Please be noted that the specified materials are in a subfolder under the bundle.

* The algorithm for face slimming and eye enlarging depends on the face detection model. Check whether the face detection model exists. In addition, modelDir needs to be imported during the initialization of the special effects handle. The directory structure and file name within this modelDir directory must be consistent with the model directory in resource.zip shown in the demo.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/df73e0a-1.png) </span>

* If the path is set correctly, make sure that the width and height of the texture imported into the init interface are correct.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/742f8fa-2.png) </span>

* If the width and height of the imported texture are correct, check whether the angle imported during the process is correct.


```Plain
 public boolean process(
     int srcTextureId,
     int dstTextureId,
     int width, int height,
     BytedEffectConstants.Rotation rotation,
     double timestamp)
```


Because the image output by the Android camera is rotated anticlockwise by 90 or 270 degrees by default, and the rotation angle of the mobile phone itself also needs be taken into account, we recommend that you use the method shown in the demo. You can first straighten the image output by the camera. To straighten the image, the human face should be upright on the image, and there should be no horizontal mirroring when using the rear camera. Then, use the direction registered by the mobile phone's accelerometer as the input direction for your algorithm detection.

<span id="3. The stickers have been set, but have not taken any effect."></span>
### 3. The stickers have been set, but have not taken any effect.

A: It is recommended to follow the steps below:


* Make sure the special effects handle has been initialized successfully

* If the initialization was successful, check whether the file corresponding to the set sticker material path exists.

* Check whether the face, hand, and body detection models exist. In addition, modelDir needs to be imported during the initialization of the special effects handle. The directory structure and file name within this modelDir directory must be consistent with the directory in resource.zip.

* Make sure that the license file is valid and is compatible with the sticker materials. If the test materials from our demo are used with the official license file, the stickers will not work properly. This can be confirmed by checking the log with **EffectSDK** tag.


<span id="4. After the stickers are set, only part of the foreground appears, and there are no face props."></span>
### 4. After the stickers are set, only part of the foreground appears, and there are no face props.

A: This problem may be caused by the same reason as in Question 2, that is, the human face is not detected. You can first troubleshoot the problem by following the steps for solving Question 3.

<span id="5. Blank screen occurs after calling processTexure on iOS."></span>
### 5. Blank screen occurs after calling processTexure on iOS.

A: If you are using the GPUImage framework, add the following two lines of code after processtexture.

```Plain
glEnableVertexAttribArray(0);
glEnableVertexAttribArray(1);
```


If the problem was not caused by the above issue, take the following steps to troubleshoot the problem.


* Is there correct EAGL operating environment?

* Check whether the input texture is correct, which can be analyzed by viewing the texture with the Xcode packet sniffer.

* After the input texture is confirmed to be correct, the effect of the output texture can also be analyzed by viewing the texture with the Xcode packet sniffer.

* As for the processing of the output texture, users can convert it to Ulimage and display and view it.


<span id="6. If GLSurfaceView is not used for Android projects and results in no GL context, can special effects processing be supported?"></span>
### 6. If GLSurfaceView is not used for Android projects and results in no GL context, can special effects processing be supported?

A: GLSurfaceView is a rendering solution provided by Android officially with the GL context encapsulated. We recommend using GLSurfaceView to complete rendering.

<span id="7. Screen preview is normal on iOS, but the image obtained by memcpy turns blue."></span>
### 7. Screen preview is normal on iOS, but the image obtained by memcpy turns blue.

A: The image output by iOS camera is encoded in BGRA format by default. Please pay attention to the encoding order.

<span id="8. Both the material setting interface and the process interface return the value "true", but there are no corresponding special effects."\>

<span id="_8-both-the-material-setting-interface-and-the-process-interface-return-the-value-true-but-there-are-no-corresponding-special-effects"></span>
### 8. Both the material setting interface and the process interface return the value "true", but there are no corresponding special effects.

A: In this scenario, the input image and parameters may be incorrect, which causes the underlying algorithms for detecting human faces, gestures, etc to fail to detect faces or hands. As a result, the face slimming, eye enlarging or mask functions may fail to take effect. It is recommended to print the input image and check input parameters.

<span id="9. After the live stream is pushed, texts on stickers are reversed."></span>
### 9. After the live stream is pushed, texts on stickers are reversed.

A: During live broadcasts, the images seen by the host and the viewers are mirrored, in order to conform with how people usually see. If stickers containing text are used, the host and the viewers will see mirrored text throughout. The solution to this problem is to not use stickers with texts during live broadcasts.

<span id="10. Special effects such as stickers, eye enlarging and face slimming have taken effect, but disappear easily."></span>
### 10. Special effects such as stickers, eye enlarging and face slimming have taken effect, but disappear easily.

A: Check the input image and input angle to ensure that the face is upright after the input image has been rotated clockwise by the above angle.

<span id="11. Undefine symbols __isPlatformVersionAtLeast"></span>
### 11. Undefine symbols __isPlatformVersionAtLeast

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/0d71025-3.png) </span>

A: The Xcode version used is too old. We recommend that the Xcode version should not be older than v11. Please upgrade the Xcode version. For specific causes for this error, please check: [Undefine symbols __isPlatformVersionAtLeast](https://stackoverflow.com/questions/60124860/undefined-symbols-isplatformversionatleast)

<span id="12. Effect SDK ERROR: Parser: ccJSON parse fail"></span>
### 12. Effect SDK ERROR: Parser: ccJSON parse fail

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/c657d9f-4.png) </span>

A: Effect SDK ERROR: Parser: The cJSON parse fail error usually indicates that the materials and the Bundle ID/Application ID license do not match.Each set of materials is bound to its license, and they must be used together. Check whether the material being used and the license are matching.

<span id="13 ERROR: FileUtil: readFile: file ……… xxx.config.json does not exist"></span>
### 13 ERROR: FileUtil: readFile: file ……… xxx.config.json does not exist

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/doc-center/d608cd0-5.png) </span>

A: The above log indicates that the set material path may be incorrect, and the SDK fails to correctly read the material configuration file. Check whether the material path is correct.

<span id="23a0a013"></span>
### 14 Android proguard rules

First, you must confirm **what version of the SDK** is being used.

**Before V4.4.3**

```Java
-keep class com.bytedance.labcv.effectsdk.** {*;}
-keep class com.bef.effectsdk.* {*;} 
-keep class com.bytedance.labcv.licenselibrary.* {*;}
```


**After V4.4.3 (including V4.4.3)** 

```Java
-keep class com.effectsar.labcv.effectsdk.** {*;}
-keep class com.bef.effectsdk.* {*;} 
-keep class com.effectsar.labcv.licenselibrary.* {*;}
```


<span id="8a6cc15b"></span>
### 15 Effects don't follow the face when face moves, especially the make\-up and beauty/face shaping

This situation usually occurs on iOS side.

You can check `setUse3buffer` or `use3buffer` in `BEEffectManager`, if there is a no\-follow situation, you need to set its value to **false** in `initTask()` to turn off 3buffer.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ec9edd872442fbb34d354355666bd5~tplv-goo7wpa0wc-image.image) </span>

<span id="c0731431"></span>
### 16 Effects play too fast, or stop at the first frame and don't move

This phenomenon is often related to `timeStamp`, and always shows with the effect which has sequence frame, the `timeStamp` passed in the `process` method must be set to the **following system time:** 

Android side: the timeStamp can be set to `System.nanoTime()`;

iOS side: the timeStamp can be set to `[NSDate date].timeIntervalSince1970`.
