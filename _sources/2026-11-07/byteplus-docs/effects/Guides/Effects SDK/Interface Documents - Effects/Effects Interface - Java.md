---
title: "Effects Interface - Java"
product: "BytePlus Effects"
product_code: "effects"
source: "https://docs.byteplus.com/en/docs/effects/docs-java-api"
---

<span id="Java interface"></span>
# Java interface

<span id="Special effects"></span>
## Special effects

Special effects are a collection of features that currently include face beautification, shape beautification, body shaping, and beauty makeup, filters, stickers, Animoj, and AR. Corresponding class file: RenderManager.java.

<span id="1. Initialization"></span>
### 1. Initialization

```Plain
// 1. Default: parallel rendering enabled, offline license, GLES20
public int init(Context context, String modelDir, String licensePath);

// 2. Offline authentication, custom parallel rendering & GLES version
public int init(Context context, String modelDir, String licensePath, boolean usePipeline,int renderApi);

// 3. Standard: custom parallel rendering, online/offline license, GLES version
public int init(Context context, String modelDir, String licensePath, boolean usePipeline, boolean onlineLicense,int renderApi);

// 4. With model cache path
public int init(Context context, String modelDir, String licensePath, String modelCachePath, boolean usePipeline, boolean onlineLicense,int renderApi);

// 5. With toggle for loading models from assets
public int init(Context context, String modelDir, String licensePath, boolean usePipeline, boolean onlineLicense, boolean loadModelFromAsset, int renderApi);

// 6. With model cache path + toggle for loading models from assets
public int init(Context context, String modelDir, String licensePath, String modelCachePath, boolean usePipeline, boolean onlineLicense, boolean loadModelFromAsset, int renderApi);
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|context |Context |Android context |
|modelDir |String |Root directory of model files. Note: not the absolute path of individual model files. Directory hierarchy and names must exactly match the demo package. |
|licensePath |String |Absolute path of license file |
|usePipeline |boolean |Enable parallel rendering |
|onlineLicense |boolean |`true` for online license; `false` for offline license |
|renderApi |int |GLES version. 0 = GLES20, 1 = GLES30 |
|modelCachePath |String |Model cache directory |
|loadModelFromAsset |boolean |Load model files from Android assets folder |


**Return value**: Returns `BEF_RESULT_SUC` on success; returns corresponding error code on failure.

&nbsp;

<span id="ef7abb64"></span>
### 2. Set beauty material

```Plain
public boolean setBeauty(String resourcePath)
```


Applicable for SDK version 2.6 and earlier. Starting from 2.7, **use setComposerNodes** to apply beauty effects.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|resourcePath |String |Absolute path of beauty resource. Pass `null` or empty string to remove beauty effect. |


**Return value**: `true` on success; error code on failure.

&nbsp;

<span id="e1465b79"></span>
### 3. Set reshaping material

```Plain
public boolean setReshape(String resourcePath)
```


Applicable for SDK version 2.6 and earlier. Starting from 2.7, **use setComposerNodes** to apply face reshaping effects.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|resourcePath |String |Absolute path of reshaping resource. Pass `null` or empty string to remove reshaping effect. |


**Return value**: `true` on success; error code on failure.

&nbsp;

<span id="d313fd85"></span>
### 4. Set filter material

```Plain
public boolean setFilter(String resourcePath)
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|resourcePath |String |Absolute path of filter resource. Pass `null` or empty string to remove filter effect. |


**Return value**: `true` on success; error code on failure.

&nbsp;

<span id="f9b14f0e"></span>
### 5. Set makeup material

```Plain
public boolean setMakeUp(String resourcePath)
```


Applicable for SDK version 2.6 and earlier. Starting from 2.7, **use setComposerNodes** to apply makeup effects.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|resourcePath |String |Absolute path of makeup resource. Pass `null` or empty string to remove makeup effect. |


**Return value**: `true` on success; error code on failure.

&nbsp;

<span id="f13922f7"></span>
### 6. Set sticker material

```Plain
public boolean setSticker(String resourcePath)
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|resourcePath |String |Absolute path of sticker resource. Pass `null` or empty string to remove sticker effect. |


**Return value**: `true` on success; error code on failure.

&nbsp;

<span id="20701eac"></span>
### 7. Reset sticker

```Plain
public boolean resetSticker()
```


Call this method to reset loaded sticker; sequence animation restarts from beginning.

**Return value**: `true` on success; `false` on failure.

&nbsp;

<span id="44d953a8"></span>
### 8. Set virtual background image

```Plain
/**
 * Set virtual background image
 * @param key Fixed key for virtual background: "BCCustomBackground"
 * @param path Absolute path of background image. Default image inside sticker package: chroma_matting_bg/AmazingFeature/image/background.png
 * @return
 */
