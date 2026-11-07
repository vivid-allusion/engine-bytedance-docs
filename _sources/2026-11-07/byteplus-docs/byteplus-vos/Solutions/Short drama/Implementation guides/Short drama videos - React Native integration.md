---
title: "Short drama videos - React Native integration"
product: "BytePlus Video One Solution"
product_code: "byteplus-vos"
source: "https://docs.byteplus.com/en/docs/byteplus-vos/short-drama-integration-by-reactnative"
---

This document is intended for developers who want to integrate short drama capabilities based on the VideoOne ReactNative Demo. It covers the full workflow from getting the source code and preparing the environment to configuring the project, running the demo, replacing business APIs, and understanding the code structure.

## Solution overview

The ReactNative short drama solution is built on the BytePlus ReactNative VOD SDK and the Expo technology stack. It provides core capabilities for mobile short drama scenarios, including drama list browsing, channel page navigation, vertical continuous playback, episode unlocking, user interaction, and recommendation display. For teams that have already completed the basic environment setup, the most efficient integration path is to reuse the existing Demo pages, components, and service layer, then gradually replace the business\-facing parts with your own implementation.

|Dimension |Description |Recommendation |
|---|---|---|
|Target scenario |Mobile short drama playback and episodic consumption |Suitable for teams that want to validate a short drama product quickly |
|Core capabilities |Episode selection, resume playback, playback speed, quality switching, unlocking, likes, comments, and recommendations |Reuse the existing Demo pages and service boundaries as much as possible |
|Integration workload |Mainly focused on API replacement, data mapping, and UI customization |Run the Demo first, then replace business modules step by step |

## Integration approach

Similar to the Web integration path, ReactNative short drama integration is best handled in two stages. In the first stage, run the official Demo end to end and confirm that playback capability, License configuration, native projects, and device debugging all work properly. In the second stage, gradually replace the demo data source, unlock logic, and visual styles with your own business implementation. This phased approach makes issue isolation much easier because it helps you distinguish environment problems, SDK configuration problems, and business integration problems.

In the first stage, prepare the environment, configure the service address and License, and run the Demo on iOS and Android devices.

In the second stage, replace the drama and channel APIs, replace the user and unlock logic, map your business data structure, and customize styles and interactions.

## Prerequisites

Before starting the ReactNative short drama integration, make sure you already have the basic prerequisites required to run the Demo. If you have not completed the basic project setup yet, we recommend reading the sibling document **Build your first app by ReactNative** first, then returning to this document for the business integration phase.

|Item |Purpose |Output |
|---|---|---|
|BytePlus account and AK/SK |Access cloud services and authenticate business services |Access Key and Secret Key |
|VOD service and application |Provide video playback capability |App ID and License file |
|ReactNative development environment |Run iOS and Android projects |Node, Expo CLI, Xcode, CocoaPods, and Android Studio |
|Physical test devices |Validate real mobile short drama interactions |Android 6.0+ or iOS 13.0+ device |

## Run the Demo

### Steps

1. **Get the source code**

   The ReactNative Demo is located in the `Client/ReactNative` directory of the `VideoOneSolutions` repository. We recommend integrating directly on top of that project so you can reuse the existing short drama pages, service layer, and component structure.

   ```Shell
   git clone https://github.com/byteplus-sdk/VideoOneSolutions
   cd VideoOneSolutions/Client/ReactNative
   ```

> If your goal is to integrate a short drama scenario quickly, do not start from an empty project. Start from the Demo and replace the business\-facing parts instead.

2. **Install dependencies**

   After downloading the source code, install both JavaScript dependencies and iOS native dependencies. Because the project is based on Expo and ReactNative, JavaScript dependencies are used for pages, routing, and business logic, while Pods in the `ios` directory are used for native integration.

   1. Install Expo CLI.

   2. Install npm dependencies in the project root directory.

   3. Go to the `ios` directory and run `pod install` to install iOS native dependencies.

   ```Shell
   npm install -g @expo/cli
   npm install
   cd ios && pod install
   ```

