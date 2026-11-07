---
title: "Camera module UI"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/camera-module-ui"
---

This topic describes the customization of the camera feature's UI based on the following:


* Main interface customization.

* Sidebar customization.

* Functional panels customization.


<span id="5bcb7440"></span>
# Camera feature main interface

This topic guides you through the process of customizing main interface camera feature components within your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="9d90a379"></span>
## Back button

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d6e0d958e844480985286dceab0d0c6~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name:`eo_camera_close`.<br><br>* **Recommended size (pixels)** : 72 × 72 |


<span id="a09146ad"></span>
## Add music button

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f45a5f0feb84cd6840534641cfe7d50~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Icon for the Add Music button |Button icon |* Replace the icon with another icon of the same name: `eo_base_music_icon`.<br><br>* **Recommended size (pixels)** : 72 × 72 |
|2 |Text for the Add Music button |Text<br><br>Color |* Change the text.<br><br>   * **Text Key:**  `eo_base_addsound`<br><br>   * **Updated Text:**  [Specify the updated text]<br><br>* Change the color.<br><br>   * **Color Key:**  `TextPrimary`<br><br>   * **Updated Color:**  [Specify the updated color] |
|3 |Background of the button |Color |Change the color.<br><br><br>* **Color Key:**  `BGInverse2`<br><br>* **Updated Color:**  [Specify the updated color] |
|4 |Delete button |Button icon |* Replace the icon with another icon of the same name: `eo_base_music_remove`.<br><br>* **Recommended size (pixels)** : 43 × 43 |
|5 |Divider |Color |Change the color.<br><br><br>* **Color Key:**  `ConstLineInverse2`<br><br>* **Updated Color:**  [Specify the updated color] |


<span id="a41add55"></span>
## Shutter button

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f45a5f0feb84cd6840534641cfe7d50~tplv-goo7wpa0wc-image.image) </span>


|**Number** |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Inner circle icon indicating no video recording |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|2 |Outer ring icon indicating no video recording |Color |Change the color.<br><br><br>* **Color key**: `Tertiary` |
|3 |Progress bar for video recording |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|4 |Button indicating video recording |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|5 |Delete button for recorded clip |Button icon |* Replace the icon with another icon of the same name: `eo_camera_delete`.<br><br>* **Recommended size (pixels)** : 120 × 120 |
|6 |Outer ring icon indicating no photo taken |Color |Change the color.<br><br><br>* **Color key**: `ConstTextInverse4` |
|7 |Node of a recorded clip |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|8 |Confirm button for deletion of recorded clip |Button icon |* Replace the icon with another icon of the same name: `eo_camera_confirm`.<br><br>* **Recommended size (pixels)** : 120 × 120 |
|9 |Background for video recording |Color |Change the color.<br><br><br>* **Color key**: `ConstBGContainer4` |


<span id="fb158bdc"></span>
## Camera mode bar

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b75b825e75fc4237b400b6fae4f3e2e2~tplv-goo7wpa0wc-image.image) </span>


|**No** |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |2\-minute Video Recording Mode |Text |Update the text.<br><br><br>* **Text key**: `eo_camera_modes_2m` |
|2 |30\-second Video Recording Mode |Text |Update the text.<br><br><br>* **Text key**: `eo_camera_modes_30s` |
|3 |15\-second Video Recording Mode |Text |Update the text.<br><br><br>* **Text key**: `eo_camera_modes_15s` |
|4 |Photo\-taking Mode |Text |Update the text.<br><br><br>* **Text key**: `eo_camera_modes_photo` |
|5 |Selected Mode |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|6 |Unselected Mode |Color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|7 |Circle of a Selected Mode |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|8 |Background |Color |Change the color.<br><br><br>* **Color key**: `BGPrimary` |


<span id="80c87182"></span>
## Effect Sticker button

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df005d274d0047259ed689f43f3b03c5~tplv-goo7wpa0wc-image.image) </span>


|**No** |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Default Icon of the Effect Sticker Button |Button icon |* Replace with another icon of the same name, `eo_camera_effectssticker`.<br><br>* **Recommended size (pixels)** : 108 × 108 |
|2 |Text for the Effect Sticker Button |Text |* Change the text.<br><br>   * **Text key**: `eo_camera_effectssticker`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |


<span id="627749bd"></span>
## Upload button

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59f808aa270648bdaf3d5ba5e642175a~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Default icon<br><br>It changes to the image of the first photo or video in the local album after you grant. |Button icon |* Replace the icon with another icon of the same name: `eo_camera_upload`<br><br>* **Recommended size (pixels)** : 108 × 108 |
|2 |Text for the Photo Library button |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_camera_upload`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |


<span id="7f46f31a"></span>
# Sidebar customization

This topic guides you through the process of customizing the sidebar within your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/94e643d2a10b444da435c7e9c5d759ff~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Flip button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name: `eo_camera_flip`.<br><br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text ke**y: eo_camera_flip<br><br><br>Change the color.<br><br><br>* **Color key**: ConstTextInverse1 |
|2 |Flash button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name:<br><br><br>* **Enabled**: `eo_camera_flash_off`<br><br>* **Disabled**: `eo_camera_flash_on`<br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text key**: `eo_camera_flash`<br><br><br>Change the color.<br><br><br>* **Color key**: `ConstTextInverse1` |
|3 |Timer button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name.<br><br><br>* **3s**: `eo_camera_timer_3s`<br><br>* **10s**: `eo_camera_timer_10s`<br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text key**: `eo_camera_timer`<br><br><br>Change the color.<br><br><br>* **Color key**: `ConstTextInverse1` |
|4 |Filter button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name: `eo_camera_filter`<br><br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text key**: `eo_camera_filters`<br><br><br>Change the color.<br><br><br>* **Color key**: `ConstTextInverse1` |
|5 |Beauty button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name:<br><br><br>* **Disabled**: eo_camera_beauty_off<br><br>* **Enabled**: eo_camera_beauty_on<br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text key**: `eo_camera_beauty`<br><br><br>Change the color.<br><br><br>* **Color key**: `ConstTextInverse1` |
|6 |Speed button |Button icon<br><br>Text<br><br>Text color |Replace the icon with another icon of the same name:<br><br><br>* **0.3x**: eo_camera_speed_0_3x<br><br>* **0.5x**: eo_camera_speed_0_5x<br><br>* **1x**: eo_camera_speed_1x<br><br>* **2x**: eo_camera_speed_2x<br><br>* **3x**: eo_camera_speed_3x<br><br>* **Recommended size (pixels)** : 96 × 96<br><br><br>Change the text.<br><br><br>* **Text key**: `eo_camera_speed`<br><br><br>Change the color.<br><br><br>* **Color key**: `ConstTextInverse1` |
|7 |Expand/Collapse button |Button icon |Replace the icon with another icon of the same name:<br><br>`eo_base_vertical_toolbar_more`.<br><br>**Recommended size (pixels)** : 72 × 72 |


<span id="cc24de03"></span>
# Functional panels customization

This topic guides you through the process of customizing the functional panels within your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="112cfc84"></span>
## Timer

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d161677c70494eb28a68629a51e67cbd~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The prompt text indicating how to set the timer |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_camera_timer_setduration`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|2 |Time values at the start and end of the time progress bar |Color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|3 |Background of the progress bar |Color |Change the color.<br><br>**Color key**:<br><br><br>* **Not recorded part**: `ConstBGContainer8`<br><br>* **Recorded part**: `ConstBGContainer_Dark`<br><br>* **Vertical parts in the middle**: `TextTertiary` |
|4 |Start countdown button |Text<br><br>Color |* Change the text.<br><br>   * **Text key**: `eo_camera_timer_countdown`<br><br>* Change the color.<br><br>   * **Color key**:<br><br>      * **Background**: `Primary`<br><br>      * **Text**: `TextPrimary1` |
|5 |Countdown mode selection button |Color |Change the color.<br><br><br>* Color key:<br><br>   * **Background of the unselected mode**: `ConstBGContainer5`<br><br>   * **Background of the selected mode**: `ConstBGContainer_Dark`<br><br>   * **Text of the unselected mode**: `TextTertiary`<br><br>   * **Text of the selected mode**: `TextPrimary` |
|6 |Value of the current progress in the progress bar |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|7 |Pointer of the current progress in the progress bar |Button icon |* Replace the icon with another icon of the same name: `eo_camera_countdown_slider_thumb`.<br><br>* **Recommended size (pixels)** : 30 × 168 |
|8 |Background of the Timer panel |Color |Change the color.<br><br><br>* **Color ke**y: `BGPrimary2` |


<span id="cffadf7d"></span>
## Filter

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a9be62b432d420e8ba79bbc2040f459~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Intensity bar |Color |Change the color.<br><br><br>* **Color key**:<br><br>   * **Foreground**: `Primary`<br><br>   * **Background**: `BGInput3` |
|2 |Title of the Filter panel |Text |Change the text.<br><br><br>* **Text key**: `eo_previeweditor_filter_title` |
|3 |None button |Button icon<br><br>Text |* Replace the icon with another icon of the same name: `eo_base_item_none`.<br><br>* **Recommended size (pixels)** : 84 × 84<br><br>* Change the text.<br><br>   * **Text key**: `eo_base_item_none` |
|4 |Border of a selected filter |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|5 |Current intensity |Button icon<br><br>Color |* Replace the icon with another icon of the same name: `eo_base_panel_slider_thumb`.<br><br>* **Recommended size (pixels) for iOS**: 108 × 108<br><br>* **Recommended size (pixels) for Android**: 60 × 60<br><br>* Change the color.<br><br>   * **Color key**: `Primary`<br><br>   * **Intensity**: `TextPrimary` |
|6 |Background of the Filter tab |Color |Change the color.<br><br><br>* **Color key**: `BGSecondary4` |
|7 |Background of the Filter panel |Color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |
|8 |The icon indicating that a filter is being downloaded |Button icon |* Replace the icon with another icon of the same name: `eo_base_download_downloading`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|9 |The icon indicating that a filter is not downloaded |Button icon |* Replace the icon with another icon of the same name: `eo_base_download_remote`.<br><br>* **Recommended size (pixels)** : 36 × 36 |