public int setRenderCacheTexture(String key, String path);
```


Use to update virtual background / green screen background. A virtual background sticker package must be loaded before calling this API.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|key |String |Fixed key: `"BCCustomBackground"` |
|path |String |Absolute image path. SDK parses image into texture. |


**Return value**: `BEF_RESULT_SUC` on success; error code on failure.

&nbsp;

<span id="272e989e"></span>
### 9. Set virtual background from buffer

```Plain
/**
 * Set virtual background texture
 * @param key Fixed key for virtual background: "BCCustomBackground"
 * @param buffer Background image buffer
 * @param width Image width
 * @param height Image height
 * @param stride Image stride
 * @param format Pixel format
 * @param rotation Rotation angle
 * @return
 */
public int setRenderCacheTextureWithBuffer(
    String key,
    ByteBuffer buffer,
    int width,
    int height,
    int stride,
    EffectsSDKEffectConstants.PixlFormat format,
    EffectsSDKEffectConstants.Rotation rotation);
```


Use to update virtual background / green screen background. A virtual background sticker package must be loaded before calling this API.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|key |String |Fixed key: `"BCCustomBackground"` |
|buffer |ByteBuffer |Raw image buffer |
|width |int |Image width |
|height |int |Image height |
|stride |int |Image stride |
|format |PixlFormat |Only RGBA supported |
|rotation |Rotation |Rotation enum |


**Return value**: `BEF_RESULT_SUC` on success; error code on failure.

&nbsp;

<span id="1bbce522"></span>
### 10. Remove virtual background

```Plain
/**
 * Remove virtual background texture
 * @param key Fixed key for virtual background: "BCCustomBackground"
 * @return
 */
public int removeRenderCacheExternalTexture(String key);
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|key |String |Fixed key: `"BCCustomBackground"` |


**Return value**: `BEF_RESULT_SUC` on success; error code on failure.

&nbsp;

<span id="66c94364"></span>
### 11. Set virtual background texture

> Added in 4.7.1


```Plain
/**
 * Set virtual background texture
 * @param key Fixed key for virtual background: "BCCustomBackground"
 * @param textureid OpenGL texture ID
 * @param width Texture width
 * @param height Texture height
 * @return
 */
public int setRenderCacheExternalTexture(String key, int textureid, int width, int height)
```


Use to update virtual background / green screen background. A virtual background sticker package must be loaded before calling this API.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|key |String |Fixed key: `"BCCustomBackground"` |
|textureid |int |OpenGL texture ID |
|width |int |Texture width |
|height |int |Texture height |


**Return value**: `BEF_RESULT_SUC` on success; error code on failure.

&nbsp;

<span id="2d81e4a1"></span>
### 12. Set virtual background texture with rotation

> Added in 4.7.1


```Plain
/**
 * Set virtual background texture
 * @param key Fixed key for virtual background: "BCCustomBackground"
 * @param textureid OpenGL texture ID
 * @param width Texture width
 * @param height Texture height
 * @param rotation Rotation angle
 * @return
 */
public int setRenderCacheExternalTextureWithRotation(String key, int textureid, int width, int height, EffectsSDKEffectConstants.Rotation rotation)
```


Use to update virtual background / green screen background. A virtual background sticker package must be loaded before calling this API.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|key |String |Fixed key: `"BCCustomBackground"` |
|textureid |int |OpenGL texture ID |
|width |int |Texture width |
|height |int |Texture height |
|rotation |Rotation |Rotation enum |


**Return value**: `BEF_RESULT_SUC` on success; error code on failure.

&nbsp;

<span id="051c0335"></span>
### 13. Process texture input

```Plain
public boolean processTexture( int srcTextureId,  int dstTextureId,  int width, int height, BytedEffectConstants.Rotation rotation, double timestamp)
```


Process input texture and render final effects.

1.Input texture must be `TEXTURE_2D`. Face must be upright. Android camera output is usually `GL_TEXTURE_EXTERNAL_OES` with rotation (front camera:270°, back camera:90°).

2.Front camera mirror flip should be handled **before** feeding texture into this API.

3.Timestamp comes from SurfaceTexture. Contact technical support if SurfaceTexture timestamp is unavailable.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|srcTextureId |int |Input texture ID (TEXTURE_2D) |
|dstTextureId |int |Output texture ID (TEXTURE_2D) |
|width |int |Texture width |
|height |int |Texture height |
|rotation |Rotation |Image rotation |
|timestamp |double |SurfaceTexture timestamp |


**Return value**: `true` on success; `false` on failure.

&nbsp;

<span id="9f09f923"></span>
### 14. Process buffer input

```Plain
public boolean processBuffer( ByteBuffer inputdata,  BytedEffectConstants.Rotation orient,  int in_pixformat,  int imagew,  int imageh,  int imagestride,  byte[] outdata,  int out_pixformat, double timestamp)
```


