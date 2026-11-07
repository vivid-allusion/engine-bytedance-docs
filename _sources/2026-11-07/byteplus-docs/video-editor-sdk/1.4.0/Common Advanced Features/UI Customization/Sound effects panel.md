---
title: "Sound effects panel"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/140-sound-effects-panel"
---

This topic guides you through the process of customizing the sound effects selection panel of your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d96d66d6289544769626f7c60182903c~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Titlebar of the panel |Background color |Change the color.<br><br><br>* **Color key**: `ConstLineInverse` |
|2 |Title of the panel |Text<br><br>Text color |* Change the text.<br><br>   * **Text key**: `eo_base_addmusic_musiclibrary`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |Name of a sound effect |Color |* Change the color.<br><br>   * **Default color key**: `TextPrimary`<br><br>   * **Color key of a selected item**: `Primary` |
|4 |Length of a sound effect |Color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|5 |The icon indicating the playback status of a sound effect |Icon |* Replace the icon with another icon of the same name.<br><br>   * **Default icon:**  `eo_base_sound_effect_item_image_cover`.<br><br>      * **Recommended size (pixels)** : 60 × 60<br><br>   * **The .gif icon** **indicating that a sound effect is being played**:`eo_base_music_playing`.<br><br>      * **Recommended size (pixels)** : 84 × 84 |
|6 |The icon indicating the download status of a sound effect |Icon |* Replace the icon with another icon of the same name.<br><br>   * **The icon** **indicating that a sound effect is not downloaded**: `eo_base_music_sound_effect_remote`.<br><br>      * **Recommended size (pixels)** : 48 × 48<br><br>   * **The icon** **indicating that a sound effect is being downloaded**: `eo_base_download_downloading`.<br><br>      * **Recommended size (pixels)** : 36 × 36 |
|7 |Use button |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * **Text key**: `eo_base_addsoundeffects_use`<br><br>* Change the text color.<br><br>   * **Color key**: `ConstTextInverse3`<br><br>* Change the background color.<br><br>   * **Color key**: `Primary` |
|8 |Background of a sound effect |Background color |Change the color.<br><br><br>* **Default color key**: `BGPrimary2`<br><br>* **Color key of a selected item**: `ConstBGContainer7` |
|9 |Background of the entire list |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |
