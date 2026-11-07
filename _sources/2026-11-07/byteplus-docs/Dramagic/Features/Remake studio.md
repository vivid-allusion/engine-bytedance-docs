---
title: "Remake studio"
product: "Dramagic"
product_code: "Dramagic"
source: "https://docs.byteplus.com/en/docs/Dramagic/Remakestudio"
---

“Dramagic” **Remake Studio** feature

The **Remake Studio** is a new feature launched by Dramagic, powered by Doubao's latest multimodal large model Doubao\-Seed\-2.1 Pro. It is designed for Short drama remakes, overseas translation and adaptation, and the reuse of popular segments. Users upload the original drama videos and select the Target language for the remake. The platform intelligently analyzes the roles and scenes in the videos, segments the original footage into short video clips suitable for AI regeneration, adapts the original dialogue and plot to the Target language, and outputs storyboard prompts. This allows users to quickly generate new role and scene images, replicate the original plot rhythm and visual composition, and produce videos, achieving a one\-stop, efficient creative process from “original footage input” to “AI remake”.

<span id="4a288318"></span>
# Main entry


* Click the sidebar on the home page, and under Creation, select [Remake Workshop] to create a remake project;

* Supports uploading multiple videos and folders. Please ensure that the drama video file names are numbered sequentially:

   * For formal production, please upload the entire series at once;

   * To test the effect, you may try uploading 3–5 episodes;

* Users can select the Target language, aspect ratio, resolution, and on\-screen text style for the remake;


Note:


1. Uploading the complete drama series is more conducive to precise processing by the Agent. Uploading too few videos (especially a single episode) may result in inaccurate role recognition and insufficient plot understanding;

2. The Agent parses dialogue more accurately for videos with subtitles;

3. Video format supports mp4/mov, each video must not exceed 500MB, duration must not exceed 3 minutes, and the video name must contain episode information;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb9cd20867a74dd781c4c8e510bf4c68~tplv-goo7wpa0wc-image.image) </span>

<span id="cd24eaaf"></span>
# Original footage – drama video upload confirmation


* After all drama videos are uploaded, click the button at the bottom. The Agent will begin analyzing the drama videos, extracting role images, scene information, and more from the original footage;

* Supports re\-uploading videos for the drama series, but does not support adding new drama videos;


Note:


1. Only after all drama videos are uploaded can you click the settings button. Re\-parsing is not supported after completion;

2. Refreshing the page during the video upload process will cause the upload to fail;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3437adab4a7547099facdc71496d5736~tplv-goo7wpa0wc-image.image) </span>

<span id="927e5ec5"></span>
# Settings \- Asset replacement relationship confirmation


* The initial state of the settings page displays all original Roles (image, name) and original scenes (name) after parsing the entire collection, as well as the newly generated Role names, new Role image Prompts, new scene names, and new scene Prompts inferred:

   * Role cards with costumes are presented in a stacked state. Click to expand, and one\-click expansion of all stacked cards is supported;

   * After expanding Role cards with costumes, they can be edited. You can continue to add costumes for the Role in any costume card. Roles without costumes can be edited directly;

   * The automatically generated new Role and new scene Prompts have incorporated an understanding of the original Roles and scenes and are adapted and designed according to the Target language. Users can manually enter a simple Description for the new Role or scene and click the [Intelligent Optimization] Button for more detailed and structured Prompt output;

   * Supports uploading images from the Role library and local files;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d1d47b3cb17422cb082d75fd452abec~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aba04ae396cb4b07ba9d29ee32557180~tplv-goo7wpa0wc-image.image) </span>


* Supports users manually calibrating assets with parsing errors or omissions

   * Click the add role/scene/prop button in the upper right corner to add missing assets;

   * In the card menu bar, after clicking [Merge Duplicate] or [Merge Costume], you can set the card as the “target image”:

      * For merging duplicates, users continue to select image cards that are duplicates of the target image. After confirming deduplication, the selected image cards are deleted, and the target image will inherit the Episode information from the deleted cards;

      * For merging costumes, users continue to select cards mistakenly identified as other images (the selected image card is actually a costume of the target image). After confirming the merge, the selected image card will become a costume of the target image;


Note:


1. When parsing duplicate image cards, prioritize [Merge Duplicate]. Direct deletion will result in inaccurate subsequent storyboard parsing

2. For scenarios where parsing is omitted or the User accidentally deletes a Role, After Create, it is Required to add the Role to the corresponding episode and @ the corresponding asset again in the Prompt edit box.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3315a5778aeb41bba231a82171f5bb3b~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f21aa030f31d4f69a945f58147081a8c~tplv-goo7wpa0wc-image.image) </span>


* Intelligent Voice: Integrates the latest Doubao Voice 1.0 model. The Agent extracts Role biographies from the original plot to Generate character voice Prompts. The User can manually Generate Audio for Specific Roles. When the audition Text is in English, it enhances the stability of Seedance's English Voice\-over output.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cab5eedb44654fd9a75fdb5a977f5cc1~tplv-goo7wpa0wc-image.image) </span>


* After you confirm the asset Replace relationship is correct, you can proceed to storyboard parsing, which Support sync parsing for up to 5 episodes.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0283b37f2ba4595b5cf7f4256d6b201~tplv-goo7wpa0wc-image.image) </span>

<span id="5640695f"></span>
# Storyboard \- Videos Remaster

Episodes


* The left panel displays the parsing Status of Every episode. Support Parse again for episodes that have been parsed or Parsing failed.


Assets


* The left panel shows the assets Attach to the current storyboard. User can click the image to View it enlarged. Clicking the asset name allows quick @ of the asset at the cursor Location in the Videos edit box.

* Click the “+” of the corresponding asset Type to add the asset from the settings to the current storyboard.


Storyboard Prompt Editor


* Click the storyboard thumbnail at the bottom to Switch storyboards.

* Click the “Upload” Button in the Videos edit box to Upload Reference materials and call the extracted key frames.

* Support batch Generate storyboard Videos (Suggestions: perform Manual calibration of Videos Prompts before execution).


Video Preview


* Click the Original video to quickly locate the time axis of the Original video according to the current storyboard for comparison viewing.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/547634ddd37a477c859d8b529b2983f9~tplv-goo7wpa0wc-image.image) </span>


* Original video frame function: Clicking opens a pop\-up window. User can Select one or more key frames intelligently extracted by the System from the Original video segment to Generate storyboard reference images, Help the User more accurately replicate character positions, composition, and camera depth of field from the Original video.

   * Sketch mode: Directly process the selected key frames from the original film into a storyboard line drawing, annotate the corresponding character names, and Generate at a relatively fast speed;

   * Rendering mode: Replace all Role scenes in the keyframes of the original film and redraw them as a storyboard image; the Generate speed is relatively slow;

   * After the User clicks [Add as Reference Frame], they can Enter in the Prompt edit box: “Reference the Role positions, On\-screen text composition, and lens depth of field in the storyboard image of @Image1” to enhance control over Videos generation;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d312a40b95847a7aaabd12eb19dd8a6~tplv-goo7wpa0wc-image.image) </span>

<span id="5a7d573a"></span>
# Videos \- Comparison Viewing


* After clicking Compare Original video, the original and remade Videos are displayed side by side for convenient comparison viewing;

* Support Sync Play of the original and new Videos;


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30c2ada4dd144455945e7f69e6ce27d5~tplv-goo7wpa0wc-image.image) </span>
