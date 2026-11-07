---
title: "Real-time Signaling across RTC Rooms"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79000"
---

You can refer to this article for code logic and API needed for different scenarios.

<span id="send-peer-to-peer-messages-in-the-room"></span>
## Send peer\-to\-peer messages in the room

<span id="code-logic"></span>
### Code logic

With real\-time signaling, the sender can communicate with the receiver by sending peer\-to\-peer text or binary messages to the server. The receiver receives the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/p2p-message-in-room-code-logic.png) </span>

<span id="api-reference"></span>
### API reference


|No. |Code logic |Android |iOS |Windows |
|---|---|---|---|---|
|1 |Join a room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) |[JoinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) |
|2 |Callback for result of joining the room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) |[rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) |[OnRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) |
|3 |Send text message to specific user in the room |[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendusermessage) |[sendUserMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendusermessage-message-config) |[SendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendusermessage) |
|4 |Receive the text message from the sender |[onUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagereceived) |[rtsRoom:onUserMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagereceived-message) |[OnUserMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagereceived) |
|5 |Send binary message to specific user in the room |[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-senduserbinarymessage) |[sendUserBinaryMessage:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-senduserbinarymessage-message-config) |[SendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-senduserbinarymessage) |
|6 |Receive binary messages from the sender |[onUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onuserbinarymessagereceived) |[rtsRoom:onUserBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onuserbinarymessagereceived-message) |[OnUserBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onuserbinarymessagereceived) |
|7 |View message sending result |[onUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onusermessagesendresult) |[rtsRoom:onUserMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onusermessagesendresult-error) |[OnUserMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onusermessagesendresult) |


<span id="send-room-messages"></span>
## Send room messages

<span id="code-logic"></span>
### Code logic

With real\-time signaling, the sender can communicate with the receivers by sending peer\-to\-peer text or binary messages to the server. The receivers receive the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/room-message-code-logic.png) </span>

<span id="api-reference"></span>
### API reference


|No. |Code logic |Android |iOS |Windows |
|---|---|---|---|---|
|1 |Join a room |[joinRoom](https://docs.byteplus.com/en/docs/12/docs-70080#joinroom) |[joinRoom:userInfo:userVisibility:roomConfig:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRoom-joinroom-userinfo-uservisibility-roomconfig) |[JoinRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCRoom-joinroom) |
|2 |Callback reports the result of joining the room |[onRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCRoomEventHandler-onroomstatechanged) |[rtcRoom:onRoomStateChanged:withUid:state:extraInfo:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRoomDelegate-rtcroom-onroomstatechanged-withuid-state-extrainfo) |[OnRoomStateChanged](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroomstatechanged) |
|3 |Send text message to all users in the room |[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroommessage) |[sendRoomMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroommessage) |[SendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendroommessage) |
|4 |Receive text broadcast message in the room |[onRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagereceived) |[rtsRoom:onRoomMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagereceived-message) |[OnRoomMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagereceived) |
|5 |Send binary messages to all users in the room |[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#RTSRoom-sendroombinarymessage) |[sendRoomBinaryMessage:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCRTSRoom-sendroombinarymessage) |[SendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70095#IRTSRoom-sendroombinarymessage) |
|6 |Receive binary broadcast message in the room |[onRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroombinarymessagereceived) |[rtsRoom:onRoomBinaryMessageReceived:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroombinarymessagereceived-message) |[OnRoomBinaryMessageReceived](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroombinarymessagereceived) |
|7 |Get the result of sending room messages |[onRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTSRoomEventHandler-onroommessagesendresult) |[rtsRoom:onRoomMessageSendResult:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCRTSRoomDelegate-rtsroom-onroommessagesendresult-error) |[OnRoomMessageSendResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTSRoomEventHandler-onroommessagesendresult) |


<span id="send-peer-to-peer-messages-to-the-user-outside-the-room"></span>
## Send peer\-to\-peer messages to the user outside the room

<span id="code-logic"></span>
### Code logic

With real\-time signaling, the sender can communicate with the user outside the room by sending peer\-to\-peer text or binary messages to the server. The receiver receives the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/p2p-outside-room-message-code-logic.png) </span>

<span id="api-reference"></span>
### API reference


|No. |Code logic |Android |iOS |Windows |
|---|---|---|---|---|
|1 |Log in |[login](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-login) |[login:uid:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-login-uid) |[Login](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-login) |
|2 |Receive the result of login |[onLoginResult](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onloginresult) |[rtcEngine:onLoginResult:errorCode:elapsed:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onloginresult-errorcode-elapsed) |[OnLoginResult](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onloginresult) |
|3 |Renew the token used for login (optional) |[update Login Token](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-updatelogintoken) |[update Login Token:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-updatelogintoken) |[Update Login Token](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-updatelogintoken) |
|4 |Query the online status of local or remote user (optional) |[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-getpeeronlinestatus) |[getPeerOnlineStatus:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-getpeeronlinestatus) |[GetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-getpeeronlinestatus) |
|5 |Get the result of online status query (optional) |[onGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-ongetpeeronlinestatus) |[rtcEngine:onGetPeerOnlineStatus:status:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-ongetpeeronlinestatus-status) |[OnGetPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-ongetpeeronlinestatus) |
|6 |Send text messages to users outside the room |[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-sendusermessageoutsideroom) |[sendUserMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-sendusermessageoutsideroom-message-config) |[SendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-sendusermessageoutsideroom) |
|7 |Receive the text messages from user outside the room |[onUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |[rtcEngine:onUserMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onusermessagereceivedoutsideroom-message) |[OnUserMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagereceivedoutsideroom) |
|8 |Send binary messages to users outside the room |[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-senduserbinarymessageoutsideroom) |[sendUserBinaryMessageOutsideRoom:message:config:](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-senduserbinarymessageoutsideroom-message-config) |[SendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-senduserbinarymessageoutsideroom) |
|9 |Receive binary messages from users outside the room [onUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) |[rtcEngine:onUserBinaryMessageReceivedOutsideRoom:message:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onuserbinarymessagereceivedoutsideroom-message) |[OnUserBinaryMessageReceivedOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onuserbinarymessagereceivedoutsideroom) | |
|10 |Get the result of sending messages |[onUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |[rtcEngine:onUserMessageSendResultOutsideRoom:error:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onusermessagesendresultoutsideroom-error) |[OnUserMessageSendResultOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onusermessagesendresultoutsideroom) |
|11 |Log out |[logout](https://docs.byteplus.com/en/docs/12/docs-70080#RTCEngine-logout) |[logout](https://docs.byteplus.com/en/docs/12/docs-70086#ByteRTCEngine-logout) |[Logout](https://docs.byteplus.com/en/docs/12/docs-70095#IRTCEngine-logout) |
|12 |Receive logout result |[onLogout](https://docs.byteplus.com/en/docs/12/docs-70081#IRTCEngineEventHandler-onlogout) |[rtcEngine:onLogout:](https://docs.byteplus.com/en/docs/12/docs-70087#ByteRTCEngineDelegate-rtcengine-onlogout) |[OnLogout](https://docs.byteplus.com/en/docs/12/docs-70096#IRTCEngineEventHandler-onlogout) |
