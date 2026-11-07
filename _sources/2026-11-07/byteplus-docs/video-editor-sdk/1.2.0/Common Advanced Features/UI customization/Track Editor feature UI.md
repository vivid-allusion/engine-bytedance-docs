---
title: "Track Editor feature UI"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/120-track-editor-feature-ui"
---

This topic describes the customization of the Track Editor feature's UI based on the following:


* Playback control bar.

* Track panel.

* Bottom toolbar.

* Functional panels.

* Full\-screen preview UI.

* Cancellation pop\-up message window.


<span id="274738dd"></span>
# Playback control bar

This topic guides you through the process of customizing the playback control bar within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d1c76ba260f42ac9ce9dff690af258c~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The progress and total duration |Text color |Change the color. You can change the text color for the progress and the total duration separately.<br><br><br>* **Color key for progress bar**: `TextTertiary`<br><br>* **Color key for the** **total duration**: `TextQuaternary` |
|2 |The icon indicating that playback is in progress, which pauses the playback after you click it |Button icon |* Replace the icon with another icon of the same name.: `eo_base_player_pause`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|3 |Undo button, which is greyed out |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_undo_disable`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|4 |Redo button, which is greyed out |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_redo_disable`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|5 |Full screen preview button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_fullscreen`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|6 |The icon indicating that the playback is paused, which resumes the playback after you click it |Button icon |* Replace the icon with another icon of the same name: `eo_base_player_play`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|7 |Undo button, which is clickable |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_undo_enable`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|8 |Redo button, which is clickable |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_redo_enable`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|9 |Playback control bar |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary` |


<span id="23e6f8f8"></span>
# Track panel

This topic guides you through the process of customizing the track panel within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="dfacc9d2"></span>
## Timeline

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f40fbc2621d4c6296d809a8c3f16f51~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Timescale in the track area |Color of the timescale |Change the color.<br><br><br>* **Color key**: `TextTertiary` |


<span id="980270aa"></span>
## Main track

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40273f06655449469860e156916af373~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |The icon indicating that original sound is enabled. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_unmuted`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|2 |The icon for no transition between two clips. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_add_transition`.<br><br>* **Recommended size (pixels**): 72 × 72 |
|3 |The icon for a transition between two clips. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_transition`.<br><br>* **Recommended size (pixels)** : 72 × 72 |
|4 |The icon for the default soundtrack. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_none_music`.<br><br>* **Recommended size (pixels)** : 72 × 72 |
|5 |Text for the default soundtrack. |Text<br><br>Text color |* Change the text.<br><br>   * **Text key**: `eo_base_addsound`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|6 |The border of a selected clip on the track. |Border color |Change the color.<br><br><br>* **Color key**: `BGTertiary` |
|7 |Default soundtrack. |Background color |Change the color.<br><br><br>* **Color key**: `ConstBGContainer_Dark` |
|8 |The icon for adding resources. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_add`.<br><br>* **Recommended size (pixels)** : 96 × 96 |
|9 |Background of the track. |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary` |
|10 |The icon indicating that original sound is disabled. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_muted`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|11 |The left slider of a clip that is being edited on the track. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_clip_btn_left`.<br><br>* **Recommended size (pixels)** : 21 × 48 |
|12 |Tag for the length of a clip on the main track. |Color of text on the tag |Change the color.<br><br><br>* **Color key**: `TextSecondary` |
|13 |Tag for speed change of a clip on the main track. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_speed_tag`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|14 |Tag for a silent clip on the main track. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_muted_tag.xml`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|15 |Tag for voice change of a clip on the main track. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_voice_change_tag.xml`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|16 |The right slider of a clip that is being edited on the track. |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_clip_btn_right.xml`.<br><br>* **Recommended size (pixels)** : 21 × 48 |


<span id="78a4c6ab"></span>
## Music and sound effects track

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac55a8c5267147faa7351f4c5e8abff6~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Tag for the name of a sound track |Color of text on the tag |Change the color.<br><br><br>* **Color key**: `TextSecondary` |
|2 |Tag for a silent sound track |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_muted_tag.xml`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|3 |Tag for speed change of a sound track |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_speed_tag.xml`.<br><br>* **Recommended size (pixels)** : 36 × 36 |
|4 |Background of a tag |Background color |Change the color.<br><br><br>* **Color key**: `ConstBGContainer5` |
|5 |Sound wave on the background music track |Color of the sound wave |Change the color.<br><br><br>* **Color key**: `AssistColorPinkMask` |
|6 |Background of the background music track |Background color |Change the color.<br><br><br>* **Color key**: `AssistColorPink1` |
|7 |Background of a sound effect track |Background color |Change the color.<br><br><br>* **Color key:**  `AssistColorPurple1` |


