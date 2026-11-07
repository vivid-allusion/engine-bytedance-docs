---
title: "iOS Player SDK: VideoModel"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/videomodel-ios"
---

VideoModel is a self\-developed protocol for an optimal playback experience in multi\-resolution scenarios. It allows you to consolidate multi\-resolution and multi\-format video streams into a single object and directly passes the information to the Player SDK for playback. The advantages are as follows:


* **Reduced first\-frame time**: Compared to the Vid mode (the Player SDK requests playback information from the VOD server via a Vid), VideoModel skips this client\-to\-server network request. Your business server can directly generate or your client can assemble the VideoModel playback source, and then pass it to the Player SDK to initiate loading.

* **Complete features**: VideoModel supports all VOD features, including ABR (Adaptive Bitrate), smooth switching, and private encryption.

* **High flexibility**: You have complete control over the VideoModel's generation and distribution timing to better integrate with your business logic.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To implement this feature, please integrate iOS Player SDK version 1.36.2.10 or above.</div>


This document explains two methods for setting up the VideoModel playback source on the iOS client.

<span id="b10ff758"></span>
## Video data flow

Video data can originate from third\-party services or the VOD service. The typical end\-to\-end data flow is as follows:


1. **Data acquisition**: Your application server obtains the video's metadata.

   * **Source 1**: Call [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) to retrieve a structured JSON object.

   * **Source 2**: Obtain data from a third\-party service or internal media asset system. The data format depends on your specific requirements.

2. **Data distribution**: Your application server distributes the acquired data to the iOS client via APIs.

3. **Data mapping:**  The iOS client receives the data, maps it to a `TTVideoEngineVideoModelSource` object, and passes it to the player for playback.


<span id="843171c5"></span>
## Construction methods

On the iOS client, you must convert video data from the VOD service or a third\-party service into a `TTVideoEngineVideoModelSource` object for the player. The SDK supports two methods for this conversion. Both methods involve mapping the data to the player's internal `TTVideoEngineModel` format.

<span id="4c05cb8f"></span>
### Method 1: Using BareVideoInfo/BareVideoModel utility classes (recommended)

The SDK provides `BareVideoInfo` and `BareVideoModel` utility classes. These help you quickly aggregate video stream properties and convert them to the SDK's internal data types.

`BareVideoInfo.h`:

```objectivec
//
//  BareVideoInfo.h
//
#import <Foundation/Foundation.h>
#import <TTSDK/TTVideoEngineHeader.h>

NS_ASSUME_NONNULL_BEGIN

/// Playback information for a single resolution
@interface BareVideoInfo : NSObject
/// Optional values: video, audio
@property (nonatomic, copy) NSString *fileType;
/// Container format
@property (nonatomic, copy) NSString *format;
/// Encoding type: h264, h265
@property (nonatomic, copy) NSString *codec;
/// @required Resolution 540p, 480p, 720p, 1080p, 2k, 4k...
@property (nonatomic, copy) NSString *definition;
/// File ID, such as an MD5 hash or other unique ID(nullable)
@property (nonatomic, copy) NSString *fileId;
/// MD5
@property (nonatomic, copy) NSString *md5;

/// @required Playback URL
@property (nonatomic, copy) NSString *mainPlayUrl;

/// @optional Playback URL expiration time
@property (nonatomic, copy) NSString *mainUrlExpireTime;

/// Bitrate in bps
@property (nonatomic, assign) NSUInteger bitrate;
/// Video frame width
@property (nonatomic, assign) int width;
/// Video frame height
@property (nonatomic, assign) int height;

@end

/// Multi-resolution playback source data model
@interface BareVideoModel : NSObject

@property (nonatomic, copy) NSString *vid;
@property (nonatomic, assign) int version;
@property (nonatomic, assign, readonly) int status;
@property (nonatomic, assign) double duration;
@property (nonatomic, assign) bool enableAdaptive;
@property (nonatomic, copy) NSArray<BareVideoInfo *> *playInfoList;

- (TTVideoEngineModel *)engineVideoModel;

@end

NS_ASSUME_NONNULL_END  
```


`BareVideoInfo.m`:

```objectivec
//
//  BareVideoInfo.m
//

#import "BareVideoInfo.h"

@implementation BareVideoInfo

- (NSDictionary *)dictionaryRepresentation {
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];
    [dict setValue:self.fileType forKey:@"FileType"];
    [dict setValue:self.format forKey:@"Format"];
    [dict setValue:self.codec forKey:@"Codec"];
    [dict setValue:self.fileId forKey:@"FileId"];
    [dict setValue:self.md5 forKey:@"Md5"];
    [dict setValue:self.definition forKey:@"Definition"];
    [dict setValue:self.mainPlayUrl forKey:@"MainPlayUrl"];
    [dict setValue:self.mainUrlExpireTime forKey:@"MainUrlExpire"];
    [dict setValue:@(self.bitrate) forKey:@"Bitrate"];
    [dict setValue:@(self.width) forKey:@"Width"];
    [dict setValue:@(self.height) forKey:@"Height"];
    return [dict copy];
}

@end

@implementation BareVideoModel

- (instancetype)init {
    self = [super init];
    if (self) {
        _version = 4;
        _status = 10;
    }
    return self;
}

- (NSDictionary *)dictionaryRepresentation {
    NSMutableDictionary *dict = [NSMutableDictionary dictionary];
    [dict setValue:self.vid forKey:@"Vid"];
    [dict setValue:@(self.status) forKey:@"Status"];
    [dict setValue:@(self.version) forKey:@"Version"];
    [dict setValue:@(self.duration) forKey:@"Duration"];
    [dict setValue:@(self.enableAdaptive) forKey:@"EnableAdaptive"];

    NSMutableArray *playInfoList = [NSMutableArray array];
    for (BareVideoInfo *info in self.playInfoList) {
        NSDictionary *infoDict = [info dictionaryRepresentation];
        [playInfoList addObject:infoDict];
    }

    [dict setValue:playInfoList forKey:@"PlayInfoList"];
    return dict.copy;
}

- (TTVideoEngineModel *)engineVideoModel {
    return [TTVideoEngineModel videoModelWithDict:[self dictionaryRepresentation]];
}

@end 
```


