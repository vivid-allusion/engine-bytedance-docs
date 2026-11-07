---
title: "React Native Player SDK: Best practices"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-best-practices"
---

<span id="8c107237"></span>
# Displaying sprites

<video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/12596a7c6ea34eb4a1074406c6f0a89e~tplv-goo7wpa0wc-image.image" controls></video>


<span id="prerequisites"></span>
## Prerequisites


* Complete the SDK [integration](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-quickstart) and [initialization](https://docs.byteplus.com/en/docs/byteplus-vod/docs-rn-player-features#initialize-the-sdk). The SDK version must be 1.3.0 or higher.

* Generate sprite images using the BytePlus VOD media processing service. For detailed instructions, see [Sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-sprites).

* When playing videos in Vid mode, your app server must generate temporary playback tokens `PlayAuthToken` with `needThumbs=1` being set and pass the tokens to the app client. You can use the BytePlus VOD Server SDKs to issue the temporary playback token. For details, refer to the following documents:

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

   * [Node.js SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-nodejs-sdk)

* When playing videos in DirectUrl mode, thumbnail information should be obtained in advance by calling the `GetPlayInfo` API before playback.

* On iOS devices, due to [Apple’s App Transport Security](https://developer.apple.com/documentation/bundleresources/information-property-list/nsapptransportsecurity) (ATS) requirements, sprite image URLs must use the HTTPS protocol. Therefore, when generating the `PlayAuthToken`, set the parameter `Ssl=1` and ensure your SSL certificates are properly configured.


<span id="a410bcba"></span>
## Process overview

The following diagram illustrates the overall process.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2ad66b40ab64f658db581591d07dbc8~tplv-goo7wpa0wc-image.image) </span>

<span id="b1fcd541"></span>
### Step 1: Retrieve sprite sheet configuration


* In VID mode, after the player is initialized, retrieve the sprite sheet information from `videoModel?.ThumbInfoList?.[0]` in the callback parameter of the `onFetchedVideoInfo` callback. The information structure is as follows:

   ```TypeScript
   interface ThumbInfoItem {
       /** Number of screenshots */
       CaptureNum: number;
       /** Sprite image URL list */
       StoreUrls: string[];
       /** Width of the small image */
       CellWidth: number;
       /** Height of the small image */
       CellHeight: number;
       /** Number of small images per row in the sprite image */
       ImgXLen: number;
       /** Number of small images per column in the sprite image. */
       ImgYLen: number;
       /** Screenshot time interval, in seconds */
       Interval: number;
       /** Screenshot format */
       Format: string;
   }
   ```
   

* In DirectUrl mode, the sprite sheet information needs to be obtained in advance by calling the [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) API.


Playback page code examples:

```TypeScript
// Initialize the player
const player = await initPlayer({
  viewId: 'player-view-id',
} as InitPlayerOptions);

// Set event listeners
player.setListener({
  onFetchedVideoInfo(videoModel: any) {
    const thumbInfo = videoModel?.ThumbInfoList?.[0];
    if (thumbInfo && thumbInfo.StoreUrls?.length > 0) {
      // Sprite sheet data is available, enable preview functionality
      setSpriteData(thumbInfo);
      setHasSpriteData(true);
    }
  },
  onCurrentPlaybackTimeUpdate(currentTime: number) {
    setCurrentTime(currentTime);
  },
  onLoadStateChanged(_engine: TTVideoEngine, loadState: number) {
    setLoadState(loadState);
  },
  onPlaybackStateChanged(_engine: TTVideoEngine, playbackState: number) {
    setPlaybackState(playbackState);
  },
  // Other event listeners...
});

// Create video source and start playback
const vidSource = createVidSource({
  vid: 'your-video-id',
  playAuthToken: 'your-play-auth-token',
} as VidSourceInitProps);

player.setVideoSource(vidSource);
player.play();
```


<span id="371f3723"></span>
### Step 2: User interaction flow

User interaction with the progress bar and thumbnail rendering should be handled as follows.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5904b6fdf4c4d90affddd10d1e2fbf1~tplv-goo7wpa0wc-image.image) </span>

