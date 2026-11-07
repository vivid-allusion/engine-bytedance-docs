---
title: "Beauty&Face Shaping Mapping(v4.7.1 and later)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/Beauty-and-Face-Shaping-Mapping-v471-and-later"
---

From Effects SDK v4.7.1 onwards, the path and key values of the Beauty & Face Shaping resource packages can be referred to in this document. The intensity ranges from 0 to 1. Please do not exceed this range, as it may cause unknown issues.

(1) For nodes that do not support bidirectional adjustment: 0 means no change, and it gradually increases towards 1.

(2) For modes that support bidirectional adjustment: 0.5 means no change, 0 to 0.5 is negative direction, and 0.5 to 1 is positive direction.

Note: Some creatives inherently come with default intensity during production, rather than the original effect values. Therefore, it is recommended to set the default intensity again according to the business scenario when configuring the creatives.

For example, when setting up double eyelid creatives, since the creatives themselves have an inherent intensity during production, even if the intensity is not set during use, there will still be a double eyelid effect. Therefore, when setting up the creatives, it is necessary to set the default intensity according to the business scenario.


|Category |Subitem |Path |key |Unidirectional or bidirectional regulation |Remarks |
|---|---|---|---|---|---|
|lite\-Beauty Enhancement |Skin Smoothing |beauty_IOS_lite<br><br>beauty_Android_lite |smooth |One\-way | |
||Whitening \- Natural |whiten_clear_IOS_lite<br><br>whiten_clear_Android_lite |whiten |One\-way | |
||Whitening \- Fair Skin |beauty_IOS_lengbai_lite<br><br>beauty_Android_lengbai_lite |whiten |One\-way | |
||Whitening \- Pinkish White |beauty_IOS_fenbai_lite beauty_Android_fenbai_lite |whiten |One\-way | |
||Whitening \- Rosy |beauty_IOS_rosy_lite<br><br>beauty_Android_rosy_lite |whiten |One\-way | |
||Sharpen |sharpen_IOS_lite<br><br>sharpen_Android_lite |sharp |One\-way | |
||Clear |whiten_clear_IOS_lite<br><br>whiten_clear_Android_lite |clear |One\-way | |
||Abundant |beauty_face_plump |fengying |One\-way |New in v4.7.3 |
||Neck Wrinkle Removal |beauty_neck_wrinkles |necklines |One\-way |New in v4.7.3 |
||Full body skin smoothing |beauty_smooth_body |smooth |One\-way |New in v4.7.3 |
|lite\-mini plastic surgery |Face \- Slimming \- Slimming |reshape_v8_lite |Internal_Deform_Overall |\- |v4.7.1 Offline |
||Face \- Slimming \- God of Men |reshape_v8_lite |Face_ALL_boy |One\-way |Starting from v4.7.1, shared item packs require key differentiation |
||Face \- Slimming \- Goddess |reshape_v8_lite |Face_ALL_girl |One\-way ||
||Face \- Slimming \- Natural |reshape_v8_lite |Face_ALL_nature |One\-way ||
||Face \- Small Face |reshape_v8_lite |Internal_Deform_Face |One\-way | |
||Face \- Narrow Face |reshape_v8_lite |Internal_Deform_CutFace |One\-way | |
||Face \- Microcephaly |reshape_v8_lite |BEF_BEAUTY_BODY_SHRINK_HEAD |One\-way | |
||Face \- Zygomatic Bone |reshape_v8_lite |Internal_Deform_Zoom_Cheekbone |One\-way | |
||Face \- Mandible |reshape_v8_lite |Internal_Deform_Zoom_Jawbone |One\-way | |
||Facial \- Length of Chin |reshape_v8_lite |Internal_Deform_Chin |Bidirectional | |
||Face \- Hairline/Forehead |reshape_v8_lite |Internal_Deform_Forehead |Bidirectional | |
||Facial \- Nasolabial Fold |beauty_IOS_lite<br><br>beauty_Android_lite |BEF_BEAUTY_SMILES_FOLDS |One\-way | |
||Facial \- Lifting |beauty_face_lift |tila |One\-way |New in v4.7.3 |
||Facial \- V Face |reshape_v8_lite |Internal_Deform_VFace |One\-way |New in v4.7.3 |
||Eye \- Size |reshape_v8_lite |Internal_Deform_Eye |One\-way | |
||Eye \- Position |reshape_v8_lite |Internal_Deform_Eye_Move |Before 4.7.3: One\-way; 4.7.3 and later: Two\-way | |
||Eye \- Interocular Distance |reshape_v8_lite |Internal_Eye_Spacing |Before 4.7.3: One\-way; 4.7.3 and later: Two\-way | |
||Eyes \- Outer corners lifted |reshape_v8_lite |Internal_Deform_RotateEye |Before 4.7.3: One\-way; 4.7.3 and later: Two\-way | |
||Eye \- Bright Eyes |beauty_IOS_lite<br><br>beauty_Android_lite |BEF_BEAUTY_BRIGHTEN_EYE |One\-way | |
||Eyes \- Dark Circles |beauty_IOS_lite<br><br>beauty_Android_lite |BEF_BEAUTY_REMOVE_POUCH |One\-way | |
||Eyes \- Double Eyelids |double_eye_lid/newmoon |BEF_BEAUTY_EYE_SINGLE_TO_DOUBLE |One\-way | |
||Eyes \- Round Eyes |reshape_round_eye |tila |One\-way |New in v4.7.3 |
||Eye \- Lower Eyelid Lowering |reshape_v8_lite |Internal_Lower_EyeLid |Bidirectional |New in v4.7.3 |
||Eye \- Pupil Size |reshape_v8_lite |Internal_EyePupil |One\-way |New in v4.7.3 |
||Eye \- Inner Canthus |reshape_v8_lite |Internal_EyeInnerCorner |Bidirectional |New in v4.7.3 |
||Eye \- Outer Canthus |reshape_v8_lite |Internal_EyeOuterCorner |Bidirectional |New in v4.7.3 |
||Nose \- Slim Nose |reshape_v8_lite |Internal_Deform_Nose |Bidirectional | |
||Nose \- Lift |reshape_v8_lite |Internal_Deform_MovNose |Bidirectional | |
||Nose \- Comprehensive Rhinoplasty |reshape_v8_lite |Internal_Deform_Nose_All |One\-way |New in v4.7.3 |
||Nose \- Nasal Wing |reshape_v8_lite |Internal_Deform_NoseLean |One\-way |New in v4.7.3 |
||Nose \- Bridge |reshape_v8_lite |Internal_Deform_NoseBridge |One\-way |New in v4.7.3 |
||Nose \- Tip of Nose |reshape_v8_lite |Internal_Deform_NoseTip |One\-way |New in v4.7.3 |
||Nose \- Root of the Nose |reshape_v8_lite |Internal_Deform_NoseRoot |Bidirectional |New in v4.7.3 |
||Mouth \- Size |reshape_v8_lite |Internal_Deform_ZoomMouth |Bidirectional | |
||Mouth \- Position |reshape_v8_lite |Internal_Deform_MovMouth |Bidirectional | |
||Mouth \- Smile |reshape_v8_lite |Internal_Deform_MouthCorner |One\-way | |
||Mouth \- White Teeth |whiten_teeth_IOS_lite<br><br>whiten_teeth_Android_lite |BEF_BEAUTY_WHITEN_TEETH |One\-way | |
||Lips \- Lip Augmentation |reshape_v8_lite |Internal_Deform_UpperUnderLip |Bidirectional |New in v4.7.3 |
||Eyebrow \- Position |reshape_v8_lite |Internal_BrowPosition |Bidirectional |New in v4.7.3 |
||Eyebrow \- Thickness |reshape_v8_lite |Internal_BrowSize |Bidirectional |New in v4.7.3 |
|pro\-Beauty |Skin Smoothing |beauty_IOS_standard<br><br>beauty_Android_standard |smooth |One\-way | |
||Whitening \- Natural |beauty_ziran_standard |Strength: whiten<br><br>Warmth and cold: warm |Strength: Unidirectional<br><br>Heating and Cooling: Bidirectional | |
||Whitening \- Fair Skin |beauty_lengbai_standard |Strength: whiten<br><br>Warmth and cold: warm |Strength: Unidirectional<br><br>Heating and Cooling: Bidirectional | |
||Whitening \- Pinkish White |beauty_fenbai_standard |Strength: whiten<br><br>Warmth and cold: warm |Strength: Unidirectional<br><br>Heating and Cooling: Bidirectional | |
||Whitening \- Wheat |beauty_xiaomai_standard |Strength: whiten<br><br>Warmth and cold: warm |Strength: Unidirectional<br><br>Heating and Cooling: Bidirectional | |
||Whitening \- Tanning |beauty_meihei_standard |Strength: whiten<br><br>Warmth and cold: warm |Strength: Unidirectional<br><br>Heating and Cooling: Bidirectional | |
||Sharpen |beauty_IOS_standard<br><br>beauty_Android_standard |sharp |One\-way | |
||Clear |beauty_IOS_standard<br><br>beauty_Android_standard |clear |One\-way | |
||Abundant |beauty_face_plump |fengying |One\-way |New in v4.7.3 |
||Neck Wrinkle Removal |beauty_neck_wrinkles |necklines |One\-way |New in v4.7.3 |
||Full body skin smoothing |beauty_smooth_body |smooth |One\-way |New in v4.7.3 |
|pro\-minimally invasive plastic surgery |Face \- Slimming \- Slimming |reshape_v8 |Internal_Deform_Overall |\- |v4.7.1 Offline |
||Face \- Slimming \- God of Men |reshape_v8 |Face_ALL_boy |One\-way |Starting from v4.7.1, shared item packs require key differentiation |
||Face \- Slimming \- Goddess |reshape_v8 |Face_ALL_girl |One\-way ||
||Face \- Slimming \- Natural |reshape_v8 |Face_ALL_nature |One\-way ||
||Face \- Small Face |reshape_v8 |Internal_Deform_Face |One\-way | |
||Face \- Short Face |reshape_v8 |Internal_Deform_Short_Face |One\-way | |
||Face \- Narrow Face |reshape_v8 |Internal_Deform_CutFace |Bidirectional | |
||Face \- Microcephaly |reshape_v8 |BEF_BEAUTY_BODY_SHRINK_HEAD |One\-way | |
||Face \- Zygomatic Bone |reshape_v8 |Internal_Deform_Zoom_Cheekbone |Bidirectional | |
||Face \- Mandible |reshape_v8 |Internal_Deform_Zoom_Jawbone |Bidirectional | |
||Facial \- V Face |reshape_v8 |Internal_Deform_VFace |One\-way | |
||Facial \- Length of Chin |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Deform_Chin |Bidirectional | |
||Face \- Hairline/Forehead |reshape_v8 |Internal_Deform_Forehead |Bidirectional | |
||Facial \- Nasolabial Fold |beauty_IOS_video<br><br>beauty_Android_video |BEF_BEAUTY_SMILES_FOLDS |One\-way | |
||Facial \- Lifting |beauty_face_lift |tila |One\-way |New in v4.7.3 |
||Eye \- Size |reshape_v8 |Internal_Deform_Eye |Bidirectional | |
||Eye \- Eye Height |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_EyeHeight |Bidirectional | |
||Eye \- Eye Width |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_EyeWidth |Bidirectional | |
||Eye \- Position |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Deform_Eye_Move |Bidirectional | |
||Eye \- Interocular Distance |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Eye_Spacing |Bidirectional | |
||Eye \- Lower Eyelid Lowering |reshape_v8 |Internal_LowerEyelid |Bidirectional | |
||Eye \- Pupil Size |reshape_v8 |Internal_EyePupil |Bidirectional | |
||Eye \- Inner Canthus |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_EyeInnerCorner |Bidirectional | |
||Eye \- Outer Canthus |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_EyeOuterCorner |Bidirectional | |
||Eyes \- Outer corners lifted |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Deform_RotateEye |Bidirectional | |
||Eye \- Bright Eyes |beauty_IOS_lite<br><br>beauty_Android_lite |BEF_BEAUTY_BRIGHTEN_EYE |One\-way | |
||Eyes \- Dark Circles |beauty_IOS_video<br><br>beauty_Android_video |BEF_BEAUTY_REMOVE_POUCH |One\-way | |
||Eyes \- Double Eyelids |double_eye_lid/newmoon |BEF_BEAUTY_EYE_SINGLE_TO_DOUBLE |One\-way | |
||Nose \- Size (Thin Nose) |reshape_v8 |Internal_Deform_NoseSize |Bidirectional | |
||Nose \- Nasal Wing |reshape_v8 |Internal_Deform_Nose |Bidirectional | |
||Nose \- Bridge |reshape_v8 |Internal_Deform_NoseBridge |Bidirectional | |
||Nose \- Lift |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Deform_MovNose |Bidirectional | |
||Nose \- Tip of Nose |reshape_v8 |Internal_Deform_NoseTip |Bidirectional | |
||Nose \- Root of the Nose |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_Deform_NoseRoot |Bidirectional | |
||Eyebrow \- Thickness |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_BrowSize |Bidirectional | |
||Eyebrow \- Position |Before 4.7.3: reshape_standard; 4.7.3: reshape_v8_pro; 4.8.0 and later: reshape_v8 |Internal_BrowPosition |Bidirectional | |
||Eyebrow \- Tilt |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_BrowTilt |Bidirectional | |
||Eyebrow \- Brow Peak |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_BrowRidge |Bidirectional | |
||Eyebrow \- Spacing |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_BrowDistance |Bidirectional | |
||Eyebrows \- Length |Before 4.7.3: reshape_standard; 4.7.3 and later: reshape_v8 |Internal_BrowWidth |Bidirectional | |
||Mouth \- Size |reshape_v8 |Internal_Deform_ZoomMouth |Bidirectional | |
||Mouth \- Width |reshape_v8 |Internal_MouseWidth |Bidirectional | |
||Mouth \- Position |reshape_v8 |Internal_Deform_MovMouth |Bidirectional | |
||Mouth \- Smile |reshape_v8 |Internal_Deform_MouthCorner |One\-way | |
||Mouth \- White Teeth |whiten_teeth_standard |BEF_BEAUTY_WHITEN_TEETH |One\-way | |
||Mouth \- Upper Lip Augmentation |reshape_v8 |Internal_Deform_UpperLip |Bidirectional |New in v4.7.3 |
||Mouth \- Fuller Lower Lip |reshape_v8 |Internal_Deform_UnderLip |Bidirectional |New in v4.7.3 |
