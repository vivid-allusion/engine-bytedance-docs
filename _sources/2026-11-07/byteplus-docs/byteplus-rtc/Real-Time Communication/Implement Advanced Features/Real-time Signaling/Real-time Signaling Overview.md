---
title: "Real-time Signaling Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-70425"
---

The RTC SDK provides stable and reliable real\-time signaling service with low latency and high concurrency, you can customize the service to meet the needs of real\-time data synchronization and efficient data transmission.

<span id="introduction"></span>
## Introduction

By calling the real\-time signaling APIs, you can achieve the following functions:

<span id="server-interface"></span>
### Server interface


|Feature |Description |
|---|---|
|Peer\-to\-peer messaging in the room |Send and receive text or custom\-formatted messages to a specific user in the room. |
|Broadcasting in the room |Send and receive messages such as text and custom format with all users in the room. |
|Sending bulk peer\-to\-peer messages outside the room |Send and receive bulk messages such as text messages and custom format with a specific user outside the room. |
|Peer\-to\-peer messaging outside the room |Send and receive messages such as text and custom format with a user outside the room. |


<span id="client-interface"></span>
### Client interface


|Feature |Description |
|---|---|
|Peer\-to\-peer messaging in the room |Send and receive text or custom\-formatted messages to a specific user in the room. |
|Broadcasting in the room |Send and receive messages such as text and custom format with all users in the room. |
|Peer\-to\-peer messaging outside the room |Send and receive messages such as text and custom format with a user outside the room. |
|Querying a user's online status |Query online status of the specified user. |


<span id="use-cases"></span>
## Use cases

You can use real\-time signaling in a variety of scenarios:


|Scenario |Description |
|---|---|
|Online education |Teachers send messages such as screenshots or group notifications in online classes. Students ask questions through text in online classes. |
|Interactive livestreaming |The administrator sends notifications to the entire audience in the LIVE room. The host sends a message to other hosts outside the room to initiate an online competition (PK). |
|Game streaming |The administrator sends notifications to the entire audience in the LIVE room. |
|Video conferencing |The host sends messages such as QR codes or pictures to everyone in the room. Meeting members send messages to users outside the room to invite them to the meeting. |


<span id="limitations-and-prerequisites"></span>
## Limitations and prerequisites


> * When you send peer\-to\-peer messages and room broadcast messages, the maximum size of the text or binary messages is 64KB.

> * When you send bulk peer\-to\-peer messages in a room, the maximum size of the text or binary messages is 64KB.

> * Make sure both sender and receiver have successfully entered the room before sending a message to a specified user in the room. The SDK notifies users that they have successfully entered the room via the `onJoinRoomResult` callback.

> * Make sure the sender has successfully entered the room before sending messages to all members in the room, and only users who have successfully entered the room can receive these messages. SDK will notify the user(s) of having successfully entered the room through `onJoinRoomResult` callback.


<span id="maximum-message-rate-in-a-room"></span>
### Maximum message rate in a room


|Concurrent online users in a single room |Maximum message number per second |
|---|---|
|1\-500 |100 |
|500\-1000 |80 |


> Note: If the number of messages per second exceeds the limit, the latency will increase significantly.


<span id="call-limit-on-client"></span>
### Call limit on client


|Scenario |Method(Android) |Call limit(Native) |Call limit(Linux) |
|---|---|---|---|
|Peer\-to\-peer messaging in the room |[sendUserMessage](https://docs.byteplus.com/en/docs/12/docs-70080#sendusermessage) |200 |1600 |
|Peer\-to\-peer messaging in the room |[sendUserBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#senduserbinarymessage) |200 |1600 |
|Broadcasting in the room |[sendRoomMessage](https://docs.byteplus.com/en/docs/12/docs-70080#sendroommessage) |200 |1600 |
|Broadcasting in the room |[sendRoomBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#sendroombinarymessage) |200 |1600 |
|Query the user's online status |[getPeerOnlineStatus](https://docs.byteplus.com/en/docs/12/docs-70080#getpeeronlinestatus) |10 |100 |
|Peer\-to\-peer messaging outside the room |[sendUserMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#sendusermessageoutsideroom) |200 |1600 |
|Peer\-to\-peer messaging outside the room |[sendUserBinaryMessageOutsideRoom](https://docs.byteplus.com/en/docs/12/docs-70080#senduserbinarymessageoutsideroom) |200 |1600 |
|Sending server\-to\-client messages |[setServerParams](https://docs.byteplus.com/en/docs/12/docs-70080#setserverparams) |5 |5 |
|Sending server\-to\-client messages |[sendServerMessage](https://docs.byteplus.com/en/docs/12/docs-70080#sendservermessage) |5 |5 |
|Sending server\-to\-client messages |[sendServerBinaryMessage](https://docs.byteplus.com/en/docs/12/docs-70080#sendserverbinarymessage) |50 |50 |


<span id="call-limit-on-the-server"></span>
### Call limit on the server


|Call limit(per second) |
|---|
|500 |


For each AppId, the combined call limit for the three OpenAPI methods (peer\-to\-peer, bulk peer\-to\-peer, and broadcast messages) is 500 calls per second.

<span id="pricing"></span>
## Pricing

For the billing rules, you can [speak to an expert](https://www.byteplus.com/en/contact).
