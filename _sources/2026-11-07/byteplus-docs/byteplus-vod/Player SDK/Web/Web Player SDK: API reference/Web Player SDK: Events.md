---
title: "Web Player SDK: Events"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-player-sdk-events"
---

<span id="mediaevents"></span>
## MediaEvents  

Player media events. Triggered by the browser `video` element and proxied by the SDK.


* **Member**

   
   |Property |Value |Description |
   |---|---|---|
   |ABORT |`'abort'` |Triggered when playback is aborted, e.g. when a playing video restarts. |
   |CANPLAY |`'canplay'` |Triggered when enough data has buffered to start playback. |
   |CANPLAY_THROUGH |`'canplaythrough'` |Triggered when enough data has buffered for smooth playback. |
   |DURATION_CHANGE |`'durationchange'` |Triggered when the media duration changes. |
   |EMPITED |`'empited'` |(Deprecated) Triggered when media is emptied, usually during initialization. |
   |EMPTIED |`'emptied'` |Triggered when media is emptied, usually during initialization. |
   |ENDED |`'ended'` |Triggered when video playback ends. |
   |ERROR |`'error'` |Triggered when an error occurs. |
   |LOADED_DATA |`'loadeddata'` |Triggered when startup playback data has finished loading. |
   |LOADED_META_DATA |`'loadedmetadata'` |Triggered when media metadata is loaded; all `video` properties are available via `playerSdkIns.player.video`. |
   |LOAD_START |`'loadstart'` |Triggered when media content starts loading. |
   |PAUSE |`'pause'` |Triggered when video playback pauses. |
   |PLAY |`'play'` |Triggered when video playback starts. |
   |PLAYING |`'playing'` |Triggered when playback resumes after pause or buffering. |
   |PROGRESS |`'progress'` |Reports media download progress, i.e. buffered playback data progress. |
   |RATE_CHANGE |`'ratechange'` |Triggered when the playback rate changes. |
   |SEEKED |`'seeked'` |Triggered when a seek operation completes. |
   |SEEKING |`'seeking'` |Triggered when a seek operation starts. |
   |STALLED |`'stalled'` |Triggered when attempting to fetch media data that is unavailable. |
   |SUSPEND |`'suspend'` |Triggered when media resource loading is suspended, e.g. download complete or paused for other reasons. |
   |TIME_UPDATE |`'timeupdate'` |Triggered when the playback time updates. |
   |VOLUME_CHANGE |`'volumechange'` |Triggered when the volume changes. |
   |WAITING |`'waiting'` |Triggered while waiting for data to load. |
   


<span id="sdkevents"></span>
## SDKEvents  

SDK events, triggered internally by the SDK.


* **Member**

   
   |Name |Value |Description |
   |---|---|---|
   |READY |`'ready'` |Triggered when the player instance is created. |
   |COMPLETE |`'complete'` |Triggered when the player has created the `video` element and playback can start. |
   |URL_CHANGE |`'urlchange'` |Triggered when the playback resource changes. |
   |PLAYER_FOCUS |`'focus'` |Triggered when the player gains focus; the control bar is shown. |
   |PLAYER_BLUR |`'blur'` |Triggered when the player loses focus; the control bar is hidden. |
   |FULLSCREEN_CHANGE |`'fullscreen_change'` |Triggered when native fullscreen state changes. |
   |CSS_FULLSCREEN_CHANGE |`'cssFullscreen_change'` |Triggered when CSS fullscreen state changes. |
   |MINI_STATE_CHANGE |`'mini_state_change'` |Triggered when mini player (floating) mode changes. |
   |DESTROY |`'destroy'` |Triggered when the player is destroyed. |
   |REPLAY |`'replay'` |Triggered when replay starts. |
   |RETRY |`'retry'` |Triggered when the player retries playback. |
   |DEFINITION_CHANGE |`'definition_change'` |Triggered when the definition (resolution) changes. |
   |VIDEO_RESIZE |`'video_resize'` |Triggered when the player container size changes. |
   |PIP_CHANGE |`'pip_change'` |Triggered when Picture\-in\-Picture state changes. |
   |ROTATE |`'rotate'` |Triggered when the player is rotated. |
   |SHORTCUT |`'shortcut'` |Triggered when a built\-in keyboard shortcut is used. |
   |SEI_PARSED |`'SEI_PARSED'` |(Deprecated) SEI information parsing. |
   |USER_ACTION |`'user_action'` |Triggered when user actions within plugins are performed. All plugin user actions will trigger this event, which can be used for user behavior tracking. |
   |AUTOPLAY_STARTED |`'autoplay_started'` |Triggered when autoplay succeeds. |
   |AUTOPLAY_PREVENTED |`'autoplay_was_prevented'` |Triggered when autoplay fails. |
   |PLAYER_CREATED_FINISH |`'player_create_finish'` |Triggered when player creation completes. |
   |PLAYER_REBUILD |`'player_rebuild'` |Triggered when the player is rebuilt. |
   |NOT_SUPPORT_HARDWARE_DECODER |`'not_support_hardware_decoder'` |Triggered when hardware decoding is not supported. |
   |NOT_SUPPORT_SOFT_DECODER |`'not_support_soft_decoder'` |Triggered when software decoding is not supported. |
   |TOKEN_EXPIRED |`'playAuthToken_expired'` |Triggered when `playAuthToken` expires. |
   |UMD_LOAD_FAIL |`'umd_load_fail'` |Triggered when UMD loading fails. |
   |PLAYNEXT |`'playnext'` |Triggered when switching to the next video, after calling `playNext`. |
   |URL_NULL |`'urlNull'` |Triggered when the video URL is empty. |
   |LEAVE_PLAYER |`'leaveplayer'` |Triggered when the mouse leaves the player. |
   |ENTER_PLAYER |`'enterplayer'` |Triggered when the mouse enters the player. |
   |RESET |`'reset'` |Triggered when the player state is reset. |
   |SOURCE_ERROR |`'source_error'` |Triggered when a `<source>` fails to load (unsupported or playback failed). |
   |SOURCE_SUCCESS |`'source_success'` |Triggered when a `<source>` loads successfully. |
   |LICENSE_STATUS_WARNING |`'license_status_warning'` |License status warning. |
   |AUDIO_TRACKS_UPDATED |`'audio_tracks_updated'` |Triggered when the HLS audio track list updates. `data.audioTracks` is the full track array. |
   |AUDIO_TRACK_CHANGE |`'audio_track_change'` |Triggered when audio track switching completes. `data.id` is the new track id; `data.audioTrack` is the full track object. |
   


