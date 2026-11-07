---
title: "iOS Player SDK: Type definitions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-type-definitions"
---

<span id="TTVideoEngineSubDecInfoProtocol"></span>
# TTVideoEngineSubDecInfoProtocol

```objectivec
@protocol TTVideoEngineSubDecInfoProtocol <NSObject>
```


Subtitle sources in multiple languages.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**NSString** |[jsonString](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoProtocol-jsonstring) |
|**NSInteger** |[subtitleCount](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoProtocol-subtitlecount) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineSubDecInfoProtocol-jsonstring"></span>
### jsonString

```objectivec
- (NSString *_Nullable)jsonString;
```


Returns the subtitle sources in JSON format.

**Returns**

The subtitle sources in JSON format.

<span id="TTVideoEngineSubDecInfoProtocol-subtitlecount"></span>
### subtitleCount

```objectivec
- (NSInteger)subtitleCount;
```


Gets the number of subtitle languages.

**Returns**

The number of subtitle languages.

<span id="TTVideoEngineSubProtocol"></span>
# TTVideoEngineSubProtocol

```objectivec
@protocol TTVideoEngineSubProtocol <NSObject>
```


The subtitle source in a single language.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSInteger** |[languageId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-languageid) |
|**NSString** |[urlString](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-urlstring) |
|**NSString** |[format](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-format) |
|**NSInteger** |[subtitleId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-subtitleid) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**NSDictionary** |[toDictionary](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-todictionary) |
|**NSString** |[jsonString](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubProtocol-jsonstring) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineSubProtocol-languageid"></span>
### languageId

```objectivec
@property (nonatomic, assign, readonly) NSInteger languageId;
```


The language ID of the subtitle.

<span id="TTVideoEngineSubProtocol-urlstring"></span>
### urlString

```objectivec
@property (nonatomic, copy, readonly) NSString *urlString;
```


The URL of the subtitle.

<span id="TTVideoEngineSubProtocol-format"></span>
### format

```objectivec
@property (nonatomic, copy, readonly) NSString *format;
```


The format of the subtitle.

<span id="TTVideoEngineSubProtocol-subtitleid"></span>
### subtitleId

```objectivec
@property (nonatomic, assign, readonly) NSInteger subtitleId;
```


The ID of the subtitle.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineSubProtocol-todictionary"></span>
### toDictionary

```objectivec
- (NSDictionary *_Nullable)toDictionary;
```


Converts the subtitle source model to a dictionary.

<span id="TTVideoEngineSubProtocol-jsonstring"></span>
### jsonString

```objectivec
- (NSString *_Nullable)jsonString;
```


Converts the subtitle source model to a JSON string.

<span id="TTVideoEngineSubDecInfoModel"></span>
# TTVideoEngineSubDecInfoModel

```objectivec
@interface TTVideoEngineSubDecInfoModel : NSObject <TTVideoEngineSubDecInfoProtocol>
```


Subtitle sources in multiple languages, conforming to the [TTVideoEngineSubDecInfoProtocol](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubdecinfoprotocol) protocol.

<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[initWithDictionary:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoModel-initwithdictionary) |
|**instancetype** |[initWithSubModels:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoModel-initwithsubmodels) |
|**void** |[addSubModel:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoModel-addsubmodel) |
|**NSString** |[jsonString](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoModel-jsonstring) |
|**NSInteger** |[subtitleCount](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubDecInfoModel-subtitlecount) |


<span id="Function details"></span>
## Function details

<span id="TTVideoEngineSubDecInfoModel-initwithdictionary"></span>
### initWithDictionary:

```objectivec
- (instancetype)initWithDictionary:(NSDictionary *_Nonnull)dict;
```


Initializes the subtitle sources in multiple languages.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|dict |**NSDictionary** |The subtitle sources in dictionary format. |


**Returns**

An instance of the subtitle source model.

<span id="TTVideoEngineSubDecInfoModel-initwithsubmodels"></span>
### initWithSubModels:

```objectivec
- (instancetype)initWithSubModels:(NSArray<id<TTVideoEngineSubProtocol>> *_Nonnull)models;
```


Initializes the subtitle sources in multiple languages.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|models |**NSArray** |An array of subtitle source models: [TTVideoEngineSubModel](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubmodel). |


**Returns**

An instance of the [TTVideoEngineSubDecInfoModel](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubdecinfomodel) class.

<span id="TTVideoEngineSubDecInfoModel-addsubmodel"></span>
### addSubModel:

```objectivec
- (void)addSubModel:(id<TTVideoEngineSubProtocol> _Nonnull)model;
```


Adds a single language subtitle source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|model |**id** |The subtitle source model for a single language: [TTVideoEngineSubDecInfoModel](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubdecinfomodel). |


<span id="TTVideoEngineSubDecInfoModel-jsonstring"></span>
### jsonString

```objectivec
- (NSString *_Nullable)jsonString;
```


Gets the subtitle source in JSON format.

**Returns**

The subtitle source in JSON format.

<span id="TTVideoEngineSubDecInfoModel-subtitlecount"></span>
### subtitleCount

```objectivec
- (NSInteger)subtitleCount;
```


Gets the number of subtitle sources.

**Returns**

The number of subtitle sources.

<span id="TTVideoEngineSubModel"></span>
# TTVideoEngineSubModel

```objectivec
@interface TTVideoEngineSubModel : NSObject <TTVideoEngineSubProtocol>
```


The subtitle source in a single language, conforming to the [TTVideoEngineSubProtocol](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubprotocol) protocol.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSInteger** |[index](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-index) |
|**NSString** |[language](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-language) |
|**NSInteger** |[expireTime](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-expiretime) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[initWithDictionary:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-initwithdictionary) |
|**NSDictionary** |[toDictionary](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-todictionary) |
|**NSString** |[jsonString](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubModel-jsonstring) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineSubModel-index"></span>
### index

