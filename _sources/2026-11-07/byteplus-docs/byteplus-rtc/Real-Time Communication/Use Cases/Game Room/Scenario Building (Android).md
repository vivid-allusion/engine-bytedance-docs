---
title: "Scenario Building (Android)"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-154572"
---

<span id="sdk-integration"></span>
## SDK Integration

This scenario requires the integration of RTC SDK and the SUD MGP interactive mini\-game platform. You need to activate the service on the console of RTC and download the corresponding SDK of SUD MGP. Instructions are as follows:

<span id="rtc-sdk-integration"></span>
### RTC SDK Integration

The following figure shows the overall access process. For details, please see [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865)

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/intergration.png) </span>

<span id="mini-game-sdk-integration"></span>
### Mini\-game SDK Integration

For details about SUD MGP SDK integration, see [https://docs.sud.tech/en-US/](https://docs.sud.tech/en-US/)

<span id="implementation-flows"></span>
## Implementation Flows


* Overall business flow diagram


<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/f50294d9-7c2e-46a2-8f96-088a404d1ebb.png) </span>

<span id="core-feature-implementation"></span>
## Core Feature Implementation

<span id="a-room-owner-creates-a-game-room-and-users-join-the-room"></span>
### A room owner creates a game room and users join the room

<span id="sequence-diagram"></span>
#### Sequence diagram

<span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/02c2f4c8-e055-4f8c-8b97-fcc39c48984e.png) </span>

<span id="sample-code"></span>
#### Sample code

```Java
    /**
     * Join the RTC room and initialize parameters 
     * @param The token for joining the RTC room
     * @param roomId ID for joining the RTC room
     * @param userId User ID for joining the RTC room
     */
    public static void joinRoom(String token, String roomId, String uid) {
        MLog.d("joinChannel", "token:" + token + " roomId:" + roomId + " uid:" + uid);
        leaveRoom();
        if (mRTCVideo == null) {
            return;
        }
        mRTCRoom = mRTCVideo.createRTCRoom(roomId);
        mRTCRoom.setRTCRoomEventHandler(mRTCRoomEventHandler);
        UserInfo userInfo = new UserInfo(uid, null);
        RTCRoomConfig roomConfig = new RTCRoomConfig(ChannelProfile.CHANNEL_PROFILE_COMMUNICATION,
                true, true, true);
        mRTCRoom.joinRoom(token, userInfo, roomConfig);
}
    /**
     * Initialize SudMGP SDK
     *
     * @param activity Game page
     * @param gameId   Game ID
     * @param code     Token
     */
    private void initSdk(FragmentActivity activity, long gameId, String code) {
        String appId = getAppId();
        String appKey = getAppKey();
        // init sdk
        SudMGP.initSDK(activity, appId, appKey, isTestEnv(), new ISudListenerInitSDK() {
            @Override
            public void onSuccess() {
                loadGame(activity, code, gameId);
            }

            @Override
            public void onFailure(int errCode, String errMsg) {
                if (isTestEnv()) {
                    Toast.makeText(activity, "initSDK onFailure:" + errMsg + "(" + errCode + ")", Toast.LENGTH_LONG).show();
                }

                delayLoadGame(activity, gameId);
            }
        });
    }

    /**
     * Load game
     * App and game interaction
 * ISudFSTAPP: The app calls the game interface
     * ISudFSMMG: Response callback when the game calls the APP 
     *
     * @param activity Game page
     * @param code     Login token
     * @param gameId   Game ID
     */
    private void loadGame(FragmentActivity activity, String code, long gameId) {
        if (activity.isDestroyed() || !isRunning || gameId != playingGameId) {
            return;
        }

        // Set callbacks for decoration categories
        sudFSMMGDecorator.setSudFSMMGListener(this);

        // Call the game SDK to load the game
        ISudFSTAPP iSudFSTAPP = SudMGP.loadMG(activity, getUserId(), gameRoomId, code, gameId, getLanguageCode(), sudFSMMGDecorator);

// A null return value indicates a parameter error or that the call was not made on the main thread.
        if (iSudFSTAPP == null) {
            Toast.makeText(activity, "loadMG params error", Toast.LENGTH_LONG).show();
            delayLoadGame(activity, gameId);
            return;
        }

        // Decoration category settings when APP calls the game interface 
        sudFSTAPPDecorator.setISudFSTAPP(iSudFSTAPP);

// Gets the game view and passes it to the Activity for display.
        // Activity call: gameContainer.addView(view, FrameLayout.LayoutParams.MATCH_PARENT, FrameLayout.LayoutParams.MATCH_PARENT);
        gameView = iSudFSTAPP.getGameView();
        onAddGameView(gameView);
    }
    
    /**
     * Process game view information (game safe area)
     */
    public void processOnGetGameViewInfo(View gameView, ISudFSMStateHandle handle) {
        //Get the width and height of the game view
        int gameViewWidth = gameView.getMeasuredWidth();
        int gameViewHeight = gameView.getMeasuredHeight();
        if (gameViewWidth > 0 && gameViewHeight > 0) {
            notifyGameViewInfo(handle, gameViewWidth, gameViewHeight);
            return;
        }

//If the game view loading is not complete, register a callback to be notified upon completion.
        gameView.getViewTreeObserver().addOnGlobalLayoutListener(new ViewTreeObserver.OnGlobalLayoutListener() {
            @Override
            public void onGlobalLayout() {
                gameView.getViewTreeObserver().removeOnGlobalLayoutListener(this);
                int width = gameView.getMeasuredWidth();
                int height = gameView.getMeasuredHeight();
                notifyGameViewInfo(handle, width, height);
            }
        });
    }

/** Game notifications and game view information */
    private void notifyGameViewInfo(ISudFSMStateHandle handle, int gameViewWidth, int gameViewHeight) {
        GameViewInfoModel gameViewInfoModel = new GameViewInfoModel();
        gameViewInfoModel.ret_code = 0;
        // Game view size
        gameViewInfoModel.view_size.width = gameViewWidth;
        gameViewInfoModel.view_size.height = gameViewHeight;

        // Game safe operating area
        getGameRect(gameViewInfoModel);

// Return the data to the game.
        String json = SudJsonUtils.toJson(gameViewInfoModel);
        handle.success(json);
    }
```