<span id="361b1672"></span>
# Bottom toolbar

This topic guides you through the process of customizing the bottom toolbar within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9711913320564088a52c5379ad1254e0~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Toolbar |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary` |
|2 |Split button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_split`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|3 |Replace button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_replace`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|4 |Delete button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_delete`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|5 |Speed button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_speed`.<br><br>* **Recommended size (pixels**): 84 × 84 |
|6 |Music button for adding background music or sound effects |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_music`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|7 |Crop button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_crop`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|8 |Rotate button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_rotate`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|9 |Volume button |Button icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_volume`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|10 |Text for the Split button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_split`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|11 |Text for the Replace button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_replace`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|12 |Text for the Delete button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_delete`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|13 |Text for the Speed button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_speed`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|14 |Text for the Music button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_sound`<br><br>* Change the color.<br><br>   * **Color key**:`TextSecondary` |
|15 |Text for the Crop button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_crop`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|16 |Text for the Rotate button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_rotate`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|17 |Text for the Volume button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_volume`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|18 |Level\-2 back button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_back`.<br><br>* **Recommended size (pixels)** : 72 × 72 |
|19 |Replace Music button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_replace`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|20 |Add Sound Effects button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_music_add_soundeffects`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|21 |Add Music button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_func_music_add_music`<br><br>* **Recommended size (pixels)** : 84 × 84 |
|22 |Text for the Replace Music button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_sound_replacemusic`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|23 |Text for the Add Music button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_sound_addmusic`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |
|24 |Text for the Add Sound Effects button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_sound_addsoundeffects`<br><br>* Change the color.<br><br>   * **Color key**: `TextSecondary` |


<span id="b27855fa"></span>
# Functional panels

This topic guides you through the process of customizing the functional toolbar within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

This topic guides you through the process of customizing the functional toolbar within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span id="053fc567"></span>
## Speed change panel

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deddbafb1ad6411eb713e3b932b9e387~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Apply to all button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_apply_to_all`.<br><br>* **Recommended size (pixels)** : 48 × 48 |
|2 |Text for the Apply to all button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_apply_to_all`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |Scale values indicating fixed multiples of the original speed |Color of the scale value |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|4 |Scale value of the currently selected speed |Color of the scale value |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|5 |Scale line of a speed (not highlighted) |Color of the scale line |Change the color.<br><br><br>* **Color key**: `TextQuaternary` |
|6 |Scale line of a speed (highlighted) |Color of the scale line |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|7 |Speed slider |* Color of the slider<br><br>* Color of the slider border |* Change the color.<br><br>   * **Color key**: `TextPrimary`<br><br>* Change the fill color.<br><br>   * **Color key**: `TextPrimary` |
|8 |Cancel button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_cancel`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|9 |Done button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_done`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|10 |Background |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary3` |


<span id="0eb97983"></span>
## Volume panel

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7bc6dc3422cc4bfa8e1ad065601e7480~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Apply to all button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_apply_to_all`.<br><br>* Recommended size (pixels): 48 × 48 |
|2 |Text for the Apply to all button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_apply_to_all`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |Selected part of the seekbar |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|4 |Value of the current volume |Text color |Change the color.<br><br><br>* Color key: `TextPrimary` |
|5 |Unselected part of the seekbar |Color |Change the color.<br><br><br>* Color key: `BGInput3` |
|6 |Volume slider |Color of the slider<br><br>Color of the slider border |* Change the color.<br><br>   * **Color key**: `TextPrimary`<br><br>* Change the fill color.<br><br>   * **Color key**: `TextPrimary` |
|7 |Cancel button |Text content<br><br>Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_cancel`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|8 |Done button |Text content<br><br>Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_done`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|9 |Background |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary3` |


