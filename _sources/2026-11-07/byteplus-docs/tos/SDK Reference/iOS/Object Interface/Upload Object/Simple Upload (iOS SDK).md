---
title: "Simple Upload (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Simple-upload-ios-sdk"
---

Through this interface, you can upload objects to a specified bucket. The uploaded content includes both data and local files.

<span id=".5LiK5Lyg5pWw5o2u"></span>
## **Data Upload**

The following code demonstrates how to upload data to the target bucket.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSPutObjectInput *put = [TOSPutObjectInput new];
put.tosBucket = @"bucket-name";
put.tosKey = @"object-name";
put.tosMeta = @{@"usermeta-key-1" : @"usermeta-value-1", @"usermeta-key-2" : @"usermeta-value-2"};
put.tosContent = your_data; // NSData
TOSTask *task = [client putObject:put];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Put object success.");
        TOSPutObjectOutput *output = task.result;
    } else {
        NSLog(@"Put object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".5LiK5Lyg5pys5Zyw5paH5Lu2"></span>
## **Upload Local File**

The following code demonstrates how to upload a local file to the target bucket.

```objectivec
TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSPutObjectFromFileInput *put = [TOSPutObjectFromFileInput new];
put.tosBucket = @"bucket-name";
put.tosKey = @"object-name";
put.tosMeta = @{@"usermeta-key-1" : @"usermeta-value-1", @"usermeta-key-2" : @"usermeta-value-2"};
put.tosFilePath = @"your-file-path";
TOSTask *task = [client putObjectFromFile:put];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Put object from file success.");
        TOSPutObjectFromFileOutput *output = task.result;
    } else {
        NSLog(@"Put object from file failed, error: %@" ,task.error);
    }
    return nil;
}];
```
