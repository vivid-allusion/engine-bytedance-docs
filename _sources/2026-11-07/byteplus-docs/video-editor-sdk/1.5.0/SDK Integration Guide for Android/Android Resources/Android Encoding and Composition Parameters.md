---
title: "Android Encoding and Composition Parameters "
product: "BytePlus Video Editor"
product_code: "video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/video-editor-sdk/150-android-encoding-and-composition-parameters"
---

These are the parameters for encoding and configuration:


|**Parameter** |**Type** |**Description** |
|---|---|---|
|fps |Int |Video frames per second (FPS); currently uses a fixed frame rate for editing and composition. |
|outputSize |String |Output resolution of the composed video. It is calculated like the following: PairIntInt(`DEFAULT_OUTPUT_WIDTH`, `DEFAULT_OUTPUT_HEIGHT`). |
|resizeMode |Int |Video cropping mode when aspect ratio does not match: `1` for adding black bars, `2` for cropping. |
|enableUploadingWhileCompile |Boolean |Enables uploading while compiling. If `true`, use `setEncoderListener(l: INLEListenerEncoder?)` to get real\-time encoding data. |
|isSupportHWEncoder |Boolean |Indicates if hardware encoding is supported. Must be specified by the business (can also be controlled by cloud whitelist/blacklist). |
|NLEVideoCompileEncodeSettings.useHWEncoder |Boolean |Indicates if hardware encoding is used. Must be specified by the business (can also be controlled by cloud whitelist/blacklist). |
|NLEVideoCompileEncodeSettings.isSupportHWEncoder |Boolean |Indicates if hardware encoding is supported. Must be specified by the business (can also be controlled by cloud whitelist/blacklist). |
|bps |Int |Video bitrate. Note that this parameter is mutually exclusive with `swCRF` and `swQP`. |
|swMaxrate |Int |Maximum bitrate for software encoding. |
|swCRF |Int |CRF value for software encoding; lower values mean higher quality and larger file sizes. Recommended range is 15\-22. Note that this value is mutually exclusive with `bps` and `swQP`. |
|gopSize |Int |Size of the video GOP (Group of Pictures); number of frames between keyframes. |
|swQPOffset |Int |For CQP or CRF mode, the default is `0`. The value `(QP + qpoffset)` or `(crf + qpoffset)` should be within the range [0, 51]. |
|bitrateMode |String |Bitrate mode: `{ENCODE_BITRATE_MODE}` options are:<br><br><br>* `ENCODE_BITRATE_ABR`<br><br>* `ENCODE_BITRATE_CRF`<br><br>* `ENCODE_BITRATE_QP`<br><br>* `ENCODE_BITRATE_VBR` (not available). |
|softwareDecode |Boolean |Whether to use software decoding during composition. |
|encodeProfile |String |Video encoding profile:<br><br><br>* `ENCODE_PROFILE_UNKNOWN`<br><br>* `ENCODE_PROFILE_BASELINE`<br><br>* `ENCODE_PROFILE_MAIN`<br><br>* `ENCODE_PROFILE_HIGH` |
|encodeStandard |String |Video encoding format:<br><br><br>* `ENCODE_STANDARD_H264` (H.264)<br><br>* `ENCODE_STANDARD_ByteVC1` (HEVC)<br><br>* `ENCODE_STANDARD_MPEG4` (MPEG4)<br><br>* `ENCODE_STANDARD_AUTO` |


<span id="59741118"></span>
# Encoding parameters default values

These defaults help in standardizing video encoding settings and provide a starting point for configuration.

<span id="bb8ca063"></span>
## Optimized values—Video processing

```Kotlin
const val DEFAULT_FPS = 30
const val DEFAULT_RESIZE_MODE = 2 // Cropping
const val DEFAULT_HW_SUPPORT = true 
const val DEFAULT_BPS = 1024 * 1024 * 6 
const val DEFAULT_SW_MAX_RATE = 1024 * 1024 * 30L 
const val DEFAULT_SW_CRF = 17
const val DEFAULT_GOP_SIZE = 35
const val DEFAULT_SW_QP_OFFSET = 0.0f
const val DEFAULT_OUTPUT_WIDTH = 720
const val DEFAULT_OUTPUT_HEIGHT = 1280
const val DEFAULT_SOFTWARE_DECODE = true
```


<span id="1d2bd878"></span>
## Optimized values—Hard\-coded parameter configuration

```Kotlin
fps = DEFAULT_FPS  
outputSize = PairIntInt(DEFAULT_OUTPUT_WIDTH, DEFAULT_OUTPUT_HEIGHT)
resizeMode = DEFAULT_RESIZE_MODE
enableUploadingWhileCompile = false
isSupportHWEncoder = DEFAULT_HW_SUPPORT
mVideoCompileEncodeSetting.useHWEncoder = DEFAULT_HW_SUPPORT
mVideoCompileEncodeSetting.isSupportHWEncoder = DEFAULT_HW_SUPPORT
bps = DEFAULT_BPS
gopSize = DEFAULT_GOP_SIZE
softwareDecode = DEFAULT_SOFTWARE_DECODE
encodeProfile = NLE_ENCODE_PROFILE.ENCODE_PROFILE_BASELINE
encodeStandard = NLE_ENCODE_STANDARD.ENCODE_STANDARD_H264
```


<span id="15829f31"></span>
## Optimized values—soft\-coded parameter configuration

```Kotlin
fps = DEFAULT_FPS 
outputSize = PairIntInt(DEFAULT_OUTPUT_WIDTH, DEFAULT_OUTPUT_HEIGHT)
resizeMode = DEFAULT_RESIZE_MODE
enableUploadingWhileCompile = false
isSupportHWEncoder = false
mVideoCompileEncodeSetting.useHWEncoder = false
mVideoCompileEncodeSetting.isSupportHWEncoder = false
bps = DEFAULT_BPS
swMaxrate = DEFAULT_SW_MAX_RATE
swCRF = DEFAULT_SW_CRF
gopSize = DEFAULT_GOP_SIZE
swQPOffset = DEFAULT_SW_QP_OFFSET
bitrateMode = NLE_ENCODE_BITRATE_MODE.ENCODE_BITRATE_CRF
softwareDecode = DEFAULT_SOFTWARE_DECODE
encodeProfile = NLE_ENCODE_PROFILE.ENCODE_PROFILE_BASELINE
encodeStandard = NLE_ENCODE_STANDARD.ENCODE_STANDARD_H264
```
