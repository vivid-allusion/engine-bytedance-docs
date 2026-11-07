---
title: "Multipart Upload (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Shard-upload-ios-sdk"
---

For larger objects, the object can be divided into multiple data blocks (parts) and uploaded separately. Finally, the CompleteMultipartUpload operation is invoked to merge the uploaded data blocks into a single object.

<span id=".5YiG54mH5LiK5Lyg5q2l6aqk"></span>
## Multipart Upload Procedure

You can perform multipart upload of objects by following these steps:


1. CreateMultipartUpload initializes a multipart upload task.

2. Multipart upload is performed using UploadPart.

3. All parts are merged into a single object using CompleteMultipartUpload.


<span id=".56S65L6L5Luj56CB"></span>
## **Sample Code**

The following code demonstrates how to upload an object in parts using the multipart interface.

```objectivec

TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

// 1. CreateMultipartUpload
TOSCreateMultipartUploadInput *create = [TOSCreateMultipartUploadInput new];
create.tosBucket = @"bucket-name";
create.tosKey = @"object-name";

TOSTask *task = [client createMultipartUpload:create];
[task waitUntilFinished];
TOSCreateMultipartUploadOutput *createOutput = task.result;

// 2. UploadPart
NSMutableArray *uploadedParts = [NSMutableArray array];
for (int i = 1; i <= your_chunck_count; i++) {
    TOSUploadPartInput *upload = [TOSUploadPartInput new];
    upload.tosKey = createOutput.tosKey;
    upload.tosBucket = createOutput.tosBucket;
    upload.tosUploadID = createOutput.tosUploadID;
    upload.tosPartNumber = i;
    upload.tosContent = your_chunck_data;
    task = [client uploadPart:upload];
    [task waitUntilFinished];
    TOSUploadPartOutput *uploadOutput = task.result;
    
    TOSUploadedPart *uploadedPart = [TOSUploadedPart new];
    uploadedPart.tosETag = uploadOutput.tosETag;
    uploadedPart.tosPartNumber = uploadOutput.tosPartNumber;
    
    [uploadedParts addObject:uploadedPart];
}

// 3. CompleteMultipartUpload
TOSCompleteMultipartUploadInput *complete = [TOSCompleteMultipartUploadInput new];
complete.tosBucket = createOutput.tosBucket;
complete.tosKey = createOutput.tosKey;
complete.tosUploadID = createOutput.tosUploadID;
complete.tosParts = uploadedParts;
task = [client completeMultipartUpload:complete];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        TOSCompleteMultipartUploadOutput *completeOutput = task.result;
    } else {
    }
    return nil;
}];
```
