---
title: "Canvas module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-canvas-module-in-ios"
---

Canvas refers to the visual area for displaying and editing audio and video content. When using Canvas module, you can modify the background color, images, and blur radius of canvas.

<span id="6017d165"></span>
# Naming conventions

For easier reference, the following names are used to represent related objects:


|**Class Name** |**Description** |
|---|---|
|nle |Refers to an `NLEInterface_OC` object. |
|modle |Refers to an `NLEModel` object. |
|track |Refers to an `NLETrack_OC` object. |
|slot |Refers to an `NLETrackSlot_OC` object. |
|segment |Refers to an `NLESegmentVideo_OC` object. |
|resource |Refers to an `NLEResourceNode_OC` object. |
|style |Refers to an `NLEStyCanvas_OC` object. |


<span id="0b132bf5"></span>
# Module description

The following table introduces data classes related to the canvas module.


|**Module Name** |**Description** |
|---|---|
|NLEInterface_OC |The universal interface for NLE. |
|NLEModel |The core data module for NLE. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |
|NLESegmentVideo_OC |The video segment module. |
|NLEStyCanvas_OC |The canvas style module. |
|NLEResourceAV_OC |The module is used to construct resource and record resource information. |


<span id="a5cb0e03"></span>
# Primary functions

The following section provides a step\-by\-step guide on how to use the primary functions in canvas module.

<span id="5269a870"></span>
## Modifying the canvas ratio

The available value of canvas ration can be 4:3, 16:9, and more.

**To modify canvas ratio**:


1. To get your target model, use `nle.editor.getModel()`.

2. Set `model.canvasRatio`.

3. To commit changes that you have made, call `nle.editor.commit()`.


```Swift
public func change(ratio: Float) {
    let model = nle.editor.getModel()
    model.canvasRatio = ratio
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


<span id="c0afd40d"></span>
## Adding a canvas background

This section introduces how to add a canvas background. Before adding a canvas background, ensure that you have obtained your target slot. For instructions on how to obtain a slot, refer to "Common NLETrack and NLETrackSlot operations—iOS".

**To add a canvas background**:


1. To get `segment`, use the `slot` that you have obtained.

2. Configure the `sytle` object. Configuration instructions for different styles are provided in the following section.

3. Add `style` to `segment`.

4. To commit changes that you have made, call n`le.editor.commit()`.


<span id="6e670ed3"></span>
# Other functions

The following section introduces configuration instructions related to the `style` object, including the ways to set the canvas color, background, and blur radius.

<span id="adb453cf"></span>
## Setting the canvas color

This section introduces how to configure color of the `style` object.

**To configure color of the style object**:


1. Set the type of `style` to NLECanvasColor.

2. Set the color of the `style` to an ARGB value. The data type of the color is UInt32.


```Swift
public func addCanvasStyle(color: UInt32, slotID: String) {
    guard let slot = slot(with: slotID), let segment = slot.segment as? NLESegmentVideo_OC else {
        return
    }
    let style = segment.canvasStyle ?? NLEStyCanvas_OC()
    style.canvasType = .color
    style.color = UInt32(color)
    
    segment.canvasStyle = style
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


**Display effect**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e2d9d4c0d0c4438cb422e8ab6881cf64~tplv-goo7wpa0wc-image.image" width="312px" /></div>


<span id="364b6fc7"></span>
## Setting the canvas background

This section introduces how to configure an image of the `style` object. Before setting the images, ensure that you have had the address of your target image.

**To configure an image of the style object**:


1. Construct `resource` with the image address that you have obtained.

2. Set the type of `style` to `NLECanvasImage`.

3. Set `imageSource` of `style` to `resource`.


```Swift
public func addCanvasStyle(imagePath: String, slotID: String) {
    guard let slot = slot(with: slotID), let segment = slot.segment as? NLESegmentVideo_OC else {
        return
    }
    
    let url = URL(fileURLWithPath: imagePath)
    let name = url.deletingPathExtension().lastPathComponent
    let resource = NLEResourceNode_OC()
    resource.resourceId = UUID().uuidString
    resource.resourceFile = url.absoluteString
    resource.resourceName = name
    
    let style = segment.canvasStyle ?? NLEStyCanvas_OC()
    style.canvasType = .image
    style.imageSource = resource
    
    segment.canvasStyle = style
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


**Display effect**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8f23a350428e49e78e50ad5e2eb2c829~tplv-goo7wpa0wc-image.image" width="299px" /></div>


<span id="81e5019d"></span>
## Blurring the canvas

When the video is playing, blur radius can be used to add bluring effect to video and serve as a background.

**To set blur radius**:


1. Set the type of `style` to `NLECanvasVideoFrame`.

2. Set `blurRadius` of `style` to your desired value.


```Swift
public func addCanvasStyle(blurRadius: Float, slotID: String) {
    guard let slot = slot(with: slotID), let segment = slot.segment as? NLESegmentVideo_OC else {
        return
    }
    let style = segment.canvasStyle ?? NLEStyCanvas_OC()
    style.canvasType = .videoFrame
    style.blurRadius = blurRadius
    
    segment.canvasStyle = style
    nle.editor.commitAndRender()
    nle.editor.done()
}
```


**Display effect**

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8c5b325168b142de972b1120033e8387~tplv-goo7wpa0wc-image.image" width="325px" /></div>
