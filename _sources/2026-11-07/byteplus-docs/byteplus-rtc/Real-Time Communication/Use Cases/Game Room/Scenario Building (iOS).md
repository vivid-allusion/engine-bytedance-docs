---
title: "Scenario Building (iOS)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-136529"
---

<span id="sdk-integration"></span>
## SDK Integration

This scenario requires the integration of RTC SDK and the SUD MGP interactive mini\-game platform. You need to activate the service on the console of RTC and download the corresponding SDK of SUD MGP. Instructions are as follows:

<span id="rtc-sdk-integration"></span>
### RTC SDK Integration

The following diagram shows the overall integration process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/intergration.png) </span>

<span id="mini-game-sdk-integration"></span>
### Mini\-game SDK Integration

For details on integrating the SUD MGP SDK, see [https://docs.sud.tech/en-US/](https://docs.sud.tech/en-US/)

<span id="implementation-flows"></span>
## Implementation Flows


* Workflow diagram


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/f50294d9-7c2e-46a2-8f96-088a404d1ebb.png) </span>

<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="the-room-owner-creates-a-game-room-and-audience-members-join"></span>
### The room owner creates a game room and audience members join

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/617c3dfd-4011-49c4-995f-d3a314e581e3.png) </span>

<span id="sample-code"></span>
#### Sample code

```objectivec
/**
  * Join the RTC room and initialize the parameters
  * @param token: RTC Token
  * @param roomID: RTC room id
  * @param uid: RTC user id
  **/

- (void)joinChannelWithToken:(NSString *)token roomID:(NSString *)roomID uid:(NSString *)uid {
     //Set the subscribed audio and video stream fallback option
     [self.rtcEngineKit setSubscribeFallbackOption:ByteRTCSubscribeFallbackOptionAudioOnly];
 
     //Close local audio/video capture
     [self.rtcEngineKit stopAudioCapture];
     [self.rtcEngineKit stopVideoCapture];
 
// Sets the audio route: YES for speaker, NO for earpiece.
     [self.rtcEngineKit setDefaultAudioRoute:ByteRTCAudioRouteSpeakerphone];
 
// Enables audio property reporting, such as local audio volume.
     ByteRTCAudioPropertiesConfig *audioPropertiesConfig = [[ByteRTCAudioPropertiesConfig alloc] init];
     audioPropertiesConfig.interval = 200;
     [self.rtcEngineKit enableAudioPropertiesReport:audioPropertiesConfig];
    
 
// Joins the room and connects to the host. You must apply for an AppId and Token beforehand.
     ByteRTCUserInfo *userInfo = [[ByteRTCUserInfo alloc] init];
     userInfo. userId = uid;
    
     ByteRTCRoomConfig *config = [[ByteRTCRoomConfig alloc] init];
     config.profile = ByteRTCRoomProfileCommunication;
     config.isAutoPublish = YES;
     config.isAutoSubscribeAudio = YES;
    
     self.rtcRoom = [self.rtcEngineKit createRTCRoom:roomID];
     self.rtcRoom.delegate = self;
     [self.rtcRoom joinRoom:token userInfo:userInfo roomConfig:config];
    
     //Set the user as invisible
     [self.rtcRoom setUserVisibility:NO];
}

/**
  * Initialize the game SDK
  * @param appId: The appId required by the game SDK
  * @param appKey: The appKey required by the game SDK
  * @param callback: initialization game SDK callback
  **/

- (void)initSudMGPSDKWithAppId:(NSString *)appId appKey:(NSString *)appKey callback:(void(^)(BOOL success))resultCallback {
     if (self.isInitSDK) {
         if (resultCallback) {
             resultCallback(YES);
         }
         return;
     }
    
     __weak __typeof(self) wself = self;
     [SudMGP initSDK:appId appKey:appKey isTestEnv:YES listener:^(int retCode, const NSString * _Nonnull retMsg) {
         wself.isInitSDK = retCode == 0;
         if (resultCallback) {
             resultCallback(wself.isInitSDK);
         }
     }];
}

/**
* Loading the mini-game interface
  **/

- (void)initSudMGP {
     __weak __typeof(self) wself = self;
     [[GameSudMGPManager shareManager] requestSudMGPCode:NO resultCallback:^(NSString * _Nullable code) {
         if (!code) {
             [[ToastComponent shareToastComponent] showWithMessage:@"Login game failed" view:self.view];
             return;
         }
        
         [wself.iSudAPP destroyMG];
         wself.iSudAPP = nil;
         wself.iSudAPP = [SudMGP loadMG:[LocalUserComponent userModel].uid roomId:self.roomModel.room_id code:[GameSudMGPManager shareManager].sudMGPCode mgId:self.gameId language:@"zh-CN" fsmMG:self rootView:self.gameRootView ];
     }];
}

/**
  * Configuring the game interface layout
  * @param handle callback handle, The app must call handle.success or handle.fail
  * @param dataJson {}
  */
-(void)onGetGameViewInfo:(id<ISudFSMStateHandle>)handle dataJson:(NSString*)dataJson {
     CGRect rect = self.gameRootView.frame;
     CGFloat scale = [[UIScreen mainScreen] nativeScale];

     CGFloat height = rect. size. height;
     CGFloat width = 1.0 / 1.4 * height; //The aspect ratio of the game area is recommended to be 1:1.4
     width = MIN(width, rect. size. width);

     CGFloat left = 0.5 * (rect. size. width - width) * scale;
     NSDictionary *rectDict = [NSDictionary dictionaryWithObjectsAndKeys:@(0), @"top", @(left), @"left", @(0), @"bottom", @(left), @"right", nil] ;
     NSDictionary *viewDict = [NSDictionary dictionaryWithObjectsAndKeys:@(rect.size.width * scale), @"width", @(rect.size.height * scale), @"height", nil];
     NSDictionary *dataDict = [NSDictionary dictionaryWithObjectsAndKeys:@(0), @"ret_code", @"return form APP onGetGameViewInfo", @"ret_msg", viewDict, @"view_size", rectDict, @"view_game_rect", nil];
     /// callback
     [handle success:[GameUtils dictionaryToJson:dataDict]];
}
```


