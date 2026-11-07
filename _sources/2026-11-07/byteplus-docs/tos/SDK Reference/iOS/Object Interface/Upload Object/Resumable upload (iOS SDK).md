---
title: "Resumable upload (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Resumable-upload"
---

Resumable upload is for large file transfers or unstable network conditions. TOS iOS SDK splits objects into multiple parts and saves them to the `checkpoint`. After a task is paused or interrupted, restarting the same request continues from completed parts without re\-uploading the entire file.

<span id="441a3213"></span>
## Prerequisites


* Have [installed and initialized TOS iOS SDK](https://docs.byteplus.com/en/docs/tos/Quick-start-ios-sdk) v2.1.8 or later.

* Have available Endpoint, Region, and Bucket.

* Ensure the upload source path, download destination folder, and checkpoint folder are all accessible.

* Example code uses `Objective-C` and can be placed in the project’s `.m` files.


<span id="1c2d2937"></span>
## Notes


|Notes |Description |
|---|---|
|Version and interface compatibility |* The existing `TOSUploadFileInput` and `uploadFile` interfaces remain unchanged.<br><br>* Please use the `TOSUploadFileInputV2` SDK interface for resumable uploads.<br><br>* The current resumable upload interface does not support SSE\-related parameters. |
|Task management |* The same `checkpoint` path cannot be used for multiple transmission tasks simultaneously; wait for the original task to complete before resuming.<br><br>* When restoring a task, Bucket, Object, file path, part size, version number, and condition parameters must match the original task.<br><br>* A new request object and `TOSCancelHook` must be created each time a transfer task resumes.<br><br>* `Checkpoint` does not contain access credentials and does not guarantee interoperability with SDKs in other languages. |
|Operating environment |* Breakpoint resume follows the foreground transmission boundary: App may stop executing when entering the background or being terminated by the system; next launch can restore via checkpoint.<br><br>* Transmission progress and event callbacks may run on background threads; switch to the main thread when updating the UI. |
|Resume state management |After a successful upload completion, the SDK automatically deletes the `checkpoint`.<br><br><br>* `cancel:NO` Keep the resume state.<br><br>* `cancel:YES` Clear the resume state. |


<span id="633cd8ec"></span>
## Prepare checkpoint path

Each transfer task must use a separate `checkpoint` path. The following example saves the `checkpoint` in the app's `Application Support` directory:

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


<span id="e20f41ea"></span>
## Code examples

<span id="j4zLdomM"></span>
### Create upload request

Create an upload request that enables `checkpoint`. Initial and resumed uploads must use the same bucket, object, source file, chunk size, and `checkpoint` path.

```Objective-C
static TOSUploadFileInputV2 *TOSCreateUploadInput(
    NSString *bucket,
    NSString *objectKey,
    NSString *filePath,
    NSString *checkpointPath,
    TOSCancelHook *cancelHook) {

    TOSUploadFileInputV2 *input = [TOSUploadFileInputV2 new];
    input.tosBucket = bucket;
    input.tosKey = objectKey;
    input.tosFilePath = filePath;
    // Part size, set to 0 to use the default value of 20 MiB, valid range is 5 MiB to 5 GiB.
    input.tosPartSize = 20LL * 1024 * 1024; 
    // Number of concurrent parts for the current task, default is 1; the value is normalized to 1 to 1000.
    input.tosTaskNum = 3;                   
    input.tosEnableCheckpoint = YES;
    // Checkpoint file or directory path. It is recommended to use a local directory that can persist across App launches and assign a separate path for each task.
    input.tosCheckpointFile = checkpointPath;
    // Maximum retry attempts for initialization requests and individual part requests; default is 3; set to 0 to disable retries.
    input.tosMaxRetryCount = 3;
    input.tosCancelHook = cancelHook;

    input.tosDataTransferListener = ^(TOSDataTransferStatus *status) {
        if (status.tosTotalBytes <= 0) {
            return;
        }
        double progress =
            status.tosConsumedBytes * 100.0 / status.tosTotalBytes;
        dispatch_async(dispatch_get_main_queue(), ^{
            NSLog(@"Upload progress: %.2f%%", progress);
            // Update the progress bar here.
        });
    };
    return input;
}
```


<span id="bf065eb1"></span>
### Start uploading

```Objective-C
NSString *bucket = @"YOUR_BUCKET";
NSString *objectKey = @"example/large-file.bin";
NSString *sourceFilePath = @"YOUR_LOCAL_FILE_PATH";
NSString *uploadCheckpoint = TOSCheckpointPath(@"upload-large-file.json");

TOSCancelHook *uploadCancelHook = [TOSCancelHook new];
TOSUploadFileInputV2 *uploadInput =
    TOSCreateUploadInput(bucket,
                         objectKey,
                         sourceFilePath,
                         uploadCheckpoint,
                         uploadCancelHook);

TOSTask *uploadTask = [client uploadFile:uploadInput];
[uploadTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Upload file failed: %@", finishedTask.error);
        return nil;
    }

    TOSUploadFileOutputV2 *output = finishedTask.result;
    NSLog(@"Upload file succeeded, ETag: %@", output.tosETag);
    return nil;
}];
```


<span id="b6ddf52c"></span>
### Pause and resume upload

Call the following interface to pause the upload task when the user triggers the pause operation:

```Objective-C
// Cancel the current request but keep the checkpoint and the remotely uploaded parts.
[uploadCancelHook cancel:NO];
```


After waiting for the original task to complete the callback, recreate the request and `TOSCancelHook`, reusing the same `checkpoint` path:

```Objective-C
TOSCancelHook *newUploadCancelHook = [TOSCancelHook new];
TOSUploadFileInputV2 *resumedUploadInput =
    TOSCreateUploadInput(bucket,
                         objectKey,
                         sourceFilePath,
                         uploadCheckpoint,
                         newUploadCancelHook);

TOSTask *resumedUploadTask = [client uploadFile:resumedUploadInput];
[resumedUploadTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Resume upload failed: %@", finishedTask.error);
    } else {
        NSLog(@"Resume upload succeeded");
    }
    return nil;
}];
```


After a successful upload, the SDK automatically deletes the `checkpoint`.

<span id="dfed0139"></span>
### Terminate task

Calling `TOSCancelHook` immediately terminates the task and clears the resumable upload state. When calling the corresponding interface again after termination, the task restarts from the beginning.

Terminate the task through the `TOSCancelHook` in each request:

```Objective-C
// terminate upload
[uploadCancelHook cancel:YES];
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do not reuse the old <code>TOSCancelHook</code> after the task has succeeded or already terminated.</div>
