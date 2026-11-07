---
title: "Web Player SDK: Compatibility"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-player-sdk-compatibility"
---

The Player SDK for Web is compatible with major browsers and smartly chooses the best playback solution based on the user's operating system and browser. This ensures an optimized viewing experience for all users.

<span id="49c5122a"></span>
## Browser compatibility

Below is a list of browser compatibility supported by the Player SDK for Web.


|**Feature** |**Chrome** |**Edge** |**Mac Safari** |**iOS Safari** |**Android Chrome** |**FireFox** |
|---|---|---|---|---|---|---|
|Setting player size |√ |√ |√ |√ |√ |√ |
|Setting video covers |√ |√ |√ |√ |√ |√ |
|Toggling between different resolutions |√ |√ |√ |√ |√ |√ |
|Auto\-downgrading to lower resolutions |√ |√ |√ |√ |√ |√ |
|Setting playback rate |√ |√ |√ |√ |√ |√ |
|Autoplay |√ |√ |√ |√ |√ |√ |
|Loop playback |√ |√ |√ |√ |√ |√ |
|Creating multiple player instances |√ |√ |√ |√ |√ |√ |
|Screenshot |√ |√ |√ |√ |√ |√ |
|Full screen |√ |√ |√ |√ |√ |√ |
|Video rotation |√ |√ |√ |√ |√ |√ |
|Video downloading |Partly supported |Partly supported |Partly supported |Partly supported |Partly supported |Partly supported |
|Volume control |√ |√ |√ |√ |√ |√ |
|Thumbnail |√ |√ |√ |√ |√ |√ |
|Adding marks to progress bar |√ |√ |√ |√ |√ |√ |
|Picture\-in\-Picture (PiP) |√ |√ |√ |√ |X |√ |
|Seeking to a position |√ |√ |√ |√ |√ |√ |
|Playing video by VID |√ |√ |√ |√ |√ |√ |
|Timestamp anti\-hotlinking |√ |√ |√ |√ |√ |√ |
|Referer blocklist and allowlist |√ |√ |√ |√ |√ |√ |
|IP blocklist and allowlist |√ |√ |√ |√ |√ |√ |
|Customizing the UI |√ |√ |√ |√ |√ |√ |
|Bullet comments |√ |√ |√ |√ |√ |√ |
|Playlist |√ |√ |√ |√ |√ |√ |
|Playing encrypted HLS videos |√ |√ |√ |Partly supported |Partly supported |√ |
|Playing encrypted DASH videos |√ |√ |√ |Partly supported |Partly supported |√ |
|Monitoring playback quality |√ |√ |√ |√ |√ |√ |
|Remembering where the user left off and resuming playback from there |√ |√ |√ |√ |√ |√ |
|Video mirroring |√ |√ |√ |√ |√ |√ |
|Adding subtitles |√ |√ |√ |√ |√ |√ |
|Playing encrypted MP4 videos |√ |√ |√ |X |Partly supported |√ |
|H.265 |√ |√ |√ |Partly supported |Partly supported |Need to enable compatibility mode |


<span id="08d7d31c"></span>
## Protocol support

The following table lists the streaming protocols supported by the Player SDK for Web:


|**Protocol** |**PC Browser** |**Mobile Browser** |
|---|---|---|
|MP4 |√ |√ |
|HLS |√ |√ |
|DASH |√ |Supported on some Android browsers |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When creating a player instance, if you set <code>useSoftDecoding</code> as <code>true</code> to enable software decoding on mobile browsers, the Web Player SDK will automatically enable anti\-hijacking for devices that support software decoding. Note that software decoding requires <a href="https://caniuse.com/?search=webassembly">WebAssembly</a> support in the browser.</div>


* <div data-tips="true" data-tips-type="tip">Playing HLS and DASH streaming requires <a href="https://caniuse.com/?search=Media%20Source%20Extensions">Media Source Extensions</a> (MSE) support in the browser.</div>
