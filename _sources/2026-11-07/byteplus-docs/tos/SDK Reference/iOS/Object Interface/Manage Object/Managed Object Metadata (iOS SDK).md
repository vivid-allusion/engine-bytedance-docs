---
title: "Managed Object Metadata (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Manage-object-meta-information-ios-sdk"
---

Object metadata refers to the attribute descriptions of an object, comprising both HTTP standard attributes (HTTP Header) and user\-defined metadata (User Meta). This article presents example code for setting object metadata.

<span id=".6K6-572u6Ieq5a6a5LmJ5YWD5L-h5oGv"></span>
## **Configure Custom Metadata**

When uploading an object, add custom metadata to specify the object's purpose, attributes, etc.

The following code demonstrates how to set custom metadata for an object.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSSetObjectMetaInput *set = [TOSSetObjectMetaInput new];
set.tosBucket = @"bucket-name";
set.tosKey = @"object-name";
set.tosMeta = @{@"user-key-1":@"use-val-1", @"user-key-2":@"use-val-2"};
TOSTask *task = [_client setObjectMeta:set];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull task) {
    if (!task.error) {
        NSLog(@"Set object meta success.");
        TOSSetObjectMetaOutput *output = task.result;
    } else {
        NSLog(@"Set object meta failed, error: %@", task.error);
    }
    return nil;
}];
```
