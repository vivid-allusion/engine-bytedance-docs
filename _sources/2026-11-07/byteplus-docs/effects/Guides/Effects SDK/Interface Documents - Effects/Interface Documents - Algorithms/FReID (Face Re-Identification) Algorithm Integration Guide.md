---
title: "FReID (Face Re-Identification) Algorithm Integration Guide"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-faq-3d-models"
---

<span id="0521dafe"></span>
## Capability Overview

FReID receives the same frame image along with the face 106\-point detection results, and outputs the mapping from `face_id` to a stable `track_id`. It is used to maintain identity when a person leaves the frame and later reappears. FReID depends on face detection; it is **not** an independent full\-body pedestrian ReID interface.

<span id="cd629abf"></span>
## General Notes

<span id="6aa3e944"></span>
### Integration Flow


1. Initialize face detection. The init config must include the required model, detection mode, and face capabilities. The Java side must then call `FaceDetect.setFaceDetectConfig()` to set the runtime detection config, which must be a subset of the init config.

2. Create the FReID handle and complete license verification.

3. If cross\-process memory retention is needed, configure the offline TrackID cache file, then load the FReID model.

4. Run face detection frame by frame, passing the same frame image and its face results to FReID.

5. Use the returned `track_id` to maintain business identity.

6. When processing stops, persist to disk according to the save strategy and release the handle.


<span id="a41b960a"></span>
### Input and Output


|Item |Description |
|---|---|
|Prerequisite algorithm |Face 106\-point detection. C side passes `bef_ai_face_106`; Java side passes `BefFreidFaceInfo` returned by `detectFaceForFreid()` |
|Supported formats |RGBA8888, BGRA8888, BGR888, RGB888 |
|Image orientation |Clockwise 0°, 90°, 180°, 270°; corresponding enum values 0/1/2/3. **Must use enum constants, not raw degree values** |
|Output |Up to 10 `face_id → track_id` mappings; only use results in the `[0, count)` range |
|Same\-frame constraint |Face detection and FReID must use the same frame image with identical width, height, stride, pixel format, and orientation. The Java side **must** use `detectFaceForFreid()`; results from the ordinary `detectFace()` cannot be used as a substitute. |


<span id="97bf76e2"></span>
### Runtime Parameters

Runtime parameters have the same meaning on C and Java. When the business has no explicit tuning requirement, use the default values; no manual configuration is needed.


|Parameter |Value |Type |Function |Default |Required? |
|---|---|---|---|---|---|
|BEF_AI_FREID_THRESHOLD |0 |float |Sets the face re\-identification matching threshold; higher threshold = stricter matching |Determined by the model; after init, query via `getModelParam()` → `model_thresh` |Not required; set only when tuning for false matches or missed matches |
|BEF_AI_FREID_FORCE_DETECT |1 |int |Controls whether force detect is enabled: 0 = off, 1 = on |0 |Not required; keep the default for normal integration; set only under technical support guidance. |


C uses `bef_effect_ai_freid_set_param_f()` or `bef_effect_ai_freid_set_param_i()`; Java uses the float or int overload of `FreidDetect.setParam(...)`. The internal Demo does not actively set runtime parameters. For normal integration, it is recommended to use the model's default config; advanced parameters such as `USE_BUFFER`, `BUFFER_IMMEDIATE_MODE`, and `MODEL_TYPE` should only be set under technical support guidance.

<span id="c8bdd115"></span>
## C Integration

<span id="42def2b3"></span>
### Interface Overview

Public interfaces are defined in `bef_effect_ai_freid.h`; common types and error codes are defined in `bef_effect_ai_public_define.h`; the face input structure is defined in `bef_effect_ai_face_detect.h`.

<span id="29a83537"></span>
#### 1. Create the FReID Handle

```Plain
bef_effect_result_t bef_effect_ai_freid_create(
    bef_effect_handle_t *handle);
```


表格


|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t *` |Output parameter; receives the newly created FReID handle. Call `bef_effect_ai_freid_release()` to release when done. |


**Return value:**  `BEF_RESULT_SUC` on success; other return values per `bef_effect_ai_public_define.h`.

<span id="c141da3b"></span>
#### 2. Verify Offline License

```Plain
bef_effect_result_t bef_effect_ai_freid_check_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle created by `bef_effect_ai_freid_create()` |
|licensePath |`const char *` |Path to the offline license file; must not be an empty string |


