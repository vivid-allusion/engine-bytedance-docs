---
title: "Sample File Structure - Android - Magic Template"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-sample-file-structure-android-magic-template"
---

<span id="Code directory structure"></span>
## **Code directory structure**

<span>![图片](https://p-vcloud.byteimg.com/tos-cn-i-em5hxbkur4/88525df29a0a434ba1f0b41289c9c88f~tplv-em5hxbkur4-noop.image) </span>

<span id="Structure details"></span>
## **Structure details**

The sample can be divided into the following three parts.

<span id="Template display: template"></span>
### **Template display: template**

Includes template list display and template preview.


|**File/Directory** |**Description** |
|---|---|
|TemplateFeedNetActivity |Template list display |
|TemplateFeedPreviewActivity |Template preview |


<span id="Asset selection: gallery"></span>
### **Asset selection: gallery**

Including asset list display and asset preview.


|**File/Directory** |**Description** |
|---|---|
|GalleryCutPickerActivity |Asset list display |
|GalleryPreviewView |Asset preview |


<span id="Playback preview: cut"></span>
### **Playback preview: cut**

Includes video playback preview, asset editing, and video export.


|**File/Directory** |**Description** |
|---|---|
|CutPreviewPlayerActivity |UI logic of video playback preview |
|CutPlayerActivity |Business logic of video playback preview |
|CutCompressActivity |Export video |
|CutClipActivity |Video asset editing |
|PlayerTextEditView |Text asset editing |
|ExportActivity |Video export |


<span id="SDK resources"></span>
### **SDK** **resources**

SDK resources are stored in the root directory **libs**.