3. **Configure the application service**

   Business data in the Demo is abstracted through the service layer. To integrate the Demo into your own short drama business, the first step is usually to replace the application service address. You can initially use the Demo service to verify the full page flow, then switch to your own production service later.

   Open the `services/api.ts` file and update the service address configuration, such as `SERVER_HOST`. If you are only validating the Demo, you can temporarily keep the demo server address. For a real integration, replace it with your own business service domain.

   > **说明**

   > The demo service address is only suitable for testing and validation. It must not be used directly in a production environment.

4. **Configure the License and native project**

   The core playback capability depends on the VOD SDK License. Rename the License file you obtained to `ttssdk.lic` and place it in the `assets` directory. The current Demo already uses Expo Config Plugins to copy the License into the native resource directories.

   In addition to the License, make sure the Android package name, iOS Bundle Identifier, and signing configuration are aligned with your certificate setup. Otherwise, the application may fail to install or run properly.

   * Android: Update `applicationId` in `android/app/build.gradle`.

   * iOS: Update the `Bundle Identifier` in Xcode under `Signing & Capabilities`, then complete signing\-related configuration.

5. **Run the short drama Demo**

   After the basic configuration is complete, you can run the project on real devices. Real\-device testing is strongly recommended because short drama scenarios rely heavily on swipe switching, immersive full\-screen playback, portrait\-landscape adaptation, and haptic feedback, which cannot be fully validated in an emulator.

   ```Shell
   npm run start
   npm run android
   npm run ios
   ```

   |Command |Purpose |Explanation |
   |---|---|---|
   |`npm run start` |Start the Metro Server |Provides the entry point for resource bundling and debugging |
   |`npm run android` |Install and launch the Android debug build |Recommended for validating swipe and unlock experience on a real device |
   |`npm run ios` |Install and launch the iOS debug build |Recommended for validating playback, episode switching, and interactions on an iPhone |

## Adapt the Demo to your business

Once the Demo runs stably, the next step is to replace business logic layer by layer. A recommended order is **data layer → page entry → playback experience → monetization logic → interaction features**. This sequence usually gives the best balance between implementation efficiency and debugging stability.

### Steps

1. **Replace APIs**

   The `services/` directory is the most important entry point for business adaptation. In most cases, the responsibilities can be mapped as follows:

   * `dramaService.ts`: Drama list, channel data, recommendation feeds, and drama detail retrieval.

   * `unlockService.ts`: Unlock state, ad unlock, batch unlock, and VIP unlock logic.

   * `userService.ts`: User information, login state, and user\-related behaviors.

   * `api.ts`: Shared request client, host configuration, and common request handling.

   During integration, it is recommended to preserve the existing service function boundaries and replace only the internal request implementation and field mapping. This keeps page\-level refactoring to a minimum.

2. **Adapt the data structure**

   The Web short drama integration guide emphasizes replacing APIs and converting data structures. The same principle applies to the ReactNative version. Because UI components typically expect a stable frontend data model, the best practice is to normalize backend response fields into unified frontend models inside the service layer, rather than adapting multiple backend shapes directly in page components.

   > **说明**

   > Recommended practice: Convert backend fields into unified frontend models for drama, episode, user, and unlock state first, then pass those normalized models to pages and components.

3. **Replace page entry and routing**

   The project uses Expo Router for page organization. Short drama related entry points are mainly concentrated in the following files:

   |**Page file** |**Responsibility** |**Recommended customization** |
   |---|---|---|
   |`app/index.tsx` |Home entry |Can be replaced with your own homepage or traffic entry page |
   |`app/drama_channel.tsx` |Short drama channel page |Adapt it to your channel recommendation, topic, or category logic |
   |`app/drama_player.tsx` |Short drama player page |Focus on replacing drama loading, resume playback, unlock, and navigation logic |

