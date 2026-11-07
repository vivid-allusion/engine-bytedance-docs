---
title: "Video Frame Extraction (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-framing-ios-sdk"
---

The video frame extraction function enables the capture of a single frame from a video stream at a specified time and resizes it into an image of the designated dimensions.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 1000 milliseconds and download the resulting image to the local device.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectToFileInput *get = [TOSGetObjectToFileInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"video-name";
get.tosFilePath = @"your_local_file_path";
get.tosProcess = @"video/snapshot,t_1000";
TOSTask *task = [client getObjectToFile:get];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!t.error) {
        NSLog(@"Get object to file success.");
    } else {
        NSLog(@"Get object to file failed, error: %@" ,t.error);
    }
    return nil;
}];
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to video frame extraction, please refer to [Video Frame Extraction](https://docs.byteplus.com/docs/tos/docs-video-frame-capture).
