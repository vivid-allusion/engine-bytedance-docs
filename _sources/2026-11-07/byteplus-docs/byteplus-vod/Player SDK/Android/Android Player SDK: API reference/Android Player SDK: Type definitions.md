---
title: "Android Player SDK: Type definitions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-android-player-sdk-type-definitions"
---

<span id="DataLoaderHelper"></span>
# DataLoaderHelper

```java
public class com.ss.ttvideoengine.DataLoaderHelper
```


The helper for data loading management.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**int** |[DATALOADER_KEY_INT_MAXCACHESIZE](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-dataloader_key_int_maxcachesize) |
|**int** |[DATALOADER_KEY_INT_PARALLEL_NUM](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-dataloader_key_int_parallel_num) |
|**int** |[DATALOADER_KEY_INT_ENCRYPT_VERSION](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-dataloader_key_int_encrypt_version) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**static DataLoaderHelper** |[getDataLoader](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-getdataloader) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**void** |[addListener](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-addlistener) |
|**void** |[removeListener](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-removelistener) |
|**DataLoaderCacheFileInfo** |[cacheFileInfo](https://docs.byteplus.com/en/docs/25/7959#DataLoaderHelper-cachefileinfo) |


<span id="Variable details"></span>
## Variable details

<span id="DataLoaderHelper-dataloader_key_int_maxcachesize"></span>
### DATALOADER_KEY_INT_MAXCACHESIZE

```java
public static final int com.ss.ttvideoengine.DataLoaderHelper.DATALOADER_KEY_INT_MAXCACHESIZE = 1;
```


The maximum capacity of the data loading cache. The default value is 200M.

<span id="DataLoaderHelper-dataloader_key_int_parallel_num"></span>
### DATALOADER_KEY_INT_PARALLEL_NUM

```java
public static final int com.ss.ttvideoengine.DataLoaderHelper.DATALOADER_KEY_INT_PARALLEL_NUM = 11;
```


The maximum number of parallel preload tasks. The default value is 1.

<span id="DataLoaderHelper-dataloader_key_int_encrypt_version"></span>
### DATALOADER_KEY_INT_ENCRYPT_VERSION

```java
public static final int com.ss.ttvideoengine.DataLoaderHelper.DATALOADER_KEY_INT_ENCRYPT_VERSION = 30;
```


Controls whether the cached file is encrypted.

<span id="Function details"></span>
## Function details

<span id="DataLoaderHelper-getdataloader"></span>
### getDataLoader

```java
public static DataLoaderHelper com.ss.ttvideoengine.DataLoaderHelper.getDataLoader()
```


Gets the data loading helper instance.

**Returns**

An instance of `DataLoaderHelper`.

<span id="DataLoaderHelper-addlistener"></span>
### addListener

```java
public void com.ss.ttvideoengine.DataLoaderHelper.addListener(
    DataLoaderListener2 listener)
```


Adds a data loading listener.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**DataLoaderListener2** |The data loading listener. For details, see [DataLoaderListener2](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#dataloaderlistener2). |


<span id="DataLoaderHelper-removelistener"></span>
### removeListener

```java
public void com.ss.ttvideoengine.DataLoaderHelper.removeListener(
    DataLoaderListener2 listener)
```


Removes the data loading listener.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener |**DataLoaderListener2** |The data loading listener. For details, see [DataLoaderListener2](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#dataloaderlistener2). |


<span id="DataLoaderHelper-cachefileinfo"></span>
### cacheFileInfo

```java
public DataLoaderCacheFileInfo com.ss.ttvideoengine.DataLoaderHelper.cacheFileInfo(
    String key)
```


Gets the information about the local cached file.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**String** |The cache key. |


**Returns**

The information about the local cached file.

<span id="DataLoaderCacheInfo"></span>
# DataLoaderCacheInfo

```java
public class com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheInfo
```


Cache information.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**long** |[mMediaSize](https://docs.byteplus.com/en/docs/25/7959#DataLoaderCacheInfo-mmediasize) |
|**String** |[mLocalFilePath](https://docs.byteplus.com/en/docs/25/7959#DataLoaderCacheInfo-mlocalfilepath) |


<span id="Variable details"></span>
## Variable details

<span id="DataLoaderCacheInfo-mmediasize"></span>
### mMediaSize

```java
public long com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheInfo.mMediaSize = 0;
```


The total size of the cached video file, in bytes.

<span id="DataLoaderCacheInfo-mlocalfilepath"></span>
### mLocalFilePath

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheInfo.mLocalFilePath = null;
```


The local path of the cached file.

<span id="DataLoaderTaskProgressInfo"></span>
# DataLoaderTaskProgressInfo

```java
public class com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo
```


Task progress information.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**String** |[mKey](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mkey) |
|**String** |[mVideoId](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mvideoid) |
|**String** |[mLocalFilePath](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mlocalfilepath) |
|**long** |[mMediaSize](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mmediasize) |
|**Resolution** |[mResolution](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mresolution) |
|**String** |[mDecryptionKey](https://docs.byteplus.com/en/docs/25/7959#DataLoaderTaskProgressInfo-mdecryptionkey) |


<span id="Variable details"></span>
## Variable details

<span id="DataLoaderTaskProgressInfo-mkey"></span>
### mKey

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mKey = null;
```


The cache key, which is the unique identifier of the local cached file.

<span id="DataLoaderTaskProgressInfo-mvideoid"></span>
### mVideoId

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mVideoId = null;
```


The video ID. Can be null.

<span id="DataLoaderTaskProgressInfo-mlocalfilepath"></span>
### mLocalFilePath

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mLocalFilePath = null;
```


The local path of the cached file.

<span id="DataLoaderTaskProgressInfo-mmediasize"></span>
### mMediaSize

```java
public long com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mMediaSize = 0;
```


The size of the cached file.

<span id="DataLoaderTaskProgressInfo-mresolution"></span>
### mResolution

```java
public Resolution com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mResolution = Resolution.Undefine;
```


The resolution of the cached video file.

<span id="DataLoaderTaskProgressInfo-mdecryptionkey"></span>
### mDecryptionKey

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskProgressInfo.mDecryptionKey = null;
```


The decryption key.

<span id="CacheInfo"></span>
# CacheInfo

```java
public class com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskLoadProgress.CacheInfo
```


Cache information.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**String** |[mKey](https://docs.byteplus.com/en/docs/25/7959#CacheInfo-mkey) |
|**long** |[mMediaSize](https://docs.byteplus.com/en/docs/25/7959#CacheInfo-mmediasize) |
|**String** |[mLocalFilePath](https://docs.byteplus.com/en/docs/25/7959#CacheInfo-mlocalfilepath) |


<span id="Variable details"></span>
## Variable details

<span id="CacheInfo-mkey"></span>
### mKey

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskLoadProgress.CacheInfo.mKey = null;
```


The cache key.

<span id="CacheInfo-mmediasize"></span>
### mMediaSize

```java
public long com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskLoadProgress.CacheInfo.mMediaSize = 0;
```


The total size of the cached video file, in bytes.

<span id="CacheInfo-mlocalfilepath"></span>
### mLocalFilePath

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderTaskLoadProgress.CacheInfo.mLocalFilePath = null;
```


The file path of the cached video.

<span id="DataLoaderCacheFileInfo"></span>
# DataLoaderCacheFileInfo

```java
public class com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheFileInfo
```


Cache file information.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**String** |[mLocalFilePath](https://docs.byteplus.com/en/docs/25/7959#DataLoaderCacheFileInfo-mlocalfilepath) |
|**long** |[mMediaSize](https://docs.byteplus.com/en/docs/25/7959#DataLoaderCacheFileInfo-mmediasize) |


<span id="Variable details"></span>
## Variable details

<span id="DataLoaderCacheFileInfo-mlocalfilepath"></span>
### mLocalFilePath

```java
public String com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheFileInfo.mLocalFilePath = null;
```


The local path of the cached file.

<span id="DataLoaderCacheFileInfo-mmediasize"></span>
### mMediaSize

```java
public long com.ss.ttvideoengine.DataLoaderHelper.DataLoaderCacheFileInfo.mMediaSize = 0;
```


The size of the cached file.

<span id="DirectUrlSource"></span>
# DirectUrlSource

```java
public class com.ss.ttvideoengine.source.DirectUrlSource
```


The URL playback source.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
| **@Nullable UrlItem** |[firstItem](https://docs.byteplus.com/en/docs/25/7959#DirectUrlSource-firstitem) |
| **@NonNull @Override String** |[vid](https://docs.byteplus.com/en/docs/25/7959#DirectUrlSource-vid) |


<span id="Function details"></span>
## Function details

<span id="DirectUrlSource-firstitem"></span>
### firstItem

```java
@Nullable public UrlItem com.ss.ttvideoengine.source.DirectUrlSource.firstItem()
```


Gets the first item in the `DirectUrlSource`.

**Returns**

The first item in the `DirectUrlSource`.

<span id="DirectUrlSource-vid"></span>
### vid

```java
@NonNull @Override public String com.ss.ttvideoengine.source.DirectUrlSource.vid()
```


Gets the video ID.

**Returns**

The video ID.

<span id="UrlItem"></span>
# UrlItem

```java
public static class com.ss.ttvideoengine.source.DirectUrlSource.UrlItem
```


The URL item.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[getUrl](https://docs.byteplus.com/en/docs/25/7959#UrlItem-geturl) |
|**String[]**  |[getUrls](https://docs.byteplus.com/en/docs/25/7959#UrlItem-geturls) |
|**String** |[getCacheKey](https://docs.byteplus.com/en/docs/25/7959#UrlItem-getcachekey) |
|**String** |[getPlayAuth](https://docs.byteplus.com/en/docs/25/7959#UrlItem-getplayauth) |
|**String** |[getEncodeType](https://docs.byteplus.com/en/docs/25/7959#UrlItem-getencodetype) |


<span id="Function details"></span>
## Function details

<span id="UrlItem-geturl"></span>
### getUrl

```java
public String com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.getUrl()
```


Gets the main URL.

**Returns**

The main URL.

<span id="UrlItem-geturls"></span>
### getUrls

```java
public String[] com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.getUrls()
```


Gets all the URLs, including the main and backup URLs.

**Returns**

All the URLs.

<span id="UrlItem-getcachekey"></span>
### getCacheKey

```java
public String com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.getCacheKey()
```


Gets the cache key of the local cached file.

**Returns**

The cache key.

<span id="UrlItem-getplayauth"></span>
### getPlayAuth

```java
public String com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.getPlayAuth()
```


Gets the key for private DRM encryption.

**Returns**

The decryption key.

<span id="UrlItem-getencodetype"></span>
### getEncodeType

```java
public String com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.getEncodeType()
```


Gets the video codec.

**Returns**

The video codec.

<span id="Builder"></span>
# Builder

```java
public static class com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder
```


Builder for [UrlItem](https://docs.byteplus.com/en/docs/25/7959#urlitem).

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**Builder** |[Builder](https://docs.byteplus.com/en/docs/25/7959#Builder-builder) |
|**Builder** |[setUrl](https://docs.byteplus.com/en/docs/25/7959#Builder-seturl) |
|**Builder** |[setUrls](https://docs.byteplus.com/en/docs/25/7959#Builder-seturls) |
|**Builder** |[setCacheKey](https://docs.byteplus.com/en/docs/25/7959#Builder-setcachekey) |
|**Builder** |[setPlayAuth](https://docs.byteplus.com/en/docs/25/7959#Builder-setplayauth) |
|**Builder** |[setEncodeType](https://docs.byteplus.com/en/docs/25/7959#Builder-setencodetype) |
|**UrlItem** |[build](https://docs.byteplus.com/en/docs/25/7959#Builder-build) |


<span id="Function details"></span>
## Function details

<span id="Builder-builder"></span>
### Builder

```java
public com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.Builder()
```


Constructor.

<span id="Builder-seturl"></span>
### setUrl

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.setUrl(
    @NonNull String url)
```


Sets the URL.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|url | **@NonNull String** |The URL to set. |


**Returns**

The builder.

<span id="Builder-seturls"></span>
### setUrls

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.setUrls(
    @NonNull String[] urls)
```


Sets the URL list.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls | **@NonNull String[]**  |The URL list, including the main and backup URLs. |


**Returns**

The builder.

<span id="Builder-setcachekey"></span>
### setCacheKey

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.setCacheKey(
    @Nullable String cacheKey)
```


Sets the cache key.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|cacheKey | **@Nullable String** |The cache key, which is the unique identifier for the local cached file of the data loader module. It is recommended to use the MD5 of the URL as the cache key. |


**Returns**

The builder.

<span id="Builder-setplayauth"></span>
### setPlayAuth

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.setPlayAuth(
    @Nullable String playAuth)
```


Sets the playback auth token.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playAuth | **@Nullable String** |The playback auth token. |


**Returns**

The builder.

<span id="Builder-setencodetype"></span>
### setEncodeType

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.setEncodeType(
    @Nullable String encodeType)
```


Sets the video codec.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|encodeType | **@Nullable String** |The codec type of the video. Can be set as `h264`,`h265`, or `av1`. |


**Returns**

The builder.

<span id="Builder-build"></span>
### build

```java
public UrlItem com.ss.ttvideoengine.source.DirectUrlSource.UrlItem.Builder.build()
```


Builds the [UrlItem](https://docs.byteplus.com/en/docs/25/7959#urlitem) object.

**Returns**

The built [UrlItem](https://docs.byteplus.com/en/docs/25/7959#urlitem) object.

<span id="Builder"></span>
# Builder

```java
public static class com.ss.ttvideoengine.source.DirectUrlSource.Builder
```


Builder for [DirectUrlSource](https://docs.byteplus.com/en/docs/25/7959#directurlsource).

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**Builder** |[Builder](https://docs.byteplus.com/en/docs/25/7959#Builder-builder) |
|**Builder** |[setVid](https://docs.byteplus.com/en/docs/25/7959#Builder-setvid) |


<span id="Function details"></span>
## Function details

<span id="Builder-builder"></span>
### Builder

```java
public com.ss.ttvideoengine.source.DirectUrlSource.Builder.Builder()
```


Constructor.

<span id="Builder-setvid"></span>
### setVid

```java
public Builder com.ss.ttvideoengine.source.DirectUrlSource.Builder.setVid(
    @Nullable String vid)
```


Sets the video ID.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid | **@Nullable String** |The video ID. It can be null. |


**Returns**

The builder.

<span id="VideoModelSource"></span>
# VideoModelSource

```java
public class com.ss.ttvideoengine.source.VideoModelSource
```


The video model playback source.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[vid](https://docs.byteplus.com/en/docs/25/7959#VideoModelSource-vid) |
|**IVideoModel** |[videoModel](https://docs.byteplus.com/en/docs/25/7959#VideoModelSource-videomodel) |
|**Resolution** |[resolution](https://docs.byteplus.com/en/docs/25/7959#VideoModelSource-resolution) |


<span id="Function details"></span>
## Function details

<span id="VideoModelSource-vid"></span>
### vid

```java
public String com.ss.ttvideoengine.source.VideoModelSource.vid()
```


Gets the video ID.

**Returns**

The video ID.

<span id="VideoModelSource-videomodel"></span>
### videoModel

```java
public IVideoModel com.ss.ttvideoengine.source.VideoModelSource.videoModel()
```


Gets the video model playback source.

**Returns**

The video model playback source.

<span id="VideoModelSource-resolution"></span>
### resolution

```java
public Resolution com.ss.ttvideoengine.source.VideoModelSource.resolution()
```


Gets the resolution.

**Returns**

The resolution.

<span id="VidPlayAuthTokenSource"></span>
# VidPlayAuthTokenSource

```java
public class com.ss.ttvideoengine.source.VidPlayAuthTokenSource
```


The VID playback source.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[vid](https://docs.byteplus.com/en/docs/25/7959#VidPlayAuthTokenSource-vid) |
|**String** |[playAuthToken](https://docs.byteplus.com/en/docs/25/7959#VidPlayAuthTokenSource-playauthtoken) |
|**String** |[encodeType](https://docs.byteplus.com/en/docs/25/7959#VidPlayAuthTokenSource-encodetype) |
|**Resolution** |[resolution](https://docs.byteplus.com/en/docs/25/7959#VidPlayAuthTokenSource-resolution) |


<span id="Function details"></span>
## Function details

<span id="VidPlayAuthTokenSource-vid"></span>
### vid

```java
public String com.ss.ttvideoengine.source.VidPlayAuthTokenSource.vid()
```


Gets the video ID.

**Returns**

The video ID.

<span id="VidPlayAuthTokenSource-playauthtoken"></span>
### playAuthToken

```java
public String com.ss.ttvideoengine.source.VidPlayAuthTokenSource.playAuthToken()
```


Gets the playback auth token.

**Returns**

The playback auth token.

<span id="VidPlayAuthTokenSource-encodetype"></span>
### encodeType

```java
public String com.ss.ttvideoengine.source.VidPlayAuthTokenSource.encodeType()
```


Gets the video codec type.

**Returns**

The video codec type.

<span id="VidPlayAuthTokenSource-resolution"></span>
### resolution

```java
public Resolution com.ss.ttvideoengine.source.VidPlayAuthTokenSource.resolution()
```


Gets the resolution.

**Returns**

The resolution.

<span id="Builder"></span>
# Builder

```java
public static class com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder
```


Builder for [VidPlayAuthTokenSource](https://docs.byteplus.com/en/docs/25/7959#vidplayauthtokensource).

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**Builder** |[Builder](https://docs.byteplus.com/en/docs/25/7959#Builder-builder) |
|**Builder** |[setVid](https://docs.byteplus.com/en/docs/25/7959#Builder-setvid) |
|**Builder** |[setPlayAuthToken](https://docs.byteplus.com/en/docs/25/7959#Builder-setplayauthtoken) |
|**Builder** |[setEncodeType](https://docs.byteplus.com/en/docs/25/7959#Builder-setencodetype) |
|**Builder** |[setResolution](https://docs.byteplus.com/en/docs/25/7959#Builder-setresolution) |
|**VidPlayAuthTokenSource** |[build](https://docs.byteplus.com/en/docs/25/7959#Builder-build) |


<span id="Function details"></span>
## Function details

<span id="Builder-builder"></span>
### Builder

```java
public com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.Builder()
```


Constructor.

<span id="Builder-setvid"></span>
### setVid

```java
public Builder com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.setVid(
    @NonNull String vid)
```


Sets the video ID.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid | **@NonNull String** |The video ID. |


**Returns**

The builder.

<span id="Builder-setplayauthtoken"></span>
### setPlayAuthToken

```java
public Builder com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.setPlayAuthToken(
    @NonNull String playAuthToken)
```


Sets the playback auth token.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|playAuthToken | **@NonNull String** |The playback auth token. |


**Returns**

The builder.

<span id="Builder-setencodetype"></span>
### setEncodeType

```java
public Builder com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.setEncodeType(
    @Nullable String encodeType)
```


Sets the video codec type.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|encodeType | **@Nullable String** |The codec type. Can be set as `h264`,`h265`, or `h266`. The default value is `h264`. |


**Returns**

The builder.

<span id="Builder-setresolution"></span>
### setResolution

```java
public Builder com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.setResolution(
    @Nullable Resolution resolution)
```


Sets the initial resolution when playback starts.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|resolution | **@Nullable Resolution** |The resolution. If not set, the initial resolution is 360p. |


**Returns**

Builder

<span id="Builder-build"></span>
### build

```java
public VidPlayAuthTokenSource com.ss.ttvideoengine.source.VidPlayAuthTokenSource.Builder.build()
```


Builds the `VidPlayAuthTokenSource` object.

**Returns**

The built `VidPlayAuthTokenSource` object.

<span id="PreloaderURLItem"></span>
# PreloaderURLItem

```java
public class com.ss.ttvideoengine.PreloaderURLItem
```


Information about the URL preloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[getVideoId](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-getvideoid) |
|**void** |[setTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-settag) |
|**String** |[getTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-gettag) |
|**void** |[setSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-setsubtag) |
|**String** |[getSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-getsubtag) |
|**long** |[getPreloadSize](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-getpreloadsize) |
|**PreloaderURLItem** |[PreloaderURLItem](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-preloaderurlitem) |
|**IPreLoaderItemCallBackListener** |[getCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-getcallbacklistener) |
|**void** |[setCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderURLItem-setcallbacklistener) |


<span id="Function details"></span>
## Function details

<span id="PreloaderURLItem-getvideoid"></span>
### getVideoId

```java
public String com.ss.ttvideoengine.PreloaderURLItem.getVideoId()
```


Gets the video ID.

**Returns**

The video ID.

<span id="PreloaderURLItem-settag"></span>
### setTag

```java
public void com.ss.ttvideoengine.PreloaderURLItem.setTag(
    String tag)
```


Sets the business tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tag |**String** |The business tag can be used to differentiate different types of audio and video within the same app (appid). You can divide them based on your scenarios or video duration, such as immersive feed, short videos, and long videos. |


<span id="PreloaderURLItem-gettag"></span>
### getTag

```java
public String com.ss.ttvideoengine.PreloaderURLItem.getTag()
```


Gets the business tag.

**Returns**

The business tag.

<span id="PreloaderURLItem-setsubtag"></span>
### setSubTag

```java
public void com.ss.ttvideoengine.PreloaderURLItem.setSubTag(
    String subTag)
```


Sets the business sub\-tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subTag |**String** |The business sub\-tag can be used to further differentiate different types of audio and video with the same business tag, such as whether the audio and video are encrypted. |


<span id="PreloaderURLItem-getsubtag"></span>
### getSubTag

```java
public String com.ss.ttvideoengine.PreloaderURLItem.getSubTag()
```


Gets the business sub\-tag.

**Returns**

The business sub\-tag.

<span id="PreloaderURLItem-getpreloadsize"></span>
### getPreloadSize

```java
public long com.ss.ttvideoengine.PreloaderURLItem.getPreloadSize()
```


Gets the size of the preloaded data.

**Returns**

The size of the preloaded data in bytes.

<span id="PreloaderURLItem-preloaderurlitem"></span>
### PreloaderURLItem

```java
public com.ss.ttvideoengine.PreloaderURLItem.PreloaderURLItem(
    @NonNull DirectUrlSource source,
    long preloadSize)
```


Constructs an instance of `PreloaderURLItem`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source | **@NonNull DirectUrlSource** |The URL playback source. See [DirectUrlSource](https://docs.byteplus.com/en/docs/25/7959#directurlsource) for details. |
|preloadSize |**long** |The size of the preloaded data in bytes. |


<span id="PreloaderURLItem-getcallbacklistener"></span>
### getCallBackListener

```java
public IPreLoaderItemCallBackListener com.ss.ttvideoengine.PreloaderURLItem.getCallBackListener()
```


Gets the callback listener for the preloading.

**Returns**

The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener).

<span id="PreloaderURLItem-setcallbacklistener"></span>
### setCallBackListener

```java
public void com.ss.ttvideoengine.PreloaderURLItem.setCallBackListener(
    @Nullable IPreLoaderItemCallBackListener listener)
```


Sets the callback listener for the preloading.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener | **@Nullable IPreLoaderItemCallBackListener** |The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener). |


<span id="PreloaderVidItem"></span>
# PreloaderVidItem

```java
public class com.ss.ttvideoengine.PreloaderVidItem
```


Information about the VID preloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**PreloaderVidItem** |[PreloaderVidItem](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-preloaderviditem) |
|**void** |[setTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-settag) |
|**String** |[getTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-gettag) |
|**void** |[setSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-setsubtag) |
|**String** |[getSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-getsubtag) |
|**void** |[setCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-setcallbacklistener) |
|**IPreLoaderItemCallBackListener** |[getCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderVidItem-getcallbacklistener) |


<span id="Function details"></span>
## Function details

<span id="PreloaderVidItem-preloaderviditem"></span>
### PreloaderVidItem

```java
public com.ss.ttvideoengine.PreloaderVidItem.PreloaderVidItem(
    VidPlayAuthTokenSource source,
    long preloadSize)
```


Constructs an instance of `PreloaderVidItem`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**VidPlayAuthTokenSource** |The VID playback source. See [VidPlayAuthTokenSource](https://docs.byteplus.com/en/docs/25/7959#vidplayauthtokensource) for details. |
|preloadSize |**long** |The size of the preloaded data in bytes. |


<span id="PreloaderVidItem-settag"></span>
### setTag

```java
public void com.ss.ttvideoengine.PreloaderVidItem.setTag(
    String tag)
```


Sets the business tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tag |**String** |The business tag can be used to differentiate different types of audio and video within the same app (appid). You can divide them based on your scenarios or video duration, such as immersive feed, short videos, and long videos. |


<span id="PreloaderVidItem-gettag"></span>
### getTag

```java
public String com.ss.ttvideoengine.PreloaderVidItem.getTag()
```


Gets the business tag.

**Returns**

The business tag.

<span id="PreloaderVidItem-setsubtag"></span>
### setSubTag

```java
public void com.ss.ttvideoengine.PreloaderVidItem.setSubTag(
    String subTag)
```


Sets the business sub\-tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subTag |**String** |The business sub\-tag can be used to further differentiate different types of audio and video with the same business tag, such as whether the audio and video are encrypted. |
|  | | |


<span id="getSubTag"></span>
### getSubTag

```java
public String com.ss.ttvideoengine.PreloaderVidItem.getSubTag()
```


Gets the business sub\-tag.

**Returns**

The business sub\-tag.

<span id="PreloaderVidItem-setcallbacklistener"></span>
### setCallBackListener

```java
public void com.ss.ttvideoengine.PreloaderVidItem.setCallBackListener(
    @Nullable IPreLoaderItemCallBackListener listener)
```


Sets the callback listener for the preloading.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener | **@Nullable IPreLoaderItemCallBackListener** |The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener). |


<span id="PreloaderVidItem-getcallbacklistener"></span>
### getCallBackListener

```java
public IPreLoaderItemCallBackListener com.ss.ttvideoengine.PreloaderVidItem.getCallBackListener()
```


Gets the callback listener for the preloading.

**Returns**

The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener).

<span id="PreloaderVideoModelItem"></span>
# PreloaderVideoModelItem

```java
public class com.ss.ttvideoengine.PreloaderVideoModelItem
```


Information about the video model preloading task.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**PreloaderVideoModelItem** |[PreloaderVideoModelItem](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-preloadervideomodelitem) |
|**void** |[setCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-setcallbacklistener) |
|**IPreLoaderItemCallBackListener** |[getCallBackListener](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-getcallbacklistener) |
|**void** |[setTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-settag) |
|**String** |[getTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-gettag) |
|**void** |[setSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-setsubtag) |
|**String** |[getSubTag](https://docs.byteplus.com/en/docs/25/7959#PreloaderVideoModelItem-getsubtag) |


<span id="Function details"></span>
## Function details

<span id="PreloaderVideoModelItem-preloadervideomodelitem"></span>
### PreloaderVideoModelItem

```java
public com.ss.ttvideoengine.PreloaderVideoModelItem.PreloaderVideoModelItem(
    VideoModelSource source,
    long preloadSize)
```


Constructs an instance of `PreloaderVideoModelItem`.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**VidPlayAuthTokenSource** |The video model playback source. See [VidPlayAuthTokenSource](https://docs.byteplus.com/en/docs/25/7959#vidplayauthtokensource) for details. |
|preloadSize |**long** |The size of the preloaded data in bytes. |


<span id="PreloaderVideoModelItem-setcallbacklistener"></span>
### setCallBackListener

```java
public void com.ss.ttvideoengine.PreloaderVideoModelItem.setCallBackListener(
    @Nullable IPreLoaderItemCallBackListener listener)
```


Sets the callback listener for the preloading.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|listener | **@Nullable IPreLoaderItemCallBackListener** |The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener). |


<span id="PreloaderVideoModelItem-getcallbacklistener"></span>
### getCallBackListener

```java
public IPreLoaderItemCallBackListener com.ss.ttvideoengine.PreloaderVideoModelItem.getCallBackListener()
```


Gets the callback listener for the preloading.

**Returns**

The callback listener object [IPreLoaderItemCallBackListener](https://docs.byteplus.com/byteplus-vod/docs/android-player-sdk-callbacks?version=v1.0#ipreloaderitemcallbacklistener).

<span id="PreloaderVideoModelItem-settag"></span>
### setTag

```java
public void com.ss.ttvideoengine.PreloaderVideoModelItem.setTag(
    String tag)
```


Sets the business tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|tag |**String** |The business tag can be used to differentiate different types of audio and video within the same app (appid). You can divide them based on your scenarios or video duration, such as immersive feed, short videos, and long videos. |


<span id="PreloaderVideoModelItem-gettag"></span>
### getTag

```java
public String com.ss.ttvideoengine.PreloaderVideoModelItem.getTag()
```


Gets the business tag.

**Returns**

The business tag.

<span id="PreloaderVideoModelItem-setsubtag"></span>
### setSubTag

```java
public void com.ss.ttvideoengine.PreloaderVideoModelItem.setSubTag(
    String subTag)
```


Sets the business sub\-tag.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|subTag |**String** |The business sub\-tag can be used to further differentiate different types of audio and video with the same business tag, such as whether the audio and video are encrypted. |


<span id="getSubTag"></span>
### getSubTag

```java
public String com.ss.ttvideoengine.PreloaderVideoModelItem.getSubTag()
```


Gets the business sub\-tag.

**Returns**

The business sub\-tag.

<span id="PreLoaderItemCallBackInfo"></span>
# PreLoaderItemCallBackInfo

```java
public class com.ss.ttvideoengine.PreLoaderItemCallBackInfo
```


Callback information about preloading.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**int** |[KEY_IS_PRELOAD_END_SUCCEED](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-key_is_preload_end_succeed) |
|**int** |[KEY_IS_PRELOAD_END_FAIL](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-key_is_preload_end_fail) |
|**int** |[KEY_IS_FETCH_END_VIDEOMODEL](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-key_is_fetch_end_videomodel) |
|**int** |[KEY_IS_PRELOAD_END_CANCEL](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-key_is_preload_end_cancel) |
|**DataLoaderHelper.DataLoaderTaskProgressInfo** |[preloadDataInfo](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-preloaddatainfo) |
|**VideoModel** |[fetchVideoModel](https://docs.byteplus.com/en/docs/25/7959#PreLoaderItemCallBackInfo-fetchvideomodel) |


<span id="Variable details"></span>
## Variable details

<span id="PreLoaderItemCallBackInfo-key_is_preload_end_succeed"></span>
### KEY_IS_PRELOAD_END_SUCCEED

```java
public final static int com.ss.ttvideoengine.PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_SUCCEED = 2;
```


Preloading succeeded.

<span id="PreLoaderItemCallBackInfo-key_is_preload_end_fail"></span>
### KEY_IS_PRELOAD_END_FAIL

```java
public final static int com.ss.ttvideoengine.PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_FAIL = 3;
```


Preloading failed.

<span id="PreLoaderItemCallBackInfo-key_is_fetch_end_videomodel"></span>
### KEY_IS_FETCH_END_VIDEOMODEL

```java
public final static int com.ss.ttvideoengine.PreLoaderItemCallBackInfo.KEY_IS_FETCH_END_VIDEOMODEL = 4;
```


Valid `VideoModel` has been fetched.

<span id="PreLoaderItemCallBackInfo-key_is_preload_end_cancel"></span>
### KEY_IS_PRELOAD_END_CANCEL

```java
public final static int com.ss.ttvideoengine.PreLoaderItemCallBackInfo.KEY_IS_PRELOAD_END_CANCEL = 5;
```


Preloading has been cancelled.

<span id="PreLoaderItemCallBackInfo-preloaddatainfo"></span>
### preloadDataInfo

```java
public DataLoaderHelper.DataLoaderTaskProgressInfo com.ss.ttvideoengine.PreLoaderItemCallBackInfo.preloadDataInfo = null;
```


Preloading succeeded. The SDK returns an instance of `DataLoaderTaskProgressInfo` that provides preloading information.

<span id="PreLoaderItemCallBackInfo-fetchvideomodel"></span>
### fetchVideoModel

```java
public VideoModel com.ss.ttvideoengine.PreLoaderItemCallBackInfo.fetchVideoModel = null;
```


Valid `VideoModel` has been fetched.

<span id="VideoEngineInfos"></span>
# VideoEngineInfos

```java
public class com.ss.ttvideoengine.VideoEngineInfos
```


Information about the video engine.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**String** |[USING_MDL_HIT_CACHE_SIZE](https://docs.byteplus.com/en/docs/25/7959#VideoEngineInfos-using_mdl_hit_cache_size) |
|**String** |[USING_RENDER_SEEK_COMPLETE](https://docs.byteplus.com/en/docs/25/7959#VideoEngineInfos-using_render_seek_complete) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**String** |[getKey](https://docs.byteplus.com/en/docs/25/7959#VideoEngineInfos-getkey) |


<span id="Variable details"></span>
## Variable details

<span id="VideoEngineInfos-using_mdl_hit_cache_size"></span>
### USING_MDL_HIT_CACHE_SIZE

```java
public static final String com.ss.ttvideoengine.VideoEngineInfos.USING_MDL_HIT_CACHE_SIZE = "mdlhitcachesize";
```


This callback indicates the preloading task successfully hits the cached video. The value being greater than `0` indicates the size of the cached video that has been hit.

<span id="VideoEngineInfos-using_render_seek_complete"></span>
### USING_RENDER_SEEK_COMPLETE

```java
public static final String com.ss.ttvideoengine.VideoEngineInfos.USING_RENDER_SEEK_COMPLETE = "renderSeekComplete";
```


This callback indicates rendering has been completed after the seek operation.

<span id="Function details"></span>
## Function details

<span id="VideoEngineInfos-getkey"></span>
### getKey

```java
public String com.ss.ttvideoengine.VideoEngineInfos.getKey()
```


Gets the key of the callback.

**Returns**

The key of the callback.

<span id="PlaybackParams"></span>
# PlaybackParams

```java
public final class com.ss.ttm.player.PlaybackParams
```


Playback parameters.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**float** |[getSpeed](https://docs.byteplus.com/en/docs/25/7959#PlaybackParams-getspeed) |
|**PlaybackParams** |[setSpeed](https://docs.byteplus.com/en/docs/25/7959#PlaybackParams-setspeed) |


<span id="Function details"></span>
## Function details

<span id="PlaybackParams-getspeed"></span>
### getSpeed

```java
public float com.ss.ttm.player.PlaybackParams.getSpeed()
```


Gets the playback speed.

**Returns**

The playback speed.

<span id="PlaybackParams-setspeed"></span>
### setSpeed

```java
public PlaybackParams com.ss.ttm.player.PlaybackParams.setSpeed(
    float speed)
```


Sets the playback speed.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|speed |**float** |The playback speed. The default value is 1, and the valid range is (0,3]. |


**Returns**

The playback parameters.

<span id="StrategySource"></span>
# StrategySource

```java
public interface com.ss.ttvideoengine.strategy.source.StrategySource
```


The playback source.

<span id="SubDesInfoModelProvider"></span>
# SubDesInfoModelProvider

```java
public interface com.ss.ttvideoengine.SubDesInfoModelProvider
```


Subtitle sources in multiple languages.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**int** |[subtitleCount](https://docs.byteplus.com/en/docs/25/7959#SubDesInfoModelProvider-subtitlecount) |
|**String** |[toString](https://docs.byteplus.com/en/docs/25/7959#SubDesInfoModelProvider-tostring) |
|**void** |[addSubModel](https://docs.byteplus.com/en/docs/25/7959#SubDesInfoModelProvider-addsubmodel) |


<span id="Function details"></span>
## Function details

<span id="SubDesInfoModelProvider-subtitlecount"></span>
### subtitleCount

```java
public int com.ss.ttvideoengine.SubDesInfoModelProvider.subtitleCount()
```


Gets the number of subtitle languages.

**Returns**

The number of subtitle languages.

<span id="SubDesInfoModelProvider-tostring"></span>
### toString

```java
public String com.ss.ttvideoengine.SubDesInfoModelProvider.toString()
```


Gets the string of all subtitle sources.

**Returns**

The string of all subtitle sources.

<span id="SubDesInfoModelProvider-addsubmodel"></span>
### addSubModel

```java
public void com.ss.ttvideoengine.SubDesInfoModelProvider.addSubModel(
    SubModelProvider model)
```


Adds a single language subtitle source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|model |**SubModelProvider** |The subtitle source to add. |


<span id="SubModelProvider"></span>
# SubModelProvider

```java
public interface com.ss.ttvideoengine.SubModelProvider
```


The subtitle source in a single language.

<span id="VideoFormatInfo"></span>
# VideoFormatInfo

```java
public class com.ss.ttvideoengine.VideoFormatInfo
```


Basic information about the video file.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**String** |[fileFormat](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-fileformat) |
|**long** |[bitrate](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-bitrate) |
|**int** |[width](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-width) |
|**int** |[height](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-height) |
|**int** |[rotation](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-rotation) |
|**float** |[containerFps](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-containerfps) |
|**int** |[channels](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-channels) |
|**int** |[sampleRate](https://docs.byteplus.com/en/docs/25/7959#VideoFormatInfo-samplerate) |


<span id="Variable details"></span>
## Variable details

<span id="VideoFormatInfo-fileformat"></span>
### fileFormat

```java
public String com.ss.ttvideoengine.VideoFormatInfo.fileFormat;
```


The file format.

<span id="VideoFormatInfo-bitrate"></span>
### bitrate

```java
public long com.ss.ttvideoengine.VideoFormatInfo.bitrate;
```


The bitrate.

<span id="VideoFormatInfo-width"></span>
### width

```java
public int com.ss.ttvideoengine.VideoFormatInfo.width;
```


The width of the video.

<span id="VideoFormatInfo-height"></span>
### height

```java
public int com.ss.ttvideoengine.VideoFormatInfo.height;
```


The height of the video.

<span id="VideoFormatInfo-rotation"></span>
### rotation

```java
public int com.ss.ttvideoengine.VideoFormatInfo.rotation;
```


The rotation degree of the video.

<span id="VideoFormatInfo-containerfps"></span>
### containerFps

```java
public float com.ss.ttvideoengine.VideoFormatInfo.containerFps;
```


The frame rate.

<span id="VideoFormatInfo-channels"></span>
### channels

```java
public int com.ss.ttvideoengine.VideoFormatInfo.channels;
```


The audio channels.

<span id="VideoFormatInfo-samplerate"></span>
### sampleRate

```java
public int com.ss.ttvideoengine.VideoFormatInfo.sampleRate;
```


The audio sample rate.