```objectivec
@property (nonatomic, assign, readonly) NSInteger index;
```


The current subtitle index.

<span id="TTVideoEngineSubModel-language"></span>
### language

```objectivec
@property (nonatomic, copy, readonly) NSString *language;
```


The language of the subtitle.

<span id="TTVideoEngineSubModel-expiretime"></span>
### expireTime

```objectivec
@property (nonatomic, assign, readonly) NSInteger expireTime;
```


The expiration time of the subtitle.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineSubModel-initwithdictionary"></span>
### initWithDictionary:

```objectivec
- (instancetype)initWithDictionary:(NSDictionary * _Nonnull)dict;
```


Initializes the subtitle source in a single language.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|dict |**NSDictionary** |The subtitle data source. |


**Returns**

The subtitle source in a single language: [TTVideoEngineSubModel](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginesubmodel).

<span id="TTVideoEngineSubModel-todictionary"></span>
### toDictionary

```objectivec
- (NSDictionary *_Nullable)toDictionary;
```


Converts the subtitle source model to a dictionary.

<span id="TTVideoEngineSubModel-jsonstring"></span>
### jsonString

```objectivec
- (NSString *_Nullable)jsonString;
```


Converts the subtitle source model to a JSON string.

<span id="TTVideoEngineSubInfo"></span>
# TTVideoEngineSubInfo

```objectivec
@interface TTVideoEngineSubInfo: NSObject
```


单段字幕信息。Information about a single piece of subtitle.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSInteger** |[pts](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubInfo-pts) |
|**NSString** |[content](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubInfo-content) |
|**NSInteger** |[duration](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineSubInfo-duration) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineSubInfo-pts"></span>
### pts

```objectivec
@property (nonatomic, assign) NSInteger pts;
```


The timestamp corresponding to the subtitle segment, in milliseconds.

<span id="TTVideoEngineSubInfo-content"></span>
### content

```objectivec
@property (nonatomic, copy) NSString *content;
```


The content of the subtitle segment.

<span id="TTVideoEngineSubInfo-duration"></span>
### duration

```objectivec
@property (nonatomic, assign) NSInteger duration;
```


The duration of the subtitle segment, in milliseconds.

<span id="TTVideoEngineLoadInfo"></span>
# TTVideoEngineLoadInfo

```objectivec
@interface TTVideoEngineLoadInfo: NSObject
```


Subtitle loading information.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSInteger** |[firstPts](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLoadInfo-firstpts) |
|**NSInteger** |[code](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLoadInfo-code) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineLoadInfo-firstpts"></span>
### firstPts

```objectivec
@property (nonatomic, assign) NSInteger firstPts;
```


The timestamp of the first subtitle segment to be displayed.

<span id="TTVideoEngineLoadInfo-code"></span>
### code

```objectivec
@property (nonatomic, assign) NSInteger code;
```


The status of subtitle loading. `code` being `0` indicates successful loading.

<span id="TTVideoEngineLocalServerConfigure"></span>
# TTVideoEngineLocalServerConfigure

```objectivec
@interface TTVideoEngineLocalServerConfigure : NSObject
```


Configuration for the Media Data Loader. The Media Data Loader (MDL) is one of the key modules within the SDK, providing the player with fast, low\-cost, and reliable data loading functionality. Features such as preloading, file caching, streaming while downloading, network quality monitoring, and cost data monitoring in the SDK all rely on MDL. MDL is enabled by default when the SDK is initialized.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSInteger** |[maxCacheSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerConfigure-maxcachesize) |
|**NSInteger** |[preloadParallelNum](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerConfigure-preloadparallelnum) |
|**NSString** |[downloadDirectory](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerConfigure-downloaddirectory) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineLocalServerConfigure-maxcachesize"></span>
### maxCacheSize

```objectivec
@property(nonatomic, assign) NSInteger maxCacheSize;
```


Sets the maximum amount of data that can be cached locally, in bytes.

<span id="TTVideoEngineLocalServerConfigure-preloadparallelnum"></span>
### preloadParallelNum

```objectivec
@property(nonatomic, assign) NSInteger preloadParallelNum;
```


Sets the number of concurrent preload tasks. The default value is 2.

<span id="TTVideoEngineLocalServerConfigure-downloaddirectory"></span>
### downloadDirectory

```objectivec
@property(nonatomic, nullable, copy) NSString *downloadDirectory;
```


Sets the storage path for downloaded files. This path must be set if you are using the download function.

