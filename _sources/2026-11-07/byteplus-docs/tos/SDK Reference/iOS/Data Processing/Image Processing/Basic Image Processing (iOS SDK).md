---
title: "Basic Image Processing (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Basic-image-processing-ios-sdk"
---

TOS supports processing of stored images, including image resizing, image cropping, image watermarking, format conversion, and other image processing operations.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Only JPG, PNG, BMP, GIF, WEBP, and TIFF formats are supported for original images.

* The size of the original image must not exceed 20MB.

* The original image width and height must not exceed 30,000 px, and the total number of pixels must not exceed 250 million px. For rotation operations, the original image width and height must not exceed 4,096 px.

* The width and height of the scaled image must not exceed 16,384 px, and the total number of pixels must not exceed 16,777,216 px.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to resize an image to a height of 100 pixels and then save the processed image locally.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectToFileInput *get = [TOSGetObjectToFileInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"image-name";
get.tosFilePath = @"your_local_file_path";
get.tosProcess = @"image/resize,h_100";
TOSTask *task = [client getObjectToFile:get];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!task.error) {
        NSLog(@"Get object to file success.");
    } else {
        NSLog(@"Get object to file failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to image processing, please refer to the [Image Processing Overview](https://docs.byteplus.com/docs/tos/docs-overview_2).
