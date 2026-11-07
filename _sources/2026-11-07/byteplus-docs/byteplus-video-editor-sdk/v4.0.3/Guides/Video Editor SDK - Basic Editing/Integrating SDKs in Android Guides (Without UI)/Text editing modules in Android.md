---
title: "Text editing modules in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-text-editing-modules-in-android"
---

Text is used to add various text elements (with various styles) to videos or images to enhance visual effects and convey intent. When using the text function, you can add, delete, and modify.

<span id="8ae6fa3f"></span>
# Adding text

Describes the steps to add text content and style to your project, including adding it to tracks and committing changes.

These are the file paths for required resources:


|**Parameter** |**Action/Description** |
|---|---|
|fontPath |Set the path for the font resource. |
|bubblePath |Set the path for the bubble resource. |
|outAnimPath |Set the path for the text animation resource. |


**To add text:** 


1. Add text content to `NLESegmentTextSticker`.

2. Configure text style with `NLEStyleText`.

3. Add it to `NLESegmentTextSticker`.

4. Add `NLESegmentTextSticker` in `NLETrackSlot`.

5. Add `NLETrackSlot` to `NLETrack`.

6. Use `NLEEditor.commit` to submit changes and render the text effect.'


```Kotlin
val fontPath = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/NotoSansSC-Regular.otf"
val bubblePath = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/bubble.bundle/zhuangshibeijing50_6945244052808384525/zhuangshibeijing50_6945244052808384525"
val outAnimPath = "/sdcard/Android/data/com.volcengine.ck.sample/files/assets/resource/text_animation.bundle/zhuzixuying_7074738958005993485/zhuzixuying_7074738958005993485"

val track = NLETrack().apply {
    mainTrack = false
    layer = nleEditor.model.layerMax + 1
    extraTrackType = NLETrackType.STICKER
}

val slot = NLETrackSlot().apply {
    layer = nleEditor.model.layerMax + 1
    startTime = 0
    endTime = 3 * 1000 * 1000
    mainSegment = NLESegmentTextSticker().apply {
        content = strContent

        style = NLEStyText().apply {
            background = true         
            // Background color switch
            backgroundColor = 0XFFF5F5DC   
            // Background color, 0xFFFFFFFF -> AARRGGBB, Alpha, Red, Green, Blue
            fontSize = 14     
            // Line height, in points, conversion: px = pt / 72*300
            font = NLEResourceNode().apply {
                /**
                 * On Android, when adding text for the first time, a valid font path must be set,
                 * as higher version phones cannot access and use the system default font.
                 * */
                resourceFile = fontPath
                resourceType = NLEResType.FONT
            }

            style.shape = NLEResourceNode().apply {
                resourceFile = bubblePath
                resourceType = NLEResType.BUBBLE
            }

            textColor = 0XFF90EE90  
            // Text color, 0xFFFFFFFF -> AARRGGBB, Alpha, Red, Green, Blue

            animation = NLEStyStickerAnim().apply {
                loop = false    // Whether it is a looping animation.
                outAnim = NLEResourceNode().apply {
                    resourceFile = outAnimPath
                    resourceType = NLEResType.ANIMATION_TEXT
                }
                outDuration = 1 * 1000 * 1000  // 1 second
            }

            /**
             * For more parameter settings, please refer to the NLEStyText field description in the document.
             * Note that some settings, such as fancy text, are mutually exclusive with shadow, font color, and so on, as described in the NLEStyText section of the document.
             * */
        }

        transformX = 0f 
        // Displacement -1.0f~1.0f Coordinate origin: screen center; X-axis positive direction: user's view: screen left -> screen right;
        transformY = 0f 
        // Displacement -1.0f~1.0f Y-axis positive direction: user's view: screen bottom -> screen top;
    }
    duration = 3 * 1000 * 1000
}

track.addSlot(slot)
nleEditor.model.addTrack(track)
nleEditor.commit()
```


<span id="9ba8ed01"></span>
# Deleting text

Explains the process of removing text from your project, including how to handle tracks and slots.

**To delete the text:** 


1. Find and retrieve the specific slot you want to remove.

2. Call `track.removeSlot()` to delete the slot.

3. If track.slots are empty, call `model.removeTrack()` to delete the track.

4. Call `nle.editor.commit()` to save the changes.


```Kotlin
// Step 1: Retrieve the Slot
val slotToDelete = track.getSlotByIndex(slotIndex) // Replace slotIndex with the index of the slot you want to delete

// Step 2: Delete the Slot
if (slotToDelete != null) {
    track.removeSlot(slotToDelete)
}

// Step 3: Check for Empty Slots and Delete the Track
if (track.slots.isEmpty()) {
    model.removeTrack(track)
}

// Step 4: Save Changes
nleEditor.commit()
```


<span id="9539834f"></span>
# Changing text

Details the steps for modifying existing text, including finding the appropriate segment and committing changes.

**To change the text:** 


1. Define a function to update text within a Text Sticker in a given NLEEditor.

   ```Kotlin
   fun updateText(nleEditor: NLEEditor, strContent: String) {
   ```
   

2. Retrieve the Text Sticker Segment using a helper function.

   ```Kotlin
   val textStickerSegment = getTextStickerSegment(nleEditor)
   ```
   