<span id="TTVideoEngineStrategyType"></span>
# TTVideoEngineStrategyType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineStrategyType)
```


The playback strategy types. The SDK supports multiple strategies, which can be used individually or in combination.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineStrategyTypeNone |1 << 0 |(Default) No strategy is enabled. |
|TTVideoEngineStrategyTypeCommon |1 << 1 |Common strategy, enabled by default in the SDK. |
|TTVideoEngineStrategyTypePreload |1 << 2 |Preload strategy. |
|TTVideoEngineStrategyTypePreRender |1 << 3 |Pre\-render strategy. |


<span id="TTVideoEnginePreloaderURLItem"></span>
# TTVideoEnginePreloaderURLItem

```objectivec
@interface TTVideoEnginePreloaderURLItem : NSObject
```


Information about preloading URL playback sources.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[key](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-key) |
|**NSArray** |[urls](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-urls) |
|**NSString** |[videoId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-videoid) |
|**NSString** |[cacheFilePath](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-cachefilepath) |
|**NSInteger** |[preloadSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-preloadsize) |
|**NSInteger** |[priorityLevel](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-prioritylevel) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**nullable instancetype** |[urlItemWithKey:videoId:urls:preloadSize:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-urlitemwithkey-videoid-urls-preloadsize) |
|**nullable instancetype** |[urlItemWithVideoSource:preloadSize:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderURLItem-urlitemwithvideosource-preloadsize) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEnginePreloaderURLItem-key"></span>
### key

```objectivec
@property (nonatomic, copy, nullable) NSString *key;
```


(Required) Sets the unique identifier for the preloading task. It is recommended to use the MD5 value of the URL as the key. If the MD5 value of the URL is used as the key, note that some URLs may contain variable parts such as timestamps or signatures. These variable parts need to be removed before use to ensure that the MD5 value used is for the unchanged URL.

<span id="TTVideoEnginePreloaderURLItem-urls"></span>
### urls

```objectivec
@property (nonatomic, copy, nullable) NSArray<NSString *> *urls;
```


(Required) Sets the URLs of the video source to be preloaded. Supports primary and backup URLs.

<span id="TTVideoEnginePreloaderURLItem-videoid"></span>
### videoId

```objectivec
@property (nonatomic, copy, nullable) NSString *videoId;
```


(Required) The unique identifier of the video, which must correspond to the video source. It can be the unique identifier of the video in your own video management system, or it can be the same as the value of `key`.

<span id="TTVideoEnginePreloaderURLItem-cachefilepath"></span>
### cacheFilePath

```objectivec
@property (nonatomic, copy, nullable) NSString *cacheFilePath;
```


Specifies the cache path. The SDK has a default cache path, and it is not recommended to set it separately.

<span id="TTVideoEnginePreloaderURLItem-preloadsize"></span>
### preloadSize

```objectivec
@property (nonatomic, assign) NSInteger preloadSize;
```


Sets the size of the data to be preloaded, for example, 800 \* 1024 represents 800 KB of preloaded data.

<span id="TTVideoEnginePreloaderURLItem-prioritylevel"></span>
### priorityLevel

```objectivec
@property (nonatomic, assign) NSInteger priorityLevel;
```


Sets the priority level of preloading. The default value is `TTVideoEnginePreloadPriorityDefault`.

<span id="Function details"></span>
## Function details

<span id="TTVideoEnginePreloaderURLItem-urlitemwithkey-videoid-urls-preloadsize"></span>
### urlItemWithKey:videoId:urls:preloadSize:

```objectivec
- (nullable instancetype)urlItemWithKey:(NSString *)key videoId:(nullable NSString *)videoId urls:(NSArray<NSString *> *)urls preloadSize:(NSInteger)preloadSize;
```


Constructs an instance of the URL preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|key |**NSString** |The unique identifier for the preloading task. It is recommended to use the MD5 value of the URL as the key. If the MD5 value of the URL is used as the key, it is important to note that some URLs may contain variable parts such as timestamps or signatures. These variable parts should be removed before use to ensure that the MD5 value of the unchanging URL is used. |
|videoId |**nullable NSString** |The unique identifier for the video, which must correspond to the video source. It can be the unique identifier of the video in your own video management system or the same value as `key`. |
|urls |*NSArray*\* |URLs for preloading. Supports primary and backup URLs. |
|preloadSize |**NSInteger** |The size of preloaded data in bytes. For example, 800 \* 1024 represents preloading 800 KB of data. |


**Returns**

An instance of URL preloading item.

<span id="TTVideoEnginePreloaderURLItem-urlitemwithvideosource-preloadsize"></span>
### urlItemWithVideoSource:preloadSize:

```objectivec
- (nullable instancetype)urlItemWithVideoSource:(id<TTVideoEngineMediaSource>)source preloadSize:(NSInteger)preloadSize;
```


Constructs an instance of the URL preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The URL playback source information: [TTVideoEngineMediaSource](https://docs.byteplus.com/en/docs/25/7970#ttvideoenginemediasource). |
|preloadSize |**NSInteger** |The size of preloaded data in bytes. For example, 800 \* 1024 represents preloading 800 KB of data. |


**Returns**

An instance of URL preloading item.

<span id="TTVideoEnginePreloaderVideoModelItem"></span>
# TTVideoEnginePreloaderVideoModelItem

```objectivec
@interface TTVideoEnginePreloaderVideoModelItem : NSObject
```


Information about preloading video model playback sources.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**TTVideoEngineResolutionType** |[resolution](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-resolution) |
|**TTVideoEngineModel** |[videoModel](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-videomodel) |
|**NSInteger** |[preloadSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-preloadsize) |
|**NSInteger** |[priorityLevel](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-prioritylevel) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[videoModelItem:resolution:preloadSize:params:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-videomodelitem-resolution-preloadsize-params) |
|**nullable instancetype** |[videoModelItemWithVideoSource:preloadSize:params:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVideoModelItem-videomodelitemwithvideosource-preloadsize-params) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEnginePreloaderVideoModelItem-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign) TTVideoEngineResolutionType resolution;
```


Sets the resolution of the video source. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype) for details.

<span id="TTVideoEnginePreloaderVideoModelItem-videomodel"></span>
### videoModel

```objectivec
@property (nonatomic, strong, nullable) TTVideoEngineModel *videoModel;
```


Sets the video source information.

<span id="TTVideoEnginePreloaderVideoModelItem-preloadsize"></span>
### preloadSize

```objectivec
@property (nonatomic, assign) NSInteger preloadSize;
```


Sets the size of preloaded data in bytes. For example, 800 \* 1024 represents preloading 800 KB of data.

<span id="TTVideoEnginePreloaderVideoModelItem-prioritylevel"></span>
### priorityLevel

```objectivec
@property (nonatomic, assign) NSInteger priorityLevel;
```


The priority level of preloading. The default value is `TTVideoEnginePreloadPriorityDefault`.

<span id="Function details"></span>
## Function details

<span id="TTVideoEnginePreloaderVideoModelItem-videomodelitem-resolution-preloadsize-params"></span>
### videoModelItem:resolution:preloadSize:params:

```objectivec
- (instancetype)videoModelItem:(TTVideoEngineModel *)data resolution:(TTVideoEngineResolutionType)resolution preloadSize:(NSInteger)preloadSize params:(nullable NSDictionary *)params;
```


