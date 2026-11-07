---
title: "Image Processing Persistence (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/image-processing-persistence-ios-sdk"
---

TOS does not save processed images by default. You can use code to save the processed images to the designated storage bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* An account used for persistent image processing must have read permission for the bucket containing the original image and write permission for the target bucket where the image will be transferred.

* When saving processed images to a designated storage bucket as an anonymous user, the bucket must be configured with public write permissions.

* The bucket containing the original image and the target bucket for image transfer must be located in the same region.

* The default access permission for transferred images is set to private, and the default storage type is standard storage.


<span id=".56S65L6L5Luj56CB"></span>
### Sample Code

The following code demonstrates how to scale an image to a height of 100px and then save the processed image to the target storage bucket with the specified object name.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"image-name";
get.tosProcess = @"image/resize,h_100";
get.tosProcessSaveAsBucket = @"target-bucket-name";
get.tosProcessSaveAsObject = @"target-image-name";
TOSTask *task = [client getObject:get];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!task.error) {
        NSLog(@"Get object to file success.");
     
        TOSGetObjectOutput *out = t.result;
        NSLog(@"%@", [[NSString alloc] initWithData:out.tosContent encoding:NSUTF8StringEncoding]);
    } else {
        NSLog(@"Get object to file failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to image processing persistence, see [Image Processing Persistence](https://docs.byteplus.com/docs/tos/docs-image-storage).
