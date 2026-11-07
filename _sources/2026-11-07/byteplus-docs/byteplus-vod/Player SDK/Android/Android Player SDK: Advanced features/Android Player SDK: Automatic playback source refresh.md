---
title: "Android Player SDK: Automatic playback source refresh"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-automatic-playback-source-refresh-android"
---

This document describes how to implement automatic refresh functionality for expired playback URLs. When a video's CDN playback address (URL) has a limited lifespan due to security policies (such as signature verification), this feature can automatically retrieve a new valid address after the URL expires, ensuring continuous and smooth video playback and preventing interruptions caused by address expiration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">To implement this feature, please integrate Android Player SDK version 1.42.300.1 or later.</div>


<span id="d265702c"></span>
## Prerequisites

Before implementing the automatic playback URL refresh feature on the client\-side, ensure you've completed the following:


1. Confirm the CDN URL signing algorithm and obtain the signing key:

   * If you are using BytePlus VOD's CDN, go to the [console](https://console.byteplus.com/vodpaas/region:vodpaas+ap-singapore-1/totalOverview/) to obtain the signing key. Refer to [URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview) and [Signature demos](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview#d6ba5f27) to understand the signing algorithm.

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
      


<span id="96891397"></span>
## Overall process

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2ea3901a53a4dfe97eca64411d85f60~tplv-goo7wpa0wc-image.image) </span>

<span id="340c6db9"></span>
## Implementation steps


1. Initialize the Player SDK and set the URL refresher factory.

   ```Java
   // 1. Initialize the player SDK.
   Env.init(/* ... */);
   
   // 2. Set the TTVideoEngineUrlFetcher factory using TTVideoEngineSourceRefreshStrategy.setUrlFetcherFactory.
   TTVideoEngineSourceRefreshStrategy.setUrlFetcherFactory(new TTVideoEngineUrlFetcher.Factory() {
       @Override
       public TTVideoEngineUrlFetcher create(TTVideoEngine engine) {
           return new AppUrlFetcher();
       }
   });
   
   // 3. Implement TTVideoEngineUrlFetcher.  In the fetch method, request the refreshed URL from your application server's refresh URL interface.
   //  - On success: Call callback.onSuccess and pass the new URL and expiration time.
   //  - On failure: Call callback.onError and pass the error code and message.
   public class AppUrlFetcher implements TTVideoEngineUrlFetcher {
       
       // Example App network engine; replace with OKHttp/Retrofit, etc.
       private AppNetClient mClient;
   
       @Override
       public void fetch(UrlRequest urlRequest, Callback<UrlResult> callback) {
           mClient = new AppNetClient();
           mClient.getRefreshedCdnUrl(urlRequest.url, new Callback() {
               @Override
               public void onSuccess(String newUrl, long expireTimeInMS) {
                   callback.onSuccess(new UrlResult(newUrl, expireTimeInMS));
               }
   
               @Override
               public void onError(String errorCode, String errorMsg) {
                   callback.onError(errorCode, errorMsg);
               }
           });
       }
   
       @Override
       public void cancel() {
           if (mClient != null) {
               mClient.release();
           }
       }
   };
   
   // 4. (Optional) Customize the CacheKey for HLS sources.  For non-HLS sources, do not call CacheSettings.getInstance().setGenerateFileKeyCallback.
   //
   // For HLS, the default cacheKey generation rule for the TS address is md5(pathOf(tsUrl)).
   // If the TS address signature is calculated in the path, to ensure the uniqueness of the cacheKey, customize the TS cacheKey generation rule using the interface below.
   CacheSettings.getInstance().setGenerateFileKeyCallback(new CacheSettings.IGenerateFileKeyCallback() {
       /**
        * @param url: TS address
        * @param fileKey: HLS key
        * @param extraInfo: Currently empty; for future compatibility
        * @return Custom TS cacheKey
        */
       @Override
       public String generateFileKey(String url, String fileKey, Map<String, String> extraInfo) {
           // Generate the cacheKey based on the URL rules, ensuring that the cacheKey generated from the CDN URL after two signature calculations for the same TS file is consistent.
       }
   }
   ```
   

2. Call `setIntOption` to enable automatic source refresh before calling `play`.

   ```Java
   videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_INT_ENABLE_SOURCE_REFRESH_STRATEGY, 1);
   
   // Set this before setStrategySource.
   videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_INT_ENABLE_SOURCE_REFRESH_STRATEGY, 1); 
   // For HLS video sources, it is recommended to enable the PLAYER_OPTION_ENABLE_SEG_ERROR option as well.
   videoEngine.setIntOption(TTVideoEngine.PLAYER_OPTION_ENABLE_SEG_ERROR, 1); 
   videoEngine.setStrategySource(xxx);
   ```
