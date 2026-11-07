---
title: "在 iOS 上實現媒體上下滑動"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/Implementing-media-up-and-down-swiping-for-iOS-zh-TW"
---

為了在您的 iOS 應用中建立高效能、可滑動的媒體資訊流，本指南為點播（VOD）和直播內容提供最佳化策略。您將學習如何使用 BytePlus VOD SDK 實現短影片的預載入和預渲染，以及使用 BytePlus MediaLive SDK 對直播內容進行預流，確保使用者滑動時播放體驗流暢、緩衝最小。

<span id="a04bd286"></span>
# 開發環境


* Xcode 14.0 或更高版本。

* CocoaPods 1.10.0 或更高版本

* 執行 iOS 13.0 或更高版本的實體移動裝置。


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">暫不支援模擬器。</div>


<span id="3d1ba1f0"></span>
# 前置條件


* 擁有一個有效的 [BytePlus 賬號](http://console.byteplus.com/)，並已啟用 [BytePlus VOD](https://console.byteplus.com/vodpaas) 和 [BytePlus MediaLive](https://console.byteplus.com/live)。

* 在 [SDK 管理](https://console.byteplus.com/vodpaas/sdk/)頁面的 [BytePlus VOD 控制檯](https://docs.byteplus.com/en/byteplus-vod/docs/sdk-management)上完成以下操作：

   * 建立應用並獲取應用 ID 及應用英文名稱。

   * 為應用註冊，併購買及下載用於 Player 的許可證。

   * 需要高階版 SDK 與許可證以支援 預載入和預渲染。

      * [Player SDK 功能](https://docs.byteplus.com/docs/byteplus-vod/docs-player-features)

      * [iOS Player SDK：自定義預載入](https://docs.byteplus.com/en/docs/byteplus-vod/docs-custom-preloading-ios)

* 已完成 [直播基礎配置](https://docs.byteplus.com/en/byteplus-media-live/docs/getting-started)。

* 已獲得 BytePlus MediaLive SDK 許可證。

   * 有關獲取許可證的詳細說明，請參見 [訪問您的 SDK 許可證](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-sdk-management#accessing-your-sdk-license)。

   * 如需瞭解如何選擇適合您需求的許可證型別，請參考 [SDK 介紹](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-introduction)。


<span id="c4e0d0bf"></span>
# 版本要求


* 要訪問 **影片播放**和**直播**功能，必須使用 BytePlus VOD 和 BytePlus MediaLive SDK。

> 有關各方案所用 SDK 的對應版本，請參見[客戶端 SDK 元件](https://docs.byteplus.com/docs/byteplus-vos/docs-version-combination-zh-TW)。


<span id="8cf67321"></span>
# 整合

<span id="4e4b9a14"></span>
## 步驟 1：修改 Podfile

在專案目錄中按如下方式修改 Podfile：

```Ruby
source 'https://cdn.cocoapods.org/'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'

$RTC_SDK = 'TTSDK/RTCSDK'
target 'YourProjectTarget' do
  # BytePlus VOD SDK and MediaLive SDK dependencies
  pod 'TTSDK', '1.43.300.2-premium', :subspecs => ['LivePull-RTS', 'Player', 'RTCSDK']
end
```


<span id="e1b77a40"></span>
## 步驟 2：安裝 Podfile 中列出的指定依賴項

要完成 SDK 安裝，請在終端執行 `pod install`。安裝成功後，可開啟生成的 `VideoOne.xcworkspace` 檔案配置專案。

```Bash
pod install
```


<span id="b1d3e711"></span>
# 實現

<span id="9f99730b"></span>
## 短影片最佳化策略

<span id="16117a3f"></span>
### 步驟 1：實現影片播放

如需整合 BytePlus VOD 播放器實現影片播放功能，可參考[在 iOS 上實現影片播放](https://docs.byteplus.com/docs/byteplus-vos/docs-implementing-video-playback-edit-for-ios-zh-TW)。

<span id="3fd93a31"></span>
### 步驟 2：啟用 BytePlus VOD 播放器的預載入與預渲染策略

呼叫 [TTVideoEngine:enableEngineStrategy: scene:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#enableenginestrategy-scene) 啟用預載入與預渲染策略

```objectivec
- (void)startVideoStrategy {
    [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreload scene:TTVEngineStrategySceneSmallVideo];
    [TTVideoEngine enableEngineStrategy:TTVideoEngineStrategyTypePreRender scene:TTVEngineStrategySceneSmallVideo];
    [TTVideoEngine setPreRenderVideoEngineDelegate:self];
}
```


<span id="47c37d97"></span>
### 步驟 3：設定預載入源

在適當時機將播放列表設定為預載入源，例如影片播放列表的網路請求返回後。


1. 首次載入播放源資料或重新整理頁面顯示新資料時，呼叫 [TTVideoEngine:setStrategyVideoSources:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#setstrategyvideosources)。

2. 載入更多資料時，呼叫 [TTVideoEngine:addStrategyVideoSources:](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#addstrategyvideosources)。

> 在此場景下，點播媒體與直播媒體混合，因此設定預載入源時需排除直播媒體。否則可能導致意外問題。


根據所提供的播放列表，BytePlus VOD SDK 會根據當前播放狀態自動管理預載入的時機與配置，如併發預載入數量及資料大小。

```objectivec
// Set preload sources
- (void)configVideoEngineStrategyMediaSources:(NSArray<VEVideoModel *> *)videoModels refresh:(BOOL)refresh {
    NSMutableArray *sources = [NSMutableArray array];
    [videoModels enumerateObjectsUsingBlock:^(VEVideoModel * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
        [sources addObject:[VEVideoModel videoEngineVidSource:obj]];
    }];
    if (refresh) { 
        /// Called when loading for the first time or refreshing the list
        [TTVideoEngine setStrategyVideoSources:sources];
    } else { 
        /// Called when loading more by scrolling up
        [TTVideoEngine addStrategyVideoSources:sources];
    }
}
```


<span id="b22f4dfa"></span>
### 步驟 4：封面展示與預渲染

開啟預渲染後，SDK 會根據您提供的播放列表提前建立播放器，並在播放當前影片時對播放列表中的下一個影片進行解碼和渲染。透過呼叫[TTVideoEngine:getPreRenderVideoEngineWithVideoSource: ](https://docs.byteplus.com/en/docs/byteplus-vod/docs-ios-player-sdk-api-details#getprerendervideoenginewithvideosource)，可以判斷預渲染是否完成。

在滑動影片流場景下，當下一個影片即將顯示時，我們會載入其封面圖片。如果此時影片已完成預渲染，則不再載入封面圖片，直接使用影片的首幀作為封面。

```objectivec
// using the prerendered player.
TTVideoEngine *preRenderVideoEngine = [TTVideoEngine getPreRenderFinishedVideoEngineWithVideoSource:mediaSource];
// set prerendered player scaling mode
[preRenderVideoEngine setOptionForKey:VEKKeyViewScaleMode_ENUM value:@(TTVideoEngineScalingModeAspectFill)];
if (preRenderVideoEngine) {
    preRenderVideoEngine.playerView.hidden = NO;
    preRenderVideoEngine.playerView.backgroundColor = [UIColor clearColor];
    // hide image cover
    self.posterImageView.hidden = YES;
    // attach prerender view
    [self.view insertSubview:preRenderVideoEngine.playerView aboveSubview:self.posterImageView];
    [preRenderVideoEngine.playerView mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.equalTo(self.view);
    }];
    return;
}
// prerender not ready, using image cover
self.posterImageView.hidden = NO;
[self.posterImageView sd_setImageWithURL:[NSURL URLWithString:[self __getBackgroudImageUrl:mediaSource]] completed:nil];
```


<span id="7419411b"></span>
### 步驟 5：播放影片

播放下一個影片時，若預渲染已完成，則直接使用預渲染播放器；否則新建一個播放器。

```objectivec
TTVideoEngine *preRenderVideoEngine = [TTVideoEngine getPreRenderVideoEngineWithVideoSource:mediaSource];
if (preRenderVideoEngine) {
    self.videoEngine = nil;
    self.videoEngine = preRenderVideoEngine;
} else {
    self.videoEngine = [[TTVideoEngine alloc] initWithOwnPlayer:YES];;
}
```


<span id="46d1216b"></span>
## 直播流最佳化策略

<span id="87c5e4a2"></span>
### 步驟 1：初始化 SDK

使用如下程式碼初始化 SDK：

```objectivec
#import <TTSDK/TTSDKManager.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Your code.
    [self configTTSDK];
    // Your code.
    return YES;
}

- (void)configTTSDK {
    // Create TTSDKConfiguration with your App ID.
    TTSDKConfiguration *configuration = [TTSDKConfiguration defaultConfigurationWithAppID:@"Your App ID"];
    // Configure information about your SDK application.
    configuration.appName = @"Your application name";
    configuration.channel = @"Your app channel";
    configuration.bundleID = @"Your bundle ID";
    
    // Configure the URI of your license file.
    configuration.licenseFilePath = [NSBundle.mainBundle pathForResource:@"Your license path" ofType:nil];
    
    // Pass TTSDKConfiguration to TTSDKManager.
    [TTSDKManager startWithConfiguration:configuration];
}
```


<span id="9ee7765d"></span>
### 步驟 2：初始化播放器

```objectivec
- (void)setupPlayer {
    _playerManager = [[TVLManager alloc] initWithOwnPlayer:YES];
    if (!_playerManager) {
        return;
    }

    VeLivePlayerConfiguration *config = [[VeLivePlayerConfiguration alloc] init];
    config.enableStatisticsCallback = YES;
    [self.playerManager setConfig:config];
    
    [self.playerManager setPlayerViewRenderType:(TVLPlayerViewRenderTypeMetal)];
    [self.playerManager setObserver:self];
    [self.playerManager setProjectKey:[NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleName"]];
}
```


<span id="676a7e04"></span>
### 步驟 3：預載入流

滑動開始時將流靜音，滑動完成後取消靜音。

```objectivec
- (void)partiallyShow {
    [self.view  addSubview:self.playerContainer]
    [self.playerContainer mas_makeConstraints:^(MASConstraintMaker *make) {
        make.edges.equalTo(streamView);
    }];

    [self.playerManager setPlayUrl:url];
    [self.playerManager play];
    [self.player setMute:YES];
}
```


<span id="cdf30ccd"></span>
### 步驟 4：取消靜音

當前檢視顯示時取消流靜音

```objectivec
- (void)completelyShow {
   [self.player setMute:NO];
}
```


<span id="e050c92c"></span>
### 步驟 5：播放器狀態重置

當前影片滑出後，重置播放狀態並停止流。

```objectivec
- (void)endShow {
    [self.playerManager stop];
}
```
