---
title: "Retrieving Video Information (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Get-vdeo-information-ios-sdk"
---

The video information retrieval function enables the acquisition of metadata for a specified video resource.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to retrieve video information.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"video-name";
get.tosProcess = @"video/info";
TOSTask *task = [client getObject:get];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull t) {
    if (!task.error) {
        NSLog(@"Get object success.");
   
        TOSGetObjectOutput *out = t.result;
        NSLog(@"%@", [[NSString alloc] initWithData:out.tosContent encoding:NSUTF8StringEncoding]);
    } else {
        NSLog(@"Get object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".55u45YWz5paH5qGj"></span>
## Relevant Documentation

For a detailed introduction to obtaining video information, please see [View Video Information](https://docs.byteplus.com/docs/tos/docs-viewing-video-information).