Handle progress bar dragging, thumbnail display, and seek operations as follows:

```TypeScript
// Progress bar drag handling
const handleProgressMove = useCallback((event: any) => {
  if (!hasSpriteData() || !duration) return;
  const locationX = event.nativeEvent.locationX;
  // Calculate the corresponding time progress from the progress bar drag position
  const newTime = calculateTimeFromPosition(locationX);
  
  // Show thumbnail preview
  showThumbnailPreview(newTime);
}, [hasSpriteData, duration, calculateTimeFromPosition, showThumbnailPreview]);

// Progress bar click/release handling
const handleProgressTouch = useCallback((event: any) => {
  const locationX = event.nativeEvent.locationX;
  // Calculate the corresponding time progress from the progress bar drag position
  const newTime = calculateTimeFromPosition(locationX);
  
  // Validate the time range
  if (duration <= 0 || newTime < 0 || newTime > duration) {
    return;
  }
  
  // Seek video
  player.seek(newTime, (success: boolean) => {
    if (!success) {
      console.warn('Video seek failed');
    }
  });
  
  // Hide preview
  hideThumbnailPreview();
}, [calculateTimeFromPosition, duration, hideThumbnailPreview]);
```


<span id="43453ad1"></span>
### Step 3: Thumbnail information calculation

<span id="1dded493"></span>
#### Algorithm overview

The thumbnail calculation uses a 4\-step algorithm to convert a time point into specific coordinates within the sprite sheet:


1. **Time index calculation**: Calculate the thumbnail index based on the time interval.

2. **Sprite sheet location**: Determine which sprite sheet file contains the thumbnail.

3. **Grid position calculation**: Calculate the row and column position in the sprite sheet grid.

4. **Pixel coordinate conversion**: Convert to the actual pixel coordinates.


```TypeScript
// Thumbnail position information interface (calculation result)
interface ThumbnailInfo {
  url: string;    // Sprite sheet URL containing the thumbnail
  x: number;      // X coordinate of the thumbnail in the sprite sheet
  y: number;      // Y coordinate of the thumbnail in the sprite sheet
  width: number;  // Thumbnail width
  height: number; // Thumbnail height
}

const calculateThumbnailInfo = useCallback(
  (time: number): ThumbnailInfo | null => {
    const spriteConfig = getSpriteConfig();
    if (!spriteConfig || !spriteConfig.StoreUrls?.length) {
      return null;
    }

    // Step 1: Calculate thumbnail index
    const thumbIndex = Math.floor(time / spriteConfig.Interval);
    const clampedIndex = Math.min(thumbIndex, spriteConfig.CaptureNum - 1);

    // Step 2: Determine sprite sheet file
    const thumbsPerSprite = spriteConfig.ImgXLen * spriteConfig.ImgYLen;
    const spriteImageIndex = Math.floor(clampedIndex / thumbsPerSprite);
    const localThumbIndex = clampedIndex % thumbsPerSprite;

    // Step 3: Calculate grid position
    const row = Math.floor(localThumbIndex / spriteConfig.ImgXLen);
    const col = localThumbIndex % spriteConfig.ImgXLen;

    // Step 4: Convert to pixel coordinates
    const x = col * spriteConfig.CellWidth;
    const y = row * spriteConfig.CellHeight;

    //Error Handling for out of bounds spriteImageIndex
    if (spriteImageIndex >= spriteConfig.StoreUrls.length || spriteImageIndex < 0){
        console.error("spriteImageIndex out of bounds");
        return null;
    }

    return {
      url: spriteConfig.StoreUrls[spriteImageIndex],
      x,
      y,
      width: spriteConfig.CellWidth,
      height: spriteConfig.CellHeight,
    };
  },
  [getSpriteConfig],
);
```


<span id="89e3fc89"></span>
#### Algorithm example

Let's assume the following configuration:


* `Interval: 10` (one thumbnail every 10 seconds)

