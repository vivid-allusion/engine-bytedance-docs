---
title: "Retrieving Bucket Metadata (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-bucket-metadata-ios-sdk"
---

A storage bucket serves as a container for storage objects; this operation can verify the existence of a bucket and retrieve the bucket's metadata.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve the metadata of a bucket.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSHeadBucketInput *head = [TOSHeadBucketInput new];
head.tosBucket = @"bucket-name";
TOSTask *task = [client headBucket:head];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Head bucket success.");
        TOSHeadBucketOutput *output = task.result;
    } else {
        NSLog(@"Head bucket failed, error: %@" ,task.error);
    }
    return nil;
}];
```
