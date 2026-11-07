---
title: "iOS Player SDK: Displaying sprites"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-displaying-sprites-ios"
---

The Player SDK allows users to quickly preview the video content at a specified point of time in thumbnail view by dragging the progress bar or jumping to a new position. Thumbnail previews are based on video sprites, which are big images consisting of multiple screenshots. These have the following advantages:


* Smaller image size: Combining multiple smaller images into a big one can reduce the size of the image.

* Fewer request times: By integrating images, user requests to the server are reduced, thereby improving the page opening speed.


Below is an example of a sprite image that consists of 25 thumbnail images.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4a684923212f48c78f32792b3ed3f3ed~tplv-goo7wpa0wc-image.image) </span>

This article explains how to display sprites using the Player SDK.

<span id="b0cdf3e0"></span>
## Prerequsites


* Generate sprite images using the BytePlus VOD media processing service. For detailed instructions, see [Sprites](https://docs.byteplus.com/docs/byteplus-vod/docs-sprites).

* The Player SDK currently only supports thumbnail previews of videos played in **Vid mode**. Your app server needs to generate temporary playback tokens with `needThumbs=1` being set and pass the token to the app client. You can use the BytePlus VOD Server SDKs to issue the temporary playback token. For details, refer to the following documents:

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)


<span id="33ae639f"></span>
## Obtain sprite info

Use the `videoEngine:fetchedVideoModel:` callback to obtain the sprite info `TTVideoEngineThumbInfo`. Below is a code sample:

```objectivec
- (void)videoEngine:(TTVideoEngine *)videoEngine fetchedVideoModel:(TTVideoEngineModel *)videoModel {
    // Retrieve the sprite information. Currently, the sprite information is returned as an array, and we can simply take the first value from the array.
    TTVideoEngineThumbInfo *firstThumbInfo = videoModel.videoInfo.bigThumbs.firstObject；
    self.thumbInfo = firstThumbInfo;
}
```


