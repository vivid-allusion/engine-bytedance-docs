---
title: "Enumerating Buckets (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-buckets-ios-sdk"
---

A bucket is a container for storing objects. This operation returns a list of all buckets.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to list all buckets.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSListBucketsInput *listBuckets = [TOSListBucketsInput new];
TOSTask *task = [client listBuckets:listBuckets];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"List buckets success.");
        TOSListBucketsOutput *output = task.result;
    } else {
        NSLog(@"List buckets failed, error: %@" ,task.error);
    }
    return nil;
}];
```
