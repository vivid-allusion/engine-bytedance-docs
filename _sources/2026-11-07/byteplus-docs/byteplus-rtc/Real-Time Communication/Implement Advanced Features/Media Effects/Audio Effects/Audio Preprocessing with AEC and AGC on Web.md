---
title: "Audio Preprocessing with AEC and AGC on Web"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/web-client-audio-preprocessing-aec-agc"
---

Use audio preprocessing extensions in the Web audio capture pipeline to apply acoustic echo cancellation and automatic gain control to locally captured audio. Acoustic echo cancellation (AEC) reduces the echo caused when audio played through a speaker is captured again by the local microphone. Automatic gain control (AGC) automatically adjusts the capture gain to keep the volume stable across different devices and microphone distances. This guide explains how to integrate the AEC and AGC extensions for Web.

<span id="prerequisites"></span>
## Prerequisites


1. Integrate Web SDK 4.69.1 or later.

2. Implement audio and video calls on Web. For details, see [Build a Video Application for Web](https://docs.byteplus.com/docs/byteplus-rtc/docs-106914).

3. Complete the basic audio capture integration.


<span id="notes"></span>
## Notes


* Register the extensions before starting audio capture, and then call `startAudioCapture()`.

* If you use the AEC, AINR, and AGC extensions together, use the processing order `AEC -> AINR -> AGC`. Web SDK 4.69.1 or later guarantees this order. Earlier versions do not.

* AEC and AGC both preprocess captured audio. Specify the target audio stream carefully to avoid conflicts with existing custom audio processing logic.

* AEC usually provides no noticeable benefit when the user wears headphones. It is intended primarily for speaker playback scenarios.

* If an extension triggers `onOverload`, disable unnecessary audio preprocessing features or advise the user to switch to a more capable device.


<span id="acoustic-echo-cancellation"></span>
## Acoustic echo cancellation

AEC is intended for speaker playback scenarios. It reduces the echo that occurs when remote audio played through a speaker is captured again by the local microphone.

<span id="aec-example"></span>
### Example

```typescript
import RTCAECExtension, { AECProfile } from '@byteplus/rtc/extension-aec';
import BytePlusRTC from '@byteplus/rtc';

// Create an AEC extension instance.
const aecExtension = new RTCAECExtension();
// Check whether the current browser supports the AEC extension.
const isSupported = await aecExtension.isSupported();

const engine = BytePlusRTC.createEngine('<YOUR_APP_ID>');

if (isSupported) {
  try {
    await engine.registerExtension(aecExtension);
  } catch (error) {
    // Registration failed. See error.message for details.
  }
}

// Set the AEC profile.
// AI: AI scenarios
// BROADCASTER: interactive live streaming scenarios
// AUTO: automatic profile
await aecExtension.setProfile(AECProfile.AI);

// Start capture after registering the extension.
await engine.startAudioCapture();
```


<span id="aec-key-considerations"></span>
### Key considerations


* When `enable()` or `disable()` is called without an argument, the extension applies to internally captured audio in the main stream by default.

* AEC takes effect only when a remote reference audio stream is available.

* The extension automatically maintains remote reference streams. You usually do not need to call `addReferenceTrack()` manually.

* Register the AEC extension before starting audio capture. If you register it before capture starts, the SDK sets `echoCancellation` to `false` in the browser capture constraints used for subsequent capture. If you register it after capture starts, the SDK cannot change this constraint for the active capture pipeline and reports a console warning and telemetry event.

* This behavior is not guaranteed if the extension is used with an earlier SDK version.

* To support an earlier SDK version, wait until a remote audio stream has been subscribed to, obtain its `MediaStreamTrack` by calling [getRemoteStreamTrack](https://docs.byteplus.com/docs/byteplus-rtc/docs-104478#rtcengine-getremotestreamtrack), and pass the track to the extension manually.


```typescript
import BytePlusRTC, { StreamIndex } from '@byteplus/rtc';

engine.on(BytePlusRTC.events.onRemoteAudioFirstFrame, ({ userId, isScreen }) => {
  if (isScreen) {
    return;
  }

  const track = engine.getRemoteStreamTrack(userId, StreamIndex.STREAM_INDEX_MAIN, 'audio');
  if (track) {
    aecExtension.addReferenceTrack(track);
  }
});
```


<span id="aecprofile"></span>
### AECProfile


|Profile |Value |Description |
|---|---|---|
|AUTO |`'auto'` |Automatic profile. The detailed configuration is controlled by the SDK parameter `AEC_AUTO_CONFIG`. |
|AI |`'AI'` |AI scenario. |
|BROADCASTER |`'broadcaster'` |Broadcaster scenario. |


<span id="aec-common-methods"></span>
### Common methods


* `enable(constraint?)`: Enables acoustic echo cancellation.

* `disable(constraint?)`: Disables acoustic echo cancellation.

* `isSupported()`: Checks whether the current browser supports the extension.

* `setProfile(profile)`: Sets the AEC profile.

* `resume()`: Attempts to recover the extension after a recoverable error.

* `addReferenceTrack(track)`: Adds a remote reference audio stream manually.

* `removeReferenceTrack(track)`: Removes a remote reference audio stream.

* `clearReferenceTracks()`: Removes all remote reference audio streams.


<span id="automatic-gain-control"></span>
## Automatic gain control

AGC is useful when microphone input levels vary significantly between users or when the distance between a user and the microphone changes. It automatically adjusts the capture gain to keep the volume more stable.

<span id="agc-example"></span>
### Example

```typescript
import RTCAGCExtension from '@byteplus/rtc/extension-agc';
import BytePlusRTC from '@byteplus/rtc';

// Create an AGC extension instance.
const agcExtension = new RTCAGCExtension();
// Check whether the current browser supports the AGC extension.
const isSupported = await agcExtension.isSupported();

const engine = BytePlusRTC.createEngine('<YOUR_APP_ID>');

if (isSupported) {
  try {
    await engine.registerExtension(agcExtension);
  } catch (error) {
    // Registration failed. See error.message for details.
  }
}

// Start capture after registering the extension.
await engine.startAudioCapture();
```


<span id="agc-key-considerations"></span>
### Key considerations


* When `enable()` or `disable()` is called without an argument, the extension applies to internally captured audio in the main stream by default.

* The AGC extension currently exposes only the `AUTO` profile.

* Register the AGC extension before starting audio capture. If you register it before capture starts, the SDK sets `autoGainControl` to `false` in the browser capture constraints used for subsequent capture. If you register it after capture starts, the SDK cannot change this constraint for the active capture pipeline and reports a console warning and telemetry event.

* This behavior is not guaranteed if the extension is used with an earlier SDK version.


<span id="agcprofile"></span>
### AGCProfile


|Profile |Value |Description |
|---|---|---|
|AUTO |`'auto'` |Automatic profile. The detailed configuration is controlled by the SDK parameter `AGC_AUTO_CONFIG`. |


<span id="agc-common-methods"></span>
### Common methods


* `enable(constraint?)`: Enables automatic gain control.

* `disable(constraint?)`: Disables automatic gain control.

* `isSupported()`: Checks whether the current browser supports the extension.

* `setProfile(profile)`: Sets the AGC profile.

* `resume()`: Attempts to recover the extension after a recoverable error.


<span id="listen-for-events"></span>
## Listen for events

The AEC and AGC extensions support the following events:


* `onUnsupported`: The current browser environment or audio processing pipeline does not support the extension.

* `onOverload`: Processing takes too long, usually because the device is under heavy load.

* `onError`: An error occurs while the extension is running. Depending on the error, call `resume()` to attempt recovery.


```typescript
import { EventTypes as AECEventTypes } from '@byteplus/rtc/extension-aec';
import { EventTypes as AGCEventTypes } from '@byteplus/rtc/extension-agc';

aecExtension.on(AECEventTypes.onUnsupported, ({ message }) => {});
aecExtension.on(AECEventTypes.onOverload, ({ elapsedTime }) => {});
aecExtension.on(AECEventTypes.onError, async ({ message }) => {
  await aecExtension.resume();
});

agcExtension.on(AGCEventTypes.onUnsupported, ({ message }) => {});
agcExtension.on(AGCEventTypes.onOverload, ({ elapsedTime }) => {});
agcExtension.on(AGCEventTypes.onError, async ({ message }) => {
  await agcExtension.resume();
});
```
