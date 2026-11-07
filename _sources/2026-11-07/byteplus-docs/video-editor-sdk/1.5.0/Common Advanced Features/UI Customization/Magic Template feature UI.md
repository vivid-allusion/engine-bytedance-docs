---
title: "Magic Template feature UI"
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-magic-template-feature-ui"
---

This topic describes the customization of the Magic Template feature UI based on the following pages:


* Template page.

* Album page.

* Edit page.

* Export page.

* Highlight clipping page.


<span id="9ef88af6"></span>
# Template page

You can customize the template page in Video Editor SDK.

<span id="097fad57"></span>
## Template list page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/44ec8078bb0640b690408b1f92ecb6b5~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_view_back`<br><br>   * **Recommended size (pixels):**  108 x 108 |
|2 |Page title |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_list_magictemplates`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|3 |Material |* Text color<br><br>* Background color |* Change the text color.<br><br>   * **Text key**：`TextSecondary`<br><br>* Change the background color.<br><br>   * **Color key**：`ConstBGContainer5` |
|4 |Template title |Text color |* Change the text color.<br><br>   * **Color key**：`TextSecondary` |


<span id="d4fb5f8e"></span>
## Template preview page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb0d6439a59849eeb4fd2ae85e2beff1~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_view_back`<br><br>   * **Recommended size (pixels)** : 108 x 108 |
|2 |EffectOne button |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_view_magictemplates`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the background color of the button<br><br>   * **Color key**：`Primary` |
|3 |Material |* Text color<br><br>* Background color |* Change the text.<br><br>   * **Text key**：`TextSecondary`<br><br>* Change the background color<br><br>   * **Color key**：`ConstBGContainer5` |
|4 |Template title |Text color |* Change the text.<br><br>   * **Color key**：`TextSecondary` |


<span id="baf2ad2a"></span>
# Camera roll selection screen

For more information on camera roll selection screen customization, refer to [Camera roll selection screen](https://docs.byteplus.com/docs/video-editor-sdk/150-camera-roll-selection-screen).

<span id="e953bfd0"></span>
# Edit page

You can edit different edit screens and its components within Video Editor SDK.

<span id="c7d3555f"></span>
## Edit track page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/29be4b20644749b19fea7fda3bdf70e6~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_view_back`<br><br>   * **Recommended size (pixels)** : 108 x 108 |
|2 |Export button |* Text<br><br>* Text color<br><br>* Button color |* Change the text.<br><br>   * **Text key**：`mt_magictemplates_export`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the button color.<br><br>   * **Color key**：`Primary` |
|3 |Play/ Pause button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * Play button<br><br>      * `mt_edit_start_play`<br><br>   * Pause button<br><br>      * `mt_edit_pause_play`<br><br>   * **Recommended size (pixels)** : 60 x 60 |
|4 |Progress bar |Color |* Change the color.<br><br>   * Played part<br><br>      * `Primary`<br><br>   * Unplayed part<br><br>      * `BGInput3`<br><br>   * Progress bar handle<br><br>      * `BGTertiary` |
|5 |Progress text |Text color |* Change the color.<br><br>   * Progress of played part<br><br>      * `TextTertiary \|<br><br>   * Total progress<br><br>      * `TextQuaternary` |
|6 |Prompt for selecting slots |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：mt_slot_tips<br><br>* Change the color.<br><br>   * **Color key**：TextSecondary |
|7 |Text editing icon |* Button icon<br><br>* Text<br><br>* Text color |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_text`<br><br>   * **Recommended size (pixels)** : 96 x 96<br><br>* Change the text.<br><br>   * **Text key**：`mt_edit_text`<br><br>* Change the color.<br><br>   * **Color key**：`TextSecondary` |
|8 |Selected slots |* Icon<br><br>* Text<br><br>* Text color<br><br>* Background color |* Replace the icon with another icon of the same name:<br><br>   * `mt_item_edit`<br><br>   * **Recommended size (pixels)** : 60 x 60<br><br>* Change the text.<br><br>   * **Text key**：`mt_edit`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary`<br><br>* Change the background color.<br><br>   * **Color key**：`Tertiary` |
|9 |Slot number |Text color |* Change the text color.<br><br>   * **Color key**：`TextTertiary` |
|10 |Text for slot duration |Text color |* Change the text color.<br><br>   * **Color key**：`TextPrimary` |


<span id="adfb9073"></span>
## Text editing page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3f7d5f5ccc644e281aed9e0f30e1285~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Edit text of page title |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_video_edit`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Selected text item border color |Color |* Change the color.<br><br>   * **Color key**：`Primary` |
|3 |Close editing button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_close`<br><br>   * **Recommended size (pixels)** : 96 x 96 |
|4 |Edit text panel title |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_edit_text`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|5 |Edit confirm button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * mt_edit_confirm<br><br>   * **Recommended size (pixels)** : 96 \* 96 |
|6 |Slot number |Text color |* Change the color.<br><br>   * **Color key**：TextTertiary |
|7 |Click to edit icon |* Button icon<br><br>* Text<br><br>* Text color |* Replace the icon with another icon of the same name:<br><br>   * `mt_item_edit`<br><br>   * **Recommended size (pixels)** : 60 x 60<br><br>* Change the text.<br><br>   * **Text key**：mt_edit<br><br>* Change the color.<br><br>   * **Color key**：TextPrimary |
|8 |Input box color |* Text color<br><br>* Background color |* Change the color.<br><br>   * **Color key**：TextPrimary<br><br>* Change the color.<br><br>   * **Color key**：ConstBGContainer8 |
|9 |Finish button |* Text<br><br>* Text color<br><br>* Button color |* Change the text.<br><br>   * **Text key**：mt_edit_text_finish<br><br>* Change the color.<br><br>   * **Color key**：TextPrimary1<br><br>* Change the color.<br><br>   * **Color key**：Primary |


<span id="8971560a"></span>
## Video cutting page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/70721cf7b61145239d250bfba44b832e~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Prompt text of cutting page |* Text<br><br>* Text color |* Change the text.<br><br>   * Cut video text<br><br>      * `eo_album_video_cut_select`<br><br>   * Cut image text<br><br>      * `eo_album_image_cut_select`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Color of progress box and progress bar |Color |* Change the color.<br><br>   * **Color key**：`Primary` |
|3 |Text of current slot duration |Text color |* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|4 |Close cutting button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_close`<br><br>   * **Recommended size (pixels)** : 96 x 96 |
|5 |Text of editing panel title |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_edit_cut`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|6 |Confirm cutting button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_confirm`<br><br>   * **Recommended size (pixels)** : 96 x 96 |


<span id="d8d86e66"></span>
## **Give up editing screen**

This section is shared by text editing page and video cutting page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4733754c6f984f4faba325283d3d2727~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Give up editing the text of title |* Text<br><br>* Text color |* Change the text.<br><br>   * `eo_album_give_up_edit_title`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Confirm button and text |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * `eo_album_give_up_edit_btn`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**：`Primary` |
|3 |Text of cancel |* Text<br><br>* Text color |* Change the text.<br><br>   * `eo_album_cancel_edit_btn`<br><br>* Change the color.<br><br>   * **Color key**：`TextTertiary` |
|4 |Close pop\-up button icon |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_dialog_close`<br><br>   * **Recommended size (pixels)** : 72 x 72 |


&nbsp;

<span id="f4bf42a9"></span>
## Volume control page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3625d70e16cb40db88b32fa69efca3b4~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Volume down prompt icon |Icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_voice_down`<br><br>   * **Recommended size (pixels)** : 60 x 60 |
|2 |Color of set volume section |Color |* Change the color.<br><br>   * **Color key**：`Primary` |
|3 |Current volume value title |Text color |* Change the color.<br><br>   * **Color key**：`TextTertiary` |
|4 |Current volume value text |Text color |* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|5 |Color of unset volume section |Color |* Change the color.<br><br>   * **Color key**：`ConstBGContainer_Dark` |
|6 |Volume up promp icon |Icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_voice_rise`<br><br>   * **Recommended size (pixels)** : 60 x 60 |
|7 |Adjustment confirm button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_confirm`<br><br>   * **Recommended size (pixels)** : 96 x 96 |
|8 |Volume panel title |* Text<br><br>* Text color |* Change the text.<br><br>   * **Text key**：`mt_voice`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|9 |Adjustment confirm button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_edit_confirm`<br><br>   * **Recommended size (pixels)** : 96 x 96 |


<span id="2452947f"></span>
## Exiting screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69cdbd7ee15c4fbb94f8f8db385a6e7a~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Exit edit title text |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_preview_edit_back_title`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Confirm button and text |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * `mt_preview_edit_back_sure`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**：`Primary` |
|3 |Cancel text |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_preview_edit_back_cancel`<br><br>* Change the color.<br><br>   * **Color key**：`TextTertiary` |
|4 |Close popup button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_dialog_close`<br><br>   * **Recommended size (pixels)** : 72 x 72 |


<span id="95ff9d8a"></span>
# Export page

You can customize the export page in Magic Template.

