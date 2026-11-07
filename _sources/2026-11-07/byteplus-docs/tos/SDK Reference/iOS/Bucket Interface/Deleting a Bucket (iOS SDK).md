---
title: "Deleting a Bucket (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-bucket-ios-sdk"
---

This article presents sample code for deleting a bucket.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* All objects in the storage bucket have been deleted.

* All shards pending merge have been deleted.

* If multiple versions of an object exist, ensure that all versions of the object have been deleted.


<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to delete empty buckets.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSDeleteBucketInput *delete = [TOSDeleteBucketInput new];
delete.tosBucket = @"bucket-name";
task = [client deleteBucket:delete];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Delete bucket success.");
        TOSDeleteBucketOutput *output = task.result;
    } else {
        NSLog(@"Delete bucket failed, error: %@" ,task.error);
    }
    return nil;
}];
```