Below is an example of `TTVideoEngineThumbInfo`. For detailed parameters, see [VodThumbInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo#fb299ec7).

```JSON
// In this example, the video duration is 270 seconds. The interval is set to 10, which means a thumbnail image is captured every 10 seconds. A total of 27 images are captured, indicated by CaptureNum.
// Each sprite image contains 25 thumbnail images (5*5), so 2 sprite images are generated.
// The URLs of the two sprite images can be obtained from the StoreUrls parameter.
[{
        "CaptureNum": 27,
        "StoreUrls": ["http://vod-demo-cover.volccdn.com/tos-cn-v-c9****/622ceb0b7f5b41afadf0f******2971_1639039860~tplv-vod-noop.image", "http://vod-demo-cover.volccdn.com/tos-cn-v-c9****/26d92b1fdbc74599a713******c3824_1639039860~tplv-vod-noop.image"],
        "CellWidth": 242,
        "CellHeight": 136,
        "ImgXLen": 5,
        "ImgYLen": 5,
        "Interval": 10,
        "Format": "jpg"
}]
```


Refer to the code sample below to obtain sprite parameter values:


* For version 1.41.2 or later, directly use the `TTVideoEngineModel property` to obtain the parameter values:

   ```objectivec
   @interface TTVideoEngineThumbInfo : NSObject<NSSecureCoding>
   
   // Total number of thumbnail images.
   @property (nonatomic, assign) NSInteger imageNum; 
      
   // Width of each thumbnail image in pixels.
   @property (nonatomic, assign) NSInteger imageXSize;
      
   // Height of each thumbnail image in pixels.
   @property (nonatomic, assign) NSInteger imageYSize;
      
   // Number of thumbnail images per row in the sprite image.
   @property (nonatomic, assign) NSInteger imageXLen;
      
   // Number of thumbnail images per column in the sprite image.
   @property (nonatomic, assign) NSInteger imageYLen;
      
   // Time interval between adjacent thumbnail images in seconds.
   @property (nonatomic, assign) CGFloat interval;
      
   // Format of the sprite image.
   @property (nonatomic, nullable, copy) NSString *fext;
      
   // URL list of the sprite image.
   @property (nonatomic, nullable, copy) NSArray<NSString *> *imageURLs;
   
   /**
    * Get an integer value from the specified key.
    *
    * @param key The key associated with the value.
    * @return The integer value.
    */
   - (NSInteger)getValueInt:(NSInteger)key;
     
   /**
    * Get a float value from the specified key.
    *
    * @param key The key associated with the value.
    * @return The float value.
    */
   - (CGFloat)getValueFloat:(NSInteger)key;
   
   /**
    * Get a string value from the specified key.
    *
    * @param key The key associated with the value.
    * @return The string value.
    */
   - (nullable NSString *)getValueStr:(NSInteger)key;
    
   /**
    * Get an array of string values from the specified key.
    *
    * @param key The key associated with the value.
    * @return The array of string values.
    */
   - (nullable NSMutableArray<NSString *> *)getValueArray:(NSInteger)key;
   @end
   ```
   

* For versions below 1.41.2, you need to use the `key - value` method to obtain the parameter values:

   ```objectivec
   - (void)_parseThumbInfo:(TTVideoEngineThumbInfo *)thumbInfo {
      
       // Total number of thumbnail images.
       NSInteger imageNum = [thumbInfo getValueInt:VALUE_THUMB_IMG_NUM];
      
       // Number of thumbnail images per row in the sprite image.
       NSInteger imageXLen = [thumbInfo getValueInt:VALUE_THUMB_IMG_X_LEN];
      
       // Number of thumbnail images per column in the sprite image.
       NSInteger imageYLen = [thumbInfo getValueInt:VALUE_THUMB_IMG_Y_LEN];
      
       // Width of each thumbnail image in pixels.
       NSInteger imageXSize = [thumbInfo getValueInt:VALUE_THUMB_IMG_X_SIZE];
      
       // Height of each thumbnail image in pixels.
       NSInteger imageYSize = [thumbInfo getValueInt:VALUE_THUMB_IMG_Y_SIZE];
      
       // Time interval between adjacent thumbnail images in seconds.
       CGFloat interval = [thumbInfo getValueFloat:VALUE_THUMB_INTERVAL];
      
       // Format of the sprite image.
       NSString *format = [thumbInfo getValueArray:VALUE_THUMB_FEXT];
      
       // URL list of the sprite image.
       NSArray *imageURLs = [thumbInfo getValueArray:VALUE_THUMB_IMG_URLS];
   }
   ```
   


<span id="692a7b0e"></span>
## Display thumbnail previews

Refer to the code sample below to obtain and display the thumbnail preview at a specified progress:

```objectivec
/**
 * Get the current sprite image to display based on the playback progress.
 *
 * @param progress The playback progress, ranging from 0 to 1.
 * @return The image for the current sprite.
 */
- (UIImage * _Nullable)_updateImageWithProgress:(CGFloat)progress {
    NSInteger imageNum = self.thumbInfo.imageNum;
    NSInteger imageXLen = self.thumbInfo.imageXLen;
    NSInteger imageYLen = self.thumbInfo.imageYLen;
    if (imageNum <= 0 || imageXLen <= 0 || imageYLen <= 0) {
        return nil;
    }
    
    NSInteger imageXSize = self.thumbInfo.imageXSize;
    NSInteger imageYSize = self.thumbInfo.imageYSize;
    NSArray *imageURLs = self.thumbInfo.imageURLs;
    
    // The following code example shows how to find the current sprite index. You can design a more optimized implementation as needed.
    NSInteger index = MAX(0, ceil((imageNum - 1) * progress));
    NSInteger urlIndex = index / (imageXLen * imageYLen);
    
    // The logic for loading the sprite image.
    // 1. Get the URL for the current sprite image.
    NSString *urlString = nil;
    if (urlIndex < imageURLs.count) {
        urlString = imageURLs[urlIndex];
    }
    if (!urlString.length) {
        return nil;
    }
    
    // 2. Download the sprite image. The following code is for demonstration purposes only. Business should design different multithreading approaches to improve efficiency.
    // For example, start loading the sprite image and caching it locally before playback starts, and seek to reduce the time for loading the sprite image.
    ThumbnailHelper *thumbnailHelper = [ThumbnailHelper shared];
    UIImage *thumbBigImage = [thumbnailHelper getImageWithUrl:urlString];
    
    // 3. Extract the current thumbnail image from the sprite image. The following code is for demonstration purposes only. Business can design a more optimized implementation as needed.
    if (thumbBigImage) {
        CGFloat x = (index % imageXLen) * imageXSize;
        CGFloat y = (index / imageXLen % imageYLen) * imageYSize;
        CGRect rect = CGRectMake(x, y, imageXSize, imageYSize);
        UIImage *thumbImage = [self getThumbImgFromBigImage:thumbBigImage rect:rect];
        return thumbImage;
    }
    
    return nil;
}

/**
 * Crop a thumbnail image from the sprite image.
 *
 * @param bigImage The sprite image.
 * @param rect The cropping rect.
 * @return The cropped thumbnail image.
 */
- (UIImage *)getThumbImgFromBigImage:(UIImage *)bigImage rect:(CGRect)rect {
    CGImageRef subImageRef = CGImageCreateWithImageInRect(bigImage.CGImage, rect);
    CGRect smallBounds = CGRectMake(0, 0, CGImageGetWidth(subImageRef), CGImageGetHeight(subImageRef));
    
    UIGraphicsBeginImageContext(smallBounds.size);
    CGContextRef context = UIGraphicsGetCurrentContext();
    CGContextDrawImage(context, smallBounds, subImageRef);
    UIImage *img = [UIImage imageWithCGImage:subImageRef];
    CGImageRelease(subImageRef);
    UIGraphicsEndImageContext();
    return img;
}
```
