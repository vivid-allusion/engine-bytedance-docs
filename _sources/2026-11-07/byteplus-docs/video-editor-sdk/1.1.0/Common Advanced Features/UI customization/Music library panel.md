---
title: "Music library panel"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/music-library-panel_1_1_0"
---

This topic guides you through the process of customizing the music library panel of your user interface (UI). Learn how to change these essential elements to meet the specific visual and functional requirements of your application.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3eb33ce75414e37abab3ce48f868abb~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Titlebar of the music library |Background color |Change the color.<br><br><br>* **Color key**: `ConstLineInverse` |
|2 |Title of the music library |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_base_addmusic_musiclibrary`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|3 |Divider between the title and list |Background color |Change the color.<br><br><br>* **Color key**: `ConstLineInverse` |
|4 |Name of a music work |Color |Change the color.<br><br><br>* **Default color key**: `TextPrimary`<br><br>* **Color key of a selected item**: `Primary` |
|5 |Artist of the music work |Color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|6 |Length of the music work |Color |Change the color.<br><br><br>* **Color key**: `TextTertiary` |
|7 |Border of the selected music work |Background color |Change the color.<br><br><br>* **Color key**: `Primary` |
|8 |The .gif image indicating that a music work is being played |GIF icon |* Replace the icon with another icon of the same name: `eo_base_music_playing`.<br><br>* **Recommended size (pixels)** : 84 × 84 |
|9 |Play icon |Icon |* Replace the icon with another icon of the same name: `eo_base_music_play`.<br><br>* **Recommended size (pixels)** : 72 × 72 |
|10 |The icon indicating whether a music work is downloaded |Icon |* Replace the icon with another icon of the same name.<br><br>   * The icon indicating that a music work is not downloaded: `eo_base_download_remote`.<br><br>      * **Recommended size (pixels)** : 36 × 36<br><br>   * The icon indicating that a music work is being downloaded: `eo_base_download_downloading`.<br><br>      * **Recommended size (pixels)** : 36 × 36 |
|11 |The icon indicating that original sound is enabled |Icon |* Replace the icon with another icon of the same name.<br><br>   * **Enabled:**  `eo_base_music_select_icon`<br><br>      * **Recommended size (pixels)** : 48 × 48<br><br>   * **Disabled**: `eo_base_music_unselect_icon`<br><br>      * **Recommended size (pixels)** : 48 × 48 |
|12 |Original sound text |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**: `eo_base_musicvoice_original_sound`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|13 |Volume icon |Icon |* Replace the icon with another icon of the same name: `eo_base_music_volume_icon`.<br><br>* **Recommended size (pixels)** : 60 × 60 |
|14 |Text for the Volume icon |Text<br><br>Text color |* Change the text.<br><br>   * **Text key**: `eo_base_musicvoice_volume`<br><br>* Change the color.<br><br>   * **Color key**: `TextPrimary` |
|15 |Background of a listed item |Background color |* Change the color.<br><br>   * **Default color key**: `BGPrimary2`<br><br>   * **Color key of a selected item**: `ConstBGContainer7` |
|16 |Background of the entire list |Background color |Change the color.<br><br><br>* **Color key**: `BGPrimary2` |
