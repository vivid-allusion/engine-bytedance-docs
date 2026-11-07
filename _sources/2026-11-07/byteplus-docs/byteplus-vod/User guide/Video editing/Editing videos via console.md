---
title: "Editing videos via console"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/editing_videos_via_console"
---

To edit videos directly within the VOD console, you can use the built\-in video editor. This guide demonstrates the complete workflow, covering how to create a project, import assets, perform edits like splitting clips and applying effects, and export the final video to your VOD space.

<span id="88a34c59"></span>
## Prerequisites

Ensure you have a domain name and a certificate. For details, see [Adding domain name](https://docs.byteplus.com/docs/byteplus-vod/docs-domain-name-management).

<span id="91885758"></span>
## Interface overview

The following image shows the video editing project interface.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c884b2bd320846cc86324785f7f307da~tplv-goo7wpa0wc-image.image) </span>

The interface is divided into the following functional areas:


|Area |Function |Operation |
|---|---|---|
|Navigation bar |Return to the previous page, edit project names, and export video files. |* Click **Back** to return to the **Project** page.<br><br>* Click the text box to rename your project.<br><br>* Click **Export video** to proceed to the **Tasks** page. |
|Asset library |Local upload, system import and drag\-and\-drop. |* **Upload from local**: Click to select local video, audio, or image files. Select storage space if prompted and click **Confirm**.<br><br>* **Import from system**: Click to select from the **Video library** (search by Vid/Name) or **Material library** (filter by type or search by Mid/Name).<br><br>* **Direct upload**: Click the upload area or drag and drop files directly. |
|Function area |Materials, transitions, effects and filters. |Select a category and drag the desired element onto the timeline to start editing. |
|Preview window |Playback, fullscreen, and aspect ratio switch. |* Check the real\-time preview of the timeline. This defaults to displaying the frame at the current playhead position.<br><br>* Switch the aspect ratio between 16:9 and 9:16. |
|Timeline |Undo/redo, split, copy and delete. |Select a clip on the track and click the toolbar buttons to perform basic editing operations. |


<span id="91e125da"></span>
## Timeline logic

The timeline requires at least one element on the main track (video track). Tracks follow a top\-down layering logic:


* **Above main track:**  Overlaid video tracks, audio tracks, and effects/filters.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The visual layering in the preview window depends on the track order (top tracks appear in front of bottom tracks).   </div>
   

* **Main track:**  Primary video track.

* **Below main track:**  Background audio tracks.


The following operations are available on the timeline:


|Operation |Description |
|---|---|
|Add |New assets are added to the corresponding track at the current playhead position. |
|Edit |Click any asset on the track to open its specific settings. For details about these settings, see [Track settings](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_console#30d61e34). |
|Split |Splits the currently selected clip on a track. |
|Overwrite |If you drag asset A over asset B on the same track, the overlapping portion of asset B will be replaced by asset A. |


<span id="30d61e34"></span>
## Track settings

The editor supports three track types, each with specific configuration options:


|Type |Category |Description |
|---|---|---|
|Audio |Audio |Volume, playback speed, fade\-in, fade\-out. |
|Video/Image |Basic |Position, size, rotation, display settings, volume, speed. |
||Color |Brightness, saturation, hue. |


<span id="9aa61b26"></span>
## Procedures

<span id="b592d4a6"></span>
### Step 1: Creating a new project


1. Log in to [the BytePlus VOD console](https://console.byteplus.com/vodpaas) and enter the specific space.

2. Select **Video editing \> Projects** in the left navigation bar.

3. Click the **Create project** button and rename the project on the top navigation bar.


<span id="74a44f23"></span>
### Step 2: Editing the video


1. Click to upload local files or import existing assets from the VOD system. You can also drag files onto the **Asset library** area.

2. Drag materials from the **Asset library** to the **Timeline**.

3. Adjust clip duration, add transitions, or apply effects/filters as needed.


<span id="8922f49e"></span>
### Step 3: Previewing the result


1. Click the playback button in the preview window to check your edits.

2. Click the fullscreen toggle to check the visual effects in detail.

3. Click the aspect ratio toggle to switch the video's aspect ratio.


<span id="f01e3b55"></span>
### Step 4: Exporting the video


1. Click **Export Video**.

2. In the export dialog, set the video name and frame rate.

   
   |Parameter |Description |
   |---|---|
   |Video name |You can enter no more than 32 characters.<br><br>Supports Chinese characters, English letters, numbers, colons (:), periods (.), underscores (_), and hyphens (\-). |
   |Resolution |Defaults to 1080P. |
   |Codec |* H.264<br><br>* H.265 |
   |Format |* MP4<br><br>* HLS |
   |Frame rate |You can set it in the range of 15 to 60 FPS. |
   

3. Click **Confirm**. The system will redirect you to the **Tasks**.


<span id="9afb4175"></span>
### Step 5: Checking task progress


1. Navigate to **Video editing** \> **Tasks** in the left navigation bar.

2. Track the processing status of your exported videos here.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69628633e12d491da9e424fcf05eda74~tplv-goo7wpa0wc-image.image) </span>
