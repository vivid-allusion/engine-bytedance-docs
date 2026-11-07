---
title: "Short drama videos - iOS integration"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-ios-integration"
---

To quickly add a feature\-rich short drama video experience to your iOS application, you can integrate the BytePlus VideoOne short drama demo. This guide provides step\-by\-step instructions to integrate the demo source code, customize the data layer for your business needs, and implement key features like paid content unlocking and screen capture protection.

<span id="c07773ac"></span>
# Overview of integration solutions

BytePlus VideoOne offers three integration solutions tailored for short drama videos. The table below highlights the distinctions among these three solutions.


|**Solution / Introduction** |**Integrating the short drama demo** |**Integrating the PlayerKit controls** |**Integrating the player SDK** |
|---|---|---|---|
|Description |Built for short drama videos. This solution supports screen capture protection, episode switching, resuming playback seamlessly when switching pages, unlocking paid content and other short drama\-specific features. |Built on the player SDK. This solution provides the ability to play videos on the View level and hides the player's implementation details. |This solution directly integrates the player SDK. |
|Target client |Clients who are developing new apps and are able to replace the business APIs. |Clients who are developing new apps or have existing apps and are able to replace the player architecture. |* Clients with existing apps who want to quickly release short drama features by reusing existing playback code and replacing the player engine.<br><br>* Clients with strong development capabilities, extensive player experience, and ample time for development. |
|Required development |Clients only need to replace the business APIs and convert the data structures. |Clients need to implement network connectivity, UI components for the short drama player, playback page switching, payment and other features themselves. |Clients need to implement the player features and short drama specific features themselves. |
|Time to market |As little as one week |Two weeks to one month |Approximately one month |
|Related links |This document |[MDPlayerKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama/Classes/Player) |[iOS Player SDK: Quickstart](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk) |


<span id="da38a728"></span>
# Running the demo

Before integrating the short drama demo, we recommend that you refer to the document [Running the demo (iOS)](https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-ios-) and try the short drama video features.

<span id="de1247be"></span>
# Integrating the short drama demo

The source code of the short drama demo is located in the [MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama) folder under the [VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS) repository. Its directory structure is as follows:

```Bash
.
├── VideoOne               # Project main entry
├── Component              # Component modules
│   ├── App                # App entry
│   ├── AppConfig          # App configs 
│   ├── ToolKit            # Toolkit
│   ├── LoginKit           # Login kit
│   ├── VideoPlaybackEdit  # Video playback scene
│   ├── MiniDrama          # Short drama scene
│   └── ...
```


<span id="24ac2979"></span>
## Step 1: Download the source code

Run the following commands to download the source code to your local device:

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions
cd Client/iOS
```


<span id="2f08751b"></span>
## Step 2: Copy the code

Copy the following folders to the root directory of your project：

```Bash
Component/App
Component/AppConfig
Component/ToolKit
Component/MiniDrama
Component/LoginKit
```


<span id="c1deef88"></span>
## Step 3: Configure the Podfile

Refer to [VideoOneSolutions/Client/iOS/Podfile](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Podfile) and copy the following dependencies to your own Podfile. If a dependency version in your project conflicts with a version required by the demo, your project's existing version takes precedence.

```Ruby
source 'https://cdn.cocoapods.org/'
source 'https://github.com/byteplus-sdk/byteplus-specs.git'
source 'https://github.com/volcengine/volcengine-specs.git'

platform :ios, '13.0'

target 'YourProjectTarget' do
    # use_frameworks!
    use_modular_headers!

    # pod 'App', :path => './Component/App'
    pod 'AppConfig', :path => './Component/AppConfig'
    pod 'ToolKit', :path => './Component/ToolKit'

    pod 'LoginKit', :path => './Component/LoginKit'
    pod 'MiniDrama', :path => './Component/MiniDrama'

    pod 'TTSDKFramework', 'x.x.x-premium', :subspecs => ['Player']

    pod 'AFNetworking', '~> 4.0'
    pod 'SDWebImage', '~> 5.12.0'
