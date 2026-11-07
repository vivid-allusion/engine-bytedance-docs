---
title: "TVUSinglePlayerView"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/tvusingleplayerview"
---

The custom player's `TVUSinglePlayerView` instance supports customization of the video control interface.

<span id="ef40d04f"></span>
## Member Functions

<span id="bf477a17"></span>
### Init

Calls the `init` method to get the `InitConfig` parameter and initialize the custom player's `TVUSinglePlayerView` instance.

```Java
public void init(InitConfig config)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|config |[InitConfig](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#142a3b71) |The initialization configuration of the custom player. |


<span id="615a183b"></span>
### refreshLive

Refreshes the current live stream. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `2`.

```Java
public void refreshLive()
```


<span id="1be9767d"></span>
### play

Plays the video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is not `0`.

```java
public void play()
```


<span id="c5ee7ddf"></span>
### pause

Pauses the video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is not `0`.

```java
public void pause()
```


<span id="4d7c8619"></span>
### isPlaying

Gets whether the video is playing.

```java
public boolean isPlaying()
```


**Return Value**


* `true`: The video is playing.

* `false`: The video is not playing.


<span id="3a0455cd"></span>
### getPlayableStatus

Gets the current playable status of resources.

```java
public int getPlayableStatus()
```


**Return Value**


* `0`: No resources are playable, so you cannot call the [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#1be9767d) method.

* `1`: Video On Demand (VOD) videos are playable. You can call the [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#1be9767d) method to play the videos.

* `2`: A live stream is playable. You can call the [play](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#1be9767d) method to play the video.


<span id="04ae6102"></span>
### isStalling

Gets whether the video is stuttering.

```java
public boolean isStalling()
```


**Return Value**


* `true`: The video is stuttering.

* `false`: The video is not stuttering.


<span id="34c994a8"></span>
### setPlayerLayoutMode

Sets the video scaling mode.

```java
public void setPlayerLayoutMode(int playerLayoutMode)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|playerLayoutMode |Integer |The video scaling mode. Valid values:<br><br><br>* `0`: `ImageAspectFit`. Fill the player and keep the video's aspect ratio. The width or height of the video fills the width or height of the player. If the aspect ratio of the video is different from that of the player, the video is scaled to fit, with no content cropping.<br><br>* `1`: `ImageToFill`. Fill the player with the video. The aspect ratio of the video may be changed.<br><br>* `2`: `ImageAspectFill`. Fill the player and keep the video's aspect ratio. The width of the video fills the width of the player, and the height of the video fills the height of the player. If the aspect ratio of the video is different from that of the player, the video is cropped to fit. |


<span id="944e752b"></span>
### getResolutions

Gets the list of currently supported resolutions. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is not `0`.

```java
public String[] getResolutions()
```


**Return Value**

The list of resolutions currently supported.

<span id="87d359b1"></span>
### getCurResolution

Gets the currently selected resolution. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is not `0`.

```java
public String getCurResolution()
```


**Return Value**

The currently selected resolution.

<span id="39974b24"></span>
### setCurResolution

Sets the resolution for the current video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is not `0`.

