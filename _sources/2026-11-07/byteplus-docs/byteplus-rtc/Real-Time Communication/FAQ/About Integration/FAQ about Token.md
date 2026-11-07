---
title: "FAQ about Token"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1157360"
---

<span id="what-is-token"></span>
### What is Token?

Token is a parameter that users must pass when entering a room, used for authentication on the RTC server.

<span id="when-is-token-required"></span>
### When is Token required?

Token is required for authentication, when every user enters a room.

<span id="is-token-required-during-the-testing-phase-how-to-obtain-it"></span>
### Is Token required during the testing phase? How to obtain it?

Yes. You can generate a temporary Token on the BytePlus Console, or you can refer to the Token generation example code to generate a test Token locally. For details, please refer to [Authentication with Token](https://docs.byteplus.com/en/docs/12/docs-70121).

Note: Before you project is launched, you need to integrate the logic of generating Token into your business server and distribute Tokens to users for joining room.

<span id="why-do-i-receive-the-error-code-1000-in-the-onroomstatechanged-callback-after-calling-joinroom"></span>
### Why do I receive the error code `-1000` in the `onRoomStateChanged` callback after calling `joinRoom`?

Only when `onRoomStateChanged` returns `state=0`, it means that joining room is successful. The error code `-1000` indicates a Token error. In this case, you need to check:


* Whether the `appId` passed in `createRTCVideo` and the `roomid` and `userid` passed in `joinRoom` are consistent with the `appId`, `roomid`, and `userid` used to generate the Token.

* Check if the `expire_time` passed in the Token generation has expired.

   The value of `expire_time` is a timestamp, not the length of the expiration time. For example, the image below represents an expiration time of 1 hour from the current time. You need to write the timestamp of the current time plus 1 hour, instead of writing `3600`.

   <span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Token/token.png) </span>

* Check if the expiration time set in `addPrivilege` has expired.

   In general, there is no need to separately control the expiration time of the permission of pushing or pulling streams. It is recommended to keep it consistent with `expireTime`.


<span id="what-is-the-maximum-validity-period-of-a-token"></span>
### What is the maximum validity period of a Token?

After the Token is generated, the maximum validity period is 7 days. If the Token is not used to join a room within 7 days, it will still expire. In this case, using it will result in a failed joining room.

> The maximum stay time for a user in a room is 3 days. Even if the Token has not expired, if users have stayed in the room for 3 days, they will be kicked out of the room, and the client sides will receive the `onTokenWillExpire` callback before users being kicked out.


<span id="if-the-token-expires-after-entering-the-room-will-the-user-be-kicked-out-of-the-room"></span>
### If the Token expires after entering the room, will the user be kicked out of the room?

Yes. 30 seconds before the Token expires, the client will receive the `onTokenWillExpire` callback. At this time, the client needs to call `updateToken` and pass in a new unexpired Token in order for the user to continue with audio and video interaction. Otherwise, the user will be kicked out of the room.

<span id="will-the-server-receive-a-callback-when-the-token-expires-and-the-user-is-kicked-out-of-the-room"></span>
### Will the server receive a callback when the Token expires and the user is kicked out of the room?

Yes. Taking a visible user as an example, after being kicked out of the room due to Token expiration, the server will receive the `UserLeaveRoom` event callback, with the reason being `onUserTokenDidExpire`.
