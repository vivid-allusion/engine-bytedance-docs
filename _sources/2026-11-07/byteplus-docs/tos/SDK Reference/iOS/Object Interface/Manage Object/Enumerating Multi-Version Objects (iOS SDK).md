---
title: "Enumerating Multi-Version Objects (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-multiversion-objects-ios-sdk"
---

This article presents sample code for listing multi\-version objects within a bucket, with each request returning up to 1,000 objects.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to enumerate multi\-version objects.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSListObjectVersionsInput *listVersions = [[TOSListObjectVersionsInput alloc] init];
listVersions.tosBucket = @"bucket-name";
TOSTask *task = [client listObjectVersions:listVersions];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"List object versions success.");
        TOSListObjectVersionsOutput *output = task.result;
    } else {
        NSLog(@"List object versions failed, error: %@" ,task.error);
    }
    return nil;
}];
```
