---
title: "Temporary Access Authorization (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Temporary-access-authorization-ios-sdk"
---

By default, TosClient includes a signature in the request header when initiating a request to the server. The SDK also supports constructing signed URLs. These URLs can be used directly to initiate HTTP requests or shared with third parties to enable access authorization.

<span id=".56S65L6L5Luj56CB"></span>
## Sample Code

The following code demonstrates how to generate a signed URL.

```objectivec
TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSPreSignedURLInput *input = [TOSPreSignedURLInput new];
input.tosBucket = @"bucket-name";
input.tosKey = @"object-name";
input.tosHttpMethod = TOSHTTPMethodTypeGet;
TOSTask *task = [client preSignedURL:input];
[task continueWithBlock:^id _Nullable(TOSTask * _Nonnull task) {
    if (!task.error) {
        NSLog(@"Presigned success.");
        TOSPreSignedURLOutput *output = task.result;
        NSString *url = output.tosSignedUrl;
    } else {
        NSLog(@"Presigned failed, error: %@.", task.error);
    }
    return nil;
}];
```