**Return value:**  `BEF_RESULT_SUC` on success; the corresponding error code if the license is invalid or the license file does not include the FReID (face re\-identification) capability.

<span id="43fb9172"></span>
#### 3. Verify Online License

```Plain
bef_effect_result_t bef_effect_ai_freid_check_online_license(
    bef_effect_handle_t handle,
    const char *licensePath);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle created by `bef_effect_ai_freid_create()` |
|licensePath |`const char *` |Path to the online license file; must not be an empty string |


**Return value:**  `BEF_RESULT_SUC` on success; the corresponding error code if the license is invalid or the license file does not include the FReID capability.

<span id="f5ff705c"></span>
#### 4. Load the FReID Model

```Plain
bef_effect_result_t bef_effect_ai_freid_init(
    bef_effect_handle_t handle,
    const char *freidModelPath);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle that has completed license verification |
|freidModelPath |`const char *` |Path to the FReID model file; must not be empty and the file must be readable. If an offline TrackID config is set, automatic recovery is attempted during init. |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` for an empty path; model\-related error codes if the model is unreadable or invalid.

<span id="435ee4cb"></span>
#### 5. Set Floating\-Point Runtime Parameter

```Plain
bef_effect_result_t bef_effect_ai_freid_set_param_f(
    bef_effect_handle_t handle,
    bef_ai_freid_param_type type,
    float value);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle |
|type |`bef_ai_freid_param_type` |Parameter type. The current implementation accepts `BEF_AI_FREID_THRESHOLD` and `BEF_AI_FREID_MODEL_TYPE`. |
|value |`float` |Parameter value. Normal integration only sets the matching threshold when tuning is needed. |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` for an unsupported parameter type.

<span id="0552d6bd"></span>
#### 6. Set Integer Runtime Parameter

```Plain
bef_effect_result_t bef_effect_ai_freid_set_param_i(
    bef_effect_handle_t handle,
    bef_ai_freid_param_type type,
    int value);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle |
|type |`bef_ai_freid_param_type` |Parameter type. The current implementation accepts `BEF_AI_FREID_FORCE_DETECT`, `BEF_AI_FREID_USE_BUFFER`, `BEF_AI_FREID_BUFFER_IMMEDIATE_MODE`, and `BEF_AI_FREID_MODEL_TYPE`. |
|value |`int` |Parameter value. Normal integration sets `BEF_AI_FREID_FORCE_DETECT` only when explicitly needed. |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` for an unsupported parameter type.

<span id="06920a2a"></span>
#### 7. Configure Offline TrackID

```Plain
bef_effect_result_t bef_effect_ai_freid_set_offline_track_id_config(
    bef_effect_handle_t handle,
    int enable_offline_track_id,
    const char *offline_track_id_path,
    bef_ai_freid_offline_save_mode save_mode);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle |
|enable_offline_track_id |`int` |Whether to enable offline TrackID: 0 = off, non\-zero = on |
|offline_track_id_path |`const char *` |Cache file path; must not be empty when offline TrackID is enabled |
|save_mode |`bef_ai_freid_offline_save_mode` |`BEF_AI_FREID_MANUAL_FLUSH_ONLY` = manual save only; `BEF_AI_FREID_AUTO_SAVE_ON_NEW_TRACK_ID` = auto\-save when a new TrackID is added |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` if the path or save mode is invalid. If the handle is already initialized, recovery of existing cache is attempted immediately after a successful config.

<span id="d419b4c9"></span>
#### 8. Restore Offline TrackID

```Plain
bef_effect_result_t bef_effect_ai_freid_restore_offline_track_id(
    bef_effect_handle_t handle);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle that is initialized and has an offline TrackID path configured |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_FILE_NOT_FIND` if the cache file does not exist; `BEF_RESULT_INVALID_PARAM_VALUE` if the config is invalid.

<span id="20a54f5d"></span>
#### 9. Write Offline TrackID

```Plain
bef_effect_result_t bef_effect_ai_freid_flush_offline_track_id(
    bef_effect_handle_t handle);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |FReID handle that is initialized and has an offline TrackID path configured |