<span id="promoting-an-audience-member-to-a-guest"></span>
### Promoting an audience member to a guest

<span id="sequence-diagram"></span>
#### Sequence diagram


* An audience member requests to become a guest

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/08b7e66b-b51f-42fa-adfa-b84ee20d0c16.png) </span>

* The host promotes an audience member to a guest

   <span>![图片](https://lf3-static.bytednsdoc.com/obj/eden-cn/pkupenuhr/usecase/2e35a1b9-bf21-47f4-a593-a2d58ef1361c.png) </span>


<span id="code-sample"></span>
#### Code sample

```Java
/**
 * An audience member raises their hand
 */
public void onCSRaiseHandsMicEvent(RaiseHandsMicEvent event) {
    mChatRoomAdapter.updateRaiseHandStatus(event.userId);
    mIsSomeoneRaiseHand = true;
    updateUI();
}

/**
 * Request to start co-hosting
 */
public void onCSInviteMicEvent(InviteMicEvent event) {
    if (!GameRoomDataManger.isSelf(event.userId)) {
        return;
    }
    if (mDialog != null) {
        mDialog.dismiss();
    }
    if (TextUtils.equals(event.userId, mUserId)) {
        CommonDialog dialog = new CommonDialog(this);
        dialog.setMessage("The host is inviting you to become a co-host");
        dialog.setPositiveListener(v -> {
            GameRoomRtmClient rtmClient = GameRoomRtcManager.getRtmClient();
            if (rtmClient != null) {
                rtmClient.confirmBecomeSpeaker();
            }
            dialog.dismiss();
        });
        dialog.setNegativeListener(v -> dialog.dismiss());
        dialog.show();
        mDialog = dialog;
    }
}

/**
 * Receiving the invitation to become a guest
 */
public void onCSInviteMicEvent(InviteMicEvent event) {
    if (!GameRoomDataManger.isSelf(event.userId)) {
        return;
    }
    if (mDialog != null) {
        mDialog.dismiss();
    }
    if (TextUtils.equals(event.userId, mUserId)) {
        CommonDialog dialog = new CommonDialog(this);
        dialog.setMessage("The host is inviting you to become a co-host");
        dialog.setPositiveListener(v -> {
            GameRoomRtmClient rtmClient = GameRoomRtcManager.getRtmClient();
            if (rtmClient != null) {
                rtmClient.confirmBecomeSpeaker();
            }
            dialog.dismiss();
        });
        dialog.setNegativeListener(v -> dialog.dismiss());
        dialog.show();
        mDialog = dialog;
    }
}

/**
 * Notification of becoming a guest
 */
public void onCSMicOnEvent(MicOnEvent event) {
    if (TextUtils.equals(event.user.userId, mUserId)) {
        if (!hasAudioPermission()) {
            SafeToast.show("Microphone permission is disabled. Please go to the device Settings page to enable it");
            requestPermissions(Manifest.permission.RECORD_AUDIO);
        }
        showToast("You are now a co-host", true);
        mIsSpeaker = true;
        mIsRaiseHand = false;
        switchMic(true);
    }
    mChatRoomAdapter.onUserRoleChange(event.user.userId, true);
    updateUI();
}

/**
 * Notification of being returned to the audience
 */
public void onCSMicOffEvent(MicOffEvent event) {
    if (TextUtils.equals(event.userId, mUserId)) {
        showToast("You have returned to the viewer seat", true);
        mIsSpeaker = false;
        switchMic(false);
    }
    mChatRoomAdapter.onUserRoleChange(event.userId, false);
    updateUI();
}
```


<span id="api-and-callback"></span>
## API and callback

<span id="api"></span>
### API


|Function |API |
|---|---|
|Creates an RTCVideo object |createRTCVideo |
|Create RTCRoom object |[createRTCRoom](https://docs.byteplus.com/en/docs/12/docs-70080#creatertcroom) |
|Set user visibility |[setUserVisibility](https://docs.byteplus.com/en/docs/12/docs-70080#setuservisibility) |
|Start local audio capture |[startAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#startaudiocapture) |
|Join RTC room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |
|Leave Room |[leaveRoom](https://docs.byteplus.com/en/docs/12/docs-70080#leaveroom) |
|Stop audio capture |[stopAudioCapture](https://docs.byteplus.com/en/docs/12/docs-70080#stopaudiocapture) |
|Destroy the RTCRoom object |[destroy](https://docs.byteplus.com/en/docs/12/docs-70080#destroy) |


<span id="callback"></span>
### Callback


|Function |Callback |
|---|---|
|Triggered when the local user joins the RTC room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#onroomstatechanged) |
|A remote, visible user joins the room. |[onUserJoined](https://docs.byteplus.com/en/docs/12/docs-70081#onuserjoined) |
