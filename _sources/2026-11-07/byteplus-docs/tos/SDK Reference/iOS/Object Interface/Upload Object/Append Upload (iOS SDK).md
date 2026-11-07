---
title: "Append Upload (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Append-upload-ios-sdk"
---

This interface is used for appending data to objects. Objects created via the AppendObject interface are classified as Appendable Objects, while objects uploaded using the PutObject interface are classified as Normal Objects.

<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code demonstrates how to append objects to the target bucket.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSAppendObjectInput *append = [TOSAppendObjectInput new];
append.tosBucket = @"bucket-name";
append.tosKey = @"object-name";
append.tosOffset = 0;
append.tosContent = your_data; // NSData
TOSTask *task = [client putObjectFromFile:append];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Append object success.");
        TOSPutObjectFromFileOutput *output = task.result;
    } else {
        NSLog(@"Append object failed, error: %@" ,task.error);
    }
    return nil;
}];
```