* `ImgXLen: 5, ImgYLen: 4` (a 5\-column, 4\-row grid)

* `CellWidth: 160, CellHeight: 90` (size of each thumbnail)


For a playback time of 65 seconds:


1. **Index calculation:**  `Math.floor(65 / 10) = 6`

2. **Sprite sheet location:**  `6 / (5 × 4) = 0` (0th sprite sheet), `6 % 20 = 6` (local index)

3. **Grid position:**  `row = Math.floor(6 / 5) = 1`, `col = 6 % 5 = 1`

4. **Pixel coordinates:**  `x = 1 × 160 = 160`, `y = 1 × 90 = 90`


Therefore, the thumbnail at 65 seconds would be located at coordinates (160, 90) within sprite sheet 0.

<span id="b424d5d7"></span>
### Step 4: Thumbnail preview window rendering

As shown below, the specified thumbnail is displayed by adjusting the offset of the `<Image/>` component.

```TypeScript
const renderThumbnailPreview = () => {
  if (!showPreview || !previewTime) return null;

  const thumbnailInfo = calculateThumbnailInfo(previewTime);
  if (!thumbnailInfo) return null;

  return (
    <View style={styles.previewContainer}>
      <View style={styles.previewWindow}>
        {/* Thumbnail container - used for cropping display */}
        <View style={[styles.thumbnailContainer, {
          width: thumbnailInfo.width,
          height: thumbnailInfo.height,
        }]}>
          {/* Full sprite image - displays the specified thumbnail through offset */}
          <Image
            source={{uri: thumbnailInfo.url}}
            style={{
              width: thumbnailInfo.width * spriteData.ImgXLen,
              height: thumbnailInfo.height * spriteData.ImgYLen,
              marginLeft: -thumbnailInfo.x,
              marginTop: -thumbnailInfo.y,
            }}
            resizeMode="stretch"
          />
        </View>

        {/* Time display */}
        <Text style={styles.timeText}>
          {formatTime(previewTime)}
        </Text>
      </View>
    </View>
  );
};
```


<span id="beeda563"></span>
### (Optional) Sprite sheet preloading optimization

To avoid image loading delays when the user first drags the progress bar, it is recommended to implement a sprite sheet preloading mechanism:


1. After obtaining the sprite sheet configuration, automatically extract all sprite sheet URLs.

2. Create transparent 1 × 1 pixel image components, positioned off\-screen.

3. As the sprite sheet image is already cached on the device, the thumbnail appears immediately, eliminating any loading delay.


```TypeScript
// State management
const [preloadUrls, setPreloadUrls] = useState<string[]>([]);

// Preload sprite images
const preloadSpriteImages = useCallback(() => {
  const spriteConfig = getSpriteConfig();
  if (spriteConfig?.StoreUrls?.length) {
    setPreloadUrls(spriteConfig.StoreUrls);
  }
}, [getSpriteConfig]);

// Listen for modelInfo changes to trigger preloading
useEffect(() => {
  if (modelInfo?.ThumbInfoList?.length) {
    preloadSpriteImages();
  }
}, [modelInfo, preloadSpriteImages]);

// Render hidden preload images
const renderPreloadImages = () => {
  return preloadUrls.map((url, index) => (
    <Image
      key={`preload-${index}`} // Corrected key generation
      source={{uri: url}}
      style={{
        position: 'absolute',
        width: 1,
        height: 1,
        opacity: 0,
        left: -9999,
      }}
      onLoad={() => {
        // Preload complete
      }}
      onError={() => {
        // Preload failed
      }}
    />
  ));
};

// Use in JSX
return (
  <View>
    {/* Other components */}
    {renderPreloadImages()}
  </View>
);
```


<span id="2ad4744d"></span>
## Code examples

You can use the code below for testing. Replace `VID` and `PLAY_AUTH_TOKEN` with the video's `vid` and `playAuthToken`.

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4d4bd9dd8c24647b1d8762fce146d93~tplv-goo7wpa0wc-image.image" name="ThumbPreview.tsx">ThumbPreview.tsx</Attachment>
