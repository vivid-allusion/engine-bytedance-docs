---
title: "短剧视频 - iOS 集成"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-videos-ios-integration-zh-CN"
---

要快速为您的 iOS 应用添加功能丰富的短剧视频体验，您可以集成 BytePlus VideoOne 短剧 Demo。本指南提供分步说明，帮助您集成 Demo 源代码、根据业务需求定制数据层，并实现付费内容解锁和屏幕截图保护等关键功能。

<span id="c07773ac"></span>
# 集成方案概述

BytePlus VideoOne 提供三种针对短剧视频的集成方案。下表突出显示了这三种方案之间的区别。


|**方案 / 介绍** |**短剧 Demo 集成** |**PlayerKit 控件集成** |**播放器 SDK 集成** |
|---|---|---|---|
|方案说明 |专为短剧视频打造。本方案支持防录屏、剧集切换、页面切换无缝续播、付费内容解锁等短剧专项功能。 |基于播放器 SDK 构建。本方案支持在 View 层播放视频，并隐藏播放器实现细节。 |本方案直接集成播放器 SDK。 |
|适用客户 |正在开发新应用且可替换业务 API 的客户。 |正在开发新应用或已有应用且可替换播放器架构的客户。 |* 已有应用、希望通过复用现有播放代码并替换播放器引擎，快速上线短剧功能的客户。<br><br>* 具备较强开发能力、丰富播放器经验且开发周期充裕的客户。 |
|开发要求 |客户仅需替换业务 API 并完成数据结构转换。 |客户需自行实现网络连接、短剧播放器 UI 组件、播放页面切换、支付等功能。 |客户端需自行实现播放器功能及短剧相关功能。 |
|上线时间 |最快一周 |两周至一个月 |约一个月 |
|相关链接 |本文档 |[MDPlayerKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama/Classes/Player) |[iOS 播放器 SDK：快速入门](https://docs.byteplus.com/en/docs/byteplus-vod/docs-getting-started-with-the-ios-player-sdk) |


<span id="da38a728"></span>
# 运行 Demo

在集成短剧 Demo 之前，建议您参考文档[运行 Demo (iOS)](https://docs.byteplus.com/docs/byteplus-vos/docs-running-the-demo-ios--zh-CN)并体验短剧视频功能。

<span id="de1247be"></span>
# 集成短剧 Demo

短剧 Demo 的源代码位于[MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama)文件夹下的[VideoOneSolutions](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS)仓库中。其目录结构如下：

```Bash
.
├── VideoOne               # 项目主入口
├── Component              # 组件模块
│   ├── App                # 应用入口
│   ├── AppConfig          # 应用配置
│   ├── ToolKit            # 工具包
│   ├── LoginKit           # 登录工具包
│   ├── VideoPlaybackEdit  # 视频播放场景
│   ├── MiniDrama          # 短剧场景
│   └── ...
```


<span id="24ac2979"></span>
## 步骤 1：下载源代码

运行以下命令，将源代码下载到您的本地设备：

```Bash
git clone https://github.com/byteplus-sdk/VideoOneSolutions
cd Client/iOS
```


<span id="2f08751b"></span>
## 步骤 2：复制代码

将以下文件夹复制到您的项目根目录：

```Bash
Component/App
Component/AppConfig
Component/ToolKit
Component/MiniDrama
Component/LoginKit
```


<span id="c1deef88"></span>
## 步骤 3：配置 Podfile

参考[VideoOneSolutions/Client/iOS/Podfile](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Podfile)，并将以下依赖项复制到您自己的 Podfile 中。如果您的项目中的依赖版本与 Demo 所需版本冲突，则以您项目现有版本为准。

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
## 步骤 4：导入短剧模块

短剧模块的源代码位于文件夹[VideoOneSolutions/Client/iOS/Component](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component)中。如果您只需集成短剧视频，只需复制以下文件夹：[App](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/App)、[AppConfig](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/AppConfig)、[ToolKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/ToolKit)、[LoginKit](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/LoginKit)`、` 以及[MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/tree/main/Client/iOS/Component/MiniDrama)。

<span id="ee5031b1"></span>
## 步骤 5：初始化播放器 SDK

参考[MiniDrama.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Entry/MiniDrama.m)并初始化播放器 SDK。

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
## 步骤 6：集成短剧页面

[MiniDramaMainViewController](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaMainViewController.m)是短剧视频的主视图控制器。它包含两个默认标签页：“首页”和“For you”。您可以根据业务需求开发更多标签页。您可以将[MiniDramaMainViewController](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaMainViewController.m)添加到 `rootViewController` 的 `UINavigationController` 中进行集成。

<span id="7f60339e"></span>
# 业务需求定制

要快速使短剧 Demo 与您的业务需求对齐，请按照以下步骤操作：


1. 定制数据层，以高效集成短剧视频的核心功能。具体包括：

   1. 替换业务 API：实现[MiniDrama/Main/Data/Network/NetworkingManager+MiniDrama.h](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h)中定义的 API。

   2. 转换数据结构：将您的应用服务器返回的数据结构适配为短剧 Demo 中定义的结构，以便在 Demo 中利用现有业务流程。

2. 定制短剧相关功能，如付费内容解锁。


<span id="c52a5f7e"></span>
## 短剧 Demo 源代码结构

```Bash
├── VideoOne                   # 项目主入口
├── Component                  # 组件模块
│   ├── App                    # 应用入口
│   ├── AppConfig              # 应用配置
│   ├── ToolKit                # 工具包
│   ├── LoginKit               # 登录工具包
│   ├── VideoPlaybackEdit      # 视频播放场景
│   ├── MiniDrama              # 短剧场景
        ├──Resources           # 短剧资源
        ├──Classes
            ├── Entry
            │    └── MiniDrama.m    # BytePlus VOD播放器初始化配置
            ├── Main
            │    ├── MiniDramaMainViewController.m # 短剧主控制器
            │    ├── CommonUI   # 短剧通用UI
            │    ├── Data
            │    │   ├── Model  # 短剧数据模型
            │    │   └── Network  # 短剧API
            │    ├── MiniDramaChannelPage  # For you页面
            │    ├── MiniDramaHomePage   # 首页
            │    └── PlayerModules   # 播放器UI组件
            └── Player        # 播放器工具包
```


<span id="f94e0e14"></span>
## 数据层适配

<span id="286fa08e"></span>
### 数据结构转换

短剧 Demo 层已定义数据结构，包括[MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h)（短剧信息）、[MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h)（短剧剧集信息）和[MDSimpleEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDSimpleEpisodeInfoModel.h)（剧集解锁信息）。您需要将应用服务器返回的数据结构转换为上述数据结构。下表详细说明了这些数据结构。


|**类** |**参数** |**类型** |**必填** |**描述** |
|---|---|---|---|---|
|[MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h)<br><br>（短剧信息） |dramaId |NSString |必填 |短剧 ID |
||dramaTitle |NSString |必填 |短剧名称 |
||dramaCoverUrl |NSString |必填 |短剧封面 URL |
||dramaPlayTimes |NSInteger |必填 |播放次数 |
||dramaDisplayType |MiniDramaVideoDisplayType |必填 |视频方向<br><br>0 : MiniDramaVideoDisplayTypeVertical<br><br>1 : MiniDramaVideoDisplayTypeHorizontal |
||dramaLength |NSInteger |必填 |剧集总数 |
||newReleased |BOOL |选填 |是否显示“新”标签（默认 NO）。<br><br>YES : 显示<br><br>NO : 隐藏 |
|[MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h)<br><br>（剧集信息） |videoId |NSString |必填 |视频 ID |
||dramaTitle |NSString |选填 |短剧名称 |
||duration |NSString |必填 |视频时长（单位：秒） |
||coverUrl |NSString |必填 |视频封面 URL |
||playAuthToken |NSString |选填 |视频的 PlayAuthToken，由您的应用服务器通过 BytePlus VOD Server SDK 颁发。 |
||subtitleToken |NSString |选填 |视频数据源的字幕 token，可由 AppServer 通过 BytePlus VOD Server SDK 颁发。 |
||playTimes |NSInteger |选填 |播放次数 |
||videoTitle |NSString |选填 |视频标题 |
||videoDescription |NSString |选填 |视频副标题 |
||createTime |NSString |选填 |上传时间，格式为*RFC3339* |
||authorName |NSString |选填 |上传者名称 |
||authorId |NSString |选填 |上传者 userId |
||likeCount |NSUInteger |选填 |点赞数 |
||commentCount |NSUInteger |选填 |评论数 |
||videoHeight |NSString |必填 |视频高度 |
||videoWidth |NSString |必填 |视频宽度 |
||order |NSInteger |必填 |剧集列表中的视频位置 |
||dramaId |NSString |必填 |短剧 ID |
||vip |BOOL |必填 |是否需要付费解锁（默认 NO）。 |
||displayType |MDDisplayCardType |必填 |For you 页面短剧卡片展示类型<br><br>0 : MDDisplayCardTypeDefault，无封面图<br><br>1 : MDDisplayCardTypeCard，有封面图 |
|[MDSimpleEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDSimpleEpisodeInfoModel.h)<br><br>（剧集解锁信息） |subtitleToken |NSString |必填 |视频数据源的字幕 token，可由 AppServer 通过 BytePlus VOD Server SDK 颁发。 |
||videoId |NSString |必填 |视频 ID |
||order |NSInteger |选填 |剧集列表中的视频位置 |
||playAuthToken |NSString |必填 |视频的 PlayAuthToken，由您的应用服务器通过 BytePlus VOD Server SDK 颁发。 |


<span id="2a50ed4a"></span>
### 替换业务 API


1. 更新“首页”页面 API：参考[getDramaDataForHomePageData](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API 及[NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h)对象，实现一个用于获取“首页”短剧推荐的 API。您可以将 API 请求替换为自有请求，并将请求到的数据封装为[MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h)对象，返回至页面进行展示。如果当前[MDDramaInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaInfoModel.h)对象中的字段无法满足您的业务需求，也可以修改源码以增加更多字段。


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



2. 更新“详情”页面 API：参考[getDramaDataForDetailPage](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API 及[NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h)对象，实现一个用于获取“详情”页面短剧信息的 API。您可以将 API 请求替换为自有请求，并将请求到的数据封装为[MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h)对象，返回至页面进行展示。如果当前[MDDramaEpisodeInfoModel](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaEpisodeInfoModel.h)对象中的字段无法满足您的业务需求，也可以修改源码以增加更多字段。


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



3. 更新“为你推荐”页面 API：参考[getDramaDataForChannelPage](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h) API 及[NetworkingManager+MiniDrama](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Network/NetworkingManager%2BMiniDrama.h)对象，实现一个用于获取“为你推荐”页面短剧列表的 API。可根据需要自定义 API 请求，并将获取到的数据封装为[MDDramaFeedInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaFeedInfo.h)对象，返回用于页面展示。如[MDDramaFeedInfo](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/Data/Model/MDDramaFeedInfo.h)对象内现有字段无法满足业务需求，可灵活扩展源码，添加额外字段。


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
## 短剧专项功能定制

<span id="e220d76c"></span>
### 防录屏保护

参考[MDVideoPlayerController+DisRecordScreen.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Player/MDPlayerKit/Classes/PlayerCore/MDVideoPlayerController%2BDisRecordScreen.m)，通过监听系统截屏事件实现防录屏功能。

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
### 付费内容解锁

短剧 Demo 中付费内容解锁及播放流程如下图所示。

<img src="data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB2ZXJzaW9uPSIxLjEiIHdpZHRoPSI5MjZweCIgaGVpZ2h0PSI4MDdweCIgdmlld0JveD0iLTAuNSAtMC41IDkyNiA4MDciPjxkZWZzLz48Zz48cmVjdCB4PSI0MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNDA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkRyYW1hIFNjZW5lIEtpdDwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMjAzIiB5PSIzIiB3aWR0aD0iMTIwIiBoZWlnaHQ9IjQwIiByeD0iNiIgcnk9IjYiIGZpbGw9IiNjY2U1ZmYiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMTE4cHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMjNweDsgbWFyZ2luLWxlZnQ6IDIwNHB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEycHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyB3aGl0ZS1zcGFjZTogbm9ybWFsOyB3b3JkLXdyYXA6IG5vcm1hbDsgIj5BcHAvV2ViIFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iMyIgeT0iMyIgd2lkdGg9IjEyMCIgaGVpZ2h0PSI0MCIgcng9IjYiIHJ5PSI2IiBmaWxsPSIjY2NlNWZmIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDExOHB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIzcHg7IG1hcmdpbi1sZWZ0OiA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPkFwcC9XZWIgQ2xpZW50PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogNjA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBheW1lbnQgU0RLPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI4MDMiIHk9IjMiIHdpZHRoPSIxMjAiIGhlaWdodD0iNDAiIHJ4PSI2IiByeT0iNiIgZmlsbD0iI2NjZTVmZiIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxMThweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyM3B4OyBtYXJnaW4tbGVmdDogODA0cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTJweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IHdoaXRlLXNwYWNlOiBub3JtYWw7IHdvcmQtd3JhcDogbm9ybWFsOyAiPlBsYXltZW50IFNlcnZlcjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA2MyA1MyBMIDYzIDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHJlY3QgeD0iNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iNzQwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNjMgODAzIEwgNjMgNzkzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNjIuNTggNTMgTCAyNjIuNSA0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDYzIDgwMyBMIDQ2Mi41IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NjMuMzEgMzEzIEwgNjY0IDQzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4NjIuOTIgMzQzIEwgODYyLjUgNDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cmVjdCB4PSIyNTMiIHk9IjUzIiB3aWR0aD0iMjAiIGhlaWdodD0iMTEwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDQzMyBMIDI2MyAxNjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc2IDczIEwgMjQ0Ljc2IDczLjk1IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNTAuNzYgNzMuOTkgTCAyNDIuNzQgNzcuOTQgTCAyNDQuNzYgNzMuOTUgTCAyNDIuNzkgNjkuOTQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3NHB4OyBtYXJnaW4tbGVmdDogMTY1cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bMV1nZXREcmFtYUxpc3Q8L3NwYW4+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA4MC41IEwgMzQzIDgwLjUgUSAzNTMgODAuNSAzNTMgOTAuNSBMIDM1MyAxMjUuNSBRIDM1MyAxMzUuNSAzNDMgMTM1LjUgTCAyODEuMjQgMTM1LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3NS4yNCAxMzUuNSBMIDI4My4yNCAxMzEuNSBMIDI4MS4yNCAxMzUuNSBMIDI4My4yNCAxMzkuNSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDEwOXB4OyBtYXJnaW4tbGVmdDogMzUzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzEuMV1VbmxvY2tlZCBlcGlzb2RlczxiciAvPsKgbm8gcGxheWJhY2sgYXV0aCB0b2tlbi91cmw8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjU0IDE0OS40NyBMIDg1LjI0IDE0Ny44IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDc5LjI0IDE0Ny43NCBMIDg3LjI4IDE0My44MiBMIDg1LjI0IDE0Ny44IEwgODcuMiAxNTEuODIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxNDlweDsgbWFyZ2luLWxlZnQ6IDE2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPlsyXVJldHVybiBkcmFtYUxpc3Q8YnIgLz57RHJhbWFGZWVkW119PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI0NTMiIHk9IjE4MyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjgwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gNzYgMTkzIEwgNDQxLjc2IDE5Ni40NCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDQ3Ljc2IDE5Ni41IEwgNDM5LjczIDIwMC40MiBMIDQ0MS43NiAxOTYuNDQgTCA0MzkuOCAxOTIuNDIgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAxOTVweDsgbWFyZ2luLWxlZnQ6IDI2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzNdc2V0SXRlbXModmlkZW9JdGVtc1tdKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNDczIDIwMyBMIDUzMyAyMDMgUSA1NDMgMjAzIDU0MyAyMTMgTCA1NDMgMjMzIFEgNTQzIDI0MyA1MzMgMjQzIEwgNDgxLjI0IDI0MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNDc1LjI0IDI0MyBMIDQ4My4yNCAyMzkgTCA0ODEuMjQgMjQzIEwgNDgzLjI0IDI0NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDIyM3B4OyBtYXJnaW4tbGVmdDogNTQzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzMuMV1QcmV2aWV3L1BsYXliYWNrPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSI2NTMiIHk9IjMxMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjI0MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDY2NCA4MDMgTCA2NjMuMzIgNTUzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iMyAzIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3MyAzMjMgTCA2MzkuNzYgMzI0LjUiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDY0NS43NiAzMjQuNTEgTCA2MzcuNzUgMzI4LjQ5IEwgNjM5Ljc2IDMyNC41IEwgNjM3Ljc3IDMyMC40OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDMyNHB4OyBtYXJnaW4tbGVmdDogMzYxcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNF1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iODUzIiB5PSIzNDMiIHdpZHRoPSIyMCIgaGVpZ2h0PSIxMjAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSA4NjMgODAzIEwgODYzIDQ2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNjczIDM1MyBMIDg0NC43NyAzNTYuODIiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MC43NiAzNTYuOTUgTCA4NDIuNjggMzYwLjc3IEwgODQ0Ljc3IDM1Ni44MiBMIDg0Mi44NiAzNTIuNzcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAzNTVweDsgbWFyZ2luLWxlZnQ6IDc2M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxzcGFuIHN0eWxlPSJmb250LXNpemU6MTNweDtiYWNrZ3JvdW5kLWNvbG9yOnJnYigyNDgsIDI0OSwgMjUwKSI+WzQuMV1yZXF1ZXN0UGF5KG9yZGVySWQpPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA4NTMgMzkzIEwgNjgxLjI0IDM5NS4xMyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA2NzUuMjQgMzk1LjIgTCA2ODMuMTkgMzkxLjEgTCA2ODEuMjQgMzk1LjEzIEwgNjgzLjI4IDM5OS4xIFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogMzk0cHg7IG1hcmdpbi1sZWZ0OiA3NjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bNC4yXVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cmVjdCB4PSIyNTMiIHk9IjQzMyIgd2lkdGg9IjIwIiBoZWlnaHQ9IjkwIiByeD0iMyIgcnk9IjMiIGZpbGw9IiNjY2NjZmYiIHN0cm9rZT0iIzAwMDAwMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxwYXRoIGQ9Ik0gMjYzIDU3MyBMIDI2MyA1MjMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSIzIDMiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDg1MyA0NDMgTCAyODIuMjQgNDQ1LjQ3IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBzdHJva2UtZGFzaGFycmF5PSI2IDYiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDI3Ni4yNCA0NDUuNSBMIDI4NC4yMiA0NDEuNDcgTCAyODIuMjQgNDQ1LjQ3IEwgMjg0LjI1IDQ0OS40NyBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDQ0NHB4OyBtYXJnaW4tbGVmdDogNTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTNweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+WzQuM11Ob3RpZnkgcGF5IHN1Y2Nlc3Mob3JkZXJJZCk8L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gNjUzIDU0Mi45MiBMIDg2LjI0IDU0NC4zNCIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgc3Ryb2tlLWRhc2hhcnJheT0iNiA2IiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA4MC4yNCA1NDQuMzUgTCA4OC4yMyA1NDAuMzMgTCA4Ni4yNCA1NDQuMzQgTCA4OC4yNSA1NDguMzMgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA1NDRweDsgbWFyZ2luLWxlZnQ6IDM2NXB4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls1XVBheSBzdWNjZXNzPC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDI3MyA0NTUuNSBMIDMzMyA0NTUuNSBRIDM0MyA0NTUuNSAzNDMgNDY1LjUgTCAzNDMgNDkwLjUgUSAzNDMgNTAwLjUgMzMzIDUwMC41IEwgMjgxLjI0IDUwMC41IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSAyNzUuMjQgNTAwLjUgTCAyODMuMjQgNDk2LjUgTCAyODEuMjQgNTAwLjUgTCAyODMuMjQgNTA0LjUgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA0NzlweDsgbWFyZ2luLWxlZnQ6IDM0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDExcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxmb250IHN0eWxlPSJmb250LXNpemU6MTNweCI+WzQuNF08Zm9udCBzdHlsZT0iZm9udC1zaXplOjEzcHgiPlJlY29yZCA8YnIgLz5wYXltZW50IHN0YXR1czwvZm9udD48L2ZvbnQ+PC9kaXY+PC9kaXY+PC9kaXY+PC9mb3JlaWduT2JqZWN0PjwvZz48cGF0aCBkPSJNIDczIDI2MyBMIDEzMyAyNjMgUSAxNDMgMjYzIDE0MyAyNzMgTCAxNDMgMjkzIFEgMTQzIDMwMyAxMzMgMzAzIEwgODEuMjQgMzAzIiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA3NS4yNCAzMDMgTCA4My4yNCAyOTkgTCA4MS4yNCAzMDMgTCA4My4yNCAzMDcgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiAyODNweDsgbWFyZ2luLWxlZnQ6IDE0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPjxkaXY+U3dpcGUgdG88L2Rpdj48ZGl2PnVubG9ja2VkIGVwaXNvZGU8L2Rpdj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxyZWN0IHg9IjI1MyIgeT0iNTczIiB3aWR0aD0iMjAiIGhlaWdodD0iOTAiIHJ4PSIzIiByeT0iMyIgZmlsbD0iI2NjY2NmZiIgc3Ryb2tlPSIjMDAwMDAwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PHBhdGggZD0iTSAyNjMgODAzIEwgMjYzIDY2MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjMgMyIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzMgNTgzIEwgMjQ0Ljc2IDU4MyIgZmlsbD0ibm9uZSIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gMjUwLjc2IDU4MyBMIDI0Mi43NiA1ODcgTCAyNDQuNzYgNTgzIEwgMjQyLjc2IDU3OSBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDU3M3B4OyBtYXJnaW4tbGVmdDogMTYzcHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bNl1nZXREcmFtYURldGFpbChvcmRlcklkKTwvc3Bhbj48L2Rpdj48L2Rpdj48L2Rpdj48L2ZvcmVpZ25PYmplY3Q+PC9nPjxwYXRoIGQ9Ik0gMjUzIDY0NC43NSBMIDE3MyA2NDMuMTkgUSAxNjMgNjQzIDE1MyA2NDMgTCA4NC4yNCA2NDMiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHN0cm9rZS1kYXNoYXJyYXk9IjYgNiIgcG9pbnRlci1ldmVudHM9InN0cm9rZSIvPjxwYXRoIGQ9Ik0gNzguMjQgNjQzIEwgODYuMjQgNjM5IEwgODQuMjQgNjQzIEwgODYuMjQgNjQ3IFoiIGZpbGw9IiMwMDAwMDAiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48ZyB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtMC41IC0wLjUpIj48Zm9yZWlnbk9iamVjdCBzdHlsZT0ib3ZlcmZsb3c6IHZpc2libGU7IHRleHQtYWxpZ246IGxlZnQ7IiBwb2ludGVyLWV2ZW50cz0ibm9uZSIgd2lkdGg9IjEwMCUiIGhlaWdodD0iMTAwJSI+PGRpdiB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94aHRtbCIgc3R5bGU9ImRpc3BsYXk6IGZsZXg7IGFsaWduLWl0ZW1zOiB1bnNhZmUgY2VudGVyOyBqdXN0aWZ5LWNvbnRlbnQ6IHVuc2FmZSBjZW50ZXI7IHdpZHRoOiAxcHg7IGhlaWdodDogMXB4OyBwYWRkaW5nLXRvcDogNjIzcHg7IG1hcmdpbi1sZWZ0OiAxNjNweDsiPjxkaXYgc3R5bGU9ImJveC1zaXppbmc6IGJvcmRlci1ib3g7IGZvbnQtc2l6ZTogMDsgdGV4dC1hbGlnbjogY2VudGVyOyAiPjxkaXYgc3R5bGU9ImRpc3BsYXk6IGlubGluZS1ibG9jazsgZm9udC1zaXplOiAxM3B4OyBmb250LWZhbWlseTogSGVsdmV0aWNhOyBjb2xvcjogIzAwMDAwMDsgbGluZS1oZWlnaHQ6IDEuMjsgcG9pbnRlci1ldmVudHM6IGFsbDsgYmFja2dyb3VuZC1jb2xvcjogI2ZmZmZmZjsgd2hpdGUtc3BhY2U6IG5vd3JhcDsgIj5bN11SZXR1cm4gRHJhbWFVbmxvY2sgbWV0YTwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHJlY3QgeD0iNDUzIiB5PSI2NzAiIHdpZHRoPSIyMCIgaGVpZ2h0PSI4MCIgcng9IjMiIHJ5PSIzIiBmaWxsPSIjY2NjY2ZmIiBzdHJva2U9IiMwMDAwMDAiIHBvaW50ZXItZXZlbnRzPSJhbGwiLz48cGF0aCBkPSJNIDQ3MyA2OTAgTCA1MzMgNjkwIFEgNTQzIDY5MCA1NDMgNzAwIEwgNTQzIDcyMCBRIDU0MyA3MzAgNTMzIDczMCBMIDQ4MS4yNCA3MzAiIGZpbGw9Im5vbmUiIHN0cm9rZT0iIzAwMDAwMCIgc3Ryb2tlLXdpZHRoPSIyIiBzdHJva2UtbWl0ZXJsaW1pdD0iMTAiIHBvaW50ZXItZXZlbnRzPSJzdHJva2UiLz48cGF0aCBkPSJNIDQ3NS4yNCA3MzAgTCA0ODMuMjQgNzI2IEwgNDgxLjI0IDczMCBMIDQ4My4yNCA3MzQgWiIgZmlsbD0iIzAwMDAwMCIgc3Ryb2tlPSIjMDAwMDAwIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZS1taXRlcmxpbWl0PSIxMCIgcG9pbnRlci1ldmVudHM9ImFsbCIvPjxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKC0wLjUgLTAuNSkiPjxmb3JlaWduT2JqZWN0IHN0eWxlPSJvdmVyZmxvdzogdmlzaWJsZTsgdGV4dC1hbGlnbjogbGVmdDsiIHBvaW50ZXItZXZlbnRzPSJub25lIiB3aWR0aD0iMTAwJSIgaGVpZ2h0PSIxMDAlIj48ZGl2IHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hodG1sIiBzdHlsZT0iZGlzcGxheTogZmxleDsgYWxpZ24taXRlbXM6IHVuc2FmZSBjZW50ZXI7IGp1c3RpZnktY29udGVudDogdW5zYWZlIGNlbnRlcjsgd2lkdGg6IDFweDsgaGVpZ2h0OiAxcHg7IHBhZGRpbmctdG9wOiA3MTBweDsgbWFyZ2luLWxlZnQ6IDU0M3B4OyI+PGRpdiBzdHlsZT0iYm94LXNpemluZzogYm9yZGVyLWJveDsgZm9udC1zaXplOiAwOyB0ZXh0LWFsaWduOiBjZW50ZXI7ICI+PGRpdiBzdHlsZT0iZGlzcGxheTogaW5saW5lLWJsb2NrOyBmb250LXNpemU6IDEzcHg7IGZvbnQtZmFtaWx5OiBIZWx2ZXRpY2E7IGNvbG9yOiAjMDAwMDAwOyBsaW5lLWhlaWdodDogMS4yOyBwb2ludGVyLWV2ZW50czogYWxsOyBiYWNrZ3JvdW5kLWNvbG9yOiAjZmZmZmZmOyB3aGl0ZS1zcGFjZTogbm93cmFwOyAiPls4LjFdUHJldmlldy9QbGF5YmFjazwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PHBhdGggZD0iTSA3OSA2NzMgTCA0NDQuNzYgNjc2LjQ0IiBmaWxsPSJub25lIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0ic3Ryb2tlIi8+PHBhdGggZD0iTSA0NTAuNzYgNjc2LjUgTCA0NDIuNzMgNjgwLjQyIEwgNDQ0Ljc2IDY3Ni40NCBMIDQ0Mi44IDY3Mi40MiBaIiBmaWxsPSIjMDAwMDAwIiBzdHJva2U9IiMwMDAwMDAiIHN0cm9rZS13aWR0aD0iMiIgc3Ryb2tlLW1pdGVybGltaXQ9IjEwIiBwb2ludGVyLWV2ZW50cz0iYWxsIi8+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTAuNSAtMC41KSI+PGZvcmVpZ25PYmplY3Qgc3R5bGU9Im92ZXJmbG93OiB2aXNpYmxlOyB0ZXh0LWFsaWduOiBsZWZ0OyIgcG9pbnRlci1ldmVudHM9Im5vbmUiIHdpZHRoPSIxMDAlIiBoZWlnaHQ9IjEwMCUiPjxkaXYgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGh0bWwiIHN0eWxlPSJkaXNwbGF5OiBmbGV4OyBhbGlnbi1pdGVtczogdW5zYWZlIGNlbnRlcjsganVzdGlmeS1jb250ZW50OiB1bnNhZmUgY2VudGVyOyB3aWR0aDogMXB4OyBoZWlnaHQ6IDFweDsgcGFkZGluZy10b3A6IDY3NXB4OyBtYXJnaW4tbGVmdDogMjY2cHg7Ij48ZGl2IHN0eWxlPSJib3gtc2l6aW5nOiBib3JkZXItYm94OyBmb250LXNpemU6IDA7IHRleHQtYWxpZ246IGNlbnRlcjsgIj48ZGl2IHN0eWxlPSJkaXNwbGF5OiBpbmxpbmUtYmxvY2s7IGZvbnQtc2l6ZTogMTFweDsgZm9udC1mYW1pbHk6IEhlbHZldGljYTsgY29sb3I6ICMwMDAwMDA7IGxpbmUtaGVpZ2h0OiAxLjI7IHBvaW50ZXItZXZlbnRzOiBhbGw7IGJhY2tncm91bmQtY29sb3I6ICNmZmZmZmY7IHdoaXRlLXNwYWNlOiBub3dyYXA7ICI+PHNwYW4gc3R5bGU9ImZvbnQtc2l6ZToxM3B4O2JhY2tncm91bmQtY29sb3I6cmdiKDI0OCwgMjQ5LCAyNTApIj5bOF1hcHBlbmRJdGVtcyh2aWRlb0l0ZW1zW10pPC9zcGFuPjwvZGl2PjwvZGl2PjwvZGl2PjwvZm9yZWlnbk9iamVjdD48L2c+PC9nPjwvc3ZnPg==" />

Demo 实现了完整的付费内容解锁流程，但未集成第三方 SDK。仅在[MiniDramaDetailFeedViewController.m](https://github.com/byteplus-sdk/VideoOneSolutions/blob/main/Client/iOS/Component/MiniDrama/Classes/Main/MiniDramaChannelPage/DramaDetailPage/MiniDramaDetailFeedViewController.m)中实现了模拟支付流程，需替换为自有代码。

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
