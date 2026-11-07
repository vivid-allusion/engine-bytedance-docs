---
title: "Enumerating Objects (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/List-objects-ios-sdk"
---

This article presents sample code for listing objects, with a default maximum of 1,000 objects returned.

<span id=".5YiX5Li-5a-56LGh"></span>
## Enumerated Objects

The following code demonstrates how to list objects.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSListObjectsInput *list = [TOSListObjectsInput new];
list.tosBucket = @"tos-test";
TOSTask *task = [_client listObjects:list];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"List objects success.");
        TOSListObjectsOutput *output = task.result;
    } else {
        NSLog(@"List objects failed, error: %@" ,task.error);
    }
    return nil;
}];
```
