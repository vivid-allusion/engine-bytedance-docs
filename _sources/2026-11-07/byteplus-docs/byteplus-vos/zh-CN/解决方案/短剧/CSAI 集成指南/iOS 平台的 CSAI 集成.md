---
title: "iOS 平台的 CSAI 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/csai-integration-for-ios-zh-CN"
---

本指南介绍如何在 iOS 上将 BytePlus MediaAds SDK 和 Google IMA SDK 集成到基于 VideoOne 的短剧应用中。

<span id="39e090fd"></span>
## 前置条件

在开始之前，请确保您具备以下条件：


1. **现有集成**：您已集成 VideoOne 短剧解决方案（详见[短剧视频 - iOS 集成](https://docs.byteplus.com/docs/byteplus-vos/short-drama-videos-ios-integration-zh-CN)）。

2. **广告标签 URL**：您需要一个有效的 VAST/VMAP 广告标签 URL。

   * 测试时：您可以使用 [Google 的 VAST 标签示例](https://developers.google.com/interactive-media-ads/docs/sdks/html5/client-side/tags)。

   * 生产环境：请从您的广告服务器（如 Google Ad Manager）获取广告标签 URL。

3. **最低 SDK 要求**：

   * `iOS 部署目标`：14.0 或更高版本。


<span id="dc415611"></span>
## SDK 集成

请按照以下步骤将 MediaAds SDK 集成到您的 iOS 项目中。


1. **引入 BytePlus CocoaPods 规格仓库**：在 `Podfile` 中添加 BytePlus 规格仓库以访问 SDK。

   ```Ruby
   # Source BytePlus's CocoaPods specs repo in the Podfile
   source 'https://github.com/byteplus-sdk/byteplus-specs.git'
   ```
   

2. **设置 iOS 最低版本**：确保您的项目目标为 iOS 14.0 或更高，这是 MediaAds SDK 的最低要求。

   ```Ruby
   # Minimum required version is at least 14.0
   platform :ios, '14.0'
   ```
   

3. **添加 MediaAds SDK 依赖项**：为短剧 In\-Stream Ads 场景定义新的 pod 集，并将其包含到您的 target 中。

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
## 快速开始

<span id="543fb340"></span>
### 通用指南

MediaAds SDK 设计为播放器无关。为适配任意播放器，提供了名为 `AdPlaybackSession` 的实体，用于封装内容播放器和广告播放器，并协调主内容中的广告插入。

请按照以下步骤创建 `AdSchedule` 并构建 `AdPlaybackSession`。


1. 创建 `MediaAdsInitConfig`：使用您的应用 ID、名称和渠道初始化配置对象。

   ```objectivec
   MediaAdsInitConfig *config = [[MediaAdsInitConfig alloc] init];
   config.appID = VODAPPID;
   config.appName = [NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleName"];
   config.appChannel = [NSBundle.mainBundle.infoDictionary objectForKey:@"CHANNEL_NAME"];
   ```
   

2. 创建 `AdSchedule`：定义内容的广告插播点。在本示例中，我们通过 VAST 标签 URL 配置了前贴片、中贴片和后贴片广告。

   ```objectivec
   AdSchedule *adSchedule = [[AdSchedule alloc] init];
   
   // Add pre-roll ad with VAST tags (offset: "pre")
   [adSchedule addLinearAdWithOffset:@"pre" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?iu=/21775744923/external/single_preroll_skippable&sz=640x480&ciu_szs=300x250%2C728x90&gdfp_req=1&output=vast&unviewed_position_start=1&env=vp&correlator="];
   
   // Add mid-roll ad with VAST tags (offset: "00:00:15")
   [adSchedule addLinearAdWithOffset:@"00:00:15" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_skip_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dmidskiponly&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=midroll&pod=1&ppos=1&min_ad_duration=0&max_ad_duration=30000&vrid=1445984&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
   
   // Add post-roll ad with VAST tags (offset: "post")
   [adSchedule addLinearAdWithOffset:@"post" adTagUrl:@"https://pubads.g.doubleclick.net/gampad/ads?slotname=/21775744923/external/vmap_ad_samples&sz=640x480&ciu_szs=300x250&cust_params=sample_ar%3Dpremidpost&url=&unviewed_position_start=1&output=xml_vast3&impl=s&env=vp&gdfp_req=1&ad_rule=0&vad_type=linear&vpos=postroll&pod=3&ppos=1&lip=true&min_ad_duration=0&max_ad_duration=30000&vrid=1264775&cmsid=496&video_doc_id=short_onecue&kfa=0&tfcd=0"];
   ```
   

3. 创建 `AdPlaybackSession`：实例化会话，将其绑定到您的视图和视图控制器，并启动。

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
### 与 VideoOne 集成

<span id="b4ffab7e"></span>
#### 实现 `MDVideoWithAdsPlayerController`

`MDVideoWithAdsPlayerController` 类继承自 `MDVideoPlayerController`。它重写了播放方法，将控制权委托给 `MediaAds` 会话，而不是直接操作视频播放器。

该类的主要职责：


1. **初始化广告会话**：创建 `AdPlaybackSession` 并绑定广告容器视图。

2. **拦截播放指令**：重写 `play`、`pause` 和 `stop`，通过 `adPlaybackSession` 路由这些指令。

3. **代理委托回调**：使用 `VideoEngineDelegateProxy`，确保广告会话和应用都能收到播放器事件。

4. **动态调度广告**：在 `videoEnginePrepared` 回调中配置 `AdSchedule`，当视频时长已知时。


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
#### 实现 `VideoEngineDelegateProxy`

如果使用 `TTVideoEngine` 播放器，MediaAds 会设置自己的播放器委托以接收回调。为防止覆盖此委托，同时允许您的控制器接收事件，您必须实现代理。

该代理对 `mediaAdsDelegate` 和您的 `adsPlayerDelegate` 都采用弱引用，并在响应 selector 时将每个回调转发给双方。

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

VideoOne 演示使用 `TTVideoEngine` 播放器，但只要符合 `PlayerWrapperDelegate` 协议，任何视频播放器都可创建 `AdPlaybackSession`。如果您选择使用不同的播放器后端，这将提供更大的灵活性。

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