Constructs an instance of the video model preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|data |**TTVideoEngineModel** |The video model playback source. |
|resolution |**TTVideoEngineResolutionType** |The video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype) for details. |
|preloadSize |**NSInteger** |The size of preloaded data. For example, 800 \* 1024 represents preloading 800 KB of data. |
|params |**nullable NSDictionary** |Reserved parameter. No need to set. |


**Returns**

An instance of the video model preloading task.

<span id="TTVideoEnginePreloaderVideoModelItem-videomodelitemwithvideosource-preloadsize-params"></span>
### videoModelItemWithVideoSource:preloadSize:params:

```objectivec
- (nullable instancetype)videoModelItemWithVideoSource:(id<TTVideoEngineMediaSource>)source preloadSize:(NSInteger)preloadSize params:(nullable NSDictionary *)params;
```


Constructs an instance of the video model preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The video model playback source. |
|preloadSize |**NSInteger** |The size of preloaded data. For example, 800 \* 1024 represents preloading 800 KB of data. |
|params |**nullable NSDictionary** |Reserved parameter. No need to set. |


**Returns**

An instance of the video model preloading task.

<span id="TTVideoEnginePreloaderVidItem"></span>
# TTVideoEnginePreloaderVidItem

```objectivec
@interface TTVideoEnginePreloaderVidItem : NSObject
```


Information about preloading a VID playback source.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[videoId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-videoid) |
|**NSString** |[playAuthToken](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-playauthtoken) |
|**TTVideoEngineResolutionType** |[resolution](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-resolution) |
|**NSInteger** |[preloadSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-preloadsize) |
|**TTVideoEngineEncodeType** |[codecType](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-codectype) |
|**BOOL** |[encryptionEnable](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-encryptionenable) |
|**BOOL** |[hlsEnable](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-hlsenable) |
|**NSInteger** |[priorityLevel](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-prioritylevel) |


<span id="Static functions"></span>
## Static functions


|**Return** |**Name** |
|---|---|
|**nullable instancetype** |[vidItemWithVideoSource:preloadSize:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEnginePreloaderVidItem-viditemwithvideosource-preloadsize) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEnginePreloaderVidItem-videoid"></span>
### videoId

```objectivec
@property (nonatomic, nullable, copy) NSString *videoId;
```


(Required) Sets the video ID.

<span id="TTVideoEnginePreloaderVidItem-playauthtoken"></span>
### playAuthToken

```objectivec
@property (nonatomic,   copy) NSString *playAuthToken;
```


(Required) Sets the video playback auth token.

<span id="TTVideoEnginePreloaderVidItem-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign) TTVideoEngineResolutionType resolution;
```


(Required) Sets the resolution of the preloaded video. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype) for more details. The resolution of the preloaded video should match the resolution of the playback for successful preloading.

<span id="TTVideoEnginePreloaderVidItem-preloadsize"></span>
### preloadSize

```objectivec
@property (nonatomic, assign) NSInteger preloadSize;
```


Sets the size of the data to be preloaded. For example, 800 \* 1024 represents preloading 800 KB of data.

<span id="TTVideoEnginePreloaderVidItem-codectype"></span>
### codecType

```objectivec
@property (nonatomic, assign) TTVideoEngineEncodeType codecType;
```


Sets the codec of the playback source to be preloaded. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype) for more details. The default value is `TTVideoEngineH264`.

<span id="TTVideoEnginePreloaderVidItem-encryptionenable"></span>
### encryptionEnable

```objectivec
@property (nonatomic, assign) BOOL encryptionEnable;
```


Whether the playback source to be preloaded is encrypted.

<span id="TTVideoEnginePreloaderVidItem-hlsenable"></span>
### hlsEnable

```objectivec
@property (nonatomic, assign) BOOL hlsEnable;
```


Whether the playback source to be preloaded is HLS.

<span id="TTVideoEnginePreloaderVidItem-prioritylevel"></span>
### priorityLevel

```objectivec
@property (nonatomic, assign) NSInteger priorityLevel;
```


The priority level of preloading. The default value is `TTVideoEnginePreloadPriorityDefault`.

<span id="Function details"></span>
## Function details

<span id="TTVideoEnginePreloaderVidItem-viditemwithvideosource-preloadsize"></span>
### vidItemWithVideoSource:preloadSize:

```objectivec
- (nullable instancetype)vidItemWithVideoSource:(id<TTVideoEngineMediaSource>)source preloadSize:(NSInteger)preloadSize;
```


Builds an instance of the VID the VID preloading task.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|source |**id** |The playback source. |
|preloadSize |**NSInteger** |The size of the data to be preloaded in bytes. For example, 800 \* 1024 represents preloading 800k data. |


**Returns**

An instance of the VID preloading task.

<span id="TTVideoEngineLocalServerTaskInfo"></span>
# TTVideoEngineLocalServerTaskInfo

```objectivec
@interface TTVideoEngineLocalServerTaskInfo : NSObject
```


Information for the cache task in MDL.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[key](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-key) |
|**NSString** |[videoId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-videoid) |
|**TTVideoEngineResolutionType** |[resolution](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-resolution) |
|**NSString** |[localFilePath](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-localfilepath) |
|**int64_t** |[mediaSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-mediasize) |
|**int64_t** |[preloadSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-preloadsize) |
|**TTVideoEngineURLInfo** |[urlInfo](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerTaskInfo-urlinfo) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineLocalServerTaskInfo-key"></span>
### key

```objectivec
@property (nonatomic,   copy) NSString *key;
```


The unique identifier for the video source.

<span id="TTVideoEngineLocalServerTaskInfo-videoid"></span>
### videoId

```objectivec
@property (nonatomic, nullable, copy) NSString *videoId;
```


The video ID.

<span id="TTVideoEngineLocalServerTaskInfo-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign) TTVideoEngineResolutionType resolution;
```


Resolution of the video source. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype) for more details.

