---
title: "Deleting Objects (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Delete-object-ios-sdk"
---

This article presents example code for deleting objects.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to delete an object.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSDeleteObjectInput *input = [TOSDeleteObjectInput new];
input.tosBucket = @"bucket-name";
input.tosKey = @"object-name";
TOSTask *task = [_client deleteObject:input];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Delete object success.");
    } else {
        NSLog(@"Delete object failed, error: %@" ,task.error);
    }
    return nil;
}];
```