<span id="9b7a0d02"></span>
## Beauty effects tab

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/15e20d9865de448c9a512b23776b5e05~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Intensity bar |Color |Change the color.<br><br><br>* **Color key**:<br><br>   * Foreground: `Primary`<br><br>   * Background: `BGInput3` |
|2 |Text of a tab |Color |Change the color.<br><br><br>* **Color key**:<br><br>   * Selected: `TextPrimary`<br><br>   * Unselected: `TextTertiary` |
|3 |None button |Button icon<br><br>Text |* Replace the icon with another icon of the same name: `eo_base_item_none`.<br><br>* **Recommended size (pixels)** : 84 × 84<br><br>* Change the text.<br><br>   * **Text key**: `eo_base_item_none` |
|4 |Border of a selected beauty effect |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|5 |Current intensity |Color |* Replace the icon with another icon of the same name: `eo_base_panel_slider_thumb`.<br><br>* **Recommended size (pixels) for iOS**: 108 × 108<br><br>* **Recommended size (pixels) for Android**: 60 × 60<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|6 |Reset icon |Button icon |* Replace the icon with another icon of the same name`eo_camera_beauty_reset`.<br><br>* **Recommended size (pixels)** : 48 × 48 |
|7 |Background of a tab |Color |Change the color.<br><br><br>* **Color key**: `BGSecondary4` |
|8 |Background of the panel |Color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |


<span id="7bca5376"></span>
## Beauty effect—Reset confirmation message

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/757638245cf44dccb6f2e78453ff5f93~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The confirmation text message confirming whether to reset the beauty effects. |Text |Change the text.<br><br><br>* Text key: `eo_base_popup_resetbeauty` |
|2 |Text for the No button. |Text |Change the text.<br><br><br>* Text key: `eo_base_popout_no` |
|3 |Text for the Yes button. |Text |Change the text.<br><br><br>* Text key: `eo_base_popout_confirm` |


<span id="c9d8df9b"></span>
## Beauty effects—Prompt message

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/53a95afeac174d0f92555bd33ba953f9~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The prompt text indicating a conflict between a beauty effect and an effect sticker |Text |Change the text.<br><br>Text key: `eo_camera_toast_beauty_items_conflict_with_stick` |


<span id="e5946f58"></span>
## Speed bar

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/59c55b1357c641ab85a18627a257d980~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Text of an unselected speed |Color |Change the color.<br><br><br>* Color key: `TextPrimary2` |
|2 |Text of a selected speed |Color |Change the color.<br><br><br>* Color key: `ConstTextInverse1` |
|3 |Background of a selected speed |Color |Change the color.<br><br><br>* Color key: `ConstBGContainer9` |
|4 |Background of an unselected speed |Color |Change the color.<br><br><br>* Color key: `BGInverse3` |


<span id="77960730"></span>
## Facial stickers

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4c3365f2ea948b7844f269efea688f1~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The Unselect button for an effect sticker |Button icon |* Replace the icon with another icon of the same name: `eo_base_unselect`<br><br>* **Recommended size (pixels)** : 72 × 72 |
|2 |Selected tab |Color |Change the color.<br><br><br>* **Color key**:<br><br>   * **Selected**: `TextPrimary`<br><br>   * **Unselected**: `TextTertiary` |
|3 |Border of a selected effect |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|4 |Background of the tabs |Color |Change the color.<br><br><br>* **Color key**: `BGSecondary4` |
|5 |Background of the panel |Color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |


<span id="eaf66c8a"></span>
## Exit panel

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/054d03653d4241a4b40c682c6f775619~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Text for the Discard button |Text |Change the text.<br><br><br>* **Text key**: `eo_camera_discard` |
|2 |Text for the Start over button |Text |Change the text.<br><br><br>* **Text key**: `eo_camera_startover` |
|3 |Text for the Cancel button |Text |Change the text.<br><br><br>* **Text key**: `eo_camera_cancel` |
|4 |Background of the panel |Color |Change the color.<br><br><br>* **Color key**: `BGContainerModal` |
|5 |Thin divider |Color |Change the color.<br><br><br>* **Color key**: `LinePrimary` |
|6 |Thick divider |Color |Change the color.<br><br><br>* **Color key**: `LineDarker` |


<span id="80da2ec0"></span>
## Confirmation dialog box for discarding last clip

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4347100f8a8c4965948dcffd3e4193d2~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The prompt text |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popup_discardclip` |
|2 |Text for the No button |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popout_no` |
|3 |Text for the Confirm button |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popout_confirm` |


<span id="d6eeb591"></span>
## Focus and exposure adjustment

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/daae7843ca3d4973accbcf100d7fa4b4~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Focus icon |Button icon |* Replace the icon with another icon of the same name: `eo_camera_focus`.<br><br>* **Recommended size (pixels)** : 180 × 180 |
|2 |Exposure icon |Button icon |* Replace the icon with another icon of the same name: `eo_camera_exposure`.<br><br>* **Recommended size (pixels)** : 54 × 54 |
