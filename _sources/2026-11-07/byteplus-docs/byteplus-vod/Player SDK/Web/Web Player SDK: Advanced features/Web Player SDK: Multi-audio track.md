---
title: "Web Player SDK: Multi-audio track"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-multi-audio-track-web"
---

VePlayer supports playback and switching of multi\-audio track videos. Depending on the runtime environment, two underlying implementations are used:


|Scenario |Implementation |Typical Platforms |
|---|---|---|
|MSE / MMS playback |hls.js `audioTracks` API |PC (all browsers), Android H5 (requires configuration), iOS 17.1+ (requires configuration) |
|Native HLS playback |`HTMLMediaElement.audioTracks` API |iOS Safari (default), iOS below 17.1 |


Both implementations expose the same SDK APIs and events, so developers do not need to handle the underlying differences.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="default">Multi\-audio tracks are only available for HLS\-format videos, and the video source must declare multiple audio tracks via <code>#EXT-X-MEDIA</code> tags.</div>


<span id="968c4357"></span>
## Platform support


|Platform |Multi\-audio track supported by default |Notes |
|---|---|---|
|PC (Chrome / Edge / Firefox) |✅ Yes |Uses hls.js (MSE) playback by default |
|PC Safari |✅ Yes |Uses hls.js (MSE) by default (`useHlsPluginForSafari` defaults to `true`); if explicitly set to `false`, falls back to native playback, but multi\-audio track remains functional |
|iOS Safari |✅ Yes |Uses native playback by default; multi\-audio track is supported via `HTMLMediaElement.audioTracks`. When `enableMobileHlsPlugin: true` is configured, devices running iOS 17.1+ (with `ManagedMediaSource` support) can switch to hls.js playback |
|Android H5 |❌ No |Uses native playback by default; Android does not support `HTMLMediaElement.audioTracks`. Configure `enableMobileHlsPlugin: true` (browser must support MSE) to enable hls.js playback and unlock multi\-audio track support |


<span id="63110fa1"></span>
## Enabling multi\-audio track on mobile (enableMobileHlsPlugin)

Use `enableMobileHlsPlugin` to enable multi\-audio track support on mobile with a single configuration. The player automatically determines the behavior based on the runtime platform:


|Platform |Condition |Behavior |
|---|---|---|
|Android |Browser supports MSE (`MediaSource`) |Enables hls.js playback |
|iOS 17.1+ |Device supports `ManagedMediaSource` (`VePlayer.isMMSSupported()` returns `true`) |Enables hls.js playback |
|iOS below 17.1 |— |Falls back to native HLS; multi\-audio track is supported via `HTMLMediaElement.audioTracks` |


```JavaScript
const player = new VePlayer({
  id: 'video',
  url: 'https://example.com/multi-audio.m3u8',
  enableMobileHlsPlugin: true,
});
```


When enabled, eligible Android and iOS 17.1+ devices use hls.js for playback, unlocking features such as `setAudioOption` preference persistence and audio track memory across quality switches. Devices that do not meet the conditions fall back gracefully without affecting basic playback.

<span id="f84a4d60"></span>
## Initialization configuration

<span id="a936a097"></span>
### Specifying the initial audio track

Use `audioPreference` to specify the audio track to activate on playback start. The type is `AudioTrackOption` — pass any matching fields that are sufficient to identify the target track (commonly `lang`).

```JavaScript
const player = new VePlayer({
  id: 'video',
  url: 'https://example.com/multi-audio.m3u8',
  audioPreference: { lang: 'en' },  // Automatically switch to the English track on start
});
```


For more precise matching (when multiple tracks share the same language):

```JavaScript
audioPreference: { lang: 'en', name: 'Stereo' }
```



* `lang` is case\-insensitive: `"zh"` and `"ZH"` are equivalent.

* All provided fields must match (AND logic); fields not provided are not evaluated.

* **hls.js path:**  Preference is applied via `hls.setAudioOption()`; the selected track is automatically restored after quality switches.

* **Native path** (iOS Safari native HLS): Matches using `id`, `lang`, and `name` with AND logic; `name` corresponds to the native `AudioTrack.label`.

* If no match is found, the default track declared in the manifest is used; no error is thrown.

* On quality switch, the player first attempts to restore the last manually selected track. If that track does not exist in the new quality level, it falls back to `audioPreference`. If neither is available, the player's default behavior applies.

* When `playNext()` is called to play a new video, the previous track memory is reset and `audioPreference` takes effect again.


<span id="be0af9f5"></span>
### Configuring the audio track plugin (PC)

```JavaScript
const player = new VePlayer({
  id: 'video',
  url: 'https://example.com/multi-audio.m3u8',
  AudioTrack: {
    index: 70,             // Position in the control bar; lower values appear further left. Default: 70
    isShowIcon: true,      // Whether to show the switch button. Default: true
    showNameSuffix: true,  // Whether to append the original track name in parentheses after the
                           // language name, e.g. "Japanese (Stereo AudioTrack1)". Default: true
  },
});
```


Pass `false` to disable the plugin:

```JavaScript
AudioTrack: false,
```


<span id="00dadf18"></span>
### Configuring the audio track plugin (Mobile)

```JavaScript
const player = new VePlayer({
  id: 'video',
  url: 'https://example.com/multi-audio.m3u8',
  AudioTrackMobile: {
    index: 2.6,            // Position in the control bar; lower values appear further left. Default: 2.6
    isShowIcon: true,      // Whether to show the switch button. Default: true
    showNameSuffix: true,  // Whether to append the original track name in parentheses after the
                           // language name, e.g. "Japanese (Stereo AudioTrack1)". Default: true
  },
});
```


Pass `false` to disable the plugin:

```JavaScript
AudioTrackMobile: false,
```


<span id="e203fccc"></span>
## Type definitions

<span id="13464cd8"></span>
### `AudioTrackInfo`

The item type returned by `getAudioTracks()` and `getCurrentAudioTrack()`, and also the parameter type for `switchAudioTrack()`. All three APIs share this type.

```TypeScript
interface AudioTrackInfo {
  id: number;           // Track index in the list (number for both hls.js and native paths)
  name: string;         // Display name
  default: boolean;     // Whether this is the default track in the manifest
  selected: boolean;    // Whether this is the currently active track
  lang?: string;        // Language code (BCP-47)
  assocLang?: string;   // Associated language code, corresponding to #EXT-X-MEDIA ASSOC-LANGUAGE=
  characteristics?: string; // Track characteristics string, corresponding to #EXT-X-MEDIA CHARACTERISTICS=
  channels?: string;    // Channel count, corresponding to #EXT-X-MEDIA CHANNELS=
  audioCodec?: string;  // Audio codec
  groupId?: string;     // Audio group ID, corresponding to #EXT-X-MEDIA GROUP-ID=
  [key: string]: unknown;
}
```


<span id="2255a303"></span>
## API

<span id="7dced795"></span>
### `getAudioTracks()`

Returns the full list of audio tracks for the current video.

```TypeScript
player.getAudioTracks(): AudioTrackInfo[]
```



* Returns an empty array `[]` if the video has a single audio track or no audio tracks.


**Example**

```JavaScript
const tracks = player.getAudioTracks();
console.log(tracks);
// [
//   { id: 0, name: 'Mandarin', lang: 'zh-cn', default: true,  selected: true  },
//   { id: 1, name: 'English',  lang: 'en',    default: false, selected: false },
// ]
```


<span id="f4125568"></span>
### `getCurrentAudioTrack()`

Return the currently active audio track.

Returns `null` if no track is active; the `selected` field of the return value is always `true`.

```TypeScript
player.getCurrentAudioTrack(): AudioTrackInfo | null
```


**Example**

```JavaScript
const current = player.getCurrentAudioTrack();
console.log(current);
// { id: 0, name: 'Mandarin', lang: 'zh-cn', default: true, selected: true }
```


<span id="12d1e858"></span>
### `switchAudioTrack(track)`

Switches to the specified audio track. Items returned by `getAudioTracks()` are of type `AudioTrackInfo` and can be passed directly.

```TypeScript
player.switchAudioTrack(track: AudioTrackInfo): void
```



|Parameter |Type |Description |
|---|---|---|
|`track` |`AudioTrackInfo` |The target track object. Pass an item directly from the array returned by `getAudioTracks()`. |
|`track.id` |`number` |Index of the target track |
|`track.name` |`string` |Track name. On the hls.js path, corresponds to `#EXT-X-MEDIA NAME=`; on the native path, corresponds to `HTMLMediaElement AudioTrack.label`. |
|`track.default` |`boolean` |Whether this is the default track in the manifest |
|`track.selected` |`boolean` |Whether this is the currently active track |
|`track.lang` |`string` (optional) |Language code (BCP\-47) |
|`track.assocLang` |`string` (optional) |Associated language code, corresponding to `#EXT-X-MEDIA ASSOC-LANGUAGE=` |
|`track.characteristics` |`string` (optional) |Track characteristics string, corresponding to `#EXT-X-MEDIA CHARACTERISTICS=` |
|`track.channels` |`string` (optional) |Channel count, corresponding to `#EXT-X-MEDIA CHANNELS=` |
|`track.audioCodec` |`string` (optional) |Audio codec |
|`track.groupId` |`string` (optional) |Audio group ID, corresponding to `#EXT-X-MEDIA GROUP-ID=` |



* All provided fields must match (AND logic); if any field does not match, the call is silently ignored.

* No operation is performed if the target track is already the active track.

* The `Events.AUDIO_TRACK_CHANGE` event is triggered after the switch completes.

* **hls.js path** (MSE playback): Switches via `hls.setAudioOption({ lang, name })`; the selection is persisted as a preference and automatically restored after quality switches. Falls back to `hls.audioTrack = id` direct assignment for older versions of hls.js that do not support this method.

* **Native path** (iOS Safari): Matches by `id`, `lang` (corresponding to `AudioTrack.language`), and `name` (corresponding to `AudioTrack.label`) using AND logic, then switches the `enabled` property.


**Example**

```JavaScript
// Switch to the first English audio track
const tracks = player.getAudioTracks();
const enTrack = tracks.find(t => t.lang === 'en');
if (enTrack) {
  player.switchAudioTrack(enTrack);
}
```


<span id="1e72abb8"></span>
## Events

<span id="e6d7a176"></span>
### `Events.AUDIO_TRACKS_UPDATED`

Fired when the audio track list is ready or updated (triggered after video load and source changes).

```TypeScript
player.on(VePlayer.Events.AUDIO_TRACKS_UPDATED, (data) => {
  // data.audioTracks: full track array, same structure as the return value of getAudioTracks()
});
```


**Example**

```JavaScript
player.on(VePlayer.Events.AUDIO_TRACKS_UPDATED, ({ audioTracks }) => {
  console.log('Audio track list updated:', audioTracks);
});
```


<span id="47ece50f"></span>
### `Events.AUDIO_TRACK_CHANGE`

Fired when an audio track switch completes.

```TypeScript
player.on(VePlayer.Events.AUDIO_TRACK_CHANGE, (data) => {
  // data.id:         id of the new track
  // data.audioTrack: full object of the new track
});
```


**Example**

```JavaScript
player.on(VePlayer.Events.AUDIO_TRACK_CHANGE, ({ id, audioTrack }) => {
  console.log('Switched to track:', audioTrack.name, '(id:', id, ')');
});
```


<span id="4abbcea7"></span>
## Full example

```JavaScript
import VePlayer from '@volcengine/veplayer';
import '@volcengine/veplayer/index.min.css';

const player = new VePlayer({
  id: 'video',
  url: 'https://example.com/multi-audio.m3u8',
  audioPreference: { lang: 'en' },      // Default to English track on start
  enableMobileHlsPlugin: true,          // Required for multi-audio track on Android H5 and iOS 17.1+
  AudioTrack: { index: 70 },            // Place the switch button toward the right of the PC control bar
});

// Listen for audio track list ready
player.on(VePlayer.Events.AUDIO_TRACKS_UPDATED, ({ audioTracks }) => {
  console.log('Available tracks:', audioTracks.map(t => t.name));
});

// Listen for audio track switch
player.on(VePlayer.Events.AUDIO_TRACK_CHANGE, ({ audioTrack }) => {
  console.log('Current track:', audioTrack.name);
});

// Manually switch to the English track
function switchToEnglish() {
  const tracks = player.getAudioTracks();
  const en = tracks.find(t => t.lang === 'en');
  if (en) player.switchAudioTrack(en);
}

// Log the currently active track
function logCurrentTrack() {
  const track = player.getCurrentAudioTrack();
  console.log(track ? `Current: ${track.name}` : 'No active track');
}
```


<span id="3cd59800"></span>
## Common language code reference


|Language Code |Language |
|---|---|
|`zh-cn` |Mandarin Chinese |
|`zh-hk` |Cantonese |
|`zh-tw` |Traditional Chinese |
|`en` |English |
|`ja` |Japanese |
|`ko` |Korean |
|`fr` |French |
|`de` |German |
|`es` |Spanish |
|`ar` |Arabic |
|`hi` |Hindi |
|`th` |Thai |
|`vi` |Vietnamese |
|`id` |Indonesian |


For the full list of language codes, refer to the [BCP-47 specification](https://www.rfc-editor.org/rfc/rfc5646).
