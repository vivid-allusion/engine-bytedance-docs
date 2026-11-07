---
title: "iOS 平臺的 CSAI 整合"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-for-ios-zh-TW"
---

本指南介紹如何在 iOS 上將 BytePlus MediaAds SDK 和 Google IMA SDK 整合到基於 VideoOne 的短劇應用中。

<span id="39e090fd"></span>
## 前置條件

在開始之前，請確保您具備以下條件：


1. **現有整合**：您已整合 VideoOne 短劇解決方案（詳見[短劇影片 - iOS 整合](https://docs.byteplus.com/docs/byteplus-vos/short-drama-videos-ios-integration-zh-TW)）。

2. **廣告標籤 URL**：您需要一個有效的 VAST/VMAP 廣告標籤 URL。

   * 測試時：您可以使用 [Google 的 VAST 標籤示例](https://developers.google.com/interactive-media-ads/docs/sdks/html5/client-side/tags)。

   * 生產環境：請從您的廣告伺服器（如 Google Ad Manager）獲取廣告標籤 URL。

3. **最低 SDK 要求**：

   * `iOS 部署目標`：14.0 或更高版本。


<span id="dc415611"></span>
## SDK 整合

請按照以下步驟將 MediaAds SDK 整合到您的 iOS 專案中。


1. **引入 BytePlus CocoaPods 規格倉庫**：在 `Podfile` 中新增 BytePlus 規格倉庫以訪問 SDK。

   ```Ruby
   # Source BytePlus's CocoaPods specs repo in the Podfile
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

2. **設定 iOS 最低版本**：確保您的專案目標為 iOS 14.0 或更高，這是 MediaAds SDK 的最低要求。

   ```Ruby
   # Minimum required version is at least 14.0
   platform :ios, '14.0'
   ```
   

3. **新增 MediaAds SDK 依賴項**：為短劇 In\-Stream Ads 場景定義新的 pod 集，並將其包含到您的 target 中。

   ```Ruby
   # Add new Mini Drama with CSAI scene
   def scene_MiniDramaWithInStreamAds_pods
     pod 'TTSDKFramework', $TT_SDK_VERSION, :subspecs => ['Player']
     pod 'MediaAdsToB', '2.0.1'
     pod 'MiniDramaWithInStreamAds', :path => './Component/MiniDramaWithInStreamAds'
   end
   
   target 'VideoOne' do
     common_pods
     scene_InteractiveLive_pods
     # ... other scenes
     
     scene_MiniDrama_pods
     # Include Mini Drama with CSAI scene in list of targets to build
     scene_MiniDramaWithInStreamAds_pods
     scene_AIChat_pods
   end
   ```
   


<span id="501b067a"></span>
## 快速開始

<span id="543fb340"></span>
### 通用指南

MediaAds SDK 設計為播放器無關。為適配任意播放器，提供了名為 `AdPlaybackSession` 的實體，用於封裝內容播放器和廣告播放器，並協調主內容中的廣告插入。

請按照以下步驟建立 `AdSchedule` 並構建 `AdPlaybackSession`。


1. 建立 `MediaAdsInitConfig`：使用您的應用 ID、名稱和渠道初始化配置物件。

   ```objectivec
   MediaAdsInitConfig *config = [[MediaAdsInitConfig alloc] init];
   config.appID = VODAPPID;
   config.appName = [NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleName"];
   config.appChannel = [NSBundle.mainBundle.infoDictionary objectForKey:@"CHANNEL_NAME"];
   ```
   

2. 建立 `AdSchedule`：定義內容的廣告插播點。在本示例中，我們透過 VAST 標籤 URL 配置了前貼片、中貼片和後貼片廣告。

   ```objectivec
   AdSchedule *adSchedule = [[AdSchedule alloc] init];
   
   // Add pre-roll ad with VAST tags (offset: "pre")
   [adSchedule addLinearAdWithOffset:@"pre" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&correlator="];
   
   // Add mid-roll ad with VAST tags (offset: "00:00:15")
   [adSchedule addLinearAdWithOffset:@"00:00:15" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_skip_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dmidskiponly&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=midroll&pod=1&ppos=1&min_ad_duration=0&max_ad_duration=30000&vrid=1445984&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
   
   // Add post-roll ad with VAST tags (offset: "post")
   [adSchedule addLinearAdWithOffset:@"post" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dpremidpost&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=postroll&pod=3&ppos=1&lip=true&min_ad_duration=0&max_ad_duration=30000&vrid=1264775&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
   ```
   

3. 建立 `AdPlaybackSession`：例項化會話，將其繫結到您的檢視和檢視控制器，並啟動。

   ```objectivec
   // Instantiate AdPlaybackSession with config
   AdPlaybackSession *adPlaybackSession = [[MediaAds sharedInstance] createAdSession:player Config:config];
   // Set ad UIView and UIViewController to handle rendering and navigation
   [adPlaybackSession setAdView:adContainerView AdViewController:viewController];
   // (optional, recommended) set AdPlaybackSessionDelegate to listen for events
   adPlaybackSession.delegate = adPlaybackSessionDelegate;
   // Set AdSchedule
   [adPlaybackSession setSchedule:adSchedule];
   // Start ad session
   [adPlaybackSession startSession];
   ```
   


<span id="56560146"></span>
### 與 VideoOne 整合

<span id="b4ffab7e"></span>
#### 實現 `MDVideoWithAdsPlayerController`

`MDVideoWithAdsPlayerController` 類繼承自 `MDVideoPlayerController`。它重寫了播放方法，將控制權委託給 `MediaAds` 會話，而不是直接操作影片播放器。

該類的主要職責：


1. **初始化廣告會話**：建立 `AdPlaybackSession` 並繫結廣告容器檢視。

2. **攔截播放指令**：重寫 `play`、`pause` 和 `stop`，透過 `adPlaybackSession` 路由這些指令。

3. **代理委託回撥**：使用 `VideoEngineDelegateProxy`，確保廣告會話和應用都能收到播放器事件。

4. **動態排程廣告**：在 `videoEnginePrepared` 回撥中配置 `AdSchedule`，當影片時長已知時。


```objectivec
@interface MDVideoWithAdsPlayerController () <
TTVideoEngineDelegate
// optionally adopt the AdPlaybackSessionDelegate protocol
AdPlaybackSessionDelegate
/* other delegate protocols */>

@property (nonatomic, strong) TTVideoEngine *videoEngine;
@property (nonatomic, strong) AdSchedule *adSchedule;
@property (nonatomic, strong) AdPlaybackSession *adPlaybackSession;
@property (nonatomic, strong) VideoEngineDelegateProxy *delegateProxy;
@property (nonatomic, strong) UIView *adContainerView;

// other properties ...

@end

@implementation MDVideoWithAdsPlayerController

// synthesizes and dynamic properties ...

// create ad playback session
- (AdPlaybackSession *)createAdPlaybackSession {
    MediaAdsInitConfig *config = [[MediaAdsInitConfig alloc] init];
    // set config ...

    AdPlaybackSession *session = [[MediaAds sharedInstance] createAdSession:self.videoEngine Config:config];
 
    // set up ad UIView constraints and insert into hierarchy
    [self __setupAdContainerView];
    [self.view addSubview:_adContainerView];

    // set ad UIView and its UIView controller
    [session setAdView:_adContainerView AdViewController:self];

    return session;
}

- (void)createVideoEngine:(id<TTVideoEngineMediaSource> _Nonnull)mediaSource needPrerenderEngine:(BOOL)needPrerender {
    if (super.videoEngine == nil) {
        // create video engine ...
    }

    // video engine configuration ...

    // AdPlaybackSession can be created after the video player
    if (self.adPlaybackSession == nil) {
        self.adPlaybackSession = [self createAdPlaybackSession];

        // CRITICAL: Delegate Proxying
        // MediaAds sets its own player delegate. To also receive callbacks in this controller,
        // we use a proxy that forwards events to both the MediaAds delegate and self.
        id<TTVideoEngineDelegate> mediaAdsDelegate = self.videoEngine.delegate;
        VideoEngineDelegateProxy *proxy = [[VideoEngineDelegateProxy alloc] initWithMediaAdsDelegate:mediaAdsDelegate adsPlayerDelegate:self];
        self.videoEngine.delegate = proxy;
        self.delegateProxy = proxy;
    }
}

// replace calls to [player <playback method>] with [AdPlaybackSession <method>]
- (void)prepareToPlay {
    BTDAssertMainThread();
    MDPlayerContextRunOnMainThread(^{
        // [self.videoEngine prepareToPlay];
        [self.adPlaybackSession prepareAD];
    });
}

- (void)play {
    BTDAssertMainThread();
    MDPlayerContextRunOnMainThread(^{
        // Retain existing anti-recording logic
        if ([DramaDisrecordManager isOpenDisrecord] && @available(iOS 11.0, *)) {
            if ([[[[UIApplication sharedApplication] keyWindow] screen] isCaptured]) {
                [[DramaDisrecordManager sharedInstance] showDisRecordView];
                return;
            }
        }
        [self __handleBeforePlayAction];
        
        // Resume session instead of directly playing video engine
        if (self.adPlaybackSessionStarted == YES) {
            [self.adPlaybackSession resumeSession];
        } else {
            [self.videoEngine play];
        }
        [self _handleAfterPlayAction];
        [self __addPeriodicTimeObserver];
        if (self.playerConfig.enableLoadSpeed) {
            [TTVideoEngine ls_setPreloadDelegate:self];
        }
    });
}

- (void)pause {
    BTDAssertMainThread();
    MDPlayerContextRunOnMainThread(^{
        [self.context post:@(YES) forKey:MDPlayerContextKeyPauseAction];
        // [self.videoEngine pause];
        [self.adPlaybackSession pauseSession];
        });
}

- (void)stop {
    [self unregisterScreenCaptureDidChangeNotification];
    BTDAssertMainThread();
    MDPlayerContextRunOnMainThread(^{
        [self.context post:@(YES) forKey:MDPlayerContextKeyStopAction];
        // [self.videoEngine stop];
        [self.adPlaybackSession stopSession];
        [self __closeVideoPlayer];
    });
}

#pragma mark - TTVideoEngineDelegate
- (void)videoEnginePrepared:(TTVideoEngine *)videoEngine {
    // Video duration is available here. Configure schedule now.
    _adSchedule = [[AdSchedule alloc] init];
    
    NSDictionary *settings = [[MDAdSettingManager universalManager] settings];
    // check settings for which ads to schedule ...

    if (preRollAdEnabled) {
        [_adSchedule addLinearAdWithOffset:@"pre" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&correlator="];
    }

    if (midRollAdEnabled) {
        // Calculate mid-roll timestamp based on actual duration
        NSString *midRollOffset = [self stringFromTimeInterval:[self duration] / 2];
        [_adSchedule addLinearAdWithOffset:midRollOffset adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_skip_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dmidskiponly&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=midroll&pod=1&ppos=1&min_ad_duration=0&max_ad_duration=30000&vrid=1445984&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
    }

    if (postRollAdEnabled) {
        [_adSchedule addLinearAdWithOffset:@"post" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dpremidpost&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=postroll&pod=3&ppos=1&lip=true&min_ad_duration=0&max_ad_duration=30000&vrid=1264775&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
    }
    
    [_adPlaybackSession setSchedule:_adSchedule];
    
    // Start session. Note: The schedule CANNOT be changed after this point.
    [self.adPlaybackSession startSession];
    self.adPlaybackSessionStarted = YES;

    // notify other delegates ...
}

// implement any relevant AdPlaybackSessionDelegate
#pragma mark - AdPlaybackSessionDelegate

- (void)sessionContentPause {
    // handle session pause ...
}

- (void)sessionContentResume {
    // handle session resume ...
}

@end
```


<span id="bab5f5d4"></span>
#### 實現 `VideoEngineDelegateProxy`

如果使用 `TTVideoEngine` 播放器，MediaAds 會設定自己的播放器委託以接收回撥。為防止覆蓋此委託，同時允許您的控制器接收事件，您必須實現代理。

該代理對 `mediaAdsDelegate` 和您的 `adsPlayerDelegate` 都採用弱引用，並在響應 selector 時將每個回撥轉發給雙方。

```objectivec
@interface VideoEngineDelegateProxy : NSObject <TTVideoEngineDelegate>

@property (nonatomic, weak) id<TTVideoEngineDelegate> mediaAdsDelegate;
@property (nonatomic, weak) id<TTVideoEngineDelegate> adsPlayerDelegate;

- (instancetype)initWithMediaAdsDelegate:(id<TTVideoEngineDelegate>)mediaAdsDelegate
                       adsPlayerDelegate:(id<TTVideoEngineDelegate>)adsPlayerDelegate;

@end

// proxy class for forwarding callbacks to both video engine delegates
@implementation VideoEngineDelegateProxy

- (instancetype)initWithMediaAdsDelegate:(id<TTVideoEngineDelegate>)mediaAdsDelegate
                       adsPlayerDelegate:(id<TTVideoEngineDelegate>)adsPlayerDelegate {
    self = [super init];
    if (self) {
        // keep a reference to the MediaAds delegate and our own delegate
        _mediaAdsDelegate = mediaAdsDelegate;
        _adsPlayerDelegate = adsPlayerDelegate;
    }
    return self;
}

#pragma mark - TTVideoEngineDelegate forwarding
// example callback forwarding method
- (void)videoEnginePrepared:(TTVideoEngine *)videoEngine {
    if ([self.mediaAdsDelegate respondsToSelector:@selector(videoEnginePrepared:)]) {
        [self.mediaAdsDelegate videoEnginePrepared:videoEngine];
    }
    if ([self.adsPlayerDelegate respondsToSelector:@selector(videoEnginePrepared:)]) {
        [self.adsPlayerDelegate videoEnginePrepared:videoEngine];
    }
}

// implement forwarding method for all other callbacks ...
@end
```


<span id="d187089c"></span>
### AdPlaybackSession 播放器

VideoOne 演示使用 `TTVideoEngine` 播放器，但只要符合 `PlayerWrapperDelegate` 協議，任何影片播放器都可建立 `AdPlaybackSession`。如果您選擇使用不同的播放器後端，這將提供更大的靈活性。

```objectivec
@protocol PlayerWrapperDelegate <NSObject, IMAContentPlayhead>

@property (nonatomic, weak) id<PlayerEventListenerDelegate> delegate;

@property (nonatomic, strong) AdSessionLog *mLog;

- (NSTimeInterval)getDuration;

- (nullable UIView *)getPlayerView;

- (NSTimeInterval)getPosition;

- (BOOL)isComplete;

- (BOOL)isPaused;

- (BOOL)isPlaying;

- (BOOL)isLooping;

- (void)mute:(BOOL)isMute;

- (void)pause;

- (void)releasePlayer;

- (void)seekTo:(NSTimeInterval)position;

- (void)play;

- (void)prepareToPlay;

- (void)stop;

- (void)setPlayerEventDelegate:(id<PlayerEventListenerDelegate> _Nonnull)delegate;

- (void)setIsCompletedForLoop:(BOOL)isCompleted;

@end
```
