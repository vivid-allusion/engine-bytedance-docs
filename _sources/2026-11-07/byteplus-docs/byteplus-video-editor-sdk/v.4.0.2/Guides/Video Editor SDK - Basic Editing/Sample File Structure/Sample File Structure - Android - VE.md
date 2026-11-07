---
title: "Sample File Structure - Android - VE"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-file-structure-android-ve-v.4.0.2"
---

<span id="77e34694"></span>
# Directory structure

Open the sample project in Android Studio and you'll find the following directory structure:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/e6c9688adcb0459d8a5105d6b47a0484~tplv-em5hxbkur4-noop.image) </span>

<span id="229e7ff6"></span>
# Dependencies

Dependencies between modules in the sample project:

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/b66faf01b1d44858babcf208e34342a1~tplv-em5hxbkur4-noop.image) </span>

<span id="bdc5fdb5"></span>
# Structure details

As shown in the preceding directory structure, there are four major parts in the sample project.

<span id="76f116be"></span>
## Main entry

<span id="4c45a3d6"></span>
### Introduction

Main entry to the project. The code is in the app module.

<span id="d3e5a75a"></span>
### Code


|**File/Directory** |**Description** |
|---|---|
|AppApplication |Provides initialization\-related functions. |
|ModuleInitName |Registers components to be initialized and uses reflection to dynamically call methods for initializing the components. |
|WelcomeActivity |App home screen, which provides entries to video recording, video Duet, video editing, and the draft folder. |
|UnzipTask |Copies asset resources from the **assets** folder to the memory card of a mobile. |
|/vebase/src/main/assets |Stores asset resources. |


<span id="61ea57f9"></span>
## Video recording/Duet

<span id="1d8a8d40"></span>
### Introduction

Provides functions like video recording, video Duet, and photo taking.

<span id="06b4954c"></span>
### Code


|**File/Directory** |**Description** |
|---|---|
|PreviewActivity |Screens for photo taking, video recording, and video Duet. |
|PreviewBottomFragment |Operation panel at the bottom, which provides entries to tools, filters, and beauty effects. |
|StickerFragment |Sticker panel. |
|EffectFragment |Filter and beauty effect panel. |


<span id="a1b10882"></span>
## Video editing

<span id="32095b3e"></span>
### Introduction

Video editing screen, which consists of the video preview panel, track panel, and operation panel.

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/871350c01b49492ea1fb63c75b2458a5~tplv-em5hxbkur4-noop.image) </span>


* editor\-preview

   * Displays the video editing effect in real time.

   * Responds to users when they tap the preview panel and displays an editable notification area that can be moved, rotated, scaled, and centered by users with specific gestures.

   * Controls whether to respond to user editing on a specific type of assets such as video assets or stickers.

* editor\-trackpanel (not open source)

   * **TrackPanel** indicates a multi\-track panel consisting of a range of custom views in the SDK for editing. It displays different types of track elements used in video editing and provides an entry to operating (selecting, cropping, rotating with drag, or scaling) the track.

* editor\-btmpanel

   * Allows you to dynamically add or delete **FunctionItem**, and enable or disable it.

   * Functions as an interface for event input and output:

      * Event input indicates operations to be implemented by **BottomPanel** as instructed by users, for example, expanding sub\-nodes of **FunctionBar** or displaying **OperationPanel**.

      * Event output indicates events triggered by operations performed on **BottomPanel** to be obtained by users, for example, which **FunctionItem** was tapped.

   * Customizes the UI. You can use it to set the basic UI style for **FunctionBar** and **OperationPanel**.


<span id="3830c782"></span>
### Code


|**File/Directory** |**Description** |
|---|---|
|EditorActivity |Video editing screen. |
|DraftFragment |Draft screen. |
|PreviewPanel |Video preview panel. |
|TrackPanel |Track panel (not open source and can be used as a whole) |
|DefaultBottomPanel |Function panel at the bottom. It can implement the IBottomPanel interface. |
|NLEEditorContext |Context for editing. It can be used to obtain the editing environment, coordinate different modules for event reporting, and access the underlying NLE capabilities. |


<span id="6f871267"></span>
## SDK resources

SDK resources are stored in the root directory **libs**.


|**File/Directory** |**Description** |
|---|---|
|vesdk\-xxx.aar |VE SDK, which provides capabilities such as video and audio recording, editing, combining, and effect processing. |
|nleeditor\-xxx.aar |Video editor SDK with a set of easy\-to\-use, data\-driven interfaces for audio and video editing. It also provides capabilities like save as draft, undo, and redo, **Note that this SDK depends on the VE SDK and cannot be used alone**. |
|editor\-trackpanel\-xxx.aar |Video editor multi\-track panel consisting of a range of custom views. It displays different types of track elements used in video editing and provides an entry to operating (selecting, cropping, rotating with drag, or scaling) the track. **You can choose whether to use it as required**. |
