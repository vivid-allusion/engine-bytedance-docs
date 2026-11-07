---
title: "Virtual Background (Native)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-97293"
---

To protect user privacy and improve video quality in scenarios like live streaming or video conferencing, you can implement a virtual background. This guide provides step\-by\-step instructions and code examples for using the RTC SDK to replace a user's real\-world background with a custom image or a solid color.

<span id="prerequisite"></span>
## Prerequisite

Ensure that you have integrated the RTC SDK v3.50+ and implemented basic audio and video calling functions.

Before implementing the virtual background, you must:


* Contact our technical support team to obtain the required license and material files from [Effects](https://docs.byteplus.com/en/effects/docs/about-license).

* Import the [Effects](https://docs.byteplus.com/en/effects/docs/android-v4101-access-guide) SDK into your project.

   For the mobile platform, you need to ensure that the license and material files are copied to the App directory. For Android, the resources should be copied to the external storage.

    &nbsp;


<span id="apply-virtual-background-to-the-video"></span>
## Apply virtual background to the video

The following example is for the Android platform:


1. Check the license and set the algorithm model. The certificate path is the absolute path of the `*.licbag` file, and the algorithm model path is the absolute path of `ModelResource.bundle`.

   ```java
   IVideoEffect mVideoEffect = mRTCVideo.getVideoEffectInterface();
   mVideoEffect.initCVResource(", ")
   ```
   

   You may receive the following error codes.



|`initCVResource` error codes |Description |Solution |
|---|---|---|
|0 |Success. |NA |
|–1000 |Failed to integrate the Effects SDK. |Check the integration of Effects SDK. |
|–121 |Incorrect path of license package. |Check whether the path input in the SDK is correct. |
|–119 |Mismatched application ID/bundle ID. |Ensure the application ID/bundle ID in the license file matches that of your app. |
|–117 |License file expired. |Check whether the license file is correct and whether it needs to be updated. |
|Other error codes |See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions. | |



2. After the `initCVResource` call is successful, you can turn on the virtual background, which supports solid background and image background.

   a. Enable the solid color background.

   ```java
   VirtualBackgroundSource source = new VirtualBackgroundSource();
   // Select solid background.
   source.sourceType = VirtualBackgroundSourceType.COLOR;;
   // Set background color. The format is 0xAARRGGBB. For example, the value for green is 0xFF00FF00.
   source.sourceColor = 0XFF00FF00;
   // Turn on virtual background.
   IVideoEffect mVideoEffect = mRTCVideo.getVideoEffectInterface();
   mVideoEffect.enableVirtualBackground(", source);
   ```
   

   b. Enable the image background.

   ```java
   VirtualBackgroundSource source = new VirtualBackgroundSource();
   // Select image background.
   source.sourceType = VirtualBackgroundSourceType.IMAGE;
   // Set the absolute path of the image.
   source.sourcePath = "/storage/emulated/0/Download/test.png";
   // Turn on virtual background.
   IVideoEffect mVideoEffect = mRTCVideo.getVideoEffectInterface();
   mVideoEffect.enableVirtualBackground(", source);
   ```
   

   c. Disable the virtual background.

   ```java
   // Turn off virtual background.
   IVideoEffect mVideoEffect = mRTCVideo.getVideoEffectInterface();
   mVideoEffect.disableVirtualBackground();
   ```
   

   d. Switch between solid background and image background.

   ```java
   VirtualBackgroundSource source = new VirtualBackgroundSource();
   // Select image background.
   source.sourceType = VirtualBackgroundSourceType.Image;
   // Set the absolute path of the image.
   source.sourcePath = "/storage/emulated/0/Download/test.png";
   // Set background color. The format is 0xAARRGGBB. Take green as an example.
   source.sourceColor = 0XFF00FF00;
   // Select image background.
   IVideoEffect mVideoEffect = mRTCVideo.getVideoEffectInterface();
   mVideoEffect.enableVirtualBackground(", source);
   // Switch to solid background.
   source.sourceType = VirtualBackgroundSourceType.Color;
   mVideoEffect.enableVirtualBackground(", source);
   ```
   

   You may receive the following error codes.



|`enableVirtualBackground` error codes |Description |Solution |
|---|---|---|
|0 |The virtual background is enabled successfully. |NA |
|–2 |Virtual background effect file not found. |Check whether the file path in the code is correct. |
|–4 |Failed to open the background image file. |Check whether the file exists and whether you have read and write permissions for the target file. |
|–38 |Invalid image format. |Check whether the format of the input image is jpg or png. |
|–37 |Invalid image data. |Ensure that the image file is not corrupted. |
|Other error codes |See [error code table](https://docs.byteplus.com/effects/docs/error-code-table) for specific instructions. | |


<span id="api-reference"></span>
## API Reference


* Android

   * [initCVResource](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-initcvresource)

   * [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-enablevirtualbackground)

   * [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70080#IVideoEffect-disablevirtualbackground)

* iOS

   * [initCVResource:withAlgoModelDir:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCVideoEffect-initcvresource-withalgomodeldir)

   * [enableVirtualBackground:withSource:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCVideoEffect-enablevirtualbackground-withsource)

   * [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCVideoEffect-disablevirtualbackground)

* Windows

   * [initCVResource](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-initcvresource)

   * [enableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-enablevirtualbackground)

   * [disableVirtualBackground](https://docs.byteplus.com/en/docs/12/docs-70095#IVideoEffect-disablevirtualbackground)