<span id="TTVideoEngineLocalServerTaskInfo-localfilepath"></span>
### localFilePath

```objectivec
@property (nonatomic, nullable, copy) NSString *localFilePath;
```


The local cache path.

<span id="TTVideoEngineLocalServerTaskInfo-mediasize"></span>
### mediaSize

```objectivec
@property (nonatomic, assign) int64_t mediaSize;
```


The size of the video source in bytes

<span id="TTVideoEngineLocalServerTaskInfo-preloadsize"></span>
### preloadSize

```objectivec
@property (nonatomic, assign) int64_t preloadSize;
```


The size of the data to be preloaded in bytes.

<span id="TTVideoEngineLocalServerTaskInfo-urlinfo"></span>
### urlInfo

```objectivec
@property (nonatomic, nullable, strong) TTVideoEngineURLInfo *urlInfo;
```


The URL information of the video source, only available when preloading VID playback source.

<span id="TTVideoEngineLocalServerCacheInfo"></span>
# TTVideoEngineLocalServerCacheInfo

```objectivec
@interface TTVideoEngineLocalServerCacheInfo : NSObject
```


The local cache configuration in MDL.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**int64_t** |[mediaSize](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerCacheInfo-mediasize) |
|**NSString** |[localFilePath](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineLocalServerCacheInfo-localfilepath) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineLocalServerCacheInfo-mediasize"></span>
### mediaSize

```objectivec
@property(nonatomic, assign) int64_t mediaSize;
```


The size of the video source in bytes.

<span id="TTVideoEngineLocalServerCacheInfo-localfilepath"></span>
### localFilePath

```objectivec
@property(nonatomic,   copy) NSString *localFilePath;
```


The local cache path.

<span id="TTVideoEngineUrlSource"></span>
# TTVideoEngineUrlSource

```objectivec
@interface TTVideoEngineUrlSource : NSObject <TTVideoEngineMediaSource>
```


The URL playback source.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSArray** |[urls](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-urls) |
|**NSString** |[cacheKey](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-cachekey) |
|**TTVideoEngineEncodeType** |[encodeType](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-encodetype) |
|**NSString** |[vid](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-vid) |
|**BOOL** |[isHDRSource](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-ishdrsource) |
|**NSString** |[decryptionKey](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-decryptionkey) |
|**NSString** |[filePath](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-filepath) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[initWithUrl:cacheKey:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-initwithurl-cachekey) |
|**instancetype** |[initWithUrls:cacheKey:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-initwithurls-cachekey) |
|**instancetype** |[initWithUrls:cacheKey:videoId:encodeType:decryptionKey:filePath:isHDRSource:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-initwithurls-cachekey-videoid-encodetype-decryptionkey-filepath-ishdrsource) |
|**void** |[addUrls:cacheKey:encodeType:decryptionKey:filePath:isHDRSource:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineUrlSource-addurls-cachekey-encodetype-decryptionkey-filepath-ishdrsource) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineUrlSource-urls"></span>
### urls

```objectivec
@property (nonatomic, strong) NSArray *urls;
```


The list of video URLs. Supports primary and backup URLs.

<span id="TTVideoEngineUrlSource-cachekey"></span>
### cacheKey

```objectivec
@property (nonatomic, copy) NSString *cacheKey;
```


The cache key. This is the unique identifier for the URL and must follow the following rules:


* Should not contain special characters and can be used as a file name.

* Should correspond to the video resource file.

* It is recommended to use the MD5 value of the URL.


<span id="TTVideoEngineUrlSource-encodetype"></span>
### encodeType

```objectivec
@property (nonatomic, assign) TTVideoEngineEncodeType encodeType;
```


The video codec. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype).

<span id="TTVideoEngineUrlSource-vid"></span>
### vid

```objectivec
@property (nonatomic, copy, nullable) NSString *vid;
```


The video ID.

<span id="TTVideoEngineUrlSource-ishdrsource"></span>
### isHDRSource

```objectivec
@property (nonatomic, assign) BOOL isHDRSource;
```


Whether the video is HDR.

<span id="TTVideoEngineUrlSource-decryptionkey"></span>
### decryptionKey

```objectivec
@property (nonatomic, strong, nullable) NSString *decryptionKey;
```


Custom decryption key for playing encrypted videos.

<span id="TTVideoEngineUrlSource-filepath"></span>
### filePath

```objectivec
@property (nonatomic, copy, nullable) NSString *filePath;
```


The file path.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineUrlSource-initwithurl-cachekey"></span>
### initWithUrl:cacheKey:

```objectivec
- (instancetype)initWithUrl:(NSString *)url cacheKey:(NSString *)cacheKey;
```


Initializes the URL playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|url |**NSString** |The video URL. |
|cacheKey |**NSString** |The cache key. This is the unique identifier for the URL and must follow the following rules:<br><br><br>* Should not contain special characters and can be used as a file name.<br><br>* Should correspond to the video resource file.<br><br>* It is recommended to use the MD5 value of the URL. |


**Returns**

An instance of the URL playback source.

<span id="TTVideoEngineUrlSource-initwithurls-cachekey"></span>
### initWithUrls:cacheKey:

```objectivec
- (instancetype)initWithUrls:(NSArray *)urls cacheKey:(NSString *)cacheKey;
```


Initializes the URL playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls |**NSArray** |The list of video URLs. Supports primary and backup URLs. |
|cacheKey |**NSString** |The cache key. This is the unique identifier for the URL and must follow the following rules:<br><br><br>* Should not contain special characters and can be used as a file name.<br><br>* Should correspond to the video resource file.<br><br>* It is recommended to use the MD5 value of the URL. |


**Returns**

An instance of the URL playback source.

<span id="TTVideoEngineUrlSource-initwithurls-cachekey-videoid-encodetype-decryptionkey-filepath-ishdrsource"></span>
### initWithUrls:cacheKey:videoId:encodeType:decryptionKey:filePath:isHDRSource:

