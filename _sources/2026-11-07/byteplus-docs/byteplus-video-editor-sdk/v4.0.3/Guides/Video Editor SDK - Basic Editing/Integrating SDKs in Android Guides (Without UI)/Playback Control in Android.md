---
title: "Playback Control in Android"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-playback-control-in-android"
---

This module explains the playback control interfaces and logic for video segments.

<span id="2b0d88c1"></span>
# Playback Control modules

The following are the Playback Control modules and their functions.

<span id="cbeec88b"></span>
## **Get Current Playback Position**

Retrieves the current playback position of the video.

```Kotlin
nleMediaSession.playerApi.currentPosition
```


<span id="9f0fec69"></span>
## **Get Total Duration of Playback**

Retrieves the total duration of the video being played.

```Kotlin
nleMediaSession.playerApi.duration
```


<span id="158167ab"></span>
## **Listen to Playback Status Changes**

Provides callbacks for various playback status changes, including play, pause, stop, and destroy events.

```Kotlin
nleMediaSession.playerApi.setPlayerStatusListener(object : INLEListenerPlayerStatus {

    override fun onPlay() {
         //Start playback
    }

    override fun onPause() {
        //Pause (corresponds to: nleMediaSession.playerApi.pause())
    }

    override fun onStop() {
        //Stop playback (corresponds to: nleMediaSession.playerApi.stop())
    }

    override fun onDestroy() {
        //Destroy the player (corresponds to: nleMediaSession.playerApi.destroy())
    }
})
```


<span id="c303a732"></span>
## **Video Playback Progress Callback**

Monitors video playback progress and provides information about the source (play or seek) and the current playback time.

```Kotlin
nleMediaSession.playerApi.setVideoOutputListener { source, time ->
    //source -> 0:play 1:seek
    // time: Current playback progress
    if (time >= nleMediaSession.playerApi.duration) {
        return@setVideoOutputListener
    }
    if (nleMediaSession.playerApi.state() == NLEPlayerState.STARTED) {
        //Perform actions using the 'time' field
    }
}
```


<span id="985a77b2"></span>
## **Determine the End of Playback**

Detects the end of video playback and takes appropriate actions. Ensure to remove the listener when the page is destroyed.

```Kotlin
private var playInfoListener: INLEListenerCommon = INLEListenerCommon { type, ext, f, msg ->
    //Playback end
    if (VECommonCallbackInfo.TE_INFO_EOF == type) {
        nleMediaSession.playerApi.pause()
    }
}

nleMediaSession.playerApi.addOnInfoListener(playInfoListener)

//When the page is destroyed
nleMediaSession.playerApi.removeOnInfoListener(playInfoListener)
```