4. **Adjust the playback experience**

   Player logic is mainly located in `components/player/` and player configuration utilities. For short drama businesses, common areas of concern include:

   * Preload and pre\-render strategy to reduce waiting time when switching episodes.

   * Portrait playback experience and landscape control layout.

   * Progress persistence and resume playback behavior.

   * Visibility strategy for playback speed, quality, and episode selector.

   * Auto\-play of the next episode and recommendation takeover at the end of playback.

   If your business goal is to maximize binge\-watching smoothness, prioritize preload strategy, next\-episode handoff, and seamless continuation after a successful unlock.

5. **Replace monetization and unlock logic**

   The Demo already provides short drama monetization examples, including ad unlock, VIP unlock, and batch unlock. The related UI and dialog logic is mainly located in:

   * `components/modals/VipUnlockModal.tsx`

   * `components/modals/UnlockMultipleModal.tsx`

   * `services/unlockService.ts`

   * `components/ui/AdComponent.tsx`

   You can replace these with your own monetization model, such as coin unlock, subscription membership, rewarded ads, or a hybrid unlock strategy. It is recommended to centralize unlock policy decisions in the service layer and state layer instead of scattering them across multiple pages.

6. **Replace interaction and recommendation logic**

   A short drama product is more than just a player. It usually includes social interaction and content distribution capabilities. The Demo already contains basic features such as likes, comments, and recommendations. During integration, focus on the following:

   * Replace like and unlike APIs.

   * Replace comment list and comment submission APIs.

   * Replace recommendation recall and recommendation display logic.

   * Adjust recommendation takeover strategy on the channel page, player page, and end\-of\-drama page.

## Developing the casting feature

The VideoOne React Native Demo implements casting at the application layer. On iOS, a system AirPlay route picker and a native AVPlayer relay handle playback. On Android, react\-native\-google\-cast loads media on a Google Cast receiver. TTVideoEngine handles local playback; the Demo coordinates the casting UI, sessions, and page interactions. Integration requires both the React Native components and the corresponding native configuration.

The following describes the current `video-one-rn` implementation. Both platforms expose a controller through `useCast()`, while their start, local pause, and stop sequences differ.

### Casting approach and media requirements

|Item |iOS |Android |
|---|---|---|
|Protocol |AirPlay |Google Cast |
|Device selection |`AVRoutePickerView` |`showCastDialog()` |
|Remote playback |A native `AirPlayRelay` owns the AVPlayer |The receiver loads the URL through `RemoteMediaClient.loadMedia()` |
|When local playback pauses |Muted during selection and startup; paused after `casting` is confirmed |Paused when `isConnecting`, `isConnected`, or `isCasting` is true |
|Stop action |Select the iPhone or another local output in the system picker |Call `endCurrentSession(true)` |

The media URL comes from `MainPlayUrl` in the current playback information in `VideoPlayer.tsx` and is passed to `EpisodePlayer` through `onPlayUrlChange`. Playback callbacks keep the position updated. Casting requires an actual URL that the receiver can access and decode. All casting interface time values are in seconds. Support depends on the resolved URL and receiver capabilities, rather than the name of the application playback mode.

The current relay requests do not forward the local player’s custom headers, cookies, or DRM license configuration. For signed URLs, encrypted media, or restricted networks, verify receiver access and decryption first. Successful playback on the phone does not establish receiver compatibility.

### Native project configuration

* **iOS**

   Include `ios/videoonern/AirPlayRelay.m` and `AirPlayRoutePickerViewManager.m` in the application target to export the bridge module and native view. The native module configures and activates the Audio Session with `Playback`, `Default`, and `LongFormVideo`. Review the local network usage description and the Bonjour services actually used by your application. The Demo also includes `audio` in `UIBackgroundModes`.

   The iOS playback path described here uses AirPlay and does not require application code to initialize `GCKCastContext`. The current Pod lockfile still includes Google Cast dependencies brought in by react\-native\-google\-cast autolinking; dependency presence and the active casting path are separate concerns.