```java
public void setCurResolution(String resolution)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|resolution |String |The resolution. |


<span id="5741df2b"></span>
### getCurVodPlayTime

Gets the playback progress of the current VOD video. The unit is ms. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```java
public int getCurVodPlayTime()
```


**Return Value**

The playback progress of the current VOD video.

<span id="73d37e7d"></span>
### seekVodTime

Seeks to a specified playback progress in the current VOD video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```java
public void seekVodTime(int timeInMills, SeekCompletionListener listener)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|timeInMills |Integer |The specified playback progress in the current VOD video. Unit: ms. |
|listener |[SeekCompletionListener](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#a24195f6) |The callback triggered when the seek operation is complete. |


<span id="708726e4"></span>
### getCurVodDuration

Gets the duration of the current VOD video. The unit is ms. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```Java
public int getCurVodDuration()
```


**Return Value**

The duration of the current VOD video.

<span id="13db6157"></span>
### getCurVodPlaySpeed

Gets the playback speed of the current VOD video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```Java
public float getCurVodPlaySpeed()
```


**Return Value**

The playback speed of the current VOD video. This is a floating point number within the range of (0,2].

If no VOD video is playing, `-1` is returned.

<span id="83257226"></span>
### setMute

Sets whether to mute the video.

```java
public void setMute(boolean isMute)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|isMute |Boolean |Whether to mute the video. Default value: `false`. Valid values:<br><br><br>* `true`: Mute.<br><br>* `false`: Do not mute. |


<span id="d5db245a"></span>
### setVodLoop

Sets whether to loop the VOD video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```java
public void setVodLoop(boolean isLoop)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|isLoop |Boolean |Whether to loop the VOD video. Valid values:<br><br><br>* `true`: Loop<br><br>* `false`: Do not loop. |


<span id="8c9860a0"></span>
### setVodPlaySpeed

Sets the playback speed of the VOD video. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```java
public void setVodPlaySpeed(float playSpeed)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|playSpeed |Float |The playback speed. Value range: (0,2] |


<span id="b16ac95d"></span>
### setInBackground

When the page containing the custom player runs in the background, call this method to notify the player.

```Java
public void setInBackground(boolean inBackground)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|inBackground |Boolean |Whether the page containing the custom player runs in the background. Valid values:<br><br><br>* `true`: In the background.<br><br>* `false`: In the foreground. |


<span id="b025f007"></span>
### getLiveRoomStatus

Gets the live room status.

```Java
public int getLiveRoomStatus()
```


**Return Value**


* `0`: Cannot get the live room status since the `TVULiveRoomServer` instance is not started.

* `1`: Live.

* `2`: Preview.

* `3`: Playback.

* `4`: Over.


<span id="0afd14cd"></span>
### getCurVodVid

Gets the video ID (Vid) of the current VOD video. This method is suitable for a live room with multiple playbacks. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1`.

```Java
public String getCurVodVid()
```


**Return Value**

The Vid of the current VOD video. If no VOD video is playing, an empty string is returned.

<span id="d6b57534"></span>
### getCurReplayList

Gets the current playback list. This method is suitable for a live room with multiple playbacks. You can call this method when the return value of [getPlayableStatus](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#3a0455cd) is `1` and that of [getLiveRoomStatus ](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#b025f007)is `3`.

```Java
public List<Replay> getCurReplayList()
```


**Return Value**

The current playback list. If the live room has no playbacks, an empty array is returned.

<span id="5cee58ed"></span>
### getCurLiveLineId

Gets the current live source ID. This method is suitable for a live room with multiple live sources. You can call this method when the return value of [getLiveRoomStatus ](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#b025f007)is `1`.

```Java
public long getCurLiveLineId()
```


**Return Value**

The current live source ID. If the return value of [getLiveRoomStatus ](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#b025f007)is not `1`, `0` is returned.

<span id="54d87f03"></span>
### getCurLiveLineList

Gets the current live source list. This method is suitable for a live room with multiple live sources. You can call this method when the return value of [getLiveRoomStatus ](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#b025f007)is `1`.

```Java
public List<PullStreamUrl> getCurLiveLineList() 
```


**Return Value**

The current live source list. If the return value of [getLiveRoomStatus ](https://docs.byteplus.com/docs/byteplus-livesaas/tvusingleplayerview#b025f007)is not `1`, an empty array is returned.

<span id="f66fc68c"></span>
### setCoverImageContainerVisibility

Sets the visibility of the live room's cover image container.

```Java
public void setCoverImageContainerVisibility(int visibility)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|visibility |Integer |The visibility of the live room's cover image container. Default value:[ ](https://developer.android.com/reference/android/view/View#VISIBLE)[View.VISIBLE](https://developer.android.com/reference/android/view/View#VISIBLE). |