end
```


<span id="50cfde6e"></span>
## Step 4: Import the short drama module

The source code for the short drama module is located in the folder [VideoOneSolutions/Client/iOS/Component](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component). If you only need to integrate short drama videos, you only need copy the following folders: [App](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/App), [AppConfig](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/AppConfig), [ToolKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/ToolKit), [LoginKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/LoginKit)`,` and [MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama).

<span id="ee5031b1"></span>
## Step 5: Initialize the Player SDK

Refer to [MiniDrama.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Entry/MiniDrama.m) and initialize the Player SDK.

```objectivec
+ (void)setupTTSDK {
    #ifdef DEBUG
    [TTVideoEngine setLogFlag:TTVideoEngineLogFlagAll];
    #endif
    TTSDKConfiguration *cfg = [TTSDKConfiguration defaultConfigurationWithAppID:VODAPPID licenseName:VODLicenseName];
    cfg.channel = [NSBundle.mainBundle.infoDictionary objectForKey:@"CHANNEL_NAME"];
    cfg.appName = [NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleName"];
    cfg.bundleID = NSBundle.mainBundle.bundleIdentifier;
    cfg.appVersion = [NSBundle.mainBundle.infoDictionary objectForKey:@"CFBundleShortVersionString"];
    cfg.shouldInitAppLog = YES;
    cfg.serviceVendor = TTSDKServiceVendorSG;
    TTSDKVodConfiguration *vodConfig = [[TTSDKVodConfiguration alloc] init];
    vodConfig.cacheMaxSize = 300 * 1024 * 1024;
    cfg.vodConfiguration = vodConfig;
    [TTSDKManager setCurrentUserUniqueID:[LocalUserComponent userModel].uid ?: @""];
    [TTSDKManager setShouldReportToAppLog:YES];
    [TTSDKManager startWithConfiguration:cfg];
}
```


<span id="ea023424"></span>
## Step 6: Integrate the short drama pages

The [MiniDramaMainViewController](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaMainViewController.m) is the main view controller for short drama videos. It includes two default tabs: "Home" and "For you". You can develop more tabs according to your business needs. You can add the [MiniDramaMainViewController](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaMainViewController.m) to the `rootViewController` of the `UINavigationController` for integration.

<span id="7f60339e"></span>
# Tailoring to your business requirements

To quickly align the short drama demo with your business requirements, follow the steps below:


1. Customize the data layer to efficiently incorporate essential short drama video features. This involves:

   1. Replacing the business APIs: Implement the APIs defined in [MiniDrama/Main/Data/Network/NetworkingManager+MiniDrama.h](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h).

   2. Converting the data structure: Adapt the data structure received from your app server to match the structure defined in the short drama demo, enabling utilization of existing business workflows in the demo.

2. Customize short drama\-specific functionalities like unlocking paid content.


<span id="c52a5f7e"></span>
## Source code structure of the short drama demo

```Bash
├── VideoOne                   # Project main entry
├── Component                  # Component modules
│   ├── App                    # App entry
│   ├── AppConfig              # App configs 
│   ├── ToolKit                # Toolkit
│   ├── LoginKit               # Login kit
│   ├── VideoPlaybackEdit      # Video playback scene
│   ├── MiniDrama              # Short drama scene
        ├──Resources           # Short drama resources
        ├──Classes
            ├── Entry
            │    └── MiniDrama.m    # BytePlus VOD Player initialization config
            ├── Main
            │    ├── MiniDramaMainViewController.m # Short drama main controller
            │    ├── CommonUI   # Short drama common UI
            │    ├── Data
            │    │   ├── Model  # Short drama data model
            │    │   └── Network  # Short drama APIs
            │    ├── MiniDramaChannelPage  # For you page
            │    ├── MiniDramaHomePage   # Home page
            │    └── PlayerModules   # Player UI widgets
            └── Player        # Player kit
```


<span id="f94e0e14"></span>
## Adapting the data layer

<span id="286fa08e"></span>
### Converting the data structure

The short drama demo layer has defined data structures including [MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h) (short drama information), [MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h) (short drama episode information), and [MDSimpleEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDSimpleEpisodeInfoModel.h) (episode unlocking information). You will be required to convert the data structures received from your app server into these data structures. The table below details these data structures.


|**Class** |**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|---|
|[MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h)<br><br>（Short drama info） |dramaId |NSString |Required |Short drama ID |
||dramaTitle |NSString |Required |Short drama name |
||dramaCoverUrl |NSString |Required |Short drama cover URL |
||dramaPlayTimes |NSInteger |Required |Playback count |
||dramaDisplayType |MiniDramaVideoDisplayType |Required |Video orientation<br><br>0 : MiniDramaVideoDisplayTypeVertical<br><br>1 : MiniDramaVideoDisplayTypeHorizontal |
||dramaLength |NSInteger |Required |Total number of episodes |
||newReleased |BOOL |Optional |Whether to display a "New" label (NO by default).<br><br>YES : Display<br><br>NO : Hide |
|[MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h)<br><br>（Episode info） |videoId |NSString |Required |Video ID |
||dramaTitle |NSString |Optional |Short drama name |
||duration |NSString |Required |Video duration (in seconds) |
||coverUrl |NSString |Required |Video cover URL |
||playAuthToken |NSString |Optional |The PlayAuthToken for the video, issued by your app server via the BytePlus VOD Server SDK. |
||subtitleToken |NSString |Optional |The subtitle token for the video's data source which can be issued by the AppServer through the BytePlus VOD Server SDK. |
||playTimes |NSInteger |Optional |Playback count |
||videoTitle |NSString |Optional |Video title |
||videoDescription |NSString |Optional |Subheading of the video |
||createTime |NSString |Optional |Time of uploading in *RFC3339* format |
||authorName |NSString |Optional |Uploader name |
||authorId |NSString |Optional |Uploader's userId |
||likeCount |NSUInteger |Optional |Number of likes |
||commentCount |NSUInteger |Optional |Number of comments |
||videoHeight |NSString |Required |Video height |
||videoWidth |NSString |Required |Video width |
||order |NSInteger |Required |Video position in the episode list |
||dramaId |NSString |Required |Short drama ID |
||vip |BOOL |Required |Whether payment is required to unlock (NO by default). |
||displayType |MDDisplayCardType |Required |Display type of the short drama card on the "For you" page<br><br>0 : MDDisplayCardTypeDefault, without cover image<br><br>1 : MDDisplayCardTypeCard, with cover image |
|[MDSimpleEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDSimpleEpisodeInfoModel.h)<br><br>（Episode unlocking info） |subtitleToken |NSString |Required |The subtitle token for the video's data source which can be issued by the AppServer through the BytePlus VOD Server SDK. |
||videoId |NSString |Required |Video ID |
||order |NSInteger |Optional |Video position in the episode list |
||playAuthToken |NSString |Required |The PlayAuthToken for the video, issued by your app server via the BytePlus VOD Server SDK. |


<span id="2a50ed4a"></span>
### Replacing the business APIs


1. Update the "Home" page API: Refer to the [getDramaDataForHomePageData](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API of the [NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) object to implement an API that fetches short drama recommendations for the "Home" page. You can change the API request to your own request and encapsulate the requested data as an [MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h) object and return it to the page for display. If the fields in the current [MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h) object do not meet your business needs, you can also modify the source code to add more fields.


```objectivec
// NetworkingManager+MiniDrama.m

@implementation NetworkingManager (MiniDrama)

+ (void)getDramaDataForHomePageData:(void (^__nullable)(MDHomePageData *))success
                            failure:(void (^__nullable)(NSString *_Nonnull))failure {
    [NetworkingManager postWithPath:@"drama/v1/getDramaChannel"
                         parameters:@{}
                              block:^(NetworkingResponse *_Nonnull response) {
        if (!response.result) {
            if (failure) {
                failure(response.error.localizedDescription);
            }
            return;
        }
        MDHomePageData *pageData = [[MDHomePageData alloc] init];
        if ([response.response isKindOfClass:[NSDictionary class]]) {
            NSDictionary *dic = (NSDictionary *)response.response;
            pageData = [MDHomePageData yy_modelWithDictionary:dic];
        }
        if (success) success(pageData);
        
    }];
}

@end
```



2. Update the "Info" page API: Refer to the [getDramaDataForDetailPage](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API of the [NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) object to implement an API that gets short drama information for the "Info" page. You can change the API request to your own request and encapsulate the requested data as an [MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h) object and return it to the page for display. If the fields in the current [MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h) object cannot meet your business needs, you can also modify the source code to add more fields.


```objectivec
// NetworkingManager+MiniDrama.m

@implementation NetworkingManager (MiniDrama)

+ (void)getDramaDataForDetailPage:(NSString *)dramaId 
                          success:(void (^)(NSArray<MDDramaEpisodeInfoModel *> * _Nonnull))success
                          failure:(void (^)(NSString * _Nonnull))failure {
    NSDictionary *param = @{ @"drama_id": dramaId, @"user_id": [LocalUserComponent userModel].uid};
    [NetworkingManager postWithPath:@"drama/v1/getDramaList"
                         parameters:param
                              block:^(NetworkingResponse * _Nonnull response) {
        if (!response.result) {
            if (failure) {
                failure(response.error.localizedDescription);
            }
            return;
        }
        NSMutableArray *dramaDataList = [[NSMutableArray alloc] init];
        if ([response.response isKindOfClass:[NSArray class]]) {
            NSArray *arr = (NSArray *)response.response;
            for (NSDictionary *dic in arr) {
                MDDramaEpisodeInfoModel *infoModel = [MDDramaEpisodeInfoModel yy_modelWithDictionary:dic];
                [dramaDataList addObject:infoModel];
            }
        }
        if (success) success(dramaDataList);
    }];
}
@end
```



3. Update the "For you" page API: Refer to the [getDramaDataForChannelPage](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API of the [NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) object to implement an API that gets short drama lists on the "For you" page. Customize the API request as needed and package the retrieved data into an [MDDramaFeedInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaFeedInfo.h) object to be returned for display on the page. If the existing fields within the [MDDramaFeedInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaFeedInfo.h) object do not align with your business requirements, you have the flexibility to enhance the source code by adding additional fields.


```objectivec
// NetworkingManager+MiniDrama.m
@implementation NetworkingManager (MiniDrama)

+ (void)getDramaDataForChannelPage:(NSRange)range 
                           success:(void (^)(NSArray<MDDramaFeedInfo *> * _Nonnull))success
                           failure:(void (^)(NSString * _Nonnull))failure {
    NSDictionary *param = @{ @"offset": @(range.location), @"page_size": @(range.length)};
    [NetworkingManager postWithPath:@"drama/v1/getDramaFeed"
                         parameters:param
                              block:^(NetworkingResponse * _Nonnull response) {
        if (!response.result) {
            if (failure) {
                failure(response.error.localizedDescription);
            }
            return;
        }
        NSMutableArray *dramaDataList = [[NSMutableArray alloc] init];
        if ([response.response isKindOfClass:[NSArray class]]) {
            NSArray *arr = (NSArray *)response.response;
            for (NSDictionary *dic in arr) {
                MDDramaFeedInfo *infoModel = [MDDramaFeedInfo yy_modelWithDictionary:dic];
                [dramaDataList addObject:infoModel];
            }
        }
        if (success) success(dramaDataList);
    }];
}
@end
```


<span id="9fede04f"></span>
## Customizing short drama\-specific features

<span id="e220d76c"></span>
### Screen capture protection

Refer to [MDVideoPlayerController+DisRecordScreen.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Player/MDPlayerKit/Classes/PlayerCore/MDVideoPlayerController%2BDisRecordScreen.m) to implement anti\-screen recording through monitoring system screen capture events.

```objectivec
- (void)registerScreenCapturedDidChangeNotification {
    if (@available(iOS 11.0, *)) {
        [[NSNotificationCenter defaultCenter] removeObserver:self name:UIScreenCapturedDidChangeNotification object:nil];
        [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onScreenCapturedChange:) name:UIScreenCapturedDidChangeNotification object:nil];
    }
}