3. Update the content of the Text Sticker Segment.

   ```Kotlin
   textStickerSegment?.apply {
           content = strContent
       }
   ```
   

4. Commit the changes to save them.

   ```Kotlin
     nleEditor.commit()
   }
   ```
   

5. Create a helper function to find the NLESegmentTextSticker within the NLEEditor.

   ```Kotlin
   private
    
   fun getTextStickerSegment(nleEditor: NLEEditor)
   : NLESegmentTextSticker? {
   ```
   

6. Iterate through the model's tracks to find the relevant Text Sticker.

   ```Kotlin
   nleEditor.model.tracks.filter { !it.mainTrack && it.trackType == NLETrackType.STICKER }
           .forEach { track ->
   ```
   

7. Within each track, iterate through slots to find the Text Sticker Segment.

   ```Kotlin
   track.slots.forEach { slot ->
                   
   val
    textStickerSegment = NLESegmentTextSticker.dynamicCast(slot.mainSegment)
   ```
   

8. If a Text Sticker Segment is found, return it.

   ```Kotlin
   if
    (textStickerSegment != 
   null
   ) {
                       
   return
    textStickerSegment
                   }
   ```
   

   If no Text Sticker Segment is found, return null.

   ```Kotlin
   return
    
   null
   
   }
   ```
   


**Full sample code**

```Kotlin
fun updateText(nleEditor: NLEEditor, strContent: String) {
    getTextStickerSegment(nleEditor)?.apply {
        content = strContent
    }
    nleEditor.commit()
}

private fun getTextStickerSegment(nleEditor: NLEEditor): NLESegmentTextSticker? {
    nleEditor.model.tracks.filter { !it.mainTrack
            && it.trackType == NLETrackType.STICKER }
        .forEach { track ->
            track.slots.forEach { slot ->
                val textStickerSegment = NLESegmentTextSticker.dynamicCast(slot.mainSegment)
                if (textStickerSegment != null) {
                    return textStickerSegment
                }
            }
        }
    return null
}
```


<span id="50de67ea"></span>
# **NLEStyText**

These are the `NLEStyText` functions, their parameters, and information.


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|FontSize |int32 |No |0x12 |Font size in points, converted from pixels to points (px = pt / 72\*300). |
|Background |bool |No |false |Controls the background label. When set to true, it enables background labels with a specific color. |
|BackgroundColor |int32 |No |0xF0F8FF32 |Background label color in the format 0xFFFFFFFF \-\> AARRGGBB. |
|TextColor |int32 |No |0x000000E0 |Text displays color in the format 0xFFFFFFFF \-\> AARRGGBB. |
|TypeSettingKind |int |No |1 |Controls whether text is displayed horizontally or vertically. Values: TypeSettingKind_Horizontal or TypeSettingKind_Vertical. |
|AlignType |int |No |1 |Specifies the alignment of text.<br><br>Available values:<br><br><br>* NLEStyText::AlignType_LEFT=0<br><br>* AlignType_CENTER=1<br><br>* AlignType_RIGHT=2<br><br>* AlignType_TOP=3<br><br>* AlignType_BOTTOM=4. |
|Shadow |bool |No |false |When set to true, it activates a shadow effect. This option is ineffective if fancy text is enabled. |
|ShadowColor |uint32_t |No |0 |Specifies the color of the shadow in the format 0xFFFFFFFF \-\> AARRGGBB. This option is ineffective if fancy text is enabled. |
|ShadowSmoothing |float |No |0f |Defines the blur radius of the shadow as a proportion of the text's line height. |
|ShadowOffsetX |float |No |0f |Specifies the horizontal offset of the shadow relative to the text's body. |
|ShadowOffsetY |float |No |0f |Specifies the vertical offset of the shadow relative to the text's body. |
|Bold |bool |No | |Indicates whether bold text is enabled. |
|BoldWidth |float |No |0f |Specifies the boldness of the text as a proportion of the text's line height. |
|ItalicDegree |float |No |0f |Specifies the angle of italic text. |
|Underline |bool |No | |Indicates whether underline is enabled. |
|UnderlineWidth |float |No |0f |Specifies the width of the underline as a proportion of the text's line height. |
|UnderlineOffset |float |No |0f |Specifies the distance of the underline from the baseline as a proportion of the text's line height. |
|LineGap |float |No |0f |Specifies the line spacing as a proportion of the text's line height. |
|CharSpacing |float |No |0f |Specifies the character spacing as a proportion of the text's line height. |
|InnerPadding |float |No |0f |Specifies the inner padding as a proportion of the text's line height. |
|LineMaxWidth |float |No |0f |Specifies the maximum width for automatic line breaks, as a percentage of the display window width. |
|Outline |bool |No |true |Indicates whether the outline effect is enabled. This option is ineffective if fancy text is enabled. |
|OutlineWidth |float |No |0f |Specifies the width of the outline as a proportion of the text's line height. This option is ineffective if fancy text is enabled. |
|OutlineColor |uint32_t |No |0xFFFFFFEB |Specifies the color of the outline in rgba format. This option is ineffective if fancy text is enabled. |
|Font |NLEResourceNode |No | |Specifies the font file's absolute path (supports ttf, otf, ttc). Must be filled after extracting the font resource package from Loki Backend. iOS can leave it empty to use the system default font, while on Android, a valid value must be provided for the desired effect. |
