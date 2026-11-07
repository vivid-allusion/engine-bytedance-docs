---
title: "Creating a Bucket (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Create-bucket-ios-sdk"
---

桶 (Bucket) is the globally unique namespace in TOS, serving as a data container for storing object data. The name of a newly created bucket must be unique within TOS.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to create a new bucket.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSCreateBucketInput *create = [TOSCreateBucketInput new];
create.tosBucket = @"bucket-name";
create.tosACL = TOSACLPublicRead;
TOSTask *task = [client createBucket:create];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull task) {
    if (!task.error) {
        NSLog(@"Create bucket success.");
        TOSCreateBucketOutput *output = task.result;
    } else {
        NSLog(@"Create bucket failed, error: %@.", task.error);
    }
    return nil;
}];
```