<span id="e0f70214"></span>
## During video export screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8e4952b07024021b47409a24a168fcb~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Back button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_view_back`<br><br>   * **Recommended size (pixels)** : 108 x 108 |
|2 |Exporting status title text |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_title_loading`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary` |
|3 |Exporting status prompt text |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_msg_loading`<br><br>* Change the text color.<br><br>   * **Color key**：`TextTertiary` |
|4 |Progress overlay color |Color |* Change the color.<br><br>   * **Color key**：`TextQuaternary` |
|5 |Progress bar color |Color |* Change the color.<br><br>   * **Color key**：`Primary` |
|6 |Progress value text color |Text color |* Change the color.<br><br>   * **Color key**：`TextPrimary` |


<span id="d6c3e280"></span>
## Export successful

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eb7135f3e84342fdaea8efcda5e571dd~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Finish button |* Text<br><br>* Text color<br><br>* Button color |* Change the text.<br><br>   * **Text key**：`mt_export_finish`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the button color.<br><br>   * **Color key**：`Primary` |
|2 |Title text for Export successful |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_title_success`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary` |
|3 |Prompt text for export successful status |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_msg_success`<br><br>* Change the text color.<br><br>   * **Color key**：`TextTertiary` |


<span id="9e936e7b"></span>
## Export failed

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aa0f293bf7a1411ea5d81c19564eb475~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Retry button |* Text<br><br>* Text color<br><br>* Button color |* Change the text.<br><br>   * **Text key**：`mt_export_repeat`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the button color.<br><br>   * **Color key**：`Primary` |
|2 |Title text for Export failed |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_title_fail`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary` |
|3 |Title text for Export failed status |* Text<br><br>* Text color |* Change the text.<br><br>   * `mt_export_msg_fail`<br><br>* Change the text color.<br><br>   * **Color key**：`TextTertiary` |


<span id="f5ec1abf"></span>
# Highlight clipping screen

In Magic Template, you can customize the highlight clipping screen.

<span id="436e6007"></span>
## Template matching screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0650aa981b2d4dc88e04a4e13962d2d2~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Text for no matching template found |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_no_find_template_title`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Prompt text for no matching template found |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_no_find_template_content`<br><br>* Change the color.<br><br>   * **Color key**：`TextTertiary` |
|3 |Confirm button and text |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * `hv_no_find_template_know`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**：`Primary` |
|4 |Close popup button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_dialog_close`<br><br>   * **Recommended size (pixels)** : 72 x 72 |


<span id="8c4bd90f"></span>
## Download failed screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/79213545179e4f54b9548a2c643aa824~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Title text for Download failed |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_down_template_error_title`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Prompt text for Download failed |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_down_template_error_content`<br><br>* Change the color.<br><br>   * **Color key**：`TextTertiary` |
|3 |Confirm button and text |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * `hv_down_template_error_know`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the color.<br><br>   * **Color key**：`Primary` |
|4 |Close popup button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_dialog_close`<br><br>   * **Recommended size (pixels)** : 72 x 72 |


<span id="98549b5d"></span>
## Analysis failed screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b2dd9e075cd47e9954f5814f4a3071d~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Title text for Analysis failed |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_template_analysis_faile_title`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Prompt text for Analysis failed |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_template_analysis_failed_content`<br><br>* Change the text color.<br><br>   * **Color key**：`TextTertiary` |
|3 |Confirm button and text |* Text<br><br>* Text color<br><br>* Background color |* Change the text.<br><br>   * `hv_template_analysis_failed_know`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary1`<br><br>* Change the background color.<br><br>   * **Color key**：`Primary` |
|4 |Close popup button |Button icon |* Replace the icon with another icon of the same name:<br><br>   * `mt_dialog_close`<br><br>   * **Recommended size (pixels)** : 72 x 72 |


<span id="9027b8f3"></span>
## Switch template page

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8354845555a549e1a533871211654dc0~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Template replace button |* Button icon<br><br>* Text<br><br>* Text color |* Replace the icon with another icon of the same name:<br><br>   * `hv_edit_template`<br><br>   * **Recommended size (pixels)** : 96 x 96<br><br>* Change the text.<br><br>   * `hv_edit_template`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary` |


<span id="80b9ef9d"></span>
## Recommended template screen

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/60a471f65c194632b98c144da4664ddf~tplv-goo7wpa0wc-image.image) </span>


|**No.**  |**Description** |**Changeable Item** |**Change Method** |
|---|---|---|---|
|1 |Title for Recommended Template |* Text<br><br>* Text color |* Change the text.<br><br>   * `hv_video_recommended_template`<br><br>* Change the color.<br><br>   * **Color key**：`TextPrimary` |
|2 |Selected template image and text |* Select box color<br><br>* Edit icon<br><br>* Edit Text<br><br>* Edit Text color<br><br>* Selected title text color |* Change the color.<br><br>   * **Color key**：`Primary`<br><br>* Replace the icon with another icon of the same name:<br><br>   * `mt_item_edit`<br><br>   * **Recommended size (pixels)** : 96 x 96<br><br>* Change the text.<br><br>   * `mt_edit`<br><br>* Change the text color.<br><br>   * **Color key**：`TextPrimary`<br><br>* Change the color.<br><br>   * **Color key**：`Primary` |
|3 |Text color for the unselected title |Text color |* Change the color.<br><br>   * **Color key**：`TextTertiary` |