```objectivec
- (instancetype)initWithUrls:(NSArray *)urls cacheKey:(NSString *)cacheKey videoId:(NSString * _Nullable)vid encodeType:(TTVideoEngineEncodeType)encodeType decryptionKey:(NSString * _Nullable)decryptionKey filePath:(NSString * _Nullable)filePath isHDRSource:(BOOL)isHDRSource;
```


Initializes the URL playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls |**NSArray** |The list of video URLs. Supports primary and backup URLs. |
|cacheKey |**NSString** |The cache key. This is the unique identifier for the URL and must follow the following rules:<br><br><br>* Should not contain special characters and can be used as a file name.<br><br>* Should correspond to the video resource file.<br><br>* It is recommended to use the MD5 value of the URL. |
|encodeType |**TTVideoEngineEncodeType** |The video codec. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype). |
|decryptionKey |**NSString** |Custom decryption key for playing encrypted videos. |
|filePath |**NSString** |The file path. |
|isHDRSource |**BOOL** |Whether the video is HDR. |


**Returns**

An instance of the URL playback source.

<span id="TTVideoEngineUrlSource-addurls-cachekey-encodetype-decryptionkey-filepath-ishdrsource"></span>
### addUrls:cacheKey:encodeType:decryptionKey:filePath:isHDRSource:

```objectivec
- (void)addUrls:(NSArray *)urls cacheKey:(NSString *)cacheKey encodeType:(TTVideoEngineEncodeType)encodeType decryptionKey:(NSString * _Nullable)decryptionKey filePath:(NSString * _Nullable)filePath isHDRSource:(BOOL)isHDRSource;
```


Adds a URL playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|urls |**NSArray** |The list of video URLs. Supports primary and backup URLs. |
|encodeType |**TTVideoEngineEncodeType** |The video codec. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype). |
|cacheKey |**NSString** |The cache key. This is the unique identifier for the URL and must follow the following rules:<br><br><br>* Should not contain special characters and can be used as a file name.<br><br>* Should correspond to the video resource file.<br><br>* It is recommended to use the MD5 value of the URL. |
|decryptionKey |**NSString** |Custom decryption key for playing encrypted videos. |
|filePath |**NSString** |The file path. |
|isHDRSource |**BOOL** |Whether the video is HDR. |


<span id="TTVideoEngineVidSource"></span>
# TTVideoEngineVidSource

```objectivec
@interface TTVideoEngineVidSource : NSObject <TTVideoEngineMediaSource>
```


The VID playback source.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[vid](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-vid) |
|**NSString** |[playAuthToken](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-playauthtoken) |
|**TTVideoEngineResolutionType** |[resolution](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-resolution) |
|**TTVideoEngineEncodeType** |[encodeType](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-encodetype) |
|**BOOL** |[isDash](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-isdash) |
|**BOOL** |[isHLS](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-ishls) |


<span id="Member functions"></span>
## Member functions


|**Return** |**Name** |
|---|---|
|**instancetype** |[initWithVid:playAuthToken:resolution:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-initwithvid-playauthtoken-resolution) |
|**instancetype** |[initWithVid:playAuthToken:resolution:encodeType:isDash:isHLS:](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineVidSource-initwithvid-playauthtoken-resolution-encodetype-isdash-ishls) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineVidSource-vid"></span>
### vid

```objectivec
@property (nonatomic, copy) NSString *vid;
```


(Required) Sets the video ID.

<span id="TTVideoEngineVidSource-playauthtoken"></span>
### playAuthToken

```objectivec
@property (nonatomic, copy) NSString *playAuthToken;
```


(Required) Sets the playback auth token.

<span id="TTVideoEngineVidSource-resolution"></span>
### resolution

```objectivec
@property (nonatomic, assign) TTVideoEngineResolutionType resolution;
```


Sets the video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype).

<span id="TTVideoEngineVidSource-encodetype"></span>
### encodeType

```objectivec
@property (nonatomic, assign) TTVideoEngineEncodeType encodeType;
```


Sets the video codec. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype). Default is H.264.

<span id="TTVideoEngineVidSource-isdash"></span>
### isDash

```objectivec
@property (nonatomic, assign) BOOL isDash;
```


Sets whether it is DASH. Default is `NO`.

<span id="TTVideoEngineVidSource-ishls"></span>
### isHLS

```objectivec
@property (nonatomic, assign) BOOL isHLS;
```


Sets whether it is HLS. Default is `NO`.

<span id="Function details"></span>
## Function details

<span id="TTVideoEngineVidSource-initwithvid-playauthtoken-resolution"></span>
### initWithVid:playAuthToken:resolution:

```objectivec
- (instancetype)initWithVid:(NSString *)vid playAuthToken:(NSString *)playAuthToken resolution:(TTVideoEngineResolutionType)resolution;
```


Initializes the VID playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |**NSString** |The video ID. |
|playAuthToken |**NSString** |(Required) The playback auth token. |
|resolution |**TTVideoEngineResolutionType** |The video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype). |


**Returns**

An instance of the VID playback source.

<span id="TTVideoEngineVidSource-initwithvid-playauthtoken-resolution-encodetype-isdash-ishls"></span>
### initWithVid:playAuthToken:resolution:encodeType:isDash:isHLS:

```objectivec
- (instancetype)initWithVid:(NSString *)vid playAuthToken:(NSString *)playAuthToken resolution:(TTVideoEngineResolutionType)resolution encodeType:(TTVideoEngineEncodeType)encodeType isDash:(BOOL)isDash isHLS:(BOOL)isHLS;
```


Initializes the VID playback source.

**Input parameters**