* **Android**

   The current `package.json` declares `react-native-google-cast: ^4.9.1`, and the application Gradle file explicitly depends on `com.google.android.gms:play-services-cast-framework:21.5.0`. `CastOptionsProvider.kt` configures the receiver and media notification. The Manifest registers `OPTIONS_PROVIDER_CLASS_NAME` and declares internet, network state, and Wi\-Fi state permissions. `MainActivity.onCreate` initializes `RNGCCastContext.getSharedInstance(this)`.

   The Demo uses Google’s default media receiver ID, `CC1AD845`. If your application needs a custom receiver, replace it with your registered ID and update the related configuration. Expo projects should retain `./plugins/withGoogleCast` in `app.json`; it generates the Android configuration and supplements iOS local network settings. If you maintain native projects manually, verify the generated files.

### Controller and page integration

`app/drama_player.tsx` creates one `castController` and passes it through `EpisodePlayer` to the button and player. The page uses that controller to render the casting overlay as well. Preserve this data flow when integrating an existing page so the button and page share session state.

```tsx
const castController = useCast();

<CastButton
  castController={castController}
  videoUrl={currentPlayUrl}
  currentTime={currentPlayTime}
  title={dramaTitle}
  coverUrl={dramaCoverUrl}
/>
```

The page maintains the media and position variables in this example. On iOS, `CastButton` renders the native picker, while `VideoPlayer` supplies media through `AirPlayRelay.configureMedia()`. On Android, the button calls `startCasting()` with the supplied URL, position, and metadata after a session is established.

|Interface or state |Current behavior |
|---|---|
|`isConnecting` |Maps to `routeSelecting / routeSelected / starting` on iOS; follows session connection events on Android. |
|`isConnected / isCasting` |Both use the native snapshot’s `isCasting` on iOS. On Android, they indicate an established session and the casting flag set by media loading or status callbacks, respectively. |
|`remotePosition` |Updated on both platforms in seconds. The device label is AirPlay on iOS; Android reads the receiver’s friendly name. |
|`showCastPicker / startCasting / updateCastMedia / seekRemote` |Perform the corresponding operations on Android. They are no\-ops in the iOS hook, where the native picker and relay drive casting. |
|`stopCasting` |Actively ends the Android session. On iOS, it restores the Audio Session only if the route is already local; it does not replace route selection in the system picker. |
|`isAvailable` |Checks native bridge presence on iOS. It currently remains false on Android, so it is not a device discovery result or a reliable condition for hiding the button. |

### iOS: AirPlay relay flow

AirPlay media is configured only for a playable episode whose player is active and whose page has navigation focus. `configureMedia()` supplies the URL, `startTime`, title, cover, and `localWasPlaying`. The picker calls `beginRouteSelection()` before presentation and `endRouteSelection()` after dismissal. The native layer also observes route notifications to determine the actual output.

```text
idle → routeSelecting → routeSelected → starting → casting
casting → stopping → idle
starting → failed
```

During `routeSelecting`, `routeSelected`, and `starting`, the React Native player is muted and records whether it was playing. The native AVPlayer also starts muted, seeks to the supplied position, and begins playback. Only after seek completion, `readyToPlay`, and `externalPlaybackActive` are all satisfied does the relay unmute and report `casting`. React Native then pauses the local player.

The native module emits snapshots through `AirPlayRelayStateChanged` and position updates approximately once per second through `AirPlayRelayProgress`. Snapshots contain the `generation`, state, route and external playback flags, position, and local resume flag. Native asynchronous operations and React Native progress listeners validate the generation to discard stale callbacks. Startup has a 12\-second timeout; failure reports an error and cleans up the relay, observers, and timers.

The overlay’s Stop casting action uses another `AVRoutePickerView`. Before presentation it calls `beginStopRouteSelection()`, and the user selects a local output in the system panel. Dismissing the panel while retaining an external route does not count as stopping. Once the route returns locally, the native layer releases the relay, restores the Audio Session, and reports `idle`; the player then restores local playback.

