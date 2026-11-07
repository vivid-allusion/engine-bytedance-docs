---
title: "Persistent Storage of Video Frame Images (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Video-capture-image-persistence-ios-sdk"
---

TOS supports saving images extracted from video frames to a specified storage bucket.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to extract the video frame at 1000 ms and save the resulting image to the specified storage bucket.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"video-name";
get.tosProcess = @"video/snapshot,t_1000";
get.tosProcessSaveAsBucket = @"target-bucket-name";
get.tosProcessSaveAsObject = @"target-image-name";
TOSTask *task = [client getObject:get];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!task.error) {
        NSLog(@"Get object success.");

        TOSGetObjectOutput *out = t.result;
        NSLog(@"%@", [[NSString alloc] initWithData:out.tosContent encoding:NSUTF8StringEncoding]);
    } else {
        NSLog(@"Get object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to the persistence of images extracted from video frames, please refer to [Image Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
