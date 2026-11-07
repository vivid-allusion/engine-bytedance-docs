---
title: "Camera roll selection screen"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/160-camera-roll-selection-screen"
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

<span id="29f7f20b"></span>
### General features

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/532a86efdaee45e0b5371405e8da195a~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Delete button |Button icon |* Replace the icon with another icon of the same name: `eo_album_list_delete`.<br><br>* **Recommended size (pixels)** : 16 x 16 |
|2 |The prompt in the lower part of the screen |Text |Change the text.<br><br><br>* **Text key**: `eo_album_tips` |
|3 |Text for the Next button |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color.<br><br>   * **Color key**: `Primary` |
|4 |Color of the duration value |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|5 |Count of selected materials |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_tips_selectedCount`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |


<span id="d9572a5d"></span>
### Magic Template feature

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd4f35d876734d129afdb2773ab3b946~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Text for the count of selected materials |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_tips_selectedCount`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|2 |Material order |* Text<br><br>* Color |* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|3 |Delete button |Icon |* Replace the icon with another icon of the same name:<br><br>   * **Text key**: `eo_album_list_delete`<br><br>   * **Recommended size**: 54 x 54 |
|4 |Material duration in the slot |Color |* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|5 |Prompt for the slot |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_material_tips`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|6 |Border |Color |* Change the color.<br><br>   * **Color key**: `Primary` |
|7 |Next button |* Text<br><br>* Color<br><br>* Background color cannot be clicked by the button |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color of text.<br><br>   * **Color key**: `TextQuaternary`<br><br>* Change the background color which cannot be clicked by the button.<br><br>   * **Color key**: `BGInput3` |
|8 |Next |Background color can be clicked by the button |* Change the color of text.<br><br>   * **Color key**: `TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**: `Primary` |


<span id="b9a0a9bc"></span>
### Magic Template replacement feature

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/65d858c287794fe39e47ac53b3581e07~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The prompt in the lower part of the screen |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_material_replace_tips`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|2 |Confirm |* Text and the color of the text<br><br>* Background color |* Change the text.<br><br>   * **Text key**: `eo_album_confirm_sure`<br><br>* Change the color of text.<br><br>   * **Color key**: `TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**: `Primary` |


<span id="cf48d906"></span>
# **Album photo selection preview screen**

This topic guides you through the process of customizing the album photo selection preview screen of your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="b0541c9d"></span>
## General features

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec54d0dda24a4ef99a276a5d163e663a~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name: `eo_album_preview_bar_back`.<br><br>* **Recommended size (pixels)** : 72 x 72 |
|2 |Add button |Icon |* Replace the icon with another icon of the same name: `eo_album_select`.<br><br>* **Recommended size (pixels)** : 48 x 48 |
|3 |Text for the Add button |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_add`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|4 |Next button |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color.<br><br>   * **Color key**: `Primary` |
|5 |Delete button |Icon |* Replace the icon with another icon of the same name: `eo_album_list_delete`.<br><br>* **Recommended size (pixels)** : 54 x 54 |
|6 |Color of the duration value |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|7 |Count of selected materials |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_tips_selectedCount`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |


<span id="09a60674"></span>
## Magic Template feature

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/78087898c59748d3b8341f397b9145ee~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Text for the count of selected materials |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_tips_selectedCount`<br><br>* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|2 |Material order |Text color |* Change the color.<br><br>   * **Color key**: `TextTertiary` |
|3 |Material duration in the slot |Color |* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|4 |Add button |Icon |* Replace the icon with another icon of the same name: `eo_album_select`.<br><br>* **Recommended size (pixels)** : 48 x 48 |
|5 |Text for the Add button |* Text<br><br>* Color |* Change the text.<br><br>   * **Text key**: `eo_album_add`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|6 |Delete button |Icon |* Replace the icon with another icon of the same name:<br><br>   * `eo_album_list_delete`<br><br>   * **Recommended size**: 54 \* 54 |
|7 |Border |Color |* Change the color.<br><br>   * **Color key**: `Primary` |
|8 |Next button |* Text<br><br>* Color<br><br>* Background color cannot be clicked by the button |* Change the text.<br><br>   * **Text key**: `eo_album_confirm`<br><br>* Change the color of text.<br><br>   * **Color key**: `TextQuaternary`<br><br>* Change the background color which cannot be clicked by the button.<br><br>   * **Color key**: `BGInput3` |
