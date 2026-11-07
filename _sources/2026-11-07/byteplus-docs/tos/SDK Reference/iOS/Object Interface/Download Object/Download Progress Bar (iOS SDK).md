---
title: "Download Progress Bar (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-progress-bar-ios-sdk"
---

The iOS SDK supports progress bar functionality, allowing users to pass in custom functions (blocks) to monitor download progress events and implement custom business logic.

<span id="f4a76c26"></span>
## Sample Code

The following code demonstrates how to use a progress bar during the download process.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"object-name";


get.tosDownloadProgress = ^(int64_t bytesWritten, int64_t totalBytesWritten, int64_t totalBytesExpectedToWrite) {
    NSLog(@"%lld, %lld, %lld", bytesWritten, totalBytesWritten, totalBytesExpectedToWrite);
};

TOSTask *task = [client getObject:get];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Get object success.");
        TOSGetObjectOutput *output = task.result;
        NSData *date = output.tosContent;
    } else {
        NSLog(@"Get object failed, error: %@" ,task.error);
    }
    return nil;
}];
```
