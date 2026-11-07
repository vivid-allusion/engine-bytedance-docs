---
title: "Chatting Room Overview"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-117919"
---

A voice chat room is a virtual online room, where the room owner holds a live audio broadcast. The room has guest seats for the room owner to manage and invite audiences to become guests or ban the guests on the mic. Real\-time voice interaction is more interactive, authentic, and easier than text chat. Users do not need to worry about the images they present in front of others in voice chat, which makes users feel relaxed in interactions. That is how voice chat gains its popularity in social networking.

An RTC room can accommodate a maximum of 50 visible users, and 30 media streams can be published simultaneously. For more information, see [Room Capacity](https://docs.byteplus.com/en/docs/12/docs-257549). There are usually the following 3 roles in a voice chat room during live streaming:


* Room owner (host): The user who creates the voice chat room has the permission to manage the room and guest seats, such as inviting someone to become a guest, and removing someone from the guest seat.

* Guest: After a user enters the voice chat room, the user can apply to be a guest or be invited to become a guest by the room owner, and the user can chat in real time with the room owner and other guests in the room.

* Audience: After a user enters the voice chat room as an audience member, the user can listen to the chat between the room owner and the speaking guests.


<span id="how-to-play"></span>
## How to Play


* Voice Chat + Mini\-games: In a game room, the host can chat with speaking guests while playing mini\-games (e.g., Turtle Soup, Truth or Dare, Who is Undercover). Audiences are more active in the interactions as guests in a more interactive and fun room. The combination of voice chat and mini\-games is more entertaining when it simulates how users play games offline.

* Voice Chat + Karaoke: In the chat room, the speaking guests can pick and sing songs to show their talent. While the guest is singing, the room owner can control whether other speaking guests can speak; The host or guests can also engage users with activities like "guess the song" games or group sing\-alongs.

* Chat + Dating/Matchmaking: In the voice chat room, the room owner usually acts as a moderator or a matchmaker, guiding the guests to discuss topics and get to know one another better. To increase revenue, there's often a special guest seat that can only be unlocked by sending a specific value of in\-app gifts.

* Voice Chat + Watching Videos or Listening to Audios Together: In the voice chat room, all users can watch videos such as movies, TV dramas, variety shows, and live games together, or listen to music together while discussing relevant topics. This creates a sense of immersive, real\-time companionship for users to socialize with acquaintances, as well as topics for them to socialize with strangers.


<span id="technical-structure"></span>
## Technical Structure

Users on the mic can push audio streams to other users in the RTC room and subscribe to them. Those not on the mic can only subscribe to such audio streams in the RTC room.

<span>![图片](https://sf16-sg.tiktokcdn.com/obj/eden-sg/jvKJ%5BY/ljhwZthlaukjlkulzlp/Img/usecase/chattingroom/structure.png) </span>

<span id="feature-list"></span>
## Feature List


|Main feature |Description |
|---|---|
|Real\-time voice interaction |The room owner and guests can have real\-time audio interactions in the voice chat room. |
|Audio live streaming |Audiences can listen to real\-time audio interactions between users on the mic. |
|Invite to be a guest |The room owner can invite audience members to be guests. After accepting the invitation, such audience members become guests so they can have real\-time audio interactions with the room owner and other guests. |
|Apply to be a guest |Audiences can apply to be guests. After being accepted by the room owner, such audiences become guests so they can have real\-time audio interactions with the room owner and other guests. |
|Background music |Music can be played in the room for all users to listen to, creating an atmosphere that suits the theme of the room. |
|Guest seat management |The room owner can manage guest seats through actions such as inviting users to become guests, removing guests, muting or unmuting them, and locking or unlocking seats. |
|Real\-time signaling |Users in the voice chat room can communicate in real\-time by sending texts or images. |
|Comments/gifts |Users in voice chat rooms can post live comments or send gifts to their favorite guests/streamers. |


<span id="advantages"></span>
## Advantages


* **High\-quality audio practices for business scenarios**

   The service supports 48kHz full\-band sampling and provides exclusive 3A optimization for real\-time scenarios.

   Supports custom cloud\-based parameter configurations and audio routing for premium audio experience.

* **Global high\-quality network coverage** **with** **unlimited concurrent capacity**

   Over 300 selected nodes around the world, a global network transmission latency of 400 ms or less for at least 99.5% of connections. Dedicated network access and scheduling optimization are provided for regions with poor infrastructure across Southeast Asia, the Middle East, South Africa, etc.; such services have covered small\- and medium\-sized service providers as well as third\-tier and fourth\-tier cities across China.

   Elastic and scalable network structure design, 100% traffic redundancy, minute\-level automatic expansion, and unlimited theoretical concurrency of the entire network.

* **Diverse gameplay for more scenarios to drive business growth**

   Robust music mixing and video effect capabilities provide an ultra\-low latency karaoke singing experience for users; reverb, voice changer and other features to add more fun to chatting; support for obtaining volume and audio spectrum data, which enables features like audio visualizers.
