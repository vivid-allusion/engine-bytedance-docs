---
title: "Copy Object (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Copy-object-ios-sdk"
---

This article provides sample code for copying objects. Copying does not support cross\-region copying and requires read permission on the source object.

<span id="4d061f70"></span>
## Prerequisites


* Have [installed and initialized TOS iOS SDK](https://docs.byteplus.com/en/docs/tos/Quick-start-ios-sdk) v2.1.8 or later.

* Available Endpoint, Region, and Bucket are prepared.

* Ensure the upload source file path, download target directory, and checkpoint directory are accessible.

* The sample code uses `Objective-C` and can be placed in the project's `.m` file.


<span id="77073df9"></span>
## Notes


|Notes |Description |
|---|---|
|Version and interface compatibility |The current breakpoint resume interface does not support SSE parameters. |
|Task management |* The same `checkpoint` path cannot be used for multiple transfer tasks simultaneously; wait for the original task to finish before resuming.<br><br>* When resuming a task, Bucket, Object, file path, part size, version ID, and condition parameters must match the original task.<br><br>* A new request object and `TOSCancelHook` are required each time a transfer task is resumed.<br><br>* `Checkpoint `does not contain access credentials and does not guarantee compatibility with SDKs in other languages. |
|Operating environment |* Breakpoint resume follows the frontend transmission boundary: after the app enters the background or the process is terminated by the system, execution is not guaranteed to continue; the next start can restore via checkpoint.<br><br>* Transmission progress and event callbacks may execute on a background thread; switch to the main thread to update the UI. |
|Resume status management |SDK automatically deletes the checkpoint after the copy completes successfully.<br><br><br>* `cancel:NO` retains the resume state.<br><br>* `cancel:YES` clears the resume state. |


<span id=".5pmu6YCa5ou36LSd"></span>
## Standard copy

The following code shows how to copy an object within the same bucket.

```Objective-C
// Temporary access key and security token (AccessKey, SecretKey, SecurityToken) obtained from the STS service
TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey" securityToken:@"securityToken"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

TOSCopyObjectInput *input = [[TOSCopyObjectInput alloc] init];
input.tosBucket = @"bucket-name";
input.tosSrcBucket = @"src-bucket-name";
input.tosKey = @"object-name";
input.tosSrcKey = @"src-object-name";
input.tosMeta = @{@"new-meta-key" : @"new-meta-value"};
input.tosMetadataDirective = TOSMetadataDirectiveReplace;

TOSTask *task = [client copyObject:input];
[task continueWithBlock:^id(TOSTask *task) {
    if (!task.error) {
        NSLog(@"Copy object success.");
    } else {
        NSLog(@"Copy object failed, error: %@" ,task.error);
    }
    return nil;
}];
```


<span id=".5YiG54mH5ou36LSd"></span>
## Multipart copy

When copying large objects, use `UploadPartCopy` to copy parts. Follow these steps:


1. Call `CreateMultipartUpload` to initialize the multipart copy task.

2. Call `UploadPartCopy` to copy the parts.

3. Call `CompleteMultipartUpload` to merge the parts.


```Objective-C
TOSCredential *credential = [[TOSCredential alloc] initWithAccessKey:@"accesskey" secretKey:@"secretkey"];
TOSEndpoint *tosEndpoint = [[TOSEndpoint alloc] initWithURLString:@"endpoint" withRegion:@"region"];
TOSClientConfiguration *config = [[TOSClientConfiguration alloc] initWithEndpoint:tosEndpoint credential:credential];
TOSClient *client = [[TOSClient alloc] initWithConfiguration:config];

// 1. CreateMultipartUpload
TOSCreateMultipartUploadInput *create = [TOSCreateMultipartUploadInput new];
create.tosBucket = @"bucket-name";
create.tosKey = @"object-name";
task = [client createMultipartUpload:create];
[task waitUntilFinished];
TOSCreateMultipartUploadOutput *createOutput = task.result;

// 2. UploadPartCopy
TOSUploadPartCopyInput *part1 = [TOSUploadPartCopyInput new];
part1.tosBucket = @"bucket-name";
part1.tosKey = @"object-name";
part1.tosSrcBucket = @"src-bucket-name";
part1.tosSrcKey = @"src-object-name";
part1.tosCopySourceRangeStart = @0;
part1.tosPartNumber = 1;
task = [client uploadPartCopy:part1];
[task waitUntilFinished];
TOSUploadPartCopyOutput *uploadOutput = task.result;
uploadOutput.tosETag = [uploadOutput.tosETag stringByReplacingOccurrencesOfString:@"\"" withString:@""];

// 3. CompleteMultipartUpload
TOSCompleteMultipartUploadInput *complete = [TOSCompleteMultipartUploadInput new];
complete.tosBucket = createOutput.bucket;
complete.tosKey = createOutput.key;
complete.tosUploadId = createOutput.uploadId;

NSMutableArray *array = [NSMutableArray array];
TOSUploadedPart *uploadedPart1 = [TOSUploadedPart new];
uploadedPart1.tosPartNumber = uploadOutput.tosPartNumber;
uploadedPart1.tosETag = uploadOutput.tosETag;
[array addObject:uploadedPart1];

complete.parts = array;
task = [client completeMultipartUpload:complete];
[task waitUntilFinished];
TOSCompleteMultipartUploadOutput *comleteOutput = task.result;
```


<span id="ee2e050b"></span>
## Resume copy

Resume copy completes on the TOS server without downloading the source object locally first. The source and destination objects can reside in different buckets.

<span id="97392434"></span>
### Prepare the checkpoint path

Each transfer task must use a separate checkpoint path. The following example saves the:

```Objective-C
static NSString *TOSCheckpointPath(NSString *fileName) {
    NSFileManager *fileManager = [NSFileManager defaultManager];
    NSURL *baseURL = [[fileManager URLsForDirectory:NSApplicationSupportDirectory
                                          inDomains:NSUserDomainMask] firstObject];
    NSURL *directoryURL = [baseURL URLByAppendingPathComponent:@"TOSCheckpoints"
                                                   isDirectory:YES];

    NSError *error = nil;
    BOOL created = [fileManager createDirectoryAtURL:directoryURL
                         withIntermediateDirectories:YES
                                          attributes:nil
                                               error:&error];
    if (!created) {
        NSLog(@"Create checkpoint directory failed: %@", error);
        return nil;
    }
    return [[directoryURL URLByAppendingPathComponent:fileName] path];
}
```


<span id="9071e6a0"></span>
### Create replication request

```Objective-C
static TOSResumableCopyObjectInput *TOSCreateCopyInput(
    NSString *sourceBucket,
    NSString *sourceObjectKey,
    NSString *destinationBucket,
    NSString *destinationObjectKey,
    NSString *checkpointPath,
    TOSCancelHook *cancelHook) {

    TOSResumableCopyObjectInput *input =
        [TOSResumableCopyObjectInput new];
    input.tosSrcBucket = sourceBucket;
    input.tosSrcKey = sourceObjectKey;
    input.tosBucket = destinationBucket;
    input.tosKey = destinationObjectKey;
    // Part size. Set to 0 to use the default value of 20 MiB, valid range is 5 MiB to 5 GiB.
    input.tosPartSize = 20LL * 1024 * 1024; 
    // Number of concurrent parts for a single task, default is 1; values normalize to between 1 and 1000.
    input.tosTaskNum = 3;
    input.tosEnableCheckpoint = YES;
    // Checkpoint file or directory path. It is recommended to use a local directory preserved across app launches and assign a separate path for each task.
    input.tosCheckpointFile = checkpointPath; 
    // Maximum retry count for initialization and single part requests, default is 3; set to 0 to disable retries.
    input.tosMaxRetryCount = 3;
    input.tosCancelHook = cancelHook;

    // Copy provides part events without byte-level progress callback.
    input.tosCopyEventListener = ^(TOSCopyEvent *event) {
        if (event.tosType == TOSCopyEventUploadPartCopySucceed) {
            NSLog(@"Copy part succeeded: %d",
                  event.tosCopyPartInfo.tosPartNumber);
        } else if (event.tosType == TOSCopyEventUploadPartCopyFailed) {
            NSLog(@"Copy part failed: %@", event.tosErr);
        }
    };
    return input;
}
```


<span id="ae251938"></span>
### Start replication

```Objective-C
NSString *sourceBucket = @"YOUR_SOURCE_BUCKET";
NSString *sourceObjectKey = @"example/source-large-file.bin";
NSString *destinationBucket = @"YOUR_DESTINATION_BUCKET";
NSString *destinationObjectKey = @"example/copied-large-file.bin";
NSString *copyCheckpoint = TOSCheckpointPath(@"copy-large-file.json");

TOSCancelHook *copyCancelHook = [TOSCancelHook new];
TOSResumableCopyObjectInput *copyInput =
    TOSCreateCopyInput(sourceBucket,
                       sourceObjectKey,
                       destinationBucket,
                       destinationObjectKey,
                       copyCheckpoint,
                       copyCancelHook);

TOSTask *copyTask = [client resumableCopyObject:copyInput];
[copyTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Copy object failed: %@", finishedTask.error);
        return nil;
    }

    TOSResumableCopyObjectOutput *output = finishedTask.result;
    NSLog(@"Copy object succeeded, ETag: %@", output.tosETag);
    return nil;
}];
```


<span id="62097f58"></span>
### Pause and resume replication

When the user triggers pause, call the following interface to pause the copy task:

```Objective-C
// Pause copy, retain checkpoint and remote part tasks.
[copyCancelHook cancel:NO];
```


After the original task callback completes, reuse the same source object, target object, part size, and checkpoint path:

```Objective-C
TOSCancelHook *newCopyCancelHook = [TOSCancelHook new];
TOSResumableCopyObjectInput *resumedCopyInput =
    TOSCreateCopyInput(sourceBucket,
                       sourceObjectKey,
                       destinationBucket,
                       destinationObjectKey,
                       copyCheckpoint,
                       newCopyCancelHook);

TOSTask *resumedCopyTask = [client resumableCopyObject:resumedCopyInput];
[resumedCopyTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Resume copy failed: %@", finishedTask.error);
    } else {
        NSLog(@"Resume copy succeeded");
    }
    return nil;
}];
```


<span id="7ea00b34"></span>
### Terminate task

Calling `TOSCancelHook` immediately terminates the task and clears the resume state; if the corresponding interface is called again after termination, the task restarts from the beginning.

Terminate the task through the `TOSCancelHook` in each request:

```Objective-C
// Terminate copy.
[copyCancelHook cancel:YES];
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do not reuse the old <code>TOSCancelHook</code> after the task has succeeded or been terminated.</div>
