---
title: "Camera roll selection screen"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-camera-roll-selection-screen"
---

This topic describes the customization of the camera roll selection screen UI based on the following:


* Album photo selection screen.

* Album photo selection preview screen.


<span id="c65b2fa1"></span>
# Album photo selection screen

This topic guides you through the process of customizing the photo selection from your album screen of your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="fa26b71f"></span>
## Album photo selection upper section

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d5cb2f5df2f418389ba3f56ed097581~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Close button |Button icon |* Replace the icon with another icon of the same name: `eo_album_list_bar_back`.<br><br>* **Recommended size (pixels)** : 48 x 48 |
|2 |Title of the album |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_title`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |All tab |Text |Change the text.<br><br><br>* **Text key**: `eo_album_all` |
|4 |Video tab |Text |Change the text.<br><br><br>* **Text key**: `eo_album_photos_videos` |
|5 |Image tab |Text |Change the text.<br><br><br>* **Text key**: `eo_album_photos` |


<span id="e90e28f1"></span>
## Photo selection section

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac65675e810f487d8a1761dd4cfc899a~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Add button |Button icon |* Replace the icon with another icon of the same name: `eo_album_picker_list_add`.<br><br>* **Recommended size (pixels)** : 24 x 24 |
|2 |The icon indicating that a resource is selected |Button icon |* Replace the icon with another icon of the same name: `eo_album_list_selected`.<br><br>* **Recommended size (pixels)** : 24 x 24 |


<span id="3a6c7a01"></span>
## Album photo selection bottom section

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c39b9a19998948d9aa6649d0fcea2bd5~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Delete button |Button icon |* Replace the icon with another icon of the same name: `eo_album_list_delete`.<br><br>* **Recommended size (pixels)** : 16 x 16 |
|2 |The prompt in the lower part of the screen |Text |Change the text.<br><br><br>* **Text key**: `eo_album_tips` |
|3 |Text for the Next button |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color.<br><br>   * **Color key**: `Primary` |
|4 |Color of the duration value |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |


<span id="cf48d906"></span>
# **Album photo selection preview screen**

This topic guides you through the process of customizing the album photo selection preview screen of your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a33d2adf9284e63890c91ec7a1f27cb~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name: `eo_album_preview_bar_back`.<br><br>* **Recommended size (pixels)** : 24 x 24 |
|2 |Add button |Icon |* Replace the icon with another icon of the same name: `eo_album_preview_add`.<br><br>* **Recommended size (pixels)** : 16 x 16 |
|3 |Text for the Add button |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_album_add`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|4 |Background of the Add button |Color |Change the color.<br><br><br>* **Color key**: `BGInput3` |
|5 |Next button |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color.<br><br>   * **Color key**: `Primary` |
|6 |Border |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|7 |Delete button |Icon |* Replace the icon with another icon of the same name: `eo_album_list_delete`.<br><br>* **Recommended size (pixels)** : 16 x 16 |
|8 |Color of the duration value |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|9 |Next button after being pressed and held |Color |Change the color.<br><br><br>* **Color key**: `ConstBGContainer` |
|10 |Background of the screen |Color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |
