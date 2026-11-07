---
title: "How to Deal with Auto-play Restrictions of Browsers"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-130302"
---

The Autoplay Policy of most browsers requires that users have interacted with the domain before a video with sound can be auto\-played. The rationale behind this is that sudden sounds without any warning are typically unwanted when a user opens a web page.

Additionally, some browsers do not permit auto playback of pure videos. For instance, Safari on iOS devices in low power mode as well as the embedded browser within WeChat on iOS. For more on this, see the [Autoplay policies in various browsers](https://docs.byteplus.com/docs/byteplus-rtc/docs-130302#reference).

This means that, prior to user interaction, both automatic playback or manually calling the `play` method to play audio and video could potentially fail, leading to reporting silent issues or inability to see the video. Hence, when developing Web RTC apps, it is necessary to guide user interaction before playing any videos. You can consider the following Best practices to achieve this.

<span id="solution-one-guide-user-to-interact-once-you-receive-onautoplayfailed"></span>
## Solution One: Guide user to interact once you receive `onAutoPlayFailed`

After creating the RTC engine, audio and video play automatically by default, meaning that the audio and video will automatically play once decoding is successful. When the `onAutoPlayFailed` callback is triggered, it signifies that there is a stream that has failed to auto\-play. At this point, create a button prompt to guide the user to interact with the page to resume playback.

```javascript
import BytePlusRTC from '@byteplus/rtc';
const engine = BytePlusRTC.createEngine('appId')
// ...
engine.on(BytePlusRTC.events.onAutoplayFailed, e => {
  const button = document.createElement("button");
  button.innerText = "Click to play";
  button.onclick = () => {
    button.remove();
    engine.play(e.userId); // for local media stream, use None for the user ID.
  };
  document.body.append(button);
});
```


<span id="solution-two-guide-users-to-interact-before-playback"></span>
## Solution Two: Guide users to interact before playback

For most browsers, autoplay with sound is allowed if a user has interacted with the domain. However, since it's not possible to perceive through JavaScript whether a browser has lifted the auto\-play restriction, in this solution, you need to guide the user to interact before starting to play, to ensure successful auto\-play of the media stream.


1. The UI design varies from the selected RTC auto\-play policy when calling the [createEngine](https://docs.byteplus.com/en/docs/12/docs-104478#createengine) method.

* `VIDEO_ONLY`: Muted autoplay is always allowed in Chrome. You can guide the user to click on the button named "Unmute" to play audio.

* `PLAY_MANUALLY`: Disable auto\-play. For browsers with strict auto\-play restrictions, like Safari on iOS, WeChat browser, and WeChat Mini Program's Webview, user interaction is required before audio and video can play. You can guide the user to click on the button named "Play" to play audio.

2. It’s important to detect if auto\-play was denied. Even if you guide users to interact with the page in advance, it doesn't guarantee that auto\-play failure errors won't occur. See [Guide user to interact once you receive ](https://docs.byteplus.com/docs/byteplus-rtc/docs-130302#failure)[onAutoPlayFailed](https://docs.byteplus.com/docs/byteplus-rtc/docs-130302#failure).

3. Display Mute status on remote users‘ avatars from the start.


```html
<div id="user1" data-user-id="{userId}">Muted</div>
```



4. Play the media stream of a remote user when the local user clicks on this user's avatar, in the callback of the button click/tap event.


```javascript
import BytePlusRTC, { RTCAutoPlayPolicy } from '@byteplus/rtc';
const engine = BytePlusRTC.createEngine('appId', { 
  autoPlayPolicy: RTCAutoPlayPolicy.PLAY_MANUALLY 
});
let playing = false;
// play the audio stream
document.getElementById("user1").onclick = (e) => {
  if (playing) {
      return;
  }
  const userId = e.target.getAttribute('data-user-id')
  engine.play(userId);
  playing = true;
  e.target.innerHTML = "playing";
}
```


<span id="reference"></span>
## Reference

Read through the auto\-play policies of the browsers:


* [Chrome](https://developers.google.com/web/updates/2017/09/autoplay-policy-changes)

* [Safari](https://docs.byteplus.com/docs/byteplus-rtc/docs-130302)

* [Firefox](https://support.mozilla.org/en-US/kb/block-autoplay)