**Return value:**  `BEF_RESULT_SUC` on success; the corresponding error code if the config is invalid, serialization fails, or the file write fails.

<span id="7d29f1d0"></span>
#### 10. Query Model Parameters

```Plain
bef_effect_result_t bef_effect_ai_freid_get_model_param(
    bef_effect_handle_t handle,
    bef_ai_freid_model_param *model_param);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |Initialized FReID handle |
|model_param |`bef_ai_freid_model_param *` |Output parameter; returns `model_version`, `model_thresh`, and `trackid_num` |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` if `model_param` is null.

<span id="50de8680"></span>
#### 11. Release the FReID Handle

```Plain
bef_effect_result_t bef_effect_ai_freid_release(
    bef_effect_handle_t handle);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |The FReID handle to release. An attempt is made to write the configured offline TrackID before release. |


**Return value:**  The current implementation returns `BEF_RESULT_SUC` after resource cleanup.

<span id="1949c817"></span>
#### 12. Run FReID Detection

```Plain
bef_effect_result_t bef_effect_ai_freid_detect_with_face(
    bef_effect_handle_t handle,
    const unsigned char *image,
    bef_ai_pixel_format pixel_format,
    int image_width,
    int image_height,
    int image_stride,
    bef_ai_rotate_type orientation,
    const bef_ai_face_106 *ptr_base_info,
    int face_count,
    bef_ai_freid_detect_result *freid_result);
```



|Parameter |Type |Description |
|---|---|---|
|handle |`bef_effect_handle_t` |Initialized FReID handle |
|image |`const unsigned char *` |Current frame image data |
|pixel_format |`bef_ai_pixel_format` |Pixel format; supports RGBA8888, BGRA8888, BGR888, RGB888 |
|image_width |`int` |Image width in pixels |
|image_height |`int` |Image height in pixels |
|image_stride |`int` |Byte stride of each image row |
|orientation |`bef_ai_rotate_type` |Clockwise rotation of the image; supports 0°, 90°, 180°, 270°. The `bef_ai_rotate_type` enum values are 0/1/2/3 — **must use enum constants, not raw degree values** |
|ptr_base_info |`const bef_ai_face_106 *` |Array of face 106\-point results from the same frame; `ID`, `tracking_cnt`, and `after_det` must be retained |
|face_count |`int` |Number of input faces; internally processes at most the number of faces the result structure can hold |
|freid_result |`bef_ai_freid_detect_result *` |Output parameter, allocated by the caller; provides the `face_id → track_id` mapping via `count` and `freid_pairs` |


**Return value:**  `BEF_RESULT_SUC` on success; the corresponding error code for null pointers, invalid orientation, or unsupported pixel format.

`ptr_base_info` must come from the face detection results of the same frame, retaining `ID`, `tracking_cnt`, and `after_det`. In the output, `face_id` is the current face tracking ID, while `track_id` is the FReID ID the business uses to associate identity across re\-entry into the frame.

<span id="4184e940"></span>
### C Example

```Plain
bef_effect_handle_t face_handle = NULL;
bef_effect_handle_t freid_handle = NULL;
bef_ai_face_info face_info = {0};
bef_ai_freid_detect_result freid_result = {0};
int freid_inited = 0;
const unsigned long long face_init_config =
    BEF_DETECT_SMALL_MODEL |
    BEF_DETECT_MODE_VIDEO |
    BEF_DETECT_FULL;
const unsigned long long face_detect_config =
    BEF_DETECT_MODE_VIDEO |
    BEF_DETECT_FULL;
bef_effect_result_t ret = bef_effect_ai_face_detect_create(
    face_init_config, face_model_path, &face_handle);
if (ret != BEF_RESULT_SUC) goto cleanup;
ret = bef_effect_ai_face_check_license(face_handle, face_license_path);
if (ret != BEF_RESULT_SUC) goto cleanup;
ret = bef_effect_ai_freid_create(&freid_handle);
if (ret != BEF_RESULT_SUC) goto cleanup;
ret = bef_effect_ai_freid_check_license(freid_handle, freid_license_path);
if (ret != BEF_RESULT_SUC) goto cleanup;
// For cross-process identity retention, use a stable, writable cache file path.
ret = bef_effect_ai_freid_set_offline_track_id_config(
    freid_handle,
    1,
    cache_path,
    BEF_AI_FREID_AUTO_SAVE_ON_NEW_TRACK_ID);
