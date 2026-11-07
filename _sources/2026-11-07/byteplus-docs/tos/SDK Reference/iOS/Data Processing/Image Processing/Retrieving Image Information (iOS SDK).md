---
title: "Retrieving Image Information (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-image-information-ios-sdk"
---

The image information retrieval function can obtain the basic attributes of an image, including its height, width, size, and format. If the image contains Exif information, the content will be returned as a JSON string.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve image information.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"image-name";
get.tosProcess = @"image/info";
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

For a detailed introduction to obtaining image information, please refer to [Obtain Information](https://docs.byteplus.com/docs/tos/docs-information-query).
