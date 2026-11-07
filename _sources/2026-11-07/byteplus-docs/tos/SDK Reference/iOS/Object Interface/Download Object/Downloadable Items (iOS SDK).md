---
title: "Downloadable Items (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Download-object10"
---

This interface enables downloading objects from a specified bucket. Before using this interface, please ensure that you have read access to this object.

<span id=".5LiL6L295a-56LGh5bm26K-75Y-W5pWw5o2u"></span>
## **Download Object and Read Data**

The following code demonstrates how to download an object and read its data.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"object-name";
TOSTask *task = [client getObject:get];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Get object success.");
        TOSGetObjectOutput *output = task.result;
        NSData *date = output.tosContent;
    } else {
        NSLog(@"Get object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".5LiL6L295a-56LGh5oyH5a6a6IyD5Zu055qE5pWw5o2u"></span>
## **Download data within a specified range of the object**

If you only need to read a specific range of data from an object, you can set the `Range` to read data within the specified range of the object. The following code demonstrates how to download data within the `Range` specified for the object.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];


TOSGetObjectInput *get = [TOSGetObjectInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"object-name";
get.tosRangeStart s= @1;
get.tosRangeEnd = @100;
TOSTask *task = [client getObject:get];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Get object success.");
        TOSGetObjectOutput *output = task.result;
        NSData *date = output.tosContent;
    } else {
        NSLog(@"Get object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".5LiL6L295a-56LGh5Yiw5paH5Lu2"></span>
## **Download Object to File**

The following code demonstrates how to download an object and save it to a local file.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSGetObjectToFileInput *get = [TOSGetObjectToFileInput new];
get.tosBucket = @"bucket-name";
get.tosKey = @"object-name";
get.tosFilePath = your_local_filepath;
TOSTask *task = [client getObjectToFile:get];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Get object to file success.");
        TOSGetObjectToFileOutput *output = task.result;
    } else {
        NSLog(@"Get object to file failed, error: %@" ,task.error);
    }
    return nil;
}];
```
