---
title: "Real-time Signaling between Client and Application Server"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-79002"
---

You can refer to this article for code logic and API needed for different scenarios.

With real\-time signaling, the client can send text or binary messages to your app server, and the app server will receive the message through the `HTTP`/ `HTTPS POST` request from the `RTC` server. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/c2as1.png) </span>

An example of a message received by the app server is as follows:

```JSON
{  "message":"xxxx",
   "binary":false,
   "signature":"00160af4c8dcb758d00ce35adb3EQD24BQDeruMYfoMjmEDAGh5ZiAARgps6T5ZgcTz9bw5DewuRkzxBmTgnGEk+ZBv3mW5n58="
}
```


The above example contains fields explained as follows:


|Field |Definition |Type |Validation |
|---|---|---|---|
|message |Message content |string |/ |
|binary |Whether it is a binary message |bool |Not null |
|signature |Signature includes the sender's user ID and AppID for authentication |string |Not null |


<span id="send-peer-to-peer-messages-in-the-room"></span>
## Send peer\-to\-peer messages in the room

With real\-time signaling, the app server can send peer\-to\-peer text or binary messages to the client in the room. The client receives the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/c2as2.png) </span>

<span id="send-room-messages"></span>
## Send room messages

With real\-time signaling, the app server can send text or binary messages to all users in the room. The clients receive the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/c2as3.png) </span>

<span id="send-bulk-peer-to-peer-messages-in-the-room"></span>
## Send bulk peer\-to\-peer messages in the room

With real\-time signaling, the app server can send bulk text or binary messages to the specified user in the room. The client receives the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/c2as4.png) </span>

<span id="send-peer-to-peer-messages-to-the-user-outside-the-room"></span>
## Send peer\-to\-peer messages to the user outside the room

With real\-time signaling, the app server can send text or binary messages to the client without entering the room. The client receives the message through the callback. The logic is as follows:

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/%E9%AB%98%E7%BA%A7%E5%8A%9F%E8%83%BD/RTS/c2as5.png) </span>