<span id="an-audience-member-becomes-a-co-host"></span>
### An audience member becomes a co\-host

<span id="sequence-diagram"></span>
#### Sequence diagram


* An audience member requests to become a guest

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/d43bc076-413d-4e1f-8d5f-3a805fac4ee1.png) </span>

* The host makes an audience member a guest

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/98d2eeed-9eda-469f-bed1-5de60effb62a.png) </span>


<span id="code-sample"></span>
#### Code sample

```objectivec
/**
 * tab button status change callback
 * @param itemButton: Tapped button
* @param status: Button status
 **/

- (void)gameRoomBottomView:(GameRoomBottomView *_Nonnull)gameRoomBottomView
                itemButton:(GameRoomItemButton *_Nullable)itemButton
           didSelectStatus:(GameRoomBottomStatus)status {
    if (status == GameRoomBottomStatusList ||
        status == GameRoomBottomStatusListRed) {
        __weak __typeof(self) wself = self;
        [self.userListComponents show:^{
            [wself restoreBottomViewMenuStatus];
        }];
    } else if (status == GameRoomBottomStatusRaiseHand) {     //Tap to raise hand
        __weak __typeof(self) wself = self;
        [GameRTSManager raiseHandsMicWithBlock:^(RTMACKModel * _Nonnull model) {
            if (model.result) {
                [[ToastComponent shareToastComponent] showWithMessage:@"Microphone connection request has been sent. Please wait"];
 
                [wself.bottomView updateButtonStatus:GameRoomBottomStatusRaiseHand close:YES];
                [wself checkMicrophoneSystemAuthority];
            }else {
                [[ToastComponent shareToastComponent] showWithMessage:@"Operation failed. Please try again"];
            }
        }];
    } else if (status == GameRoomBottomStatusMic) {
        [SystemAuthority authorizationStatusWithType:AuthorizationTypeAudio block:^(BOOL isAuthorize) {
            if (itemButton.status == ButtonStatusNone) {
                //mute
                [GameRTSManager muteMic];
                [[GameRTCManager shareRtc] muteLocalAudioStream:YES];
            } else {
                //unmute
                [GameRTSManager unmuteMic];
                [[GameRTCManager shareRtc] muteLocalAudioStream:NO];
            }
            itemButton.status = itemButton.status == ButtonStatusNone ? ButtonStatusActive : ButtonStatusNone;
        }];
    } else if (status == GameRoomBottomStatusVolume) {
        [self.volumeComponents show];
    } else if (status == GameRoomBottomStatusData) {
        [self.paramComponents show];
    } else if (status == GameRoomBottomStatusDownHand) {    // Tap to stop co-hosting
        AlertActionModel *alertModel = [[AlertActionModel alloc] init];
        alertModel.title = @"Confirm";
        AlertActionModel *cancelModel = [[AlertActionModel alloc] init];
        cancelModel.title = @"Cancel";
        __weak __typeof(self) wself = self;
        [[AlertActionManager shareAlertActionManager] showWithMessage:@"Are you sure you want to disable microphone connection?" actions:@[cancelModel, alertModel]];
        alertModel.alertModelClickBlock = ^(UIAlertAction * _Nonnull action) {
            if ([action.title isEqualToString:@"Confirm"]) {
                [GameRTSManager offSelfMicWithBlock:^(RTMACKModel * _Nonnull model) {
                    if (model.result) {
                        [wself sendDownloadHand];
                    }else {
                        [[ToastComponent shareToastComponent] showWithMessage:@"Operation failed. Please try again"];
                    }
                }];
            }
        };
    } else {
        
    }
}

/**
* Actions for audiences and co-hosts
 * @param userModel: Select the user's model
 * @param dataLists: List of corresponding users
 **/

- (void)updateTableViewWithModel:(GameControlUserModel *)userModel dataLists:(NSArray<GameControlUserModel *> *)dataLists {
    if (userModel.user_status == 0) {
        // Invite to become a guest
        [GameRTSManager inviteMic:userModel.user_id block:^(RTMACKModel * _Nonnull model) {
            if (!model.result) {
                [[ToastComponent shareToastComponent] showWithMessage:@"Operation failed. Please try again"];
            }
        }];
    } else if (userModel.user_status == 1) {
        // Raise hand - Accept
        __weak __typeof(self)wself = self;
        [GameRTSManager agreeMic:userModel.user_id block:^(RTMACKModel * _Nonnull model) {
            if (model.result) {
                userModel.user_status = 2;
                [wself updateDataLists:dataLists model:userModel];
            } else {
                [[ToastComponent shareToastComponent] showWithMessage:@"Operation failed. Please try again"];
            }
        }];
    } else if (userModel.user_status == 2) {
   // Co-host: Remove from the stage
        AlertActionModel *alertModel = [[AlertActionModel alloc] init];
        alertModel.title = @"Confirm";
        AlertActionModel *cancelModel = [[AlertActionModel alloc] init];
        cancelModel.title = @"Cancel";
        [[AlertActionManager shareAlertActionManager] showWithMessage:@"Are you sure you want to remove the user from co-host?" actions:@[cancelModel, alertModel]];
        __weak __typeof(self) wself = self;
        alertModel.alertModelClickBlock = ^(UIAlertAction * _Nonnull action) {
            if ([action.title isEqualToString:@"Confirm"]) {
                [GameRTSManager offMic:userModel.user_id block:^(RTMACKModel * _Nonnull model) {
                    if (model.result) {
                        [wself removeDataLists:dataLists model:userModel];
                    } else {
                        [[ToastComponent shareToastComponent] showWithMessage:@"Operation failed. Please try agian"];
                    }
                }];
            }
        };
    }
}

/**
* Notifications for when audience members become guests
 * @param userModel: Model of corresponding users
 **/

- (void)receivedRaiseHandSucceedWithUser:(GameControlUserModel *)userModel {
    [self.roomView audienceRaisedHandsSuccess:userModel];
    [self.userListComponents update];
    if ([userModel.user_id isEqualToString:[LocalUserComponent userModel].uid]) {
        GameControlUserModel *localUser = [self currentLoginuserModel];
        localUser.user_status = 2;
        localUser.is_mic_on = YES;
        [self.bottomView updateBottomLists:[self getBottomListsWithModel:localUser]];
        [[ToastComponent shareToastComponent] showWithMessage:@"You have become a co-host"];
        [[GameRTCManager shareRtc] makeCoHost:YES];
        [[GameRTCManager shareRtc] muteLocalAudioStream:NO];
        [self checkMicrophoneSystemAuthority];
    }
}
```


<span id="apis-and-callbacks"></span>
## APIs and Callbacks

<span id="api"></span>
### API


|Function |API |
|---|---|
|Create RTCVideo instance |createRTCVideo:delegate:parameters: |
|Create RTCRoom object |createRTCRoom: |
|Create RTCRoom object |[createRTCRoom:](https://docs.byteplus.com/en/docs/12/docs-70086#creatertcroom) |
|Set user visibility |[setUserVisibility:](https://docs.byteplus.com/en/docs/12/docs-70086#setuservisibility) |
|Start audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#startaudiocapture) |
|Join RTC room |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#joinroom-userinfo-uservisibility-roomconfig) |
|Leave Room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70086#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70086#stopaudiocapture) |
|Destroy the RTCRoom object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70086#destroy) |


<span id="callbacks"></span>
### Callbacks


|Function |Callback |
|---|---|
|The local user joins the RTC room |rtcRoom:onRoomStateChanged:uid:state:extraInfo |
|A remote visible user joins the room |rtcRoom:onUserJoined:elapsed: |