if (ret != BEF_RESULT_SUC) goto cleanup;
ret = bef_effect_ai_freid_init(freid_handle, freid_model_path);
if (ret != BEF_RESULT_SUC) goto cleanup;
freid_inited = 1;
// Run face detection first each frame, then pass the same frame image and its face results to FReID.
ret = bef_effect_ai_face_detect(
    face_handle,
    image,
    pixel_format,
    width,
    height,
    stride,
    orientation,
    face_detect_config,
    &face_info);
if (ret != BEF_RESULT_SUC) goto cleanup;
if (face_info.face_count > 0) {
    ret = bef_effect_ai_freid_detect_with_face(
        freid_handle,
        image,
        pixel_format,
        width,
        height,
        stride,
        orientation,
        face_info.base_infos,
        face_info.face_count,
        &freid_result);
    if (ret != BEF_RESULT_SUC) goto cleanup;
    for (int i = 0; i < freid_result.count; ++i) {
        int face_id = freid_result.freid_pairs[i].face_id;
        int track_id = freid_result.freid_pairs[i].track_id;
        // Use track_id to maintain business identity across re-entry.
    }
}
cleanup:
if (freid_inited) {
    // AUTO_SAVE mode does not require per-frame flush; save once more explicitly before exit.
    bef_effect_ai_freid_flush_offline_track_id(freid_handle);
}
if (freid_handle != NULL) {
    bef_effect_ai_freid_release(freid_handle);
}
if (face_handle != NULL) {
    bef_effect_ai_face_detect_destroy(face_handle);
}
```


<span id="46d255b9"></span>
## Java Integration

<span id="266bf6ad"></span>
### Interface Overview

The main FReID class is `FreidDetect`. The face input required by FReID is produced by `FaceDetect.detectFaceForFreid()`; this method belongs to `FaceDetect`, and `FaceDetect.init()` and `FaceDetect.setFaceDetectConfig()` must both succeed before calling it.

<span id="d8cc6548"></span>
#### 1. Initialize FReID

```Plain
public int init(String freidModelPath, String licensePath, boolean onlineLicense)
public int init(String freidModelPath, String licensePath)
```



|Parameter |Type |Description |
|---|---|---|
|freidModelPath |`String` |Path to the FReID model file |
|licensePath |`String` |Path to the license file |
|onlineLicense |`boolean` |Whether to use online license; the two\-parameter overload defaults to offline license |


**Return value:**  `BEF_RESULT_SUC` on success. On failure, returns the Java wrapper layer or native layer error code; troubleshoot per the "Error Handling" section of this document. Do not infer all native errors solely from same\-named constants in `EffectsSDKResultCode`. Repeated initialization directly returns success.

<span id="5114f0cb"></span>
#### 2. Set Runtime Parameters

```Plain
public int setParam(
    EffectsSDKEffectConstants.FreidParamType paramType,
    float value)
public int setParam(
    EffectsSDKEffectConstants.FreidParamType paramType,
    int value)
```



|Parameter |Type |Description |
|---|---|---|
|paramType |`FreidParamType` |Parameter type. Use the float overload for floating\-point parameters and the int overload for integer parameters. |
|value |`float` / `int` |Parameter value. Use the default when the business has no explicit tuning requirement. |


**Return value:**  `BEF_RESULT_SUC` on success; the Java wrapper layer returns \-4 if not initialized; native returns `BEF_RESULT_INVALID_PARAM_VALUE` (\-47) for an unsupported parameter type. See the "Error Handling" section for the difference in error code sources.

<span id="7fd55203"></span>
#### 3. Configure Offline TrackID

```Plain
public int setOfflineTrackIdConfig(
    boolean enable,
    String datPath,
    EffectsSDKEffectConstants.FreidOfflineTrackIdSaveMode saveMode)
