---
title: "Android Player SDK: Displaying sprites"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-displaying-sprites-android"
---

The Player SDK allows users to quickly preview the video content at a specified point of time in thumbnail view by dragging the progress bar or jumping to a new position. Thumbnail previews are based on video sprites, which are big images consisting of multiple screenshots. These have the following advantages:


* Smaller image size: Combining multiple smaller images into a big one can reduce the size of the image.

* Fewer request times: By integrating images, user requests to the server are reduced, thereby improving the page opening speed.


Below is an example of a sprite image that consists of 25 thumbnail images.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a684923212f48c78f32792b3ed3f3ed~tplv-goo7wpa0wc-image.image) </span>

This article explains how to display sprites using the Player SDK.

<span id="a34961eb"></span>
## Prerequsites


* Generate sprite images using the BytePlus VOD media processing service. For detailed instructions, see [Sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-sprites).

* The Player SDK currently only supports thumbnail previews of videos played in **Vid mode**. Your app server needs to generate temporary playback tokens with `needThumbs=1` being set and pass the token to the app client. You can use the BytePlus VOD Server SDKs to issue the temporary playback token. For details, refer to the following documents:

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)


<span id="2072035c"></span>
## Obtain sprite info

Use the `onFetchedVideoInfo` callback to obtain the sprite info `VideoThumbInfo`. Below is a code sample:

```Java
public boolean onFetchedVideoInfo(VideoModel model) {
    final List<VideoThumbInfo> thumbInfoList = videoModel.getThumbInfoList();
    if (thumbInfoList != null && thumbInfoList.size() > 0) {
        // Use the VideoThumbInfo at index 0.
        VideoThumbInfo info = thumbInfoList.get(0);
    }
}
```


Below is an example of `VideoThumbInfo`. For detailed parameters, see [VodThumbInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo#fb299ec7).

```JSON
// In this example, the video duration is 270 seconds. The interval is set to 10, which means a thumbnail image is captured every 10 seconds. A total of 27 images are captured, indicated by CaptureNum.
// Each sprite image contains 25 thumbnail images (5*5), so 2 sprite images are generated.
// The URLs of the two sprite images can be obtained from the StoreUrls parameter.
[{
        "CaptureNum": 27,
        "StoreUrls": ["http://vod-demo-cover.volccdn.com/tos-cn-v-c9**a9/622ceb0b7f5b41afadf0fd9e******1_1639039860~tplv-vod-noop.image", 
                      "http://vod-demo-cover.volccdn.com/tos-cn-v-c9**a9/26d92b1fdbc74599a713b1c3*******4_1639039860~tplv-vod-noop.image"],
        "CellWidth": 242,
        "CellHeight": 136,
        "ImgXLen": 5,
        "ImgYLen": 5,
        "Interval": 10,
        "Format": "jpg"
}]
```


Refer to the code sample below to obtain sprite parameter values:

```Java
// Total number of thumbnail images.
int imgNum = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CAPTURE_NUM);
// Number of thumbnail images per row in the sprite image.
int xLength = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_X_LEN);
// Number of thumbnail images per column in the sprite image.
int yLength = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_Y_LEN);
// Width of each thumbnail image, in pixels.
int xSize = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CELL_WIDTH);
// Height of each thumbnail image, in pixels.
int ySize = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CELL_HEIGHT);
// Format of the sprite image.
int format = info.getValueStr(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_FORMAT);
// List of URLs for the sprite image.
List<String> urls = info.getUrls();
// Time interval between adjacent thumbnail images, measured in seconds.
double interval = info.getValueDouble(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_INTERVAL);
```


<span id="abc9528a"></span>
## Display thumbnail previews

Refer to the code sample below to obtain and display the thumbnail preview at a specified progress:

```Java
// 1. Calculate the index of the thumbnail image in the sprite image based on the play position and sprite image interval.
final int currentThumbIndex = getCurrentThumbIndex(mVideoThumbInfo, position);
// 2. Determine which sprite image contains the thumbnail image based on the index of the thumbnail image and the number of thumbnail images per sprite image.
final int currentSpriteIndex = getSpriteIndex(mVideoThumbInfo, currentThumbIndex);
// 3. Download the required sprite image and cache it to disk.
downloadThumbs(mVideoThumbInfo, currentSpriteIndex);
// 4. Retrieve the thumbnail image corresponding to the play position.
Bitmap bitmap = getThumbBitmap(context, mVideoThumbInfo, currentThumbIndex);
// 5. Display the bitmap in the appropriate view.
final RoundedBitmapDrawable drawable = RoundedBitmapDrawableFactory.create(mContext.getResources(), bitmap);
drawable.setAntiAlias(true);
mImageView.setImageDrawable(drawable);

private static void downloadThumbs(VideoThumbInfo thumbInfo, int splitIndex) {
    String url = thumbInfo.getUrls().get(splitIndex);
    // The disk cache path should be customized. The following is just a simple example.
    String path = context.getCacheDir().getAbsolutePath() + "/thumb/" + md5(url) + ".jpg";
    File imageFile = new File(path);
    if (!imageFile.exists()) {
        // Download the sprite image and save it locally.
    } else {
        // Already exists, no need to download again.
    }
}

private int getCurrentThumbIndex(final VideoThumbInfo currentThumbInfo, final long position) {
    double interval = currentThumbInfo.getValueDouble(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_INTERVAL);
    return (int) (position / 1000 / interval);
}

private int getSpriteIndex(final VideoThumbInfo currentThumbInfo, final long thumbIndex) {
    final int xLength = currentThumbInfo.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_X_LEN);
    final int yLength = currentThumbInfo.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_Y_LEN);
    return (int) (thumbIndex / (xLength * yLength));
}

public Bitmap getThumbBitmap(Context context, VideoThumbInfo info, int index) {
    if (context == null || info == null) {
        return null;
    }

    Rect rect = new Rect();
    int xLength = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_X_LEN);
    int yLength = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_IMG_Y_LEN);
    int xSize = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CELL_WIDTH);
    int ySize = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CELL_HEIGHT);
    int imgNum = info.getValueInt(VideoThumbInfo.VALUE_VIDEO_THUMB_INFO_CAPTURE_NUM);

    if (index >= imgNum) {
        index = imgNum - 1;
    }
    int spriteIndex = index / (xLength * yLength);
    // Index of the thumbnail image in the sprite image
    index = index % (xLength * yLength);

    rect.left = (index % xLength) * xSize;
    rect.top = (index / xLength) * ySize;
    rect.right = rect.left + xSize;
    rect.bottom = rect.top + ySize;
    try {
        // The disk path should be customized. The following is just a simple example.
        String url = info.getUrls().get(spriteIndex);
        String path = context.getCacheDir().getAbsolutePath() + "/thumb/" + md5(url) + ".jpg";
        BitmapRegionDecoder decoder = BitmapRegionDecoder.newInstance(path, false);
        Bitmap decodeBitmap = decoder.decodeRegion(rect, null);
        decoder.recycle();
        return decodeBitmap;
    } catch (Exception e) {
        Log.d(TAG, "getThumbBitmap Exception " + e);
    }
    return null;
}
```