The following sample demonstrates how to construct a `TTVideoEngineVideoModelSource` from two different resolution video streams.

```objectivec
#import "BareVideoInfo.h"
#import "BareVideoModel.h"

- (TTVideoEngineVideoModelSource *)constructSource {
    // 1. Configure the first video stream information (such as 480p)
    BareVideoInfo *info1 = [[BareVideoInfo alloc] init];
    info1.mainPlayUrl = @"http://example.com/sample1.mp4"; // **Required**. Main URL
    info1.definition = @"480p"; // **Required**. Video resolution identifier
    info1.fileType = @"video";  // **Required**. Media type
    info1.codec = @"h264";      // **Required**. Encoding type (h264/h265)
    info1.md5 = @"your_md5_string"; // **Required**. File hash, used as the unique identifier and cache key
    // --- Information required for smooth switching and ABR ---
    info1.bitrate = 1024;       // Video bitrate
    info1.format = @"mp4";      // Container format (such as "mp4", "hls")
    
    // 2. Configure the second video stream information (such as 720p)
    BareVideoInfo *info2 = [[BareVideoInfo alloc] init];
    info2.mainPlayUrl = @"http://example.com/sample2.mp4";
    info2.definition = @"720p";
    info2.fileType = @"video";
    info2.codec = @"h264"; 
    info2.md5 = @"your_md5_string_2";
    // --- Information required for smooth switching and ABR ---
    info2.bitrate = 2048;  
    info2.format = @"mp4";
    
    // 3. Aggregate multiple video streams into one BareVideoModel
    BareVideoModel *videoModel = [[BareVideoModel alloc] init];
    videoModel.vid = @"your_video_id"; // **Required**. Video ID
    videoModel.playInfoList = @[info1, info2]; // List of all resolution streams
    // Set this to YES to enable smooth switching. This requires that video frames are aligned across all streams
    videoModel.enableAdaptive = YES; 
    
    // 4. Use the utility class method to generate the internal TTVideoEngineModel object
    TTVideoEngineModel *innerVideoModel = [videoModel engineVideoModel];
    
    // 5. Construct the final playback source object
    // Specify the Vid and a default starting playback resolution (such as TTVideoEngineResolutionTypeHD)
    TTVideoEngineVideoModelSource *source = [[TTVideoEngineVideoModelSource alloc] initWithVid:videoModel.vid resolution:TTVideoEngineResolutionTypeHD];
    
    // 6. Assign the generated video model to the playback source
    source.videoModel = innerVideoModel;
    
    return source;
}
```


<span id="785e1256"></span>
### Method 2: Constructing from a JSON string (for VOD data)

If your application server receives a JSON string from the VOD [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) API, you can use the following method to construct the `TTVideoEngineVideoModelSource` playback source:

```objectivec
/**
 * Helper method to create a TTVideoEngineVideoModelSource instance from a JSON string.
* @param jsonString The JSON string from the VOD GetPlayInfo API.
 * @return A TTVideoEngineVideoModelSource instance. Returns nil if parsing fails.
 */
+ (TTVideoEngineVideoModelSource *)createFromJsonString:(NSString *)jsonString {
    // 1. Parse the JSON string into an NSDictionary
    NSData *jsonData = [jsonString dataUsingEncoding:NSUTF8StringEncoding];
    NSError *error = nil;
    NSDictionary *jsonDict = [NSJSONSerialization JSONObjectWithData:jsonData options:0 error:&error];
    if (error) {
        NSLog(@"JSON Parse Error: %@", error.localizedDescription);
        return nil;
    }
    
    // 2. Create a TTVideoEngineModel from the jsonDict
    TTVideoEngineModel *videoModel = [TTVideoEngineModel videoModelWithDict:jsonDict];
    if (!videoModel) {
        NSLog(@"Create TTVideoEngineModel Error");
        return nil;
    }
 
    // 3. Construct the final playback source object
    // Specify the Vid and a default resolution for initial playback(such as TTVideoEngineResolutionTypeHD)
    TTVideoEngineVideoModelSource *source = [[TTVideoEngineVideoModelSource alloc] initWithVid:[videoModel.videoInfo getValueStr:VALUE_VIDEO_ID] resolution:TTVideoEngineResolutionTypeHD];
    source.videoModel = videoModel;
 
    return source;
}
```


The input JSON string must contain only the `Result` object from the `GetPlayInfo` API response, not the entire response body. The following is an example structure of the `Result` object:

```JSON
{
    "Vid": "v029c1g10003civ2i5mqib*******",
    "Status": 1,
    "PosterUrl": "https://img.***.com/1234/8511abe****.jpeg",
    "Duration": 0.1,
    "FileType": "video",
    "EnableAdaptive": true,
    "TotalCount": 1
    // ... more fields
}
```