|**Name** |**Type** |**Description** |
|---|---|---|
|vid |**NSString** |The video ID. |
|playAuthToken |**NSString** |(Required) The playback auth token. |
|resolution |**TTVideoEngineResolutionType** |The video resolution. See [TTVideoEngineResolutionType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineresolutiontype). |
|encodeType |**TTVideoEngineEncodeType** |The video codec. See [TTVideoEngineEncodeType](https://docs.byteplus.com/en/docs/25/7970#ttvideoengineencodetype). Default is H.264. |
|isDash |**BOOL** |Whether it is DASH. Default is `NO`. |
|isHLS |**BOOL** |Whether it is HLS. Default is `NO`. |


**Returns**

An instance of the VID playback source.

<span id="TTVideoEngineDownloadState"></span>
# TTVideoEngineDownloadState

```objectivec
typedef NS_ENUM(NSInteger,TTVideoEngineDownloadState)
```


The download state of the video engine.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineDownloadStateInit |0 |The download is initialized. |
|TTVideoEngineDownloadStateWaiting |1 |The download is waiting. |
|TTVideoEngineDownloadStateRunning |2 |The download is running. |
|TTVideoEngineDownloadStateSuspended |3 |The download is suspended. |
|TTVideoEngineDownloadStateCanceling |4 |The download is being canceled. |
|TTVideoEngineDownloadStateCompleted |5 |The download is completed. |


<span id="TTVideoEnginePlaybackState"></span>
# TTVideoEnginePlaybackState

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEnginePlaybackState)
```


The playback state of the video engine.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEnginePlaybackStateStopped |0 |The playback is stopped. |
|TTVideoEnginePlaybackStatePlaying |1 |The video is playing. |
|TTVideoEnginePlaybackStatePaused |2 |The playback is paused. |
|TTVideoEnginePlaybackStateError |3 |An error occurred during playback. |


<span id="TTVideoEngineLoadState"></span>
# TTVideoEngineLoadState

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineLoadState)
```


The load state of the video engine.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineLoadStateUnknown |0 |The video engine is in an unknown load state. |
|TTVideoEngineLoadStatePlayable |1 |The video engine is loaded and ready to play or resume. |
|TTVideoEngineLoadStateStalled |2 |The video engine is stalled and loading data. |
|TTVideoEngineLoadStateError |3 |There was an error loading data for the video engine. |


<span id="TTVideoEngineStallReason"></span>
# TTVideoEngineStallReason

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineStallReason)
```


The reason for the video engine freeze.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineStallReasonNone |0 |Default value. |
|TTVideoEngineStallReasonNetwork |1 |The video engine is stalling due to network issues. |
|TTVideoEngineStallReasonDecoder |2 |The video engine is stalling due to decoder issues. |


<span id="TTVideoEngineFinishReason"></span>
# TTVideoEngineFinishReason

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineFinishReason)
```


The reason for the video playback finishing.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineFinishReasonUserExited |0 |The user actively exited the video playback. |
|TTVideoEngineFinishReasonRelease |1 |The video engine was released. |
|TTVideoEngineFinishReasondReleaseAsync |2 |The video engine was released asynchronously. |
|TTVideoEngineFinishReasonPlaybackEnded |3 |The video playback ended normally. |
|TTVideoEngineFinishReasonPlaybackError |4 |An error occurred during video playback. |
|TTVideoEngineFinishReasonStatusExcp |5 |An exception occurred during video playback. |
|TTVideoEngineFinishReasonReset |6 |The video engine was reset. |


<span id="TTVideoEngineRotateType"></span>
# TTVideoEngineRotateType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineRotateType)
```


The rotation angle of the video player.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineRotateTypeNone |0 |No rotation. |
|TTVideoEngineRotateType90 |1 |Rotate 90 degrees. |
|TTVideoEngineRotateType180 |2 |Rotate 180 degrees. |
|TTVideoEngineRotateType270 |3 |Rotate 270 degrees. |


<span id="TTVideoEngineMirrorType"></span>
# TTVideoEngineMirrorType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineMirrorType)
```


The mirror mode of the video player.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineMirrorTypeNone |0 |No mirror. |
|TTVideoEngineMirrorTypeHorizontal |1 |Horizontal mirror. |
|TTVideoEngineMirrorTypeVertical |2 |Vertical mirror. |
|TTVideoEngineMirrorTypeHV |3 |Both horizontal and vertical mirror. |


<span id="TTVideoEngineScalingMode"></span>
# TTVideoEngineScalingMode

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineScalingMode)
```


The scaling mode of the video player.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineScalingModeNone |0 |No scaling, may have black bars. |
|TTVideoEngineScalingModeAspectFit |1 |Fit the video within the view bounds, preserving aspect ratio. |
|TTVideoEngineScalingModeAspectFill |2 |Fill the view bounds with the video, preserving aspect ratio. Some parts of the video may be cropped. |
|TTVideoEngineScalingModeFill |3 |Fill the view bounds with the video, stretching to fit. The aspect ratio may not be preserved. |


<span id="TTVideoEngineAudioChannelType"></span>
# TTVideoEngineAudioChannelType

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineAudioChannelType)
```


The audio channel type.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineAudioChannelNormal |0 |Default stereo audio channel. |
|TTVideoEngineAudioChannelRightDisable |1 |Disable the right audio channel. |
|TTVideoEngineAudioChannelLeftDisable |2 |Disable the left audio channel. |
|TTVideoEngineAudioChannelLeftUesdForLR |3 |Use the left audio channel to play both left and right audio. |
|TTVideoEngineAudioChannelRightUesdForLR |4 |Use the right audio channel to play both left and right audio. |


<span id="TTVideoEngineSeekModeType"></span>
# TTVideoEngineSeekModeType

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineSeekModeType)
```


The seek mode.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineSeekModeAccurateAny |0 |Accurate seek mode. |
|TTVideoEngineSeekModeInAccurateBackWard |1 |Inaccurate seek mode that helps improve startup speed. |


<span id="TTVideoEngineAudioEffectType"></span>
# TTVideoEngineAudioEffectType

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineAudioEffectType)
```


