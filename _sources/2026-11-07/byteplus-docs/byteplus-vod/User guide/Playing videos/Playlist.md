---
title: "Playlist"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-playlist"
---

BytePlus VOD supports the playlist feature, which allows you to automatically play videos in a given video list in sequential order. With a playlist, you can engage your viewers with a collection of your videos.

<span id="d21a8fa4"></span>
## **Introduction**

The diagram below demonstrates the interactions between different participants in a playlist scenario. It showcases the flow of actions involved in playlist management and playback.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/383dd4bbb04246f18a42e3d4cab6b12e~tplv-goo7wpa0wc-image.image) </span>

The participants involved in this sequence are as follows:


* **End user**: Represents the user who interacts with the browser or app to initiate actions.

* **Website/app**: Your application or website used by the end user. It is integrated with the BytePlus VOD Player SDK to facilitate playlist functionality.

* **Player SDK**: Refers to the BytePlus VOD Player SDK.

* **App server**: Refers to the server component of your application responsible for managing the creation and retrieval of playlists.

* **Server SDK**: Refers to the BytePlus VOD [Server SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk), which is used by the app server for communication with the BytePlus VOD Service.

* **BytePlus VOD Service**: The service that handles video storage and manages various video\-related information, including playlists.

* **BytePlus CDN Service**: This represents the Content Delivery Network (CDN) service provided by BytePlus, responsible for efficiently delivering video content to end users.


<span id="3e608067"></span>
## Procedure

The following section walks you through the interactions between these participants in detail:

<span id="2e359d49"></span>
### Step 1: Prepare the playlist

There are two methods to prepare the playlist.

<span id="ae1d661a"></span>
#### Method 1: Console configuration

You can create, edit, delete, and view playlists on the console. See [Playlist management](https://docs.byteplus.com/docs/byteplus-vod/docs-playlist-management) for details.

<span id="dc8b85c8"></span>
#### Method 2: API configuration


1. The app server communicates with the BytePlus VOD Service to create a playlist by calling [CreatePlaylist](https://docs.byteplus.com/docs/byteplus-vod/reference-createplaylist). Upon successful creation, the playlist ID is then returned to the app server.

2. When an end user enters a URL within the app, the app requests the playlist from the app server.

3. The app server retrieves the playlist information from the BytePlus VOD Service by making a request with the playlist ID using the [GetPlaylists](https://docs.byteplus.com/docs/byteplus-vod/reference-getplaylists) API.

4. The playlist information is returned to the app server along with a `playAuthToken`.

5. Finally, the app server sends the playlist and `playAuthToken` back to the app.


<span id="3fef07e2"></span>
### Step 2: Initiate video playback

BytePlus VOD provides demos showcasing the playlist feature. Refer to these demos for a hands\-on experience or review the sample code.


* Android & iOS: [Playlist demo](https://docs.byteplus.com/en/docs/byteplus-vos/docs-vod-playlist)

* Web: [Playlist demo](https://demo.byteplus.com/common/veplayer/basic/example?tab=function-display)


<span id="3e41a734"></span>
#### Initiate the player and play a video


1. The app creates a player using the Player SDK.

2. The Player SDK renders the playlist UI.

3. The Player SDK requests playback information from the BytePlus VOD Service using the `playAuthToken`.

4. The BytePlus VOD Service provides the video URL to the Player SDK.

5. The Player SDK retrieves the video from the BytePlus CDN Service by accessing the provided URL.

6. The video is played by the Player SDK.


<span id="2215792d"></span>
#### Switch to the next video in the playlist


1. The end user requests to switch to the next video in the playlist.

2. If the switch is manual, the Player SDK requests playback information for the next video from the BytePlus VOD Service using the `playAuthToken`. The Player SDK receives the video URL for the next video and plays it.

3. If the switch is automatic or looping, the Player SDK continuously monitors the current video's end event. When the current video ends, the Player SDK requests playback information for the next video from the BytePlus VOD Service using the `playAuthToken`. The Player SDK receives the video URL for the next video and plays it.
