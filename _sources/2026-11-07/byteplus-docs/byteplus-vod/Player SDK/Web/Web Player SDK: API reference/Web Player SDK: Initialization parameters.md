---
title: "Web Player SDK: Initialization parameters"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-web-api-reference"
---

<span id="iplayerconfig"></span>
## IPlayerConfig

Player instantiation configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|id |string |No |\- |Player container ID. The player will be inserted into this container. At least one of `id` or `root` must be provided. |
|root |HTMLElement |No |\- |Player container DOM element. VePlayer will be inserted into this container. At least one of `id` or `root` must be provided; `root` takes precedence when both are provided. |
|url |[Url](https://docs.byteplus.com/en/docs/25/7976#url) |No |\- |Video playback URL. |
|vid |string |No |\- |Video ID in the VOD service. Recommended for tracking playback quality. |
|getVideoByToken |[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/7976#iplayauthtokenconfig) |No |\- |Vid playback configuration. The app server generates a temporary play token from `vid` and passes it to the client. |
|drmType |[EDRMTYPE](https://docs.byteplus.com/en/docs/25/ref#edrmtype) |No |\- |Video encryption type. |
|encryptSessionId |string |No |\- |Private encryption session ID. |
|playAuthId |string |No |\- |Key ID for encrypted video, corresponding to `PlayAuthId` in the [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) response. |
|playAuth |string |No |\- |Encryption key for private\-encrypted playback, corresponding to `PlayAuth` in the [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) response. |
|streamType |"mp4" \| "hls" \| "dash" \| "rtm" \| "flv" |No |\- |Video format. Required when the `url` does not include a file extension. |
|width |string \| number |No |`100%` |Player width. Accepts a number (px) or a CSS `width` value. |
|height |string \| number |No |`100%` |Player height. Accepts a number (px) or a CSS `height` value. |
|volume |number |No |`0.6` |Initial playback volume. Range: [0, 1]. |
|autoplay |boolean |No |`false` |Whether to enable autoplay. Subject to browser autoplay policies. |
|poster |string \| [IPoster](https://docs.byteplus.com/en/docs/25/7976#iposter) |No |\- |Video poster image configuration. |
|autoplayMuted |boolean |No |`false` |Whether to enable muted autoplay.<br><br><br>* `true`：enable muted autoplay<br><br>* `false`：disable muted autoplay |
|enableDegradeMuteAutoplay |boolean |No |`false` |Whether to fall back to muted autoplay when autoplay with sound fails.<br><br><br>* `true`：enable degrade muted autoplay<br><br>* `false`：disable degrade muted autoplay |
|enableUserActionAutoplay |boolean |No |`false` |Whether to allow the first user interaction (any click) to trigger autoplay.<br><br><br>* `true`：enable user action autoplay<br><br>* `false`：disable user action autoplay |
|loop |boolean |No |`false` |Whether to enable loop playback.<br><br><br>* `true`：enable loop playback<br><br>* `false`：disable loop playback |
|defaultPlaybackRate |number |No |`1` |Default playback rate. Supported values: `0.5`, `0.75`, `1`, `1.5`, `2`. |
|lang |"zh" \| "zh\-cn" \| "en" \| "jp" \| "zh\-hk" |No |`zh` |UI language. Supported values:<br><br><br>* `zh`: Chinese (Simplified)<br><br>* `zh-cn`: Chinese (Simplified)<br><br>* `en`: English<br><br>* `jp`: Japanese<br><br>* `zh-hk`: Chinese (Traditional) |
|languages | |No |\- |i18n dictionary. Per\-language key\-value maps, e.g. `{ zh: { PIP: 'Picture in Picture' }, en: { PIP: 'pip' } }`. |
|pip |boolean \| [IPIPConfig](https://docs.byteplus.com/en/docs/25/7976#ipipconfig) |No |`PC: {position: 'controlsRight', index: 2.5, showIcon: true}; mobile: false` |Picture\-in\-picture configuration. Requires browser\-level PiP support. |
|fullscreen |[IFullscreenConfig](https://docs.byteplus.com/en/docs/25/7976#ifullscreenconfig) |No |\- |Fullscreen configuration. |
|alwaysShowDefinition |boolean |No |`false` |Whether to always show the definition selector, even when only one definition is available. |
|definitionText |string |No |`HD` |Display label for the definition corresponding to `url`. Only effective when `alwaysShowDefinition` is `true`. |
|definitionTextKey |string |No |\- |i18n key for the definition label of `url`, mapping to `languages`. Takes priority over `definitionText`. |
|codec |[ICodecType](https://docs.byteplus.com/en/docs/25/7976#icodectype) |No |\- |Video codec type. Recommended when the codec is known, to improve log analysis and soft\-decode initialization. |
|region |TRegionType |No |`sg` |The area where the on\-demand service is located affects the service interface and log reporting. |
|userRegion |TRegionType |No |`sg` |The region where the user is located, the domain name that affects the reporting service of the log request and the dynamic dependency pull |
|pluginPublicPath |string |No |`https://sf-unpkg.bytepluscdn.com/obj/byteplusfe-sg/sdk/@byteplus/veplayer/${version}/plugin` |plug loading public path, used to specify the loading path of the plug\-in, or the local file service to load the plug\-in |
|startTime |number |No |`0` |Start playback time in seconds. |
|playsinline |boolean |No |`true` |Whether to enable inline playback. The HTML5 `playsinline` attribute controls whether video plays inside the page document.<br><br><br>* `true`: Inline playback inside the page.<br><br>* `false`: Disable inline playback.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Effective on mobile only. When <code>true</code>, sets <code>playsinline</code>, <code>webkit-playsinline</code>, and <code>x5-playsinline</code> on the media element. See <a href="https://webkit.org/blog/6784/new-video-policies-for-ios/">New Policies for iOS</a>. On iOS Safari: supported on iOS 10+; on iOS 9 and below playback enters system fullscreen by default.</div><br> |
|videoAttributes |Partial<HTMLVideoElement\> |No |\- |Extra attributes applied to the `videoElement` / `audioElement` on initialization. See [HTMLMediaElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLMediaElement#properties). |
|fluid |boolean |No |`false` |Whether to enable fluid layout. When enabled, the player adapts its aspect ratio based on `width` / `height` (defaults to 16:9 when they are non\-numeric). |
|fitVideoSize |"fixWidth" \| "fixHeight" \| "fixed" |No |`fixed` |Container size adaptation mode after video metadata is loaded. `fixed`: keep container ratio; `fixWidth`: adapt height; `fixHeight`: adapt width. |
|videoFillMode |"cover" \| "auto" \| "fillHeight" \| "fillWidth" \| "fill" |No |`auto` |Video fill mode, equivalent to CSS `object-fit`. `auto`: browser default (may produce letterboxing); `fill`: stretch; `cover`: crop to fill; `fillWidth` / `fillHeight`: fill one axis and crop the other. |
|marginControls |boolean |No |`false` |Whether to separate the video canvas from the controls bar. When enabled, the controls bar is always visible and does not overlap the video. |
|'x5\-video\-player\-type' |string |No |\- |Enable same\-layer playback for X5 kernel browsers. |
|'x5\-video\-player\-fullscreen' |boolean |No |\- |Whether to enable fullscreen playback mode for X5 kernel browsers. |
|'x5\-video\-orientation' |"landscape" \| "portrait" \| "landscape\|portrait" |No |`landscape\\|portrait (mobile)` |Screen orientation for X5 kernel browsers. `landscape`, `portrait`, or `landscape\|portrait` (auto\-rotate). |
|commonStyle |[ICommonStyle](https://docs.byteplus.com/en/docs/25/7976#icommonstyle) |No |\- |Key point style configuration for the player. |
|isMusic |boolean |No |`false` |Whether to enable music playback mode. Use `music` for further music player configuration. |
|closeVideoStopPropagation |boolean |No |`false` |Whether to stop event propagation on the `video` element. |
|enableMenu |boolean |No |`false` |Whether to enable the right\-click context menu. |
|closeVideoClick |boolean |No |`false` |Whether to disable toggling play/pause by clicking the player area on PC. |
|closeVideoDblclick |boolean |No |`true on PC, false on mobile` |PC: disable double\-click fullscreen. Mobile: disable double\-click play/pause toggle. |
|closeDelayBlur |boolean |No |`false` |Whether to disable auto blur on the player (PC only). |
|inactive |number |No |`PC: 2000, mobile: 3000` |Delay before player focus auto\-clears, in milliseconds. |
|leavePlayerTime |number |No |`0` |Delay before hiding controls after mouse leaves the player (PC only). Set 0 to hide immediately. |
|closePlayVideoFocus |boolean |No |`true on PC, false on mobile` |Whether to disable focus state on play. |
|closePauseVideoFocus |boolean |No |`false` |Whether to disable focus state on pause (forces control bar visible). |
|needFullscreenScroll |boolean |No |`false` |Whether to scroll back to the pre\-fullscreen position after exiting fullscreen (common on Android). |
|mobile |[IMobileConfig](https://docs.byteplus.com/en/docs/25/ref#imobileconfig) |No |\- |Mobile interaction plugin configuration. |
|start |[IStartConfig](https://docs.byteplus.com/en/docs/25/ref#istartconfig) |No |\- |Center play/pause button plugin configuration. |
|enableHlsMSE |boolean |No |`false` |Whether to use MSE for HLS playback on mobile (default is native `video`). Improves compatibility, cache control, and bandwidth usage. |
|enableMobileHlsPlugin |boolean |No |`false` |Prefer hls.js (MSE/MMS) for HLS playback on mobile:<br><br><br>* **Android**: always enables hls.js.<br><br>* **iOS**: enables hls.js only when `ManagedMediaSource` is supported (iOS 17.1+,<br><br>   i.e. `VePlayer.isMMSSupported()` returns `true`); falls back to native HLS otherwise.<br><br>   Unlocks hls.js\-specific features such as multi\-audio\-track switching on mobile. |
|enableHlsJs |boolean |No |`true` |Whether to use the [hls.js](https://hlsjs.video-dev.org/) plugin for HLS playback on PC. When `false`, the built\-in HLS adapter is used instead. |
|useHlsPluginForSafari |boolean |No |`true` |Whether to use the HLS plugin on PC Safari. When `true`, the SDK loads the HLS plugin automatically. |
|enableMp4MSE |boolean |No |`false` |Whether to use MSE for MP4 playback, enabling accurate seek, seamless stream switching, and bandwidth savings. |
|playList |[Stream](https://docs.byteplus.com/en/docs/25/7976#stream)[] |No |\- |Playlist of video streams with multi\-definition and multi\-line support. |
|defaultDefinition |string |No |`First item of playList` |Default definition. Effective only when `playList` is set. |
|audioPreference |[AudioTrackOption](https://docs.byteplus.com/en/docs/25/7976#audiotrackoption) |No |\- |Default audio track preference at playback start. Accepts the same fields as<br><br>`switchAudioTrack()`. Applied via `hls.setAudioOption()` on the hls.js path (persists<br><br>across quality switches); matched by `lang` on the iOS native path.<br><br>Falls back to the manifest default when no match is found. |
|audioTrackSwitchSeekOffset |number |No |`0.1` |Micro\-seek offset in seconds applied when the user switches audio tracks, to fix occasional video\-without\-audio issues. Set to `0` to disable. |
|plugins |any[] |No |\- |Additional plugins to install. Compatible with [XGPlayer plugins](https://h5player.bytedance.com/plugins/) . |
|ignores |string[] |No |`[]` |List of built\-in plugin names to disable (case\-insensitive). |
|umdUrlMap |Record<string, string\> |No |\- |Fallback URL map for UMD plugin dependencies when the default CDN is unreachable. Supported keys: `hls`, `flv`, `XGVideo`, `hlsEncrypt`, `dash`, `mp4Encrypt`, `danmujs`, `danmuMask`, `subtitle`. |
|unionId |string |No |\- |Unique ID for [private encryption scheme](https://docs.byteplus.com/en/docs/byteplus-vod/playing_private_encrypted_videos_web). |
|useSoftDecoding |boolean |No |`false` |Whether to enable software decoding. Required for FLV on mobile. High CPU usage on high\-bitrate / high\-resolution videos. |
|enableH265Degrade |boolean |No |`false` |Whether to enable H.265 auto\-degrade mode. When enabled, VePlayer falls back to a compatible mode in browsers that do not support H.265 hardware decoding. |
|enableUrlExpireCheck |boolean |No |`false` |Whether to enable URL expiry polling. The player periodically compares the client time against `urlExpireTimestamp`. |
|urlExpireTimestamp |number |No |\- |Expiration timestamp (seconds) for the URL. Automatically fetched for VID mode. |
|urlExpireDiff |number |No |`60` |Threshold for URL expiration detection. Unit: seconds. For example, if set to 500, the SDK will trigger the `Events.MEDIA_EXPIRED` event 500 seconds before the URL expires, providing sufficient buffer time for updating the address. |
|urlCheckExpireInterval |number |No |`400` |Interval for URL expiration polling. Unit: milliseconds. The player periodically compares the client time against the expiration timestamp to check if the address has expired. |
|debug |boolean |No |`false` |Whether to enable debug log output. |
|sdkErrorPlugin |[ISdkErrorConfig](https://docs.byteplus.com/en/docs/25/7976#isdkerrorconfig) |No |\- |Error UI configuration. Controls the error message, image, and refresh button displayed on playback failure. |
|oriErrRetryCount |number |No |`3` |Maximum number of retries within the sliding window for media errors in non\-MSE mode (including encrypted HLS). |
|oriErrRetryCycle |number |No |`10000` |Sliding window duration (ms) for retry counting. Retries stop and error analysis begins once `oriErrRetryCount` is reached within the window. |
|oriErrRetryBaseDelay |number |No |`500` |Base delay (ms) for exponential backoff between retries. The delay for the nth retry is `oriErrRetryBaseDelay * 2^(n-1)`. |
|oriErrMaxTotalRetry |number |No |`0` |Maximum total retry count accumulated across all windows. Set to `0` to disable the limit. |
|needSyncAnalyzeError |boolean |No |`true` |Whether to perform error analysis after retries are exhausted, to refine the error code. |
|analyzeTimeout |number |No |`3000` |Timeout (ms) for the network analysis request. |
|ignoreErrorCodes |(string \| number)[] |No |`[]` |List of error codes to suppress and not report. |
|AudioTrack |false \| [IAudioTrackConfig](https://docs.byteplus.com/en/docs/25/7976#iaudiotrackconfig) |No |\- |PC audio track selector plugin configuration. Pass `false` to disable. Only effective for multi\-track videos. |
|AudioTrackMobile |false \| [IAudioTrackMobileConfig](https://docs.byteplus.com/en/docs/25/7976#iaudiotrackmobileconfig) |No |\- |Mobile audio track selector plugin configuration. Pass `false` to disable. Only effective for multi\-track videos. |
|DanmuPlugin |boolean \| [IDanmuConfig](https://docs.byteplus.com/en/docs/25/7976#idanmuconfig) |No |\- |Danmaku (bullet comment) and panel configuration. Supports font size, opacity, display area, etc. |
|DefinitionDemotePlugin |[IDefinitionDemotePlugin](https://docs.byteplus.com/en/docs/25/7976#idefinitiondemoteplugin) |No |\- |Definition auto\-demote configuration. Requires `DefinitionDemotePlugin` in `plugins`. |
|EncryptHlsPlugin |boolean \| Partial<[IEncryptHlsPluginConfig](https://docs.byteplus.com/en/docs/25/7976#iencrypthlspluginconfig)\> |No |\- |Encrypted HLS playback configuration. |
|vodLogOpts |Partial<[IVodLogOptsConfig](https://docs.byteplus.com/en/docs/25/7976#ivodlogoptsconfig)\> |No |\- |Quality metrics log reporting configuration. |
|logTeaAppId |number |No |`323254` |The id of the log tea. Generally, no configuration is required and the player will automatically set it. |
|autoBitrateOpts |[IAutoBitrateOpts](https://docs.byteplus.com/en/docs/25/7976#iautobitrateopts) |No |\- |Adaptive bitrate (ABR) playback configuration. |
|adaptRange |IAdaptRange |No |\- |Dynamic buffer range configuration. |
|Subtitle |[ISubtitleConfig](https://docs.byteplus.com/en/docs/25/7976#isubtitleconfig) |No |\- |External subtitle configuration. |
|MemoryPlay |boolean \| [IMemoryPlayConfig](https://docs.byteplus.com/en/docs/25/7976#imemoryplayconfig) |No |\- |Resume playback (memory play) configuration. |
|music |[IMusicConfig](https://docs.byteplus.com/en/docs/25/7976#imusicconfig) |No |\- |Music player configuration. Effective when `isMusic` is `true`. |
|AutoplayPlugin |[IAutoplayPluginConfig](https://docs.byteplus.com/en/docs/25/7976#iautoplaypluginconfig) |No |\- |Autoplay plugin configuration. |
|playListPlugin |[IPlayListConfig](https://docs.byteplus.com/en/docs/25/7976#iplaylistconfig) |No |\- |Playlist plugin configuration. |
|dynamicwatermark |[IWatermarkConfig](https://docs.byteplus.com/en/docs/25/7976#iwatermarkconfig) |No |\- |Dynamic watermark configuration. |
|thumbnail |[IThumbnailConfig](https://docs.byteplus.com/en/docs/25/7976#ithumbnailconfig) |No |\- |Progress bar thumbnail preview configuration. |
|progressDot |[IDot](https://docs.byteplus.com/en/docs/25/7976#idot)[] |No |\- |Progress bar dot marker configuration. |
|mode |number |No |`0` |The style of the pop\-up window for selecting speed, definition, etc. on the mobile terminal<br><br><br>* `0`: Pops up from the bottom of the page<br><br>* `1`: Pops up from the right side of the player container<br><br>* `2`: Pops up in a way that covers the entire player container |
|seekedStatus |"pause" \| "play" \| "auto" |No |`play` |The state of the player after the seek operation is completed. If the value is auto, the original playback state is maintained. The default is to play directly after seeking.<br><br><br>* `play`: play<br><br>* `pause`: pause<br><br>* `auto`: keep the status before operation |
|onMediaExpired |`() => Promise<`[SourceConfig](https://docs.byteplus.com/en/docs/25/ref#sourceconfig)`>` |No |\- |Callback invoked when the playback source expires. Use it to refresh source data. |
|onTokenExpired |`() => Promise<`[IPlayAuthTokenConfig](https://docs.byteplus.com/en/docs/25/7976#iplayauthtokenconfig)`>` |No |\- |Callback invoked when the temporary play token expires. Use it to refresh the token. |


<span id="iplayauthtokenconfig"></span>
## IPlayAuthTokenConfig

Vid playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|playAuthToken |string |Yes |\- |Temporary play token generated by the app server. |
|defaultDefinition |string |No |\- |Default definition, corresponding to `Definition` in the GetPlayInfo response. Defaults to the highest available when empty. |
|playDomain |string |No |`https://vod.byteplusapi.com` |Get the requested domain name of the playback address |
|needPoster |boolean |No |`false` |Whether to use the poster image set in the VOD console. |
|needThumbs |boolean |No |`false` |Whether to use the sprite sheet (thumbnail) generated by the VOD media processing service. |
|needBarrageMask |boolean |No |`false` |Whether to use the masked danmaku generated by the VOD media processing service. |
|needDefinitionList |boolean |No |`true` |Whether to fetch and display multiple definition options. |
|keyToken |string |No |\- |Key token required for HLS standard\-encrypted playback. |
|reqParams |Record<string, string \| number \| boolean\> |No |\- |Extra pass\-through query parameters (e.g. `{ aid: 1234 }`). Parameters from `playAuthToken` take highest priority. |
|definitionMap |Record<string, string \| [definitionItem](https://docs.byteplus.com/en/docs/25/7976#definitionitem)\> |No |\- |Definition label mapping. |
|retryCount |number |No |`1` |Number of retries when the VOD service returns a 502 error. |
|autoDemoteDefinition |string |No |\- |Auto\-demote definition target when definition auto\-demote is enabled. Corresponds to `Definition` in GetPlayInfo response. |
|autoDemoteDefinitionTextKey |string |No |\- |i18n key for the auto\-demote definition label, mapping into `languages`. |
|urlQueryParams |Record<string, string\> |No |\- |Extra query parameters appended to video URL requests. Typically used for HLS standard\-encrypted playback. |
|useMasterM3u8 |boolean |No |\- |Whether to use the master m3u8 URL as the playback source for HLS. |
|getDrmAuthToken |`(playAuthIds: string, vid: string, unionInfo: string) => Promise<string>` |No |\- |Async callback to fetch `PrivateDrmAuthToken`. Receives `playAuthIds` (comma\-separated key IDs), `vid`, and `unionInfo`. |


<span id="definitionitem"></span>
## definitionItem

Definition item.


|Property |Description |
|---|---|
|definition |Definition level. |
|definitionTextKey |i18n key for the definition label. |


<span id="iposter"></span>
## IPoster

Poster configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|poster |string |Yes |\- |Poster image URL. |
|isEndedShow |boolean |No |`true` |Whether to show the poster after playback ends. |
|hideCanplay |boolean |No |`false` |Whether to hide the poster after playback starts. When `true`, the poster re\-appears after a URL update. |
|notHidden |boolean |No |`false` |Whether to keep the poster always visible. |
|fillMode |"fixWidth" \| "fixHeight" \| "cover" \| "contain" |No |\- |Poster fill mode: `fixWidth`, `fixHeight`, `cover` (crop to fill), or `contain` (stretch to fill). |


<span id="ipipconfig"></span>
## IPIPConfig

Picture\-in\-picture configuration.


|Property |Description |
|---|---|
|showIcon |Whether to show the picture\-in\-picture button. |
|preferDocument |Whether to prefer `DocumentPictureInPicture` (web PiP) when available. |
|width |Width of the document PiP window. |
|height |Height of the document PiP window. |
|docPiPNode |Root element of the document PiP window. |
|[docPiPStyle](https://docs.byteplus.com/en/docs/25/7976#ipipconfig-docpipstyle) |CSS style for the document PiP window. |


<span id="ifullscreenconfig"></span>
## IFullscreenConfig

Fullscreen configuration.


|Property |Description |
|---|---|
|useCssFullscreen |Whether to use CSS fullscreen instead of native system fullscreen. |
|rotateFullscreen |Whether to rotate the DOM 90° to achieve landscape fullscreen. Takes priority over `useCssFullscreen`. Mainly for mobile. |
|useScreenOrientation |Whether to lock the screen orientation after rotating to fullscreen. Only supported in some browsers. See [ScreenOrientation API: lock](https://caniuse.com/mdn-api_screenorientation_lock) |
|lockOrientationType |Orientation type to lock after rotating to fullscreen. See [orientation](https://developer.mozilla.org/en-US/docs/Web/API/ScreenOrientation/lock#orientation) |
|target |Custom DOM element for fullscreen. Must be an ancestor of `player.root`. Defaults to the player root node. |
|disable |Whether to disable the fullscreen button. When `true`, the button is not rendered. |
|needBackIcon |Whether to show a back button in the top\-right corner during fullscreen. Mainly for mobile. |
|[switchCallback](https://docs.byteplus.com/en/docs/25/7976#ifullscreenconfig-switchcallback) |Custom fullscreen toggle implementation. Completely replaces the built\-in toggle logic. |


<span id="icodectype"></span>
## ICodecType

Codec type.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|


<span id="icommonstyle"></span>
## ICommonStyle

Common style configuration.


|Property |Description |
|---|---|
|progressColor |Progress bar track color. |
|playedColor |Color of the played portion of the progress bar. |
|cachedColor |Color of the buffered portion of the progress bar. |
|sliderBtnStyle |Style of the progress bar thumb/slider. |
|volumeColor |Volume control color. |


<span id="stream"></span>
## Stream

Playback URL list; supports multiple lines and definitions.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|streamType |string |No |\- |Stream type: `"rtm"`, `"flv"`, `"mp4"`, or `"hls"`. |
|url |[Url](https://docs.byteplus.com/en/docs/25/7976#url) |Yes |\- |Video playback URL. |
|definition |string |No |\- |Definition key for this stream. |
|mapDefinition |string |No |\- |Mapped definition key. |
|definitionTextKey |string |No |\- |i18n dictionary key for the definition label. E.g. with `definitionTextKey: HD_TEXT_KEY` and `languages: { zh: { HD_TEXT_KEY: 'HD' } }`, the switcher shows "HD". Falls back to `definition` when unset. |
|codec |[ICodecType](https://docs.byteplus.com/en/docs/25/7976#icodectype) |No |`unknown` |Codec type of this stream. |
|lineId |string \| number |No |\- |Unique line (CDN route) ID. |
|lineTextKey |string |No |\- |i18n dictionary key for the line label, e.g. `lineTextKey: LINE_ONE`. |
|width |number |No |\- |Stream video width in pixels. |
|height |number |No |\- |Stream video height in pixels. |
|bitrate |number |No |\- |Average bitrate of the stream. |
|bandwidth |number |No |\- |Bandwidth required for smooth playback of this stream. |
|urlExpireTimestamp |number |No |\- |URL expiration timestamp in seconds. Omit in vid mode (auto\-fetched). For Volcengine CDN URLs without a timestamp, specify `urlType` (supports [types A–E](https://www.volcengine.com/docs/4/177191)); not supported for other CDNs or self\-hosted URLs. |
|kid |string |No |\- |Encryption key ID for private\-encrypted playback, corresponding to `PlayAuthId` in the [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) response. |
|secretKey |string |No |\- |Encryption key for private\-encrypted playback, corresponding to `PlayAuth` in the [GetPlayInfo](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) response. |
|drmType |[EDRMTYPE](https://docs.byteplus.com/en/docs/25/ref#edrmtype) |No |\- |Encryption type for encrypted video. |


<span id="audiotrackoption"></span>
## AudioTrackOption

Audio track selection options.

Corresponding to all fields of hls.js `AudioSelectionOption`, all fields are optional.

Used for `switchAudioTrack()` and `audioPreference` configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|lang |string |No |\- |Primary track language in BCP\-47 format (e.g. `zh`, `en`). Maps to `#EXT-X-MEDIA` `LANGUAGE`. |
|assocLang |string |No |\- |Associated language code. Maps to `#EXT-X-MEDIA` `ASSOC-LANGUAGE`. |
|characteristics |string |No |\- |Track characteristics string. Maps to `#EXT-X-MEDIA` `CHARACTERISTICS`. |
|channels |string |No |\- |Number of audio channels. Maps to `#EXT-X-MEDIA` `CHANNELS` (e.g. `"2"`). |
|name |string |No |\- |Track name for display or precise matching (e.g. `Stereo`). With `lang`, uniquely identifies a track on the hls.js path. |
|audioCodec |string |No |\- |Audio codec identifier (e.g. `mp4a.40.2`). |
|groupId |string |No |\- |Audio group ID. Maps to `#EXT-X-MEDIA` `GROUP-ID`. |
|default |boolean |No |\- |Whether this is the default track declared in the manifest. |


<span id="ivolume"></span>
## IVolume

Volume configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|position |[POSITIONS](https://docs.byteplus.com/en/docs/25/ref#positions) |No |`POSITIONS.CONTROLS_RIGHT` |The position of the plugin dom. The default value is `POSITIONS.CONTROLS_RIGHT`. |
|index |number |No |`1` |The index of the plugin in the position. The default value is `1`. |
|disable |boolean |No |`false` |Whether to disable the plugin interaction behavior, i.e., whether to hide the volume adjustment button. |
|showValueLabel |boolean |No |`false` |Whether to show the current volume value on the volume adjustment slider. |
|default |number |No |`0.6` |The default volume value. The value range is `[0, 1]`. |
|miniVolume |number |No |`0.2` |The minimum volume value when unmuting. The value range is `[0, 1]`. |


<span id="isdkerrorconfig"></span>
## ISdkErrorConfig

UI configuration when the player encounters an error.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|errorImg |boolean |No |`true` |Whether to show an error image when playback fails. |
|errorTips |boolean |No |`true` |Whether to show error text when playback fails. |
|isNeedRefreshButton |boolean |No |`true` |Whether to show a refresh button when playback fails. |
|retryLoopNum |number |No |`1` |Number of retries after an error. |
|errorTipsText |[TipsTextConfig](https://docs.byteplus.com/en/docs/25/7976#tipstextconfig) |No |`An error occurred while playing, click refresh to try` |Error prompt text per language. |


<span id="tipstextconfig"></span>
## TipsTextConfig

Error message text configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|zh |string \| HTMLElement |No |`An error occurred while playing, click refresh to try` |Chinese error message. |
|en |string \| HTMLElement |No |`An error occurred while playing, click refresh to try` |English error message. |
|jp |string \| HTMLElement |No |`An error occurred while playing. Click refresh to try again.` |Japanese error message. |
|'zh\-hk' |string \| HTMLElement |No |`An error occurred while playing. Click refresh to try again.` |Hong Kong Traditional Chinese error message. |


<span id="iaudiotrackconfig"></span>
## IAudioTrackConfig

PC audio track selector plugin configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|index |number |No |`70` |Sort weight in the control bar; smaller values appear further left. |
|isShowIcon |boolean |No |`true` |Whether to show the audio track switcher icon. |
|hidePortrait |boolean |No |`false` |Whether to hide the audio track control in portrait orientation. |
|showNameSuffix |boolean |No |`true` |Whether to append the raw track name in parentheses after the language label, e.g. `Japanese (Stereo AudioTrack1)`. |


<span id="iaudiotrackmobileconfig"></span>
## IAudioTrackMobileConfig

Mobile audio track selector plugin configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|index |number |No |`2.6` |Sort weight in the control bar; smaller values appear further left. |
|isShowIcon |boolean |No |`true` |Whether to show the audio track switcher icon. |
|showNameSuffix |boolean |No |`true` |Whether to append the raw track name in parentheses after the language label, e.g. `Japanese (Stereo AudioTrack1)`. |


<span id="idanmuconfig"></span>
## IDanmuConfig

Danmu (bullet comment) configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|opacity |number |No |`99` |Danmu opacity. Enum [0, 33, 66, 99] maps to 0, 0.33, 0.66, 1. |
|area |number |No |`99` |Danmu display area. Enum [0, 33, 66, 99] maps to 1/4, 1/2, 3/4, full screen. |
|speed |number |No |`40` |Danmu scroll speed. Enum maps to 1/4, 1/2, 1, 5/4, 3/2, 2x. |
|fontSize |number |No |`50` |Danmu font size. Enum [0, 50, 100] maps to 14px, 16px, 20px. |
|active |boolean |No |`false` |Whether danmu is enabled by default. |
|danmuItems |[DanmuItem](https://docs.byteplus.com/en/docs/25/7976#danmuitem)[] |No |\- |Danmu (bullet comment) list. |
|maskConfig |[IMaskConfig](https://docs.byteplus.com/en/docs/25/ref#imaskconfig) |No |\- |Mask danmu configuration. |
|maskActive |boolean |No |`false` |Whether to enable mask danmu (smart occlusion). |


<span id="danmuitem"></span>
## DanmuItem

Danmu item.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|id |string |Yes |\- |Unique danmu ID. |
|txt |string |Yes |\- |Danmu text. |
|start |number |No |`0` |Danmu appear time in milliseconds. |
|duration |number |No |`5000` |Danmu display duration in milliseconds. |
|style |CSSStyleDeclaration |No |\- |Danmu style, e.g. `{ color: '#ff9500', fontSize: '20px', padding: '2px 11px' }`. |


<span id="idefinitiondemoteplugin"></span>
## IDefinitionDemotePlugin

Definition demotion configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|isNeedAutoDemote |boolean |No |\- |Is automatic downgrade enabled? The values are as follows:<br><br><br>* `false`: automatic downgrade is disabled.<br><br>* `true`: automatic downgrade is enabled. |
|demotePriority |string[] |Yes |`[]` |The order of definition downgrade. The elements in the array should correspond to the `definition` in the `playList`. |
|longWaitingTime |number |No |`5000` |The threshold for long waiting time, in milliseconds. If the waiting time exceeds this value, it is considered as long waiting. The `LONG_WAITING` event will be triggered when long waiting occurs. |
|oftenWaitingCount |number |No |`3` |The threshold for frequent stuttering, in milliseconds. If the stuttering count exceeds this value, the `OFTEN_WAITING` event will be triggered, indicating frequent stuttering. |
|oftenWaitingTime |number |No |`5000` |The time range for frequent stuttering monitoring. If the stuttering count exceeds `oftenWaitingCount` within `oftenWaitingTime`, the `OFTEN_WAITING` event will be triggered, indicating frequent stuttering. |
|isNeedShowTips |boolean |No |`true` |Whether to display the definition downgrade toast. |
|toastShowTime |number |No |`3000` |The duration of the definition downgrade toast, in milliseconds. |


<span id="idashpluginconfig"></span>
## IDashPluginConfig

DASH playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|vid |string |No |\- |Video ID. |
|playInfoType |"TOP" |Yes |`TOP` |Playback type. |
|definitionText |Record<string, string\> |Yes |\- |Definition label mapping. |
|defaultDefinition |string |No |`列表第一个` |默认清晰度。 |
|getLicenseUrl |string |No |`//i.snssdk.com/video/drm/v1/play_licenses` |Get the certificate address. |
|preloadTime |number |No |`50` |Preload time in milliseconds. |


<span id="iencrypthlspluginconfig"></span>
## IEncryptHlsPluginConfig

HLS encrypted playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|playDomain |string |No |`https://vod.byteplusapi.com` |Get the requested domain name of the playback address |
|keyDomain |string |No |`https://vod.byteplusapi.com` |Request domain name for key request |
|playAuthToken |string |No |\- |Playback address acquisition token, generated by the server and distributed by the server, see [PlayAuthToken](https://docs.byteplus.com/en/docs/byteplus-vod/reference-getplayinfo) |
|keyToken |string |Yes |\- |Key acquisition token, generated by the server and distributed by the server, see [keyToken](https://docs.byteplus.com/en/docs/byteplus-vod/docs-go-sdk#generating-hls-decryption-token) |


<span id="ivodlogoptsconfig"></span>
## IVodLogOptsConfig

Quality log configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|line_app_id |number |Yes |\- |VOD application ID. You can get the application ID (App ID) on the video [VOD Console > VOD SDK > application management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-singapore-1/sdk/app/?projectName=default) page. |
|line_user_id |string \| number |Yes |\- |The ID used to identify a single user. It can be used for user\-level filtering in [QoE indicators](https://docs.byteplus.com/en/docs/byteplus-vod/docs-quality-insight-overview), and also for [single-point tracing](https://www.volcengine.com/docs/4/106093) to find the playback logs of a single user.<br><br>The user ID corresponds to the device ID dimension in the query conditions of the single\-point tracing function. If no user ID is set, VePlayer will generate a random value according to the user's browser, which will be cached in the browser. |
|tag |string |No |`Normal` |Business tag. Corresponds to the business type dimension on the quality platform, which is used to distinguish different scenarios in the business and facilitate multi\-dimensional analysis. For example, if your application contains short video and long video scenarios, you can set `tag` to `short` and `long` respectively. This way, you can query or filter data for different scenarios through the business tag dimension on the [quality platform](https://docs.byteplus.com/en/docs/byteplus-vod/docs-end-point-tracker). |
|subtag |string |No |\- |Custom sub\-tag for quality platform analytics; use with `tag` to distinguish sub\-types such as encrypted/non\-encrypted video or audio. |
|codec_type |"h264" \| "h265" |No |`unknown` |Video codec type, values:<br><br><br>* `h264`: H.264<br><br>* `h265`: H.265 |


<span id="iautobitrateopts"></span>
## IAutoBitrateOpts

Adaptive bitrate (ABR) playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enable |boolean |Yes |`false` |Whether to enable adaptive bitrate (ABR). |
|startWithAuto |boolean |No |`false` |Whether to start playback with the auto definition level. Takes effect only when ABR is enabled and `defaultDefinition` is `auto`. |
|showRealDefinition |boolean |No |`false` |Whether the auto definition label shows the actual resolution, e.g. Auto (720p). |
|autoDefinitionText |string |No |`auto` |Display text for the auto definition level. |
|definitionTextKey |string |No |`DEFINITION_AUTO` |i18n key for the auto definition level label. |


<span id="isubtitleconfig"></span>
## ISubtitleConfig

External subtitle configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|position |string |No |`controlsRight` |Icon position. |
|index |number |No |`6` |Icon sort weight. |
|list |[ISubTitleItem](https://docs.byteplus.com/en/docs/25/7976#isubtitleitem)[] |No |\- |Subtitle list. |
|isDefaultOpen |boolean |No |`true` |Whether subtitles are open by default. |
|isShowIcon |boolean |No |`true` |Whether to show the icon. |
|mode |"external" \| "native" |No |`external` |Subtitle render mode:<br><br><br>* `"external"`: external subtitles<br><br>* `"native"`: native subtitles |
|style |[ISubtitleStyle](https://docs.byteplus.com/en/docs/25/7976#isubtitlestyle) |No |\- |Subtitle style. |


<span id="isubtitleitem"></span>
## ISubTitleItem

Subtitle item.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|language |string \| number |No |\- |Subtitle language. |
|id |string \| number |No |\- |Subtitle ID. |
|isDefault |boolean |No |`false` |Whether this is the default selected subtitle. |
|text |string |No |\- |Subtitle display name. |
|url |string |No |\- |External subtitle URL. |
|list |[IListItem](https://docs.byteplus.com/en/docs/25/7976#ilistitem)[] |No |\- |Subtitle content list when not using URL. |


<span id="ilistitem"></span>
## IListItem

Subtitle content item.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|start |number |Yes |\- |Start time in seconds. |
|end |number |Yes |\- |End time in seconds. |
|list |[ITextItem](https://docs.byteplus.com/en/docs/25/7976#itextitem)[] |Yes |\- |Subtitle cue data list. |


<span id="itextitem"></span>
## ITextItem

Subtitle text item configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|start |number |Yes |\- |Start time in seconds. |
|end |number |Yes |\- |End time in seconds. |
|text |string[] |Yes |\- |Subtitle text array. |
|index |number |No |\- |Subtitle display order. |


<span id="isubtitlestyle"></span>
## ISubtitleStyle

Subtitle style configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|follow |boolean |No |`false` |Whether position follows the control bar. |
|mode |"stroke" \| "bg" |No |`'stroke'` |Font display mode:<br><br><br>* `"stroke"`: outlined text<br><br>* `"bg"`: solid background |
|followBottom |number |No |`50` |Offset height following the bottom control bar. |
|fitVideo |boolean |No |`true` |Whether font size auto\-adjusts with video. |
|offsetBottom |number |No |`4` |Subtitle offset from bottom as percentage. |
|baseSizeX |number |No |`49` |Base font size for landscape video. |
|baseSizeY |number |No |`28` |Base font size for portrait video. |
|minSize |number |No |`16` |Minimum font size on PC. |
|minMobileSize |number |No |`13` |Minimum font size on mobile. |
|line |"double" \| "single" \| "three" |No |`double` |Maximum display lines:<br><br><br>* `"double"`: two lines<br><br>* `"single"`: one line<br><br>* `"three"`: three lines |
|fontColor |string |No |`#fff` |Font color; hex or RGB value. |


<span id="imemoryplayconfig"></span>
## IMemoryPlayConfig

Memory playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|memoryId |string \| number |Yes |`options.vid \|\| options.url` |Storage identifier for resume playback. |
|minStartTime |number |No |`1` |Minimum played duration (seconds) to count as started. Shorter playback stores position as 0. |
|minEndTime |number |No |`1` |Minimum remaining duration (seconds) before end to treat playback as finished. Clears stored progress when ended. |
|saveTime |`(id: number \| string, time: number) => unknown` |No |\- |Callback to persist the playback position. |
|getTime |`(id: number \| string) => number \| Promise<number>` |No |\- |Callback to retrieve the last saved playback position. |


<span id="imusicconfig"></span>
## IMusicConfig

Music playback mode configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|offline |boolean |No |`false` |Whether to enable offline downloaded playback. |
|abCycle |[IABCycle](https://docs.byteplus.com/en/docs/25/7976#iabcycle) \| null |No |`null` |AB loop playback configuration. |
|timeScale |number |No |`15` |Fast\-forward / rewind step in seconds. |
|mode |[PlayModeType](https://docs.byteplus.com/en/docs/25/ref#playmodetype) |No |`order` |Playback loop mode: `order`, `sloop` (single loop), `loop` (list loop), `random`. |
|list |[IMusicListItem](https://docs.byteplus.com/en/docs/25/ref#imusiclistitem)[] |No |`[]` |Music playlist. |


<span id="iabcycle"></span>
## IABCycle

AB loop playback configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|start |number |Yes |`0` |AB loop start time in seconds. |
|end |number |Yes |`End of audio` |AB loop end time in seconds. |
|loop |boolean |No |`false` |Whether to loop the AB segment. |


<span id="iautoplaypluginconfig"></span>
## IAutoplayPluginConfig

Autoplay configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enableDegradeMuteAutoplay |boolean |No |`false` |Whether to enable degraded muted autoplay. When enabled, if the current browser environment does not support sound autoplay, it will be downgraded to muted autoplay. |
|userActionDom |Node |No |`window.document.body` |\- |
|enableUserActionAutoplay |boolean |No |`false` |Whether to enable user action autoplay. When enabled, the first user's click can trigger the autoplay of the player. The following values are supported:<br><br><br>* `true`：enable<br><br>* `false`：disable |
|showUnmuteBtn |boolean |No |`true` |Whether to show the unmute button in the player container. |


<span id="iplaylistconfig"></span>
## IPlayListConfig

Playlist plugin configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|position |string |No |`controlsLeft` |Position of the button. The following values are supported:<br><br><br>* `controlsLeft`: left of the control bar<br><br>* `controlsRight`: right of the control bar<br><br>* `controlsCenter`: center of the control bar<br><br>* `rootLeft`: left of the player root node<br><br>* `rootRight`: right of the player root node<br><br>* `rootTop`: top of the player root node<br><br>* `root`: player root node |
|index |number |No |`20` |Order of the button in the region. The default value is `2`, indicating after the play button. |
|list |[IPlayListItem](https://docs.byteplus.com/en/docs/25/7976#iplaylistitem)[] |Yes |`[]` |Playlist data. |
|mode |[EPlayMode](https://docs.byteplus.com/en/docs/25/7976#eplaymode) |No |`order` |Loop mode. The following values are supported:<br><br><br>* `order`: do not loop playback, i.e., stop playing after the last video in the list is played.<br><br>* `loop`: loop playback, i.e., start playing the first video in the list after the last video is played. |
|defaultIndex |number |No |`order` |Default starting playback order. The default value is `0`, indicating the first video in the list. |
|isItemClickHide |boolean |No |`true` |Whether to hide the list after clicking on an item. |
|toggleMode |[TOGGLE_MODES](https://docs.byteplus.com/en/docs/25/ref#toggle-modes) |No |`click` |List panel trigger mode. |
|isShowIcon |boolean |No |`true` |Whether to show the list button. |


<span id="iplaylistitem"></span>
## IPlayListItem

Playlist item configuration, supporting DirectUrl and Vid + playAuthToken two playback modes.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|url |string |No |\- |Video URL.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">when <code>playAuthToken</code> is empty, this parameter is required.</div><br> |
|playAuthToken |string |No |\- |Playback temporary security credential issued by the business app server.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">when <code>url</code> is empty, this parameter is required.</div><br> |
|vid |string |Yes |\- |Unique ID for the video. If not provided, the index of the video in the list is used. |
|poster |string |No |\- |Video cover image URL. |
|title |string |No |\- |Video title. |
|duration |number |No |\- |Video duration in seconds. |


<span id="eplaymode"></span>
## EPlayMode

Playlist loop mode.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|ORDER |EPlayMode.ORDER |Yes |\- |Play in order. |
|LOOP |EPlayMode.LOOP |Yes |\- |Loop playlist. |


<span id="iwatermarkconfig"></span>
## IWatermarkConfig

watermark config


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|enable |boolean |Yes |`false` |Is dynamic watermark enabled? The value is as follows:<br><br><br>* `true`: Enable dynamic watermark<br><br>* `false`: Disable dynamic watermark |
|content |string |Yes |\- |Watermark content. |
|displayType |0 \| 1 \| 2 |No |`1` |Watermark display type. The value is as follows:<br><br><br>* `0`: Fixed position<br><br>* `1`: Full screen scrolling<br><br>* `2`: Random flickering |
|fontSize |string \| number |No |`12` |Watermark font size. When the type is `number`, the unit is px. When the type is `string`, the unit needs to be included. |
|fontColor |string |No |\- |Watermark font color. |
|opacity |number |No |`0.3` |Watermark opacity. The value is in the range of [0~1]. |
|tickerSpeed |"SLOW" \| "MODERATE" \| "FAST" |No |`MODERATE` |Watermark ticker speed. The value is as follows:<br><br><br>* `MODERATE`: Moderate<br><br>* `FAST`: Fast<br><br>* `SLOW`: Slow |
|fontFamily |string |No |\- |Watermark font family. |
|top |number |No |`0` |Watermark top distance. The unit is px. |
|left |number |No |`0` |Watermark left distance. The unit is px. |
|bottom |number |No |\- |Watermark bottom distance. The unit is px. |
|right |number |No |\- |Watermark right distance. The unit is px. |


<span id="ithumbnailconfig"></span>
## IThumbnailConfig

Thumbnail configuration for progress bar preview.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|urls |string[] |Yes |\- |Array of sprite sheet URLs. |
|pic_num |number |Yes |\- |Total number of thumbnail frames. |
|col |number |Yes |\- |Number of thumbnail columns per sprite sheet. |
|row |number |Yes |\- |Number of thumbnail rows per sprite sheet. |
|height |number |No |\- |Thumbnail frame height in px. |
|width |number |No |\- |Thumbnail frame width in px. |
|hidePortrait |false |No |`false` |Whether to hide the thumbnail in portrait orientation. |


<span id="idot"></span>
## IDot

Progress bar marker point configuration.


|Config |Type |Required |Default |Description |
|---|---|---|---|---|
|id |string \| number |Yes |`1` |The id of the progress bar marker point. |
|time |number |Yes |`0` |The time of the progress bar marker point. |
|text |string |No |\- |The text of the progress bar marker point. |
|duration |number |No |`1` |The duration of the progress bar marker point. |
|style |CSSStyleDeclaration |No |\- |The custom CSS style of the progress bar marker point. |


<span id="codectype"></span>
## CodecType

Video/audio codec type.


|Property |Description |
|---|---|


<span id="url"></span>
## Url  

URL type. Supports strings and arrays. If it's in the form of an array, each item in the array should contain the video playback address `src` and the video container format type `type`. Use the element in the HTML `<video />` element to set multiple format video sources. The addresses set with the `<source />` element do not support MSE (Media Source Extensions) playback scenarios, such as playing HLS videos on PCs or encrypted HLS videos on Android.

**Type**

```ts
string | Array<{ src: string; type?: string; [propName: string]: any }>
```


<span id="strategyinitoptions"></span>
## StrategyInitOptions  

Player pre\-initialization configuration.

**Type**

```ts
{
  appId: number;
  region?: TRegionType;
  strategies: StrategyConfigOptions;
  deviceId?: string;
  plugins?: any[];
  Module?: typeof VeStrategy;
}
```


**Member**


|Name |Type |Description |
|---|---|---|
|appId |`number` |Application ID. |
|region |`TRegionType \| undefined` |User region. |
|strategies |[StrategyConfigOptions](https://docs.byteplus.com/en/docs/25/7976#strategyconfigoptions) |Strategy configuration. |
|deviceId |`string \| undefined` |Device ID. |
|plugins |`any[] \| undefined` |Manually inject dependency plugins; loaded automatically by default. |
|Module |`any` |Strategy module; loaded automatically by default. |


<span id="strategyconfigoptions"></span>
## StrategyConfigOptions  

Strategy configuration.

**Type**

```ts
{
  [StrategyNames.H265]?: boolean | IH265Config;
  [StrategyNames.PRELOAD]?: boolean | IPreloadConfig;
  [StrategyNames.ADAPT_RANGE]?: boolean | IAdaptRangeConfig;
}
```


**Member**


|Name |Type |Description |
|---|---|---|
|preload |`boolean \| `[IPreloadConfig](https://docs.byteplus.com/en/docs/25/7976#ipreloadconfig)` \| undefined` |Preload configuration. |
|adaptRange |`boolean \| IAdaptRangeConfig \| undefined` |Dynamic buffer (range splitting) configuration. |


<span id="ipreloadconfig"></span>
## IPreloadConfig  

Preload initial configuration.

**Type**

```ts
{
  preloadScene?: PreloadScene;
  format?: PreloadFormat;
  prevCount?: number;
  nextCount?: number;
  preloadTime?: number;
  preloadMaxCacheCount?: number;
  Strategy?: any;
  disabled?: boolean;
}
```


**Member**


|Name |Type |Description |
|---|---|---|
|preloadScene |[PreloadScene](https://docs.byteplus.com/en/docs/25/7976#preloadscene)` \| undefined` |Preload scene.<br><br><br>* 0: manual execution<br><br>* 1: automatic execution |
|format |[PreloadFormat](https://docs.byteplus.com/en/docs/25/ref#preloadformat)` \| undefined` |Video format. |
|prevCount |`number \| undefined` |Number of videos to preload ahead. Effective in Feed scenarios. |
|nextCount |`number \| undefined` |Number of videos to preload behind. Effective in Feed scenarios. |
|preloadTime |`number \| undefined` |Preload duration per video (seconds). |
|preloadMaxCacheCount |`number \| undefined` |Maximum number of cached videos. |
|Strategy |`any` |Preload dependency module. |
|disabled |`boolean \| undefined` |Whether to disable preload. |


<span id="preloadscene"></span>
## PreloadScene  

Type：`enum`

Preload scene.


|Property |Value |Description |
|---|---|---|
|NORMAL |`0` |Normal scenario (manual preload). |
|FEED |`1` |Feed scenario (player auto\-preloads). |


<span id="ipreloadstream"></span>
## IPreloadStream  

Preload video resource.

**Type**

```ts
{
  vid: string;
  url: string;
  definition: string;
  streamType: string;
  codec: string;
  bitrate: number;
  duration: number;
  size: number;
}
```


**Member**


|Name |Type |Description |
|---|---|---|
|vid |`string` |Unique video ID. |
|url |`string` |Playback URL. |
|definition |`string` |Video definition (resolution). |
|streamType |`string` |Stream type; supports mp4 and hls. |
|codec |`string` |Video codec; currently supports h264. |
|bitrate |`number` |Bitrate; optional, used for analytics. |
|duration |`number` |Duration; optional, used for analytics. |
|size |`number` |File size; optional, used for analytics. |


<span id="strategynames"></span>
## StrategyNames  

Type：`enum`

Advanced capability (strategy) names.


|Property |Value |Description |
|---|---|---|
|H265 |`'h265'` |H.265 strategy. |
|PRELOAD |`'preload'` |Preload strategy. |
|ADAPT_RANGE |`'adaptRange'` |Dynamic buffer (range splitting). |