- (void)onScreenCapturedChange:(NSNotification *)notification {
    if (@available(iOS 11.0, *)) {
        UIScreen *screen = notification.object;
        if (screen) {
            if ([screen isCaptured]) {
                // Screen capture started.
            } else {
                // Screen capture stopped.
            }
        }
    }
}
```


<span id="b3cb0dac"></span>
### Unlocking paid content

The process for unlocking and playing paid content in the short drama demo is shown in the image below.

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MjZweCIgaGVpZ2h0PSI4MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDkyNiA4MDciPjxkZWZzLz48Zz48cmVjdCB4PSI0MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNDA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRyYW1hIFNjZW5lIEtpdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAzIiB5PSIzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjNweDsgbWFyZ2luLWxlZnQ6IDIwNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNjA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBheW1lbnQgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogODA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXltZW50IFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MyA1MyBMIDYzIDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iNzQwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjMgODAzIEwgNjMgNzkzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIuNTggNTMgTCAyNjIuNSA0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDYzIDgwMyBMIDQ2Mi41IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjMuMzEgMzEzIEwgNjY0IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NjIuOTIgMzQzIEwgODYyLjUgNDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSIyNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iMTEwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDQzMyBMIDI2MyAxNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2IDczIEwgMjQ0Ljc2IDczLjk1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTAuNzYgNzMuOTkgTCAyNDIuNzQgNzcuOTQgTCAyNDQuNzYgNzMuOTUgTCAyNDIuNzkgNjkuOTQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NHB4OyBtYXJnaW4tbGVmdDogMTY1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bMV1nZXREcmFtYUxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA4MC41IEwgMzQzIDgwLjUgUSAzNTMgODAuNSAzNTMgOTAuNSBMIDM1MyAxMjUuNSBRIDM1MyAxMzUuNSAzNDMgMTM1LjUgTCAyODEuMjQgMTM1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3NS4yNCAxMzUuNSBMIDI4My4yNCAxMzEuNSBMIDI4MS4yNCAxMzUuNSBMIDI4My4yNCAxMzkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwOXB4OyBtYXJnaW4tbGVmdDogMzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzEuMV1VbmxvY2tlZCBlcGlzb2RlczxiciAvPsKgbm8gcGxheWJhY2sgYXV0aCB0b2tlbi91cmw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU0IDE0OS40NyBMIDg1LjI0IDE0Ny44IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5LjI0IDE0Ny43NCBMIDg3LjI4IDE0My44MiBMIDg1LjI0IDE0Ny44IEwgODcuMiAxNTEuODIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDlweDsgbWFyZ2luLWxlZnQ6IDE2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlsyXVJldHVybiBkcmFtYUxpc3Q8YnIgLz57RHJhbWFGZWVkW119PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NTMiIHk9IjE4MyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjgwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzYgMTkzIEwgNDQxLjc2IDE5Ni40NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQ3Ljc2IDE5Ni41IEwgNDM5LjczIDIwMC40MiBMIDQ0MS43NiAxOTYuNDQgTCA0MzkuOCAxOTIuNDIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTVweDsgbWFyZ2luLWxlZnQ6IDI2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzNdc2V0SXRlbXModmlkZW9JdGVtc1tdKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDczIDIwMyBMIDUzMyAyMDMgUSA1NDMgMjAzIDU0MyAyMTMgTCA1NDMgMjMzIFEgNTQzIDI0MyA1MzMgMjQzIEwgNDgxLjI0IDI0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjI0IDI0MyBMIDQ4My4yNCAyMzkgTCA0ODEuMjQgMjQzIEwgNDgzLjI0IDI0NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyM3B4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzMuMV1QcmV2aWV3L1BsYXliYWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTMiIHk9IjMxMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjI0MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2NCA4MDMgTCA2NjMuMzIgNTUzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MyAzMjMgTCA2MzkuNzYgMzI0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY0NS43NiAzMjQuNTEgTCA2MzcuNzUgMzI4LjQ5IEwgNjM5Ljc2IDMyNC41IEwgNjM3Ljc3IDMyMC40OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyNHB4OyBtYXJnaW4tbGVmdDogMzYxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNF1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODUzIiB5PSIzNDMiIHdpZHRoPSIyMCIgaGVpZ2h0PSIxMjAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA4NjMgODAzIEwgODYzIDQ2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjczIDM1MyBMIDg0NC43NyAzNTYuODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC43NiAzNTYuOTUgTCA4NDIuNjggMzYwLjc3IEwgODQ0Ljc3IDM1Ni44MiBMIDg0Mi44NiAzNTIuNzcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTVweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzQuMV1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA4NTMgMzkzIEwgNjgxLjI0IDM5NS4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzUuMjQgMzk1LjIgTCA2ODMuMTkgMzkxLjEgTCA2ODEuMjQgMzk1LjEzIEwgNjgzLjI4IDM5OS4xIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzk0cHg7IG1hcmdpbi1sZWZ0OiA3NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bNC4yXVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNTMiIHk9IjQzMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjkwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDU3MyBMIDI2MyA1MjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MyA0NDMgTCAyODIuMjQgNDQ1LjQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3Ni4yNCA0NDUuNSBMIDI4NC4yMiA0NDEuNDcgTCAyODIuMjQgNDQ1LjQ3IEwgMjg0LjI1IDQ0OS40NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0NHB4OyBtYXJnaW4tbGVmdDogNTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzQuM11Ob3RpZnkgcGF5IHN1Y2Nlc3Mob3JkZXJJZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjUzIDU0Mi45MiBMIDg2LjI0IDU0NC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MC4yNCA1NDQuMzUgTCA4OC4yMyA1NDAuMzMgTCA4Ni4yNCA1NDQuMzQgTCA4OC4yNSA1NDguMzMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NDRweDsgbWFyZ2luLWxlZnQ6IDM2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls1XVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA0NTUuNSBMIDMzMyA0NTUuNSBRIDM0MyA0NTUuNSAzNDMgNDY1LjUgTCAzNDMgNDkwLjUgUSAzNDMgNTAwLjUgMzMzIDUwMC41IEwgMjgxLjI0IDUwMC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNzUuMjQgNTAwLjUgTCAyODMuMjQgNDk2LjUgTCAyODEuMjQgNTAwLjUgTCAyODMuMjQgNTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzlweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+WzQuNF08Zm9udCBzdHlsZT0iZm9udC1zaXplOjEzcHgiPlJlY29yZCA8YnIgLz5wYXltZW50IHN0YXR1czwvZm9udD48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDczIDI2MyBMIDEzMyAyNjMgUSAxNDMgMjYzIDE0MyAyNzMgTCAxNDMgMjkzIFEgMTQzIDMwMyAxMzMgMzAzIEwgODEuMjQgMzAzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NS4yNCAzMDMgTCA4My4yNCAyOTkgTCA4MS4yNCAzMDMgTCA4My4yNCAzMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODNweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXY+U3dpcGUgdG88L2Rpdj48ZGl2PnVubG9ja2VkIGVwaXNvZGU8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MyIgeT0iNTczIiB3aWR0aD0iMjAiIGhlaWdodD0iOTAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNjMgODAzIEwgMjYzIDY2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMgNTgzIEwgMjQ0Ljc2IDU4MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjUwLjc2IDU4MyBMIDI0Mi43NiA1ODcgTCAyNDQuNzYgNTgzIEwgMjQyLjc2IDU3OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU3M3B4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNl1nZXREcmFtYURldGFpbChvcmRlcklkKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjUzIDY0NC43NSBMIDE3MyA2NDMuMTkgUSAxNjMgNjQzIDE1MyA2NDMgTCA4NC4yNCA2NDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzguMjQgNjQzIEwgODYuMjQgNjM5IEwgODQuMjQgNjQzIEwgODYuMjQgNjQ3IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjIzcHg7IG1hcmdpbi1sZWZ0OiAxNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bN11SZXR1cm4gRHJhbWFVbmxvY2sgbWV0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUzIiB5PSI2NzAiIHdpZHRoPSIyMCIgaGVpZ2h0PSI4MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MyA2OTAgTCA1MzMgNjkwIFEgNTQzIDY5MCA1NDMgNzAwIEwgNTQzIDcyMCBRIDU0MyA3MzAgNTMzIDczMCBMIDQ4MS4yNCA3MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ3NS4yNCA3MzAgTCA0ODMuMjQgNzI2IEwgNDgxLjI0IDczMCBMIDQ4My4yNCA3MzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MTBweDsgbWFyZ2luLWxlZnQ6IDU0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls4LjFdUHJldmlldy9QbGF5YmFjazwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3OSA2NzMgTCA0NDQuNzYgNjc2LjQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0NTAuNzYgNjc2LjUgTCA0NDIuNzMgNjgwLjQyIEwgNDQ0Ljc2IDY3Ni40NCBMIDQ0Mi44IDY3Mi40MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3NXB4OyBtYXJnaW4tbGVmdDogMjY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bOF1hcHBlbmRJdGVtcyh2aWRlb0l0ZW1zW10pPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

The demo implements a complete process for unlocking paid content, but no third\-party SDK is integrated. It only has a simulated payment process in [MiniDramaDetailFeedViewController.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaChannelPage/DramaDetailPage/MiniDramaDetailFeedViewController.m), which will need to be replaced with your own code.

```objectivec
- (void)unlockEpisodes:(NSArray<MDDramaEpisodeInfoModel *> *)needPayArr {
    NSMutableArray  *vidList = [[NSMutableArray alloc] initWithCapacity:needPayArr.count];
    [needPayArr enumerateObjectsUsingBlock:^(MDDramaEpisodeInfoModel * _Nonnull obj, NSUInteger idx, BOOL * _Nonnull stop) {
        [vidList addObject:obj.videoId];
    }];
    // ...
    [NetworkingManager getDramaDataForPaymentEpisodeInfo:[LocalUserComponent userModel].uid
                                                 dramaId:self.fromDramInfo.dramaId
                                                 vidList:[vidList copy]
                                                 success:^(NSArray<MDSimpleEpisodeInfoModel *> * _Nonnull videoList) {
        // success
    } failure:^(NSString * _Nonnull errMessage) {
        // failure
    }];
}
```