> Note: Buffer input is **not recommended** for performance reasons.


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|inputdata |ByteBuffer |Input image buffer |
|orient |Rotation |Image rotation |
|in_pixformat |int |Input pixel format |
|imagew |int |Image width |
|imageh |int |Image height |
|imagestride |int |Image stride |
|outdata |byte[] |Output image buffer |
|out_pixformat |int |Output pixel format |
|timestamp |double |Timestamp |


**Return value**: `true` on success; `false` on failure.

&nbsp;

<span id="999aa809"></span>
### 15. Run algorithm detection

> Must be called before `processTextureOnly`. Splits detection and rendering, allowing different data sources for detection and render.


```Plain
// Algorithm detection with texture + buffer
public boolean algorithmTextureWithBuffer(int texture, ByteBuffer buffer,  BytedEffectConstants.Rotation orient, int pixelFormat,  int width,  int height, int stride, long timeStamp)

// Algorithm detection with buffer only
public boolean algorithmBuffer(ByteBuffer buffer, BytedEffectConstants.Rotation orient,  int pixelFormat,  int width,  int height, int stride,  long timeStamp)
```


**Return value**: `true` on success; `false` on failure.

&nbsp;

<span id="9025c975"></span>
### 16. Run effect rendering

> Must call algorithm detection API before this method.


```Plain
public boolean processTextureOnly(int srcTexture,  int dstTexture, int width,  int height,  BytedEffectConstants.Rotation rotation,  long timeStamp)
```


**Return value**: `true` on success; `false` on failure.

&nbsp;

<span id="0d725229"></span>
### 17. Update effect intensity

```Plain
public boolean updateIntensity( int intensitytype,  float intensity)
```


Applicable for SDK version 2.6 and earlier for beauty/reshaping intensity. Starting from 2.7, **use updateComposerNodes**. Filter intensity uses this API for all SDK versions.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|intensitytype |int |Intensity type enum (cheek, eye etc.) |
|intensity |float |Value range: 0 ~ 1 |


**Return value**: `BEF_RESULT_SUC` on success; refer to `BytedEffectConstants` for error codes.

&nbsp;

<span id="c7d05ccd"></span>
### 18. Update reshaping parameters

```Plain
public boolean updateReshape( float cheekintensity,  float eyeintensity)
```


Applicable for SDK version 2.6 and earlier. Starting from 2.7, **use updateComposerNodes**.

**Parameters**


|Parameter |Type |Description |
|---|---|---|
|cheekintensity |float |Face slimming intensity, range 0~1 |
|eyeintensity |float |Eye enlargement intensity, range 0~1 |


**Return value**: `BEF_RESULT_SUC` on success; refer to `BytedEffectConstants` for error codes.

&nbsp;

<span id="eb857a6c"></span>
### 19. Set composite effects (beauty, reshaping, makeup, body effects)

```Plain
public int setComposerNodes(String[] composerNodes)
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|composerNodes |String[] |Array of paths to selected effect resources |


**Return value**: `BEF_RESULT_SUC` on success; refer to `BytedEffectConstants` for error codes.

&nbsp;

<span id="84419a30"></span>
### 20. Update composite effect intensity (beauty, reshaping, makeup, body effects)

```Plain
public int updateComposerNodes( String path,  String key,  float value)
```


**Parameters**


|Parameter |Type |Description |
|---|---|---|
|path |String |Path of target effect resource |
|key |String |Parameter key of effect |
|value |float |Intensity value, range 0 ~ 1 |


**Return value**: `BEF_RESULT_SUC` on success; refer to `BytedEffectConstants` for error codes.

&nbsp;

<span id="41c01afe"></span>
### 21. Get face detection result

```Plain
public BefFaceInfo getFaceDetectResult();
```


**Return value**: `BefFaceInfo` object on success; `null` on failure.

<span id="84f56be4"></span>
#### Get face occlusion result

> Added in 4.8.1


```Plain
public BefFaceInfo getFaceOcclusionResult ()
```


**Return value**: `BefFaceInfo` object containing face occlusion info on success; `null` on failure.

&nbsp;

<span id="a9a9c383"></span>
### 22. Get hand detection result

```Plain
public BefHandInfo getHandDetectResult();
```


**Return value**: `BefHandInfo` object on success; `null` on failure.

&nbsp;

<span id="e17baf30"></span>
### 23. Get human skeleton detection result

```Plain
public BefSkeletonInfo getSkeletonDetectResult();
```


**Return value**: `BefSkeletonInfo` object on success; `null` on failure.

&nbsp;

<span id="3f7277d4"></span>
### 24. Release handle

```Plain
public void release()
```


Release SDK resources.

&nbsp;

<span id="c5c7536d"></span>
### 25. Check whether device supports advanced special effects (Android only)

> Added in 4.7.3


```Plain
public static boolean gpuIsSupport()
```


**Return value**: `true` if device supports advanced special effects; `false` otherwise.
