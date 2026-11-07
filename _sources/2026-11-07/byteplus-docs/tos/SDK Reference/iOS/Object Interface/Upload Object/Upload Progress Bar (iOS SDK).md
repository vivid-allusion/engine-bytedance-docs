---
title: "Upload Progress Bar (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Upload-progress-bar-ios-sdk"
---

The iOS SDK supports progress bar functionality, allowing developers to pass in custom functions (blocks) to monitor upload progress events and implement custom business logic.

<span id="be9f712e"></span>
## Sample Code

The following code demonstrates how to use a progress bar during the upload process.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSPutObjectInput *put = [TOSPutObjectInput new];
put.tosBucket = @"bucket-name";
put.tosKey = @"object-name";
put.tosContent = your_data; // NSData


put.tosUploadProgress = ^(int64_t bytesSent, int64_t totalBytesSent, int64_t totalBytesExpectedToSend) {
    NSLog(@"%lld, %lld, %lld", bytesSent, totalBytesSent, totalBytesExpectedToSend);
};

TOSTask *task = [client putObject:put];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Put object success.");
        TOSPutObjectOutput *output = task.result;
    } else {
        NSLog(@"Put object failed, error: %@" ,task.error);
    }
    return nil;
}];
```