**Example**

Listen to player creation completion

```typescript
playerSdkIns.on(VePlayer.Events.COMPLETE, () => {
  // can execute the apis and get the attributes of player core after sdk build complete
  console.log('player core: ', playerSdkIns.player);
})
```


Listen to definition change

```typescript
playerSdkIns.on(VePlayer.Events.DEFINITION_CHANGE, (data) => {
  const { to } = data;
  const { definition, url } = to;
  console.log('target definition is ', definition);
  console.log('target url is ', url);
})
```


Listen to fullscreen change

```typescript
playerSdkIns.on(VePlayer.Events.FULLSCREEN_CHANGE, (isFullScreen) => {
  console.log('current fullscreen: ', isFullScreen);
})
```


<span id="pluginevents"></span>
## PluginEvents  

Plugin events, triggered internally by plugins.


* **Member**

   
   |Name |Value |Description |
   |---|---|---|
   |DANMU_CHANGE |`'danmu_change'` |Triggered when danmu (bullet comment) configuration changes. |
   |CANCEL_UNMUTE |`'cancel_unmute'` |Triggered when unmute is cancelled. |
   |REFRESH_CLICK |`'refresh_click'` |Triggered when the refresh button is clicked. |
   |PLAY_BACKUP_CHANGE |`'play_backup_change'` |Triggered when playback demotes to a backup URL after an error. |
   |PLAY_BACKUP_CHANGE_FINISH |`'play_backup_change_finish'` |Triggered when error\-triggered demotion finishes. |
   |PLAY_ERROR_BUTTON_CLICK |`'play_error_button_click'` |Triggered when the error retry button is clicked. |
   |PlAY_URL_CHANGE |`'play_url_change'` |Triggered when the playback URL changes. |
   |SHOW_PLAY_ERROR |`'show_play_error'` |Triggered when the error UI is shown. |
   |LONG_WAITING |`'long_waiting'` |Triggered on prolonged stalling. The player may auto\-demote definition or prompt the user to switch manually. |
   |OFTEN_WAITING |`'often_waiting'` |Triggered on frequent stalling. |
   |DEFINITION_DEMOTE |`'definition_demote'` |Triggered when definition is demoted. |
   |INNER_DEFINITION_CHANGE |`'inner_definition_change'` |Triggered when definition changes. |
   |LINE_CHANGE |`'line_change'` |Triggered when the CDN line (route) changes. |
   |GET_PLAY_URL_ERR |`'get_play_url_err'` |Triggered when fetching the URL via `playAuthToken` fails. |
   |MEDIA_EXPIRED |`'MEDIA_EXPIRED'` |Triggered when the media resource has expired. |
   |MIRROR_CHANGE |`'mirror_change'` |Triggered when mirror mode is enabled. |
   |TIME_SCALE_CHANGE |`'time_scale_change'` |Triggered when music playback seeks forward or backward. |
   |MUSIC_MODE_CHANGE |`'music_mode_change'` |Triggered when music play mode changes. |
   |MUSIC_CHANGE |`'music_change'` |Triggered when switching tracks in music mode. |
   |MUSIC_LIST_CHANGE |`'music_list_change'` |Triggered when the music playlist changes. |
   |AUTOPLAY_SUCCESS |`'autoplay_success'` |Triggered when autoplay succeeds. |
   |AUTOPLAY_FAILED |`'autoplay_failed'` |Triggered when autoplay fails. |
   |MENU_LOG |`'MENU_LOG'` |Triggered for context menu actions. Event `data` contains details. |
   |MENU_REPORT |`'MENU_REPORT'` |Triggered when the context menu feedback button is clicked. |
   |PLAY_LIST_CHANGE |`'play_list_change'` |Triggered when the playlist is updated. |
   |PLAY_LIST_ITEM_CHANGE |`'play_list_item_change'` |Triggered when the current playlist item changes. |
   |PLAY_NEXT_START |`'play_next_start'` |Triggered when `playNext` starts. |
   |PLAY_NEXT_END |`'play_next_end'` |Triggered when `playNext` ends. |
   |ABR_AUTO_DESC_CHANGE |`'ABR_AUTO_DESC_CHANGE'` |Triggered when the actual definition behind the auto ABR level changes. |
   |CORE_EVENT |`'core_event'` |Extension events from the playback plugin core. |
   


**Example**

Listen to autoplay success

```typescript
playerSdkIns.on(VePlayer.Events.AUTOPLAY_SUCCESS, () => {
  // TODO something
})
```