<span id="1f929fc3"></span>
## Transition panel

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd52f60ee61a4dbbb8cb7fbe6aa0dc51~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Apply to all button |Icon |* Replace the icon with another icon of the same name: `eo_trackeditor_apply_to_all`.<br><br>* **Recommended size (pixels)** : 48 × 48 |
|2 |Text for the Apply to all button |* Text content<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_trackeditor_apply_to_all`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |Border of a selected transition |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|4 |The icon indicating whether a resource is downloaded |Icon |* Replace the icon that indicates a resource is not downloaded with another icon of the same name: `eo_base_download_remote`.<br><br>   * **Recommended size (pixels)** : 36 × 36<br><br>* Replace the icon that indicates a resource is being downloaded with another icon of the same name: `eo_base_download_downloading`.<br><br>   * **Recommended size (pixels)** : 36 × 36 |
|5 |Name of an unelected transition |Text color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|6 |Background |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary3` |
|7 |None button |Icon |* Replace the icon with another icon of the same name: `eo_base_item_none`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|8 |Background of the None button |Background color |Change the color.<br><br><br>* **Color key**: `ConstBGContainer_Dark` |
|9 |Minimum length of a transition |Text color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|10 |Name of a selected transition |Text color |Change the color.<br><br><br>* **Color key**: `Primary` |
|11 |Selected part of the seekbar |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|12 |Slider |* Color of the slider<br><br>* Color of the slider border |* Change the color.<br><br>   * **Color key**: `TextPrimary`<br><br>* Change the fill color.<br><br>   * **Color key**: `TextPrimary` |
|13 |Unselected part of the seekbar |Color |Change the color.<br><br><br>* **Color key**: `BGInput3` |
|14 |Maximum length of a transition |Text color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |


<span id="b1958c94"></span>
## Crop screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e403f7e1d6ad420eb0280f656c9fa58c~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Current progress |Text color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|2 |Total duration |Text color |Change the color.<br><br><br>* **Color key**: `TextQuaternary` |
|3 |Play/Pause button |Button icon |* Replace the icon with another icon of the same name.<br><br>   * **Pause**: `Resource key: eo_base_player_pause`<br><br>      * **Recommended size (pixels)** : 63 × 60<br><br>   * **Play**: `Resource key: eo_base_player_play`<br><br>      * **Recommended size (pixels)** : 60 × 60 |
|4 |Angle scale value |Text color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|5 |Angle scale value (not highlighted) |Text color |Change the color.<br><br><br>* **Color key**: `TextQuaternary` |
|6 |Angle scale value (highlighted) |Text color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|7 |Scale value and scale line of a selected angle (highlighted) |Text color |Change the color.<br><br><br>* **Color key**: `Primary` |
|8 |Reset button |Text color |Change the color.<br><br><br>* **Color key for disabled Reset button**: `TextQuaternary`<br><br>* **Color key for enabled Reset button**: `TextPrimary` |
|9 |Done button |Text color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |


<span id="665bea93"></span>
# Full\-screen preview UI

This topic guides you through the process of customizing the full screen preview screen within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/941c1aec08694737bfcf88e9a572410c~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Icon |* Replace the icon with another icon of the same name: `eo_previeweditor_back`.<br><br>* Recommended size (pixels): 96 × 96 |
|2 |The icon indicating that playback is paused |Icon |Replace the icon with another icon of the same name: `eo_base_player_play_large`. |
|3 |The icon indicating that playback is paused in the lower part of the screen |Icon |Replace the icon with another icon of the same name.<br><br><br>* **Paused**: `eo_base_player_play`<br><br>* **Playing**: `eo_base_player_pause`<br><br>* **Recommended size (pixels)** : 60 × 60 |
|4 |The played part in the progress bar |Color |Change the color.<br><br><br>* **Color key**: `Primary` |
|5 |Slider |Color |Change the color.<br><br><br>* **Color key**: `TextPrimary` |
|6 |Time value of current progress |Text color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|7 |Total duration |Text color |Change the color.<br><br><br>* **Color key**: `TextQuaternary` |


<span id="3c2af6b9"></span>
# Cancellation pop\-up message window

This topic guides you through the process of customizing the cancellation pop\-up message window within your Track Editor user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa35cd238948416a9255ca599e63f834~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Title of the pop\-up window |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popup_confirmcancel` |
|2 |Content of the pop\-up window |Text |Change the text.<br><br><br>* Text key: `eo_base_popout_cancelwarn` |
|3 |No button |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popout_no` |
|4 |Confirm button |Text |Change the text.<br><br><br>* **Text key**: `eo_base_popout_confirmm` |