```



|Parameter |Type |Description |
|---|---|---|
|enable |`boolean` |Whether to enable offline TrackID |
|datPath |`String` |Cache file path; must not be empty when `enable` is true |
|saveMode |`FreidOfflineTrackIdSaveMode` |`MANUAL_FLUSH_ONLY` = manual save only; `AUTO_SAVE_ON_NEW_TRACK_ID` = auto\-save when a new TrackID is added; `saveMode` must not be null (returns \-47 if null) |


**Return value:**  `BEF_RESULT_SUC` on success; `BEF_RESULT_INVALID_PARAM_VALUE` for invalid parameters. This method may be called before `init()`; the config is applied during initialization.

<span id="4d9df34d"></span>
#### 4. Restore Offline TrackID

```Plain
public int restoreOfflineTrackId()
```


No parameters.

**Return value:**  `BEF_RESULT_SUC` on success; the Java wrapper layer returns \-4 if not initialized; native returns `BEF_RESULT_FILE_NOT_FIND` (\-2) if the cache does not exist; `BEF_RESULT_INVALID_PARAM_VALUE` (\-47) if the config is invalid.

<span id="aff67ff5"></span>
#### 5. Write Offline TrackID

```Plain
public int flushOfflineTrackId()
```


No parameters.

**Return value:**  `BEF_RESULT_SUC` on success; the Java wrapper layer returns \-4 if not initialized; the corresponding native error code if the config is invalid, serialization fails, or the file write fails.

<span id="94255d9c"></span>
#### 6. Query Model Parameters

```Plain
public BefFreidKeyParam getModelParam()
```


No parameters.

**Return value:**  A `BefFreidKeyParam` on success, containing `model_version`, `model_thresh`, and `trackid_num`; `null` if not initialized or the native call fails.

<span id="9729fd1f"></span>
#### 7. Release FReID

```Plain
public void release()
```


No parameters. **Return value:**  none. Releases the native handle when initialized; the native layer attempts to write the configured offline TrackID before release.

<span id="f9bba14a"></span>
#### 8. Get FReID Face Input

```Plain
public BefFreidFaceInfo detectFaceForFreid(
    ByteBuffer buffer,
    EffectsSDKEffectConstants.PixlFormat pixelFormat,
    int width,
    int height,
    int stride,
    EffectsSDKEffectConstants.Rotation orientation)
```



|Parameter |Type |Description |
|---|---|---|
|buffer |`ByteBuffer` |Current frame image data; **must be a DirectByteBuffer** |
|pixelFormat |`PixlFormat` |Image pixel format |
|width |`int` |Image width in pixels |
|height |`int` |Image height in pixels |
|stride |`int` |Byte stride of each image row |
|orientation |`Rotation` |Clockwise rotation of the image; use the `Rotation` enum (`CLOCKWISE_ROTATE_0/90/180/270`, ids 0/1/2/3) — do not pass raw degree values |


**Return value:**  A `BefFreidFaceInfo` on success, containing the ordinary face detection results plus per\-face `faceId`, `trackingCnt`, `afterDet`; `null` if not initialized, face detection parameters not configured, or detection fails.

<span id="06a26dce"></span>
#### 9. Run FReID Detection

```Plain
public BefFreidDetectResult detect(
    ByteBuffer imageBuffer,
    EffectsSDKEffectConstants.PixlFormat pixelFormat,
    int width,
    int height,
    int stride,
    EffectsSDKEffectConstants.Rotation orientation,
    BefFreidFaceInfo freidFaceInfo)
