---
title: "Text editing module in iOS"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-text-editing-module-in-ios"
---

Text is used to add various text elements (with various styles) to videos or images to enhance visual effects and convey intent. When using the text function, you can add, delete, and modify text elements.

<span id="b74c4fea"></span>
# Module description

The following table introduces classes related to the text editing module.


|**Class Name** |**Description** |
|---|---|
|NLEStyleText_OC |The text styles configuration class. |
|NLESegmentTextSticker_OC |The text segment class. `NLEStyleText_OC` and text contents are linked to this text segment object. |
|NLETrackSlot_OC |Provides information about the track slot linked to a specific segment and duration of the track slot. |
|NLETrack_OC |Provides information about the track linked to a specific slot, including the properties and level of the track. |


<span id="e021a420"></span>
# Adding text

This section introduces how to add text to your videos or images.

**To add text**:


1. Add your desired text to `NLESegmentTextSticker_OC`.

2. Add `NLEStyleText_OC`, a text styles configuration class, to `NLESegmentTextSticker_OC`.

3. Add `NLESegmentTextSticker_OC` to `NLETrackSlot_OC`.

4. Add `NLETrackSlot_OC` to `NLETrack_OC`.

5. To commit changes that you have made and render the text effect, call `NLEInterface_OC.editor.commitAndRender()`.

6. To complete the process of adding texts, call `NLEInterface_OC.editor.done()`.


**Sample code**

```Swift
let style = NLEStyleText_OC.textStyle(withJSONString: paramsStr)

let segment = NLESegmentTextSticker_OC()
// 1. add text style
segment.style = style

// 2. add content
segment.content = (params["text"] as? String) ?? ""

// 3. add segment to slot
let slot = NLETrackSlot_OC()
slot.segment = segment
slot.setStart(CMTime.zero)
slot.layer = 0
slot.setEnd(CMTime(seconds: 3, preferredTimescale: Int32(NSEC_PER_SEC)))
slot.setScale(1)
slot.setRotation(0)

let point = CGPoint(x: 0.6, y:0.33)
slot.setTransformX(Float(point.x))
slot.setTransformY(Float(point.y))

// 4. add slot to track
let track = NLETrack_OC()
track.layer = 0
track.extraTrackType = .STICKER
track.addSlot(slot)

nle.editor.model.addTrack(track)

// 5. commit change
nle.editor.commitAndRender()

// 6. add completed
nle.editor.done()
```


<span id="899af7fc"></span>
# Deleting text

For instructions on how to delete text, refer to "Common NLETrack and NLETrackSlot operations—iOS".

<span id="58099bbd"></span>
# Modifying text

This section introduces how to modify text in your text editing environment.

**To modify text**:


1. Obtain the `NLETrackSlot_OC` object that you want to modify by slotID.

2. Modify relevant parameters and follow step 5 and step 6 as described in "Adding texts" to complete text rendering and revision.


**Sample code**

```Swift

let style = NLEStyleText_OC.textStyle(withJSONString: paramsStr)

let segment = NLESegmentTextSticker_OC()
segment.style = style
segment.content = (params["text"] as? String) ?? ""

// find NLETrackSlot_OC base on slotID, and change it
let slot = CommonHelper(nle: nle).slot(with: slotId)
slot?.segment = segment

nle.editor.commitAndRender()
nle.editor.done()
```


For more information about the sample code, refer to `TextStickerController` within the demo project.

<span id="4c0456c1"></span>
# **Text style parameters and description**

The following table provides a detailed explanation about text style parameters.


