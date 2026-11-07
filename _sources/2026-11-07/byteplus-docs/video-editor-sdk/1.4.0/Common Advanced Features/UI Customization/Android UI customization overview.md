---
title: "Android UI customization overview"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-android-ui-customization-overview"
---

In an Android project, APK is used for packing and the conflict caused by resources with identical names will be covered. Video Editor SDK supports performing UI customization by replacing the drawable files with another file that has an identical file name, value corresponding to string and color in the hosted project. According to the UI scenes supported by EffectOneSDK, modules can be divided into several categories: the album module, the camera module, the preview editor module, the track editor module, and the base module.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cf5c2d834f19406cbca9936b0d4e8fb6~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">In the EffectOneSDK package, sample code of relevant interfaces associated with the homepage and the export page are provided for demonstration purposes. You need to modify the sample code based on own business logic .</div>


<span id="8bf760cc"></span>
# UI customization

The BytePlus Video Editor SDK is a comprehensive audio and video editing SDK equipped with user interfaces (UIs). Users have the flexibility to customize several UI elements, including theme colors, text, and icons. This level of customization empowers developers to tailor the visual experience of their applications according to their preferences and branding requirements.

<span id="8237845b"></span>
## Theme color: color chart

The color chart comes with key\-value pairs for all colors that can be changed in BytePlus Video Editor SDK. For more information, refer to


* [Video Editor SDK Color Chart](https://docs.byteplus.com/docs/video-editor-sdk/140-video-editor-sdk-color-chart).

* `default_res_files/v_x_x/res/color/eo_color_card.xml` in the demo project.

* [Customizable UI overview](https://docs.byteplus.com/docs/video-editor-sdk/140-android-ui-customization-overview#0cb91ca0).


<span id="e94ea4ad"></span>
### Customizing color

The SDK prioritizes reading custom colors internally. If no custom colors are defined, it uses internal default colors. Custom theme colors can be set using the following API. The color names must match those defined in the color palette table.

**To customize color:** 


1. Open the `colors.xml` file under the `res/values/` directory in your project.

2. Copy the color resource item corresponding to your desired theme color to the `colors.xml` file.

3. Modify the RGBA color code.


After you complete this, the corresponding theme color for the host app will be modified.

<span id="ba524a9b"></span>
## Text

You can find all changeable texts, including texts for resources in a `string.xml` file that corresponds with your target module. In the demo project, the `string.xml` files are placed under the directory of their corresponding modules.

For specific information on the UI elements, refer to [Customizable UI overview](https://docs.byteplus.com/docs/video-editor-sdk/140-android-ui-customization-overview#0cb91ca0).

<span id="5ef56e7e"></span>
### Customizing a text

**To modify an English text for the host app**:


1. Open the `strings.xml` file of your desired module under the `default_res_files` folder.

2. Copy the string resource item that corresponds with the module to the`strings.xml`file under the `res/values/` directory in your project.

3. Modify the text.


**To modify a Chinese text for the host app**:


1. Open the `strings.xml` file of your desired module under the `default_res_files` folder.

2. Copy the string resource item that corresponds with the module to the`strings.xml`file under the `res/values-zh-rCn/` directory in your project..

3. Modify the text.


<span id="112a8209"></span>
## Icon

You can find all default `drawable` files that associated with the corresponding changeable icons in the demo project. The `drawable` files are placed under the directory of their corresponding modules. To reduce the size of package, most default icons provided by BytePlus Video Editor SDK are in SVG format. If you want to use icons in other formats, such as PNG, JPG, and WebP, the SDK also supports replacing the icons in SVG format with the ones in other image formats.

For specific information on the UI elements, refer to Android customizable UI overview.

<span id="26fc63f6"></span>
### Customizing an icon

**To replace an icon**:


1. Under the `drawable` directory in the host project, import a SVG image.

2. If you want to import a 3x PNG image, you need to import it under the `drawable-xxhdpi` directory and create an image file that has the same name as that of the image that you want to import. The suffix of the image file can be different. If you do not specify the suffix of the image file, it will be imported into the XML file as a SVG image. For more information on how to import a SVG image, refer to [Add multi-density vector graphics](https://developer.android.com/studio/write/vector-asset-studio). The original image will be placed under the `drawable` folder of the corresponding module within the `default_res_files` folder.


**To search for the key\-value pair of your desired icon for the corresponding UI elements**:

For specific information on the UI elements, refer to Android customizable UI overview.

It is suggested to import a 3x image as an icon. You can replace the icon with a PNG, JPG, WebP image that has the same file name as that of the icon that you want to replace. Also, the imported icon must be placed under the `drawable-xxhdpi` directory. If you want to replace an icon with a SVG image, the size of the SVG image must be converted into dp. You can calculate the size of a SVG image by dividing the 3x pixel value of the image by 3 or you can refer to the SVG information in the corresponding resource file.

<span id="0cb91ca0"></span>
# Customizable UI overview

This is a list of all the customizable UI screens within BytePlus Video Editor SDK:


|**Feature** |**Component** |
|---|---|
|Basic components |[Basic components UI customization](https://docs.byteplus.com/docs/video-editor-sdk/140-basic-components-ui-customization) |
|Camera |[Camera module UI](https://docs.byteplus.com/docs/video-editor-sdk/140-camera-module-ui) |
|Preview Editor |[Preview Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/140-preview-editor-feature-ui) |
|Track Editor |[Track Editor feature UI](https://docs.byteplus.com/docs/video-editor-sdk/140-track-editor-feature-ui) |
|||
|||
|||
|||
|Draft screen |[Draft mode UI](https://docs.byteplus.com/docs/video-editor-sdk/140-draft-mode-ui) |
|Music screen |[Music library panel](https://docs.byteplus.com/docs/video-editor-sdk/140-music-library-panel) |
||[Music volume panel](https://docs.byteplus.com/docs/video-editor-sdk/140-music-volume-panel) |
||[Sound effects panel](https://docs.byteplus.com/docs/video-editor-sdk/140-sound-effects-panel) |
|Album screen |[Camera roll selection screen](https://docs.byteplus.com/docs/video-editor-sdk/140-camera-roll-selection-screen) |