```



|Parameter |Type |Description |
|---|---|---|
|imageBuffer |`ByteBuffer` |Current frame image data; **must be a DirectByteBuffer** |
|pixelFormat |`PixlFormat` |Pixel format; must match the one used to produce `freidFaceInfo` |
|width |`int` |Image width; must match the face detection input |
|height |`int` |Image height; must match the face detection input |
|stride |`int` |Byte stride of each image row; must match the face detection input |
|orientation |`Rotation` |Clockwise rotation of the image; must match the face detection input. Use the `Rotation` enum (`CLOCKWISE_ROTATE_0/90/180/270`, ids 0/1/2/3) — do not pass raw degree values |
|freidFaceInfo |`BefFreidFaceInfo` |The face input obtained from `detectFaceForFreid()` on the same frame |


**Return value:**  A `BefFreidDetectResult` on success, providing the `face_id → track_id` mapping via `count` and `freid_pairs`. `null` if not initialized or the native call fails.

`imageBuffer` must be a DirectByteBuffer. `BefFreidFaceInfo` additionally stores each face's `faceId`, `trackingCnt`, and `afterDet`; the object from the same frame must be passed when calling `detect()`.

<span id="9f4a37ab"></span>
### Java Example

```Plain
import java.io.File;
import java.nio.ByteBuffer;
FaceDetect faceDetect = new FaceDetect();
FreidDetect freidDetect = new FreidDetect();
// The init config includes the model, detection mode, and required face capabilities.
int faceInitConfig =
        EffectsSDKEffectConstants.BEF_DETECT_SMALL_MODEL
        | EffectsSDKEffectConstants.DetectMode.BEF_DETECT_MODE_VIDEO
        | EffectsSDKEffectConstants.FaceAction.BEF_DETECT_FULL;
// The runtime config must be a subset of the init config.
int faceDetectConfig =
        EffectsSDKEffectConstants.DetectMode.BEF_DETECT_MODE_VIDEO
        | EffectsSDKEffectConstants.FaceAction.BEF_DETECT_FULL;
int ret = faceDetect.init(
        context,
        faceModelPath,
        faceInitConfig,
        faceLicensePath,
        onlineLicense);
if (ret != 0) {
    throw new IllegalStateException("FaceDetect init failed: " + ret);
}
faceDetect.setFaceDetectConfig(faceDetectConfig);
// Use an app-private, stable, writable path. Do not delete this file when identity retention across launches is needed.
String cachePath = new File(context.getFilesDir(), "freid_buffer.dat")
        .getAbsolutePath();
ret = freidDetect.setOfflineTrackIdConfig(
        true,
        cachePath,
        EffectsSDKEffectConstants.FreidOfflineTrackIdSaveMode
                .AUTO_SAVE_ON_NEW_TRACK_ID);
if (ret != 0) {
    throw new IllegalStateException("FReID config failed: " + ret);
}
ret = freidDetect.init(freidModelPath, freidLicensePath, onlineLicense);
if (ret != 0) {
    throw new IllegalStateException("FReID init failed: " + ret);
}
// imageBuffer must be provided by the input source as a DirectByteBuffer; when constructing it yourself, use
// ByteBuffer.allocateDirect(stride * height).
if (imageBuffer == null || !imageBuffer.isDirect()) {
    throw new IllegalArgumentException("imageBuffer must be a DirectByteBuffer");
}
// The same frame must reuse a completely consistent buffer, format, size, stride, and rotation.
BefFreidFaceInfo faceInfo = faceDetect.detectFaceForFreid(
        imageBuffer, pixelFormat, width, height, stride, rotation);