### Android: Google Cast relay flow

When the user presses the button without a connection, it opens the device dialog and records the intent to load media after connection. If already connected, it requests media loading directly. `useCast` listens for session start, resume, end, and connection failure events, subscribes to media status and progress through the Remote Media Client, and removes listeners on unmount.

The load request contains `contentId / contentUrl`, a MIME type inferred from the URL extension, title, cover, `startTime`, and `autoplay: true`. Loading is attempted up to three times: immediately, then after waits of 500 and 1200 milliseconds. Extension inference covers HLS, DASH, and WebM and otherwise submits MP4. MIME inference does not establish receiver support for the media.

Android pauses local playback during connection: `EpisodePlayer` passes `isConnecting || isCasting || isConnected` to the local player. Successful loading or media status callbacks update the casting flag, but that flag alone does not prove that the TV is rendering video. Load failures currently primarily produce console logs. Applications that require visible errors or automatic local fallback after a failure need to add that handling.

An explicit stop first suppresses automatic resumption and clears UI state, then calls `endCurrentSession(true)` and performs a bounded check for session termination. The suppression ignores late session resume and media callbacks until the user explicitly selects or starts casting again. Finishing the bounded check is not equivalent to receiving confirmation that the receiver stopped.

### Local restoration and page lifecycle

Both platforms restore using the maximum of the current snapshot or remote position, the saved remote position, and the local position. This favors avoiding a backward jump; it is not an unconditional restoration of the receiver’s exact final position. Scenarios such as seeking backward remotely need separate validation. Restoration uses the existing player instance.

* **iOS restoration**

   For an `idle` or `failed` snapshot requiring restoration, the player first requests Audio Session restoration, then seeks locally and unmutes. This handoff branch calls play only when `shouldResumeLocal` is true, local playback was active before casting, and the player is currently paused. Separate page focus and foreground handlers also resume playback; applications requiring strict preservation of a user pause should review all of these entry points together.

* **Android restoration**

   When the casting flag clears, the active local player seeks and calls play directly. It does not preserve a paused\-before\-casting intent. Applications requiring the same pause restoration policy on both platforms need to implement it explicitly.

The page uses `isCasting || isConnected` to show a full\-screen casting overlay, close episode and unlock dialogs, disable list paging, and prevent automatic episode advancement after local completion. These UI restrictions use connected or casting state; they do not establish that every connection transition is locked.

Using Stop casting alone keeps the current player page open. On iOS, a pending navigation action is stored and dispatched only after `idle` with `routeActive` false. A back action does not force a system route change; the user still needs to select a local output through the casting stop entry. The Android page back button awaits a stop attempt before navigating; other page removal events also request a stop, with an exit guard preventing repeated stops for the same session.

To prevent hidden pages from resuming playback, iOS media configuration and state subscriptions apply only to an active player with navigation focus. Foreground restoration also checks navigation focus, active state, and casting pause conditions. On page blur, the local player is paused even if its playing callback has not arrived. The current background AppState handler pauses the local player; it does not uniformly terminate remote sessions.

### Reference code and validation

|File |What to review |
|---|---|
|`hooks/useCast.ts` |Cross\-platform state, Android sessions and media requests, and iOS snapshot mapping. |
|`components/cast/CastButton.tsx`<br><br>`CastActiveOverlay.tsx` |Start entry, casting overlay, and platform\-specific stop entry. |
|`components/player/VideoPlayer.tsx`<br><br>`EpisodePlayer.tsx` |Resolved URL, position, muting, pausing, and local restoration. |
|`app/drama_player.tsx` |Shared controller, UI restrictions, and navigation handling. |
|`ios/videoonern/AirPlayRelay.m`<br><br>`AirPlayRoutePickerViewManager.m` |Native state machine, Audio Session, relay player, and system picker. |
|`android/app/src/main/java/com/byteplus/videoone/rn/CastOptionsProvider.kt`<br><br>`plugins/withGoogleCast.js` |Receiver, notification, and native project configuration. |

