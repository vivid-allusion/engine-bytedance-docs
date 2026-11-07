---
title: "Authentication with Token"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70121"
---

To join the room, the application client needs to take the token for authentication. The token is generated for each joinRoom action on the application server, based on RTC AppID, RTC AppKey, the roomID of the room to join, the UserID used to join the room, and the timestamp.

> Refer to [Value Nomenclature](https://docs.byteplus.com/docs/byteplus-rtc/docs-70114) for the specification of value assignments for roomID and userID. Store the roomID and userID you use to generate the Token. You will need them when calling `joinRoom` to start a video call.


When the RTC server receives the joinRoom request, it will check the token within the joinRoom request.

<span id="authentication-process"></span>
## Authentication process

The authentication process is as follows.


1. The client applies for a token from the app server.

2. The app server generates a token.

3. The app server issues the token to the client.

4. The client joins the RTC room with the token.

> Note: The userID and roomID used when joining the room must be consistent with those used to generate the Token. Otherwise, joining the room will fail, and you will receive the `onRoomStateChanged` callback with the error code `ERROR_CODE_INVALID_TOKEN`.


5. RTC server verifies the token.

6. The client receives a callback indicating whether joining the room was successful.

7. The `onTokenWillExpire` callback is triggered when the SDK detects that the token's privilege to join the room will expire within 30 seconds.

> Note: After the token expires, the user will be removed from the room and receives a callback with the error code `ERROR_CODE_TOKEN_EXPIRED`. You need to call `joinRoom` to join the room after applying for a new Token.


8. At this point, the client applies for a new token to rejoin the room.

9. The same as step 2.

10. The same as step 3.

11. Call `updateToken` to update the token.


You need to implement the logic for steps 1, 2, 3, 4, and 11.

<span id="generate-token"></span>
## Generate token

<span id="generate-permanent-token"></span>
### Generate permanent token

You can refer to the sample code provided by RTC to implement token generation at the app server.

The following file contains code with multiple language implementations: [RTC_Token.zip](https://sf16-sg.tiktokcdn.com/obj/eden-sg/pojnupibps/RTC_Token.zip)

The following Go code demonstrates how to generate tokens.

```go
var (
// Make sure you use the same appID, roomID, and userID when generating the token and when calling joinRoom. Otherwise, the attempt to join the room will fail.
    appID  = "xxxxx" 
    appKey = "xxxxx" 
    roomID = "room" // To generate a token for RTS, pass an empty value for it.
    userID = "uid"
)
t := AccessToken.New(appID, appKey, roomID, userID)
// Specify the expiration time for the token. The token will expire in 2 hours. After the token has expired, the user cannot join the room with it anymore.
t.ExpireTime(time.Now().Add(time.Hour * 2))
// Add privilege of subscribing.
t.AddPrivilege(AccessToken.PrivSubscribeStream, time.Time{})
// Add privilege of publishing.
t.AddPrivilege(AccessToken.PrivPublishStream, time.Time{})
// Get the token.
token,err := t.Serialize()
```



|Variable |Note |
|---|---|
|`appID` and `appKey` |You can copy them on the RTC console after adding the application. Refer to [Before Using RTC Service](https://docs.byteplus.com/en/docs/12/docs-69865). |
|`roomID` and `userID` |Refer to [Value Nomenclature](https://docs.byteplus.com/en/docs/12/docs-70114) for the naming guidance. |
|`ExpireTime` |The expiration time of the token. We recommend setting it to 24 hours. However, for data security reasons, we strongly advise against setting it for an excessively long time or to a perpetual value. |
|`PrivPublishStream` and `PrivSubscribeStream` |The expiration time of the Token's privilege of subscribing and publishing. At least one of them must be assigned to join the room.<br><br>If you need to control the privilege of publishing and subscribing through tokens, use **Native SDK v3.50.3+**  or **Web SDK v4.60+** . You also need to contact technical support to submit your request before the settings take effect. We recommend setting it to the same value as `ExpireTime`.<br><br>For earlier versions, these variables can be set to any values and will not have any effects, such as `0`. |


<span id="generate-temporary-token"></span>
### Generate temporary token

During app debugging, you can get the temporary tokens on the [console](https://console.byteplus.com/rtc/listRT?from=docC) without deploying the token generation service at your app server.

During debug, two or more devices are used for RTC calls in the same room. You should apply for a temporary token for each of the devices.

**Generation method**: Apply for the temporary token on [App Management](https://console.byteplus.com/rtc/listRTC).

During debugging, use the same roomID and userID that you use in your application.

> Do not use temporary tokens in production environments. They are intended only for debugging, as they have a short validation period and do not provide security guarantees.


<span id="verify-a-token"></span>
## Verify a token

You can verify the correctness and validity of a generated Token in the RTC console.

**Steps**:


1. Go to [RTC Console > Application Management](https://console.byteplus.com/rtc/listRTC?from=doc), select your application, and click **Verify token** in the Actions column.

2. Input your Token, RoomId, and UserId, and click **Verify**.

3. The verification result will be displayed below.


<span id="faq"></span>
## FAQ

For details, see [FAQ about Token](https://docs.byteplus.com/docs/byteplus-rtc/docs-1157360).