|**Parameter Name** |**Data Type** |**Required** |**Default Value** |**Description** |
|---|---|---|---|---|
|fontSize |uint32_t |No |0x12 |Font size in points, converted from pixels to points (px = pt / 72\*300). |
|background |bool |No |false |Controls the background label. When set to `true`, it enables background labels with a specific color. |
|backgroundColor |uint32_t |No |0xF0F8FF32 |Background label color in the format "0xFFFFFFFF \-\> AARRGGBB". |
|textColor |uint32_t |No |0x000000E0 |Text displays color in the format "0xFFFFFFFF \-\> AARRGGBB". |
|typeSettingKind |int |No |1 |Controls whether text is displayed horizontally or vertically. Acceptable values include:<br><br><br>* 0: Indicates that texts are displayed horizontally.<br><br>* 1: Indicates that texts are displayed vertically. |
|alignType |int |No |1 |Specifies the alignment of text.<br><br>Available values:<br><br><br>* NLEStyText::AlignType_LEFT=0<br><br>* AlignType_CENTER=1<br><br>* AlignType_RIGHT=2<br><br>* AlignType_TOP=3<br><br>* AlignType_BOTTOM=4. |
|shadow |bool |No |false |When set to true, it activates a shadow effect. This option is ineffective if fancy text is enabled. |
|shadowColor |uint32_t |No |0 |Specifies the color of the shadow in the format "0xFFFFFFFF \-\> AARRGGBB". This option is ineffective if fancy text is enabled. |
|shadowSmoothing |float |No |0f |Defines the blur radius of the shadow as a proportion of the text's line height. For example, 0.1 indicates the blur radius is 0.1 times the text's line height. The bigger the value, the more ambiguous the shadow. If `shadowSmoothing` is set to 0, it indicates the shadow and its referent overlap. This option is ineffective if fancy text is enabled. |
|shadowOffsetX |float |No |0f |Specifies the horizontal offset of the shadow relative to the text's body. When the value ranged from 0.1 to \-0.1, it indicates that the shadow is turning towards the lower right corner. This option is ineffective if fancy text is enabled. |
|shadowOffsetY |float |No |0f |Specifies the vertical offset of the shadow relative to the text's body. When the value ranges from 0.1 to \-0.1, it indicates that the shadow is turning towards the lower right corner. This option is ineffective if fancy text is enabled. |
|bold |bool |No |false |Indicates whether bold text is enabled. |
|boldWidth |float |No |0f |Specifies the boldness of the text as a proportion of the text's line height. The value ranges from \-0.05 to 0.05. When set to 0, it indicates normal boldness. When the value is bigger then 0, the boldness of the text increases. When the value is lower than 0, the boldness of the text decreases. |
|italicDegree |float |No |0f |Specifies the angle of italic text. The value ranges from 0 to 45 degrees. When set to 0, it indicates normal angle. |
|underline |bool |No |false |Indicates whether underline is enabled. When set to true, it indicates that underline is enabled. |
|underlineWidth |float |No |0f |Specifies the width of the underline as a proportion of the text's line height. |
|underlineOffset |float |No |0f |Specifies the distance of the underline from the baseline as a proportion of the text's line height. |
|lineGap |float |No |0f |Specifies the line spacing as a proportion of the text's line height. When set to 0.0, it indicates texts are closely lined by their line heights. |
|charSpacing |float |No |0f |Specifies the character spacing as a proportion of the text's line height. When set to 0.0, it indicates characters are closely lined by standard character spacing rule. |
|innerPadding |float |No |0f |Specifies the inner padding as a proportion of the text's line height. |
|lineMaxWidth |float |No |0f |Specifies the maximum width for automatic line breaks, as a percentage of the display window width. |
|outline |bool |No |true |Indicates whether the outline effect is enabled. This option is ineffective if fancy text is enabled. |
|outlineWidth |float |No |0f |Specifies the width of the outline as a proportion of the text's line height. This option is ineffective if fancy text is enabled. |
|outlineColor |uint32_t |No |0xFFFFFFEB |Specifies the color of the outline in RGBA format. This option is ineffective if fancy text is enabled. |
|font |NLEResourceNode |No | |Specifies the font file's absolute path (supports ttf, otf, ttc). Must be filled after extracting the font resource package from Loki Backend. iOS can leave it empty to use the system default font, while on Android, a valid value must be provided for the desired effect. |