Source regression checks cover the AirPlay state machine, relay cleanup and stale callbacks, casting overlay interactions, and page focus restoration. After integration, validate the following scenarios on physical phones and target receivers, checking video, audio, and position. State flags and passing tests do not replace receiver testing.

|Scenario |What to verify |
|---|---|
|Start casting |Correct episode and start position, visible receiver video, and no residual local audio after handoff. |
|Cancellation, failure, and network loss |State, audio, and recovery actions after picker cancellation, startup timeout, receiver load failure, and URL expiry. |
|Stop and route changes |Selecting a local iOS output versus dismissing without changing the route; late Android session resume callbacks after stopping. |
|Position and pause intent |Forward and backward receiver seeking, paused\-before\-casting behavior, and the effect of each platform’s restoration policy. |
|Page lifecycle |Overlay, episode restrictions, staying after stop, pending navigation, foreground/background transitions, and absence of audio from hidden pages. |

## Understanding the code structure

To modify the ReactNative short drama Demo efficiently, it is better to understand the project in the order of **pages → components → services → utilities** instead of jumping directly into a single API file. This helps you build a clear view of the page\-level data flow first.

### Key directories

|**Directory** |**Purpose** |**What to focus on** |
|---|---|---|
|`app/` |Pages and routing entry |Understand the relation between the short drama entry, channel page, and player page |
|`components/player/` |Player\-related components |Focus on playback controls, resume playback, episode switching, and orientation logic |
|`components/modals/` |Unlock and episode\-selection dialogs |Focus on monetization and drama consumption flow |
|`components/feed/` |Feed and recommendation display components |Focus on recommendation card and information panel adaptation |
|`components/drama/` |Drama\-specific business components |Focus on drama cover, drama list, and carousel presentation |
|`services/` |Service abstraction layer |This is the primary entry point for API replacement |
|`hooks/` |Reusable state logic |Focus on channel data fetching and theme\-related logic |
|`utils/` |Utilities and player configuration |Focus on player settings, data transformation, and image handling |

### Recommended reading order

1. Read `app/drama_channel.tsx` and `app/drama_player.tsx` first to understand the routing and interaction chain.

2. Then read `services/dramaService.ts`, `unlockService.ts`, and `userService.ts` to understand the page data sources.

3. Then read `components/player/` and `components/modals/` to understand playback, episode selection, and unlock behavior.

4. Finally review `hooks/`, `types/`, and `utils/` to complete your understanding of state management, type definitions, and utility implementations.

## Recommended implementation checklist

* Complete casting integration: both iOS AirPlay and Android Chromecast relay playback work correctly

* Verify casting breakpoint resume: the in\-app player resumes from the correct position after casting ends

* Verify mutual exclusion logic between casting and PiP to prevent simultaneous activation

* Provide reasonable error messages when no casting device is available or network errors occur

* Run the official Demo first and confirm playback, License, and native environment all work correctly.

* Define your own business API model for channel, drama, episode, unlock state, and user information.

* Complete unified data mapping in the `services/` layer.

* Validate resume playback, episode switching, orientation change, and unlock flow on real devices.

* Replace recommendation slots, operational content, and visual styles for branding.

* Add analytics, monitoring, and production configuration before release.

## Next steps

If your goal is to turn the Demo into a production\-ready business application quickly, focus on three things next. First, finalize the frontend\-backend data contract and complete service\-layer mapping. Second, define the unlock flow and user entitlement system. Third, repeatedly validate swipe switching, resume playback, unlock dialogs, and recommendation takeover on real devices. Once these parts are stable, the Demo already has a solid foundation for evolving into a real short drama product.

> **说明**

> We recommend reading this document together with the sibling document [Build your first app by ReactNative](https://docs.byteplus.com/en/docs/byteplus-vos/docs-running-the-demo-react-native): that document explains how to get the project running, while this one explains how to integrate short drama capabilities into your own business.