if (faceInfo != null) {
    BefFreidDetectResult result = freidDetect.detect(
            imageBuffer, pixelFormat, width, height, stride, rotation, faceInfo);
    if (result != null) {
        for (int i = 0; i < result.count; ++i) {
            int faceId = result.freid_pairs[i].face_id;
            int trackId = result.freid_pairs[i].track_id;
            // Use trackId to maintain business identity across re-entry.
        }
    }
}
// AUTO_SAVE mode does not require per-frame flush; save once more explicitly before exit.
freidDetect.flushOfflineTrackId();
freidDetect.release();
faceDetect.release();
```


<span id="d265c922"></span>
## Offline TrackID Persistence

**Purpose of the cache file:**  The cache file stores the TrackID memory state that FReID has established. As long as the file is not deleted, overwritten, or its path changed, and it loads successfully on the next init, FReID continues its previous memory. `freid_buffer.dat` is only the file name used by the Demo; customers may customize the file name, directory, save timing, restore timing, and cleanup policy.

<span id="0238c75c"></span>
### Save Modes


|Mode |Write Timing |Usage and Trade\-offs |
|---|---|---|
|MANUAL_FLUSH_ONLY |Written only when the business explicitly calls C `bef_effect_ai_freid_flush_offline_track_id()` or Java `flushOfflineTrackId()`; `release` also attempts to save |Call before the recognition session ends, before stopping FReID, on page exit, or before the app enters the background. Gives control over file I/O; memory added after the last successful save may be lost on abnormal exit |
|AUTO_SAVE_ON_NEW_TRACK_ID |After each successful detection, checks the total TrackID count; auto\-writes when the count changes and is greater than 0 |No per\-frame `flush` needed. Memory is persisted more promptly with lower risk of loss on abnormal exit, but adding a TrackID produces file I/O |


<span id="266028ac"></span>
### Usage Rules


* Configure the cache path before `init`; init attempts automatic recovery. The first run having no cache file is not treated as a failure.

* Both modes may explicitly call `flush`; do not rely solely on `release`, since its execution cannot be guaranteed on abnormal exit.

* Deleting, clearing, or replacing the cache file loses existing memory; changing the path enters a separate, independent memory.

* When the model, algorithm version, or business identity domain changes, it is recommended to use a new cache file.

* On Android, use an app\-private, stable, writable path, e.g., `new File(context.getFilesDir(), "freid_buffer.dat")`. The internal Demo deletes this file on init and destroy for repeated demonstrations — this is **not** an SDK requirement. Production business requiring identity retention across launches must not copy that deletion logic; only clean the file when the user actively resets the identity store.


<span id="ff86ddb6"></span>
## Error Handling

**Java error code notes:**  Some of `FreidDetect`'s initialization state checks are done by the Java wrapper layer; other errors are returned by JNI/native. Some legacy constants in the current `EffectsSDKResultCode` share names with native common error codes but have different numeric values, so troubleshoot by the actual returned integer value and the table below — do not infer native errors from Java constant names alone.


|Error Code |Symbol/Source |Troubleshooting Direction |
|---|---|---|
|0 |BEF_RESULT_SUC |Call succeeded |
|\-1 |BEF_RESULT_FAIL |General failure; also returned when offline TrackID serialization or file read/write fails. Check cache path permissions and storage space |
|\-2 |BEF_RESULT_FILE_NOT_FIND |Cache file not found on explicit restore; on first run, treat as no historical cache |
|\-4 |Java wrapper layer BEF_RESULT_INVALID_HANDLE |`FreidDetect.setParam()`, `restoreOfflineTrackId()`, or `flushOfflineTrackId()` called before init |
|\-5 |native BEF_RESULT_INVALID_EFFECT_HANDLE |JNI/native handle is null or invalidated; check init and release timing |
|\-37 |BEF_RESULT_INVALID_IMAGE_DATA |Check the image pointer; on Java, specifically check that it is a DirectByteBuffer |
|\-38 |native BEF_RESULT_INVALID_IMAGE_FORMAT |Check that RGBA8888, BGRA8888, BGR888, or RGB888 is used |
|\-47 |BEF_RESULT_INVALID_PARAM_VALUE |Check for empty paths, null objects, parameter types, orientation, save mode, and whether `BefFreidFaceInfo` matches the current frame |
|\-109 |BEF_RESULT_SMASH_E_INVALID_MODEL |Check the model path, file integrity, and SDK/model version match |
|\-114 |BEF_RESULT_INVALID_LICENSE |Check the license file, validity period, package name, or app identifier |
|\-129 |BEF_RESULT_LICENSE_BAG_INVALID_SUB_FUNC |The license file does not include the FReID (face re\-identification) capability; contact technical support to confirm the license scope |


<span id="cce9b0a0"></span>
## FAQ

**Why can't ordinary face detection results be passed to FReID?** 

Ordinary Java face detection results do not contain the complete per\-face tracking fields FReID needs. Call `detectFaceForFreid()`, and pass the returned `BefFreidFaceInfo` as\-is to `FreidDetect.detect()`.

**Why does** **`face_id`** ** change when the same person re\-enters the frame?** 

`face_id` is the continuous tracking ID of the face detector; after tracking is lost and the face is re\-detected, it may change. Business identity association should use the `track_id` output by FReID.

**Why is historical memory not restored after a restart?** 

Check whether the two launches use the same cache path, whether the app has read/write permissions, and whether the business deleted or overwrote the cache file. In manual mode, a successful `flush` must also have been called before exit.
