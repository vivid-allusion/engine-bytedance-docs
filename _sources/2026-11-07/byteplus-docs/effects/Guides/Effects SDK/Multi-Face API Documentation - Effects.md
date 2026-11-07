---
title: "Multi-Face API Documentation - Effects"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-ar"
---

Functional Description

Scope: This document only describes two multi\-face effect APIs newly added in SDK 4.9.0: setting multi\-face effect intensity by FREID and obtaining multi\-face FREID detection results.

<span id="cfb5c9fd"></span>
## Prerequisites for Integration

SDK initialization, authentication, effect handle creation, resource loading, image processing and resource reuse follow the standard effect workflow and will not be repeated here.


* Common workflow for C API: [Common Effect C APIs](https://docs.byteplus.com/en/docs/effects/docs-c-api)

* Common workflow for Android Java API: [Common Effect Java APIs](https://docs.byteplus.com/en/docs/effects/docs-java-api)


Before using the following APIs, ensure your SDK version is no lower than 4.9.0 and initialization has been completed following the standard effect workflow.

<span id="0dd81567"></span>
## C APIs

Header file: `bef_effect_ai_api.h`. Initialization, resource loading, image processing and resource release reuse the workflow at [Common Effect C APIs](https://docs.volcengine.com/docs/6705/102013?lang=zh#c%E6%8E%A5%E5%8F%A3.)

<span id="bbcc9dc5"></span>
### 1. Set multi\-face effect intensity

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_composer_update_string_node(bef_effect_handle_t handle, const char *nodePath, const char *nodeTag, const char *strVal);
```



|Parameter |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|nodePath |const char \* |Path of the effect resource |
|nodeTag |const char \* |Tag of the effect parameter |
|strVal |const char \* |Intensity value in string format |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="72450c78"></span>
### 2. Obtain multi\-face detection result

```Plain
BEF_SDK_API bef_effect_result_t bef_effect_ai_get_freid_detect_result(bef_effect_handle_t handle, bef_ai_freid_detect_result* result);
```



|Parameter |Type |Description |
|---|---|---|
|handle |bef_effect_handle_t |Created effect handle |
|result |bef_ai_freid_detect_result\* |FREID detection result |


**Return Value** Returns `BEF_RESULT_SUC` on success; returns corresponding error code on failure. See `bef_effect_ai_public_define.h` for details.

<span id="907b0f9d"></span>
## Java APIs

Class: `RenderManager.java`. Initialization, resource loading, image processing and resource release reuse the workflow at [Common Effect Java APIs](https://docs.volcengine.com/docs/6705/102013?lang=zh#java%E6%8E%A5%E5%8F%A3.)

<span id="1fa771ff"></span>
### 1. Set multi\-face effect intensity

```Plain
public int updateComposerStringNode(String path, String key, String value)
```



|Parameter |Type |Description |
|---|---|---|
|path |String |Path of the effect resource |
|key |String |Effect parameter key |
|value |String |Multi\-face intensity JSON string, format: `{"values":[{"freid":"unique face ID","value":intensity 0~1}]}` |


**Return Value** Returns `BEF_RESULT_SUC` on success. Refer to {@link BytedEffectConstants} for other return codes.

<span id="739b1a84"></span>
### 2. Obtain multi\-face FREID detection result

```Plain
/**
 * @return Current multi-face FREID detection result
 * @brief Get FREID detection result output by current RenderManager
 */
public BefFreidInfo getFreidDetectResult()
```


**Return Value** Returns `BefFreidInfo` object on success; returns `null` on failure.