The audio effect.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineAudioEffectRTCLoudNorm |4 |Volume leveling audio effect. |


<span id="TTVideoEngineRenderEngine"></span>
# TTVideoEngineRenderEngine

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineRenderEngine)
```


The rendering type.

<span id="Enums"></span>
### Enums


|Type |Value |Description |
|---|---|---|
|TTVideoEngineRenderEngineOpenGLES |0 |OpenGLES rendering. |
|TTVideoEngineRenderEngineMetal |1 |Metal rendering. |
|TTVideoEngineRenderEngineOutput |2 |External rendering, not using the SDK rendering. |


<span id="TTVideoEngineState"></span>
# TTVideoEngineState

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineState)
```


The player state.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineStateUnknown |0 |Initial state. |
|TTVideoEngineStateFetchingInfo |1 |Fetching playback information with VID. |
|TTVideoEngineStateParsingDNS |2 |DNS parsing in progress. |
|TTVideoEngineStatePlayerRunning |3 |The player is running normally. |
|TTVideoEngineStateError |4 |Error occurred during video player running. |


<span id="TTVideoEngineNetworkType"></span>
# TTVideoEngineNetworkType

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineNetworkType)
```


The network type.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineNetworkTypeWifi |0 |Using WiFi network. |
|TTVideoEngineNetworkTypeNotWifi |1 |Using non\-WiFi network. |
|TTVideoEngineNetworkTypeNone |2 |Unknown network status. |


<span id="TTVideoEngineDataLoaderErrorType"></span>
# TTVideoEngineDataLoaderErrorType

```objectivec
typedef NS_ENUM(NSUInteger, TTVideoEngineDataLoaderErrorType)
```


The error type for video data loading.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineDataLoaderErrorNone |0 |Default value. |
|TTVideoEngineDataLoaderErrorFetchVideoInfo |1 |Error occurred while fetching video information. |
|TTVideoEngineDataLoaderErrorStart |2 |Error occurred when starting MDL. |
|TTVideoEngineDataLoaderErrorFetchData |3 |Error occurred while downloading data. |
|TTVideoEngineDataLoaderErrorWriteFile |4 |Error occurred while writing data. |


<span id="TTVideoEngineLogFlag"></span>
# TTVideoEngineLogFlag

```objectivec
typedef NS_OPTIONS(NSInteger, TTVideoEngineLogFlag)
```


The log output mode of the player.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineLogFlagNone |0 |No log output. |
|TTVideoEngineLogFlagEngine |1 << 0 |Output engine logs. |
|TTVideoEngineLogFlagPlayer |1 << 1 |Output player kernel logs. |
|TTVideoEngineLogFlagMDL |1 << 2 |Output MDL logs. |
|TTVideoEngineLogFlagDefault |(TTVideoEngineLogFlagEngine |TTVideoEngineLogFlagMDL |


<span id="TTVideoEngineStallAction"></span>
# TTVideoEngineStallAction

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineStallAction)
```


The specific actions that cause the player freeze.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineStallActionNone |0 |Default value. |
|TTVideoEngineStallActionSeek |1 |User seek. |
|TTVideoEngineStallActionSwitch |2 |Resolution switch. |


<span id="TTVideoEngineStreamType"></span>
# TTVideoEngineStreamType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineStreamType)
```


The stream type.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineVideoStream |0 |Video stream. |
|TTVideoEngineAudioStream |1 |Audio stream. |


<span id="TTVideoEngineEncodeType"></span>
# TTVideoEngineEncodeType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineEncodeType)
```


The video codec type.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineH264 |0 |H.264 |
|TTVideoEngineh265 |3 |H.265 |


<span id="TTVideoEngineUserAction"></span>
# TTVideoEngineUserAction

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineUserAction)
```


The user\-controlled actions of the player.

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineUserActionInit |0 |Initialize the player. |
|TTVideoEngineUserActionPrepare |1 |Call `prepare`. |
|TTVideoEngineUserActionPlay |2 |Call `play`. |
|TTVideoEngineUserActionPause |3 |Call `pause`. |
|TTVideoEngineUserActionStop |4 |Call `stop`. |
|TTVideoEngineUserActionClose |5 |Call `close`. |


<span id="TTVideoEngineSourceType"></span>
# TTVideoEngineSourceType

```objectivec
typedef NS_ENUM(NSInteger, TTVideoEngineSourceType)
```


The playback source type

<span id="Enums"></span>
### Enums


|**Type** |**Value** |**Description** |
|---|---|---|
|TTVideoEngineSourceTypeVideoId |0 |The VID playback source. |
|TTVideoEngineSourceTypeDirectUrl |1 |The URL playback source. |
|TTVideoEngineSourceTypeVideoModel |2 |The video model playback source and assemble the playback source data according to the format of VideoModel. |


<span id="TTVideoEngineMediaSource"></span>
# TTVideoEngineMediaSource

```objectivec
@protocol TTVideoEngineMediaSource <NSObject>
```


A protocol that defines the interface of the playback source.

<span id="Member variables"></span>
## Member variables


|**Type** |**Name** |
|---|---|
|**NSString** |[uniqueId](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineMediaSource-uniqueid) |
|**TTVideoEngineSourceType** |[sourceType](https://docs.byteplus.com/en/docs/25/7970#TTVideoEngineMediaSource-sourcetype) |


<span id="Variable details"></span>
## Variable details

<span id="TTVideoEngineMediaSource-uniqueid"></span>
### uniqueId

```objectivec
@property (nonatomic, readonly, strong, getter=getUniqueId) NSString *uniqueId;
```


The unique identifier of the current playback source.


* For the types `TTVideoEngineSourceTypeVideoId` and `TTVideoEngineSourceTypeVideoModel`, the `vid` is used as the unique identifier.

* For the type `TTVideoEngineSourceTypeDirectUrl`, the `cacheKey` is used as the unique identifier.
