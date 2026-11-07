---
title: "Beauty & Reshape Multi-Material Details (v4.9.0 and above)"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-windows-access-guide-v430-and-later"
---

<span id="Development Environment"></span>
# Starting from SDK 4.9.0, refer to this document for the asset package paths and keys of Reshape & Makeup Multi.

Asset intensity ranges from 0 to 1. Do not exceed this range, as it may cause unknown issues. (1) Features that do **not** support bidirectional adjustment: 0 means no change; effect gradually increases towards 1. (2) Features that support bidirectional adjustment: 0.5 means no change; 0–0.5 for negative adjustment, 0.5–1 for positive adjustment.

Note: Some assets come with a built\-in default intensity during production, which is not the raw effect value. Therefore, it is recommended to set the default intensity according to your business scenario when configuring assets.

Example: When applying the double eyelid asset, the asset already has an embedded intensity. The double eyelid effect will appear even if you do not manually set the intensity. Hence, you need to configure the default intensity for this asset based on your business requirements.


|Category |Asset Package |Key |Description |New/Modified |Uni/Bi\-directional |
|---|---|---|---|---|---|
|Makeup Multi |makeup_multi/makeup01 |Internal_Makeup_Lips |Coral Lipstick |New |Unidirectional |
|Makeup Multi |makeup_multi/makeup01 |Internal_Makeup_Lips_ds |Bean Paste Pink Lipstick |New |Unidirectional |
|Makeup Multi |makeup_multi/makeup01 |Internal_Makeup_Lips_fg |Retro Red Lipstick |New |Unidirectional |
|Makeup Multi |makeup_multi/makeup01 |Internal_Makeup_Lips_xy |Grapefruit Lipstick |New |Unidirectional |
|Makeup Multi |makeup_multi/makeup01 |Internal_Makeup_Lips_yq |Vital Orange Lipstick |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Face_ALL_nature |Natural Face |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Face_ALL_girl |Goddess Face |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Face_ALL_boy |Male God Face |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_Face |Slim Face |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_Eye |Big Eyes |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Internal_EyePupil |Pupil |New |Unidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_NoseSize |Nose Slimming |New |Bidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_Nose |Nostril Width |New |Bidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_NoseBridge |Nasal Bridge |New |Bidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_MovMouth |Mouth Position |New |Bidirectional |
|Reshape Multi |reshape_v8_multi |Internal_MouseWidth |Mouth Width |New |Bidirectional |
|Reshape Multi |reshape_v8_multi |Internal_Deform_MouthCorner |Smiling Mouth Corner |New |Unidirectional |
