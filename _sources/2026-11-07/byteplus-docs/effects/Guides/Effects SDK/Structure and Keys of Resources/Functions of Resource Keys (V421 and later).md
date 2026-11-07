---
title: "Functions of Resource Keys (V421 and later)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-functions-of-resource-keys-v421-and-later"
---

Items' intensity range is 0\-1, please do not exceed this range, may bring unknown problems.

(1) Items that do not support bi\-direction adjustment: 0 is unchanged and gradually enhanced toward 1.

(2) Items that support bi\-direction adjustment: 0.5 is unchanged, 0\-0.5 is negative, 0.5\-1 is positive.

(3) Support bi\-direction adjustment are noted, no note item is not to support bi\-direction adjustment.

```C
// beauty effects，resources are: beauty_Android_lite, beauty_Android_standard, beauty_IOS_lite, beauty_IOS_standard
[
    "whiten",                                     // toning
    "sharp",                                      // sharpening
    "smooth"                                      // buffing
    "clear"                                      // clarity, V4.4.2 and later version added
]
// face shaping effects lite，resources are: reshape_lite
[
  // face
    "Internal_Deform_Overall",                    // lower face width (all lower face items use this key including natural/beauty/handsome)
    "Internal_Deform_Face",                       // face size
    "Internal_Deform_CutFace",                    // upper face width
    "Internal_Deform_Zoom_Cheekbone",             // cheek
    "Internal_Deform_Zoom_Jawbone",               // jaw
    "Internal_Deform_Chin",                       // chin (support bi-direction adjustment after V4.3.1)
    "Internal_Deform_Forehead",                   // hairline (support bi-direction adjustment after V4.3.1)
  
  // eye
          "Internal_Deform_Eye",                        // size 
          "Internal_Deform_Eye_Move",                   // position
          "Internal_Eye_Spacing",                       // eye space
          "Internal_Deform_RotateEye",                  // upturned eyes
  
  // nose
          "Internal_Deform_Nose",                        // nose width (support bi-direction adjustment after V4.3.1)
          "Internal_Deform_MovNose",                // nose length (support bi-direction adjustment after V4.3.1)
 
  // mouth
          "Internal_Deform_ZoomMouth",                                // size (support bi-direction adjustment after V4.3.1)
          "Internal_Deform_MovMouth",                                        // position
          "Internal_Deform_MouthCorner",                                       // smile
]
// face shaping standard（421 new），resources are: reshape_standard
[
  // face
    "Internal_Deform_Overall",                    // lower face width (support bi-direction adjustment)
    "Internal_Deform_Face",                       // face size 
    "Internal_Deform_CutFace",                    // upper face width (support bi-direction adjustment)
    "Internal_Deform_Zoom_Cheekbone",             // cheek (support bi-direction adjustment)
    "Internal_Deform_Zoom_Jawbone",               // jaw (support bi-direction adjustment)
    "Internal_Deform_Chin",                       // chin (support bi-direction adjustment)
    "Internal_Deform_Forehead",                   // hair line (support bi-direction adjustment)
          "Internal_Deform_VFace",                  // V-shaped face
  
  // eye
          "Internal_Deform_Eye",                                                        // size (support bi-direction adjustment)
          "Internal_EyeHeight",                                                        // height (support bi-direction adjustment)
          "Internal_EyeWidth",                                                        // width (support bi-direction adjustment)
          "Internal_Deform_Eye_Move",                                        // position (support bi-direction adjustment)
          "Internal_Eye_Spacing",                                                        // distance (support bi-direction adjustment)
          "Internal_LowerEyelid",                                                        // downturned eye (support bi-direction adjustment)
          "Internal_EyePupil",                                                // pupil size (support bi-direction adjustment)
          "Internal_EyeInnerCorner",                                        // inner eye corner (support bi-direction adjustment)
          "Internal_EyeOuterCorner",                                        // outter eye corner (support bi-direction adjustment)
          "Internal_Deform_RotateEye",                                // upturned eye (support bi-direction adjustment)
  
  // nose
          "Internal_Deform_NoseSize",                                                // size (support bi-direction adjustment)
          "Internal_Deform_Nose",                                                        // nose wing (support bi-direction adjustment)
          "Internal_Deform_NoseBridge",                                                // nose bridge (support bi-direction adjustment)
          "Internal_Deform_MovNose",                                                // lift (support bi-direction adjustment)
          "Internal_Deform_NoseTip",                                                        // tip (support bi-direction adjustment)
          "Internal_Deform_NoseRoot",                                                // root (support bi-direction adjustment)
          
  // eyebrow
          "Internal_BrowSize",                                                        // thickness (support bi-direction adjustment)
          "Internal_BrowPosition",                                                // position (support bi-direction adjustment)
          "Internal_BrowTilt",                                                        // tilt (support bi-direction adjustment)
          "Internal_BrowRidge",                                                        // ridge (support bi-direction adjustment)
          "Internal_BrowDistance",                                                // distance (support bi-direction adjustment)
          "Internal_BrowWidth",                                                        // width (support bi-direction adjustment)
  
  // mouth
          "Internal_Deform_ZoomMouth",                                                // size (support bi-direction adjustment)
          "Internal_MouseWidth",                                                                // width (support bi-direction adjustment)
          "Internal_Deform_MovMouth",                                                // position (support bi-direction adjustment)
          "Internal_Deform_MouthCorner",                                                // smile
]
// addtional 4 features for face shaping，resources are: beauty_4Items
[
    "BEF_BEAUTY_BRIGHTEN_EYE",                    // eye brightening
    "BEF_BEAUTY_SMILES_FOLDS",                    // laugh line
  \
    "BEF_BEAUTY_WHITEN_TEETH",                    // teeth whitening
    "BEF_BEAUTY_REMOVE_POUCH"                     // dark circle
]
// double eyelid（421 new），resources are: double_eye_lid/newmoon
[
    "BEF_BEAUTY_EYE_SINGLE_TO_DOUBLE",             // double eyelid
]
// body shaping，resources are: body/allslimqy
[
    "BEF_BEAUTY_BODY_THIN",                       // body width
    "BEF_BEAUTY_BODY_LONG_LEG"                    // leg length
]
// body shaping（new features for 3931 after: head size、leg width、waist、breast、hip、neck、arm），resources are: body/allslim
[
    "BEF_BEAUTY_BODY_SHRINK_HEAD",                 // head size
    "BEF_BEAUTY_BODY_SLIM_LEG"                     // leg width
    "BEF_BEAUTY_BODY_SLIM_WAIST",                  // waist (V4.5.2 added new waist also uses this key, tt_skeletonsquat model is required)
    "BEF_BEAUTY_BODY_ENLARGR_BREAST"               // breast (V4.5.2 added new breast also uses this key, tt_skeletonsquat model is required)
    "BEF_BEAUTY_BODY_ENHANCE_HIP",                 // hip
    "BEF_BEAUTY_BODY_ENHANCE_NECK"                 // neck
    "BEF_BEAUTY_BODY_SLIM_ARM"                     // arm
]
// makeup effects，resources are: lip blush pupil eyeshadow eyebrow facial eyelashes eyelight wocan
[
    "Internal_Makeup_Lips",                       // lite lipstick, resource: lip/lite
    "Internal_Makeup_Lips","R","G","B"            // standard lipstick, resource: lip/standard
    "Internal_Makeup_Blusher",                    // lite blusher,resource: blush/standard
    "Internal_Makeup_Blusher","R","G","B"         // standard blusher, resource: blush/standard
    "Internal_Makeup_Pupil",                      // pupil
    "Internal_Makeup_Eye",                        // eyeshadow
    "Internal_Makeup_Brow",                       // lite eyebrow, eyebrow/lite
    "Internal_Makeup_Brow","R","G","B"            // standard eyebrow,eyebrow/lite
    "Internal_Makeup_Facial",                     // contour
    "Internal_Makeup_Eyelash", "R","G","B"        // eyelash（V4.2.1 new）
    "Internal_Makeup_EyeLight",                   // eyesight（V4.2.1 new）
    "Internal_Makeup_WoCan",                             // aegyo sal（V4.2.1 new）
]
// advanced makeup sticker，resources are all belong to: style_makeup，e.g. qise, etc.
[
          "Filter_ALL",                                                                                                               // filter intensity
          "Makeup_ALL",                                                                                                        // makeup intensity
]
//Quality Before version 4.4.0, the folder is called "palette" in ComposerMakeup.bundle. All the items are using same key.
[
          "Filter_intensity",                                                                                                        // intensity
]
//Quality of version 4.4.0 and later, the folder is called "palette" in ComposerMakeup.bundle.
[
    "Intensity_Temperature",                                // Temperature，palette/color (support bi-direction adjustment)
    "Intensity_Hue",                                                // Tone，palette/light (support bi-direction adjustment)
    "Intensity_Saturation",                                // Saturation，palette/color (support bi-direction adjustment)
    "Intensity_Light",                                        // Brightness，palette/light (support bi-direction adjustment)
    "Intensity_Contrast",                                          // Contrast，palette/contrast (support bi-direction adjustment)
    "Intensity_Highlight",                                        // Highlight，palette/light (support bi-direction adjustment)
    "Intensity_Shadow",                                          // Shadow，palette/color
    "Intensity_Light_Sensation",                           // Light perception，palette/light (support bi-direction adjustment)
    "Intensity_Particle",                                                // Particles，palette/particle
    "Intensity_Fade",                                                // Fading，palette/color
    "Intensity_Vignette",                                              // Vignette，palette/vignette

 // Note: V442 version of the sample to fix the problem of superimposed effects of small items of quality, you need to pay attention to the rendering order of the small items of quality access, you can check the details in the sample or ask technical support.
]
// Hack, added after V4.4.0
[
          "clean",                                                // Acne Removal
]
// 4.4.3 Version adds new adjustable background blur
[
          "Blur_intensity",                                                                                                                // background blur intensity key，stickers/background_blur_in
]
```
