---
title: "iOS Player SDK: Automatic playback source refresh"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-automatic-playback-source-refresh-ios"
---

This document describes how to implement automatic refresh functionality for expired playback URLs. When a video's CDN playback address (URL) has a limited lifespan due to security policies (such as signature verification), this feature can automatically retrieve a new valid address after the URL expires, ensuring continuous and smooth video playback and preventing interruptions caused by address expiration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To implement this feature, please integrate iOS Player SDK version 1.42.300.2 or later.</div>


<span id="34a9b4db"></span>
## Prerequisites

Before implementing the automatic playback URL refresh feature on the client\-side, ensure you've completed the following:


1. Confirm the CDN URL signing algorithm and obtain the signing key:

   * If you are using BytePlus VOD's CDN, go to the [console](https://console.byteplus.com/vodpaas/region:vodpaas+ap-singapore-1/totalOverview/) to obtain the signing key. Refer to [URL signing overview](https://docs.byteplus.com/docs/25/31569) and [Signature demos](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview#d6ba5f27) to understand the signing algorithm.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b65551866c0f4b1aa85c7c83ceb8ab32~tplv-goo7wpa0wc-image.image) </span>

   * If you are using a third\-party cloud provider's CDN, contact your service provider to obtain the CDN signing key and signing algorithm for the corresponding domain.

2. Deploy a URL refresh interface on your application server. This interface receives an expired URL as a request parameter and returns a new valid URL and the expiration timestamp of the new URL.

   **Example server\-side interface:** 

   * Request method: `GET /api/refreshUrl`

   * Request parameter: `expiredUrl`

   * Response:

      ```JSON
      {
          "url": "https://www.example.com/1.mp4", // Refreshed address
          "expireInMS": 1705392219000 // Expiration timestamp (milliseconds) of the new address
      }
      ```
      


<span id="a3ac79bb"></span>
## Overall process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2ea3901a53a4dfe97eca64411d85f60~tplv-goo7wpa0wc-image.image) </span>

<span id="ae999da0"></span>
## Implementation steps


1. Create a class and implement the `TTVideoURLRefreshFetcher` protocol. In the `refreshNewUrls:oldUrl:complateBlock:errorBlock:cancelBlock:` method of this protocol, request the URL refresh interface provided by your application server.

   ```objectivec
   @interface CustomRefreshFetcher ()
   
   @property (nonatomic, assign) BOOL isLoading;
   
   @end
   
   @implementation CustomRefreshFetcher
   
   #pragma mark - TTVideoURLRefreshFetcher
   
   - (void)refreshNewUrls:(NSString * _Nonnull)cacheKey
                   oldUrl:(NSString * _Nonnull)oldUrl
            complateBlock:(TTVideoURLRefreshCompleteBlock)complateBlock
               errorBlock:(TTVideoURLRefreshErrorBlock)errorBlock
              cancelBlock:(TTVideoURLRefreshCancelBlock)cancelBlock
       // This callback can be triggered multiple times; here's a compatibility solution.
       if (self.isLoading) {
           return;
       }
       self.isLoading = YES;
       
       // This is example code for requesting a new URL; replace this logic with your own business logic.
       [self.networkClient fech:oldUrl success: ^(id response) {
           // Address refresh succeeded
           NSString *newUrl = [response newUrl];
           // Note: the unit is milliseconds
           NSString *expireTimeInMs = [response expireTime]; 
           !complateBlock ?: complateBlock(newUrl, expireTimeInMs);
           self.isLoading = NO;
       } failure: ^(NSError *error) {
           // Address refresh failed
           !errorBlock ?: errorBlock(error);
           self.isLoading = NO;
       } cancel: ^() {
           // User canceled the request (e.g., exited the playback page). Call cancelBlock; the SDK internally releases resources.
           !cancelBlock ?: cancelBlock();
           self.isLoading = NO;
       }];
   }
   
   // Player SDK requests cancellation of refresh
   - (void)cancel {
       // Please implement the request cancellation logic
       [self.networkClient cancelRequest];
   }
   
   @end
   ```
   

2. When creating a `TTVideoEngineUrlSource` playback source, set its `enableFallbackRefresh` property to `YES` to enable automatic refresh of expired playback sources.

   ```objectivec
       - (void)play {
       // Construct the playback source
       NSString *url = @"http://test.mp4"; // Player address
       NSString *cacheKey = @"cache key";  // Cache key; it's recommended to use the MD5 value of the URL.
       TTVideoEngineUrlSource *source = [[TTVideoEngineUrlSource alloc] initWithUrl:url cacheKey:cacheKey];
       source.enableFallbackRefresh = YES; // Enable automatic refresh of expired playback sources
   
       // If it's an HLS playback source, it's recommended to enable the following option:
       [self.videoEngine setOptionForKey:VEKKeyIsEnableSegError value:@(YES)];
   
       // Implement the playback address refresh protocol.
       // Note: The refreshFetcher should be a global variable to prevent premature release of the local variable, which would cause the automatic refresh to fail.
       self.refreshFetcher = [[CustomRefreshFetcher alloc] init];
       self.videoEngine.urlRefreshFetcher = self.refreshFetcher;
   
       // Set the playback source.
       [self.videoEngine setVideoEngineVideoSource:source];
   
       // Start playback.
       [self.videoEngine play];
   }
   ```
   

3. (Optional) Customize the CacheKey for HLS playback sources: If the URL of the HLS video TS segment contains a signature, you need to set the `HLSProxyDelegate` of `TTVideoEngine` and implement the `generateFileKey:hlsFileKey:infos:` protocol method to customize the cacheKey generation rule for the TS file.

   ```objectivec
   /*
    * Customize the CacheKey for HLS sources.  For non-HLS sources, do not call the setHLSProxyDelegate method.
    * For HLS, the player internally generates the cacheKey generation rule for the TS address; the rule is md5(pathOf(tsUrl)).
    * If the TS address signature is calculated in the path, to ensure the uniqueness of the cacheKey, the application must customize the TS cacheKey generation rule using the interface below.
    */
   // 1. Set the HLSProxy protocol
   [TTVideoEngine setHLSProxyDelegate:self];
   
   // 2. Implement the HLSProxy protocol. Customize the TS cache key based on your specific business needs. 'url' represents the TS address, and 'hlsFileKey' represents the M3U8 file key.
   - (NSString * _Nullable)generateFileKey:(NSString *_Nonnull)url 
                               hlsFileKey:(NSString *_Nonnull)hlsFileKey 
                                    infos:(NSDictionary *_Nullable)infos {
       
   }
   ```
