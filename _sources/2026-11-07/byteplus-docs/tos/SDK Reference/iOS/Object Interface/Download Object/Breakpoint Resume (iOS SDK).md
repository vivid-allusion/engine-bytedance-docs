---
title: "Breakpoint Resume (iOS SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-Resume"
---

Breakpoint resume is suitable for large file transfers or unstable network conditions. TOS iOS SDK splits the object into multiple parts and saves them to `checkpoint`. After a task is paused or interrupted abnormally, resuming the same request continues transferring from completed parts without retransmitting the entire file.

<span id="8c9da0b0"></span>
## Prerequisites


* Have [installed and initialized TOS iOS SDK](https://docs.byteplus.com/en/docs/tos/Quick-start-ios-sdk) v2.1.8 or later.

* Available Endpoint, Region, and Bucket must be prepared.

* Ensure the upload source file path, download target directory, and checkpoint directory are all accessible.

* The sample code uses `Objective-C` and can be placed in the project’s `.m` file.


<span id="06f2267a"></span>
## Notes


|Notes |Description |
|---|---|
|Version and interface compatibility |* For breakpoint resume downloads, use the `TOSDownloadFileInput` SDK interface.<br><br>* The current breakpoint resume interface does not support SSE\-related parameters. |
|Task management |* The same `checkpoint` path cannot be used for multiple transfer tasks simultaneously. Wait for the original task to finish before resuming.<br><br>* When resuming a task, Bucket, Object, file path, part size, version, and condition parameters must match the original task.<br><br>* Every time a transfer task is resumed, a new request object and `TOSCancelHook` must be created.<br><br>* `checkpoint` does not include access credentials and does not guarantee interoperability with SDKs in other languages. |
|Operating environment |* Breakpoint resume uses the frontend transfer boundary: when the App goes to the background or the process is terminated by the system, continuation is not guaranteed. You can recover at the next start using the `checkpoint`.<br><br>* The download temporary file and target file must be on the same file system; it is recommended to place them in the same directory as the target file.<br><br>* Transfer progress and event callbacks may run on background threads. Switch to the main thread when updating the UI. |
|Resume status management |The SDK automatically deletes the `checkpoint` after a successful download.<br><br><br>* `cancel:NO` retains the resume state.<br><br>* `cancel:YES` clears the resume state. |


<span id="149a5657"></span>
## Prepare checkpoint path

Each transfer task must use a separate `checkpoint` path. The following example saves the `checkpoint` in the App's `Application Support` directory:

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


<span id="0e4e555a"></span>
## Code examples

Downloaded data is first written to a temporary file. The SDK atomically replaces the target file only after all chunks are downloaded and verified successfully. Therefore, pausing or failing the transfer does not damage the existing target file.

<span id="cdb5a3a7"></span>
### Create download request

```Objective-C
static TOSDownloadFileInput *TOSCreateDownloadInput(
    NSString *bucket,
    NSString *objectKey,
    NSString *filePath,
    NSString *checkpointPath,
    TOSCancelHook *cancelHook) {

    TOSDownloadFileInput *input = [TOSDownloadFileInput new];
    input.tosBucket = bucket;
    input.tosKey = objectKey;
    input.tosFilePath = filePath;
    // Temporary files must be on the same file system as the target file; using the same directory is recommended.
    input.tosTempFilePath = [filePath stringByAppendingString:@".temp"];
    // Part size. Set to 0 to use the default value of 20 MiB, with an effective range of 5 MiB to 5 GiB.
    input.tosPartSize = 20LL * 1024 * 1024; 
    // Concurrent parts per single task; the default value is 1, normalized between 1 and 1000.
    input.tosTaskNum = 3;
    input.tosEnableCheckpoint = YES;
    // Checkpoint file or directory path. It is recommended to use a local directory that supports cross-App launch retention and assign a separate path for each task.
    input.tosCheckpointFile = checkpointPath; 
    // Maximum retry attempts for initialization request and individual chunk requests, default is 3; set to 0 to disable retry.
    input.tosMaxRetryCount = 3;
    input.tosCancelHook = cancelHook;= ^(TOSDataTransferStatus *status) {
        if (status.tosTotalBytes <= 0) {
            return;
        }
        double progress =
            status.tosConsumedBytes * 100.0 / status.tosTotalBytes;
        dispatch_async(dispatch_get_main_queue(), ^{
            NSLog(@"Download progress: %.2f%%", progress);
            // Update the progress bar here.
        });
    };
    return input;
}
```


<span id="dae5695a"></span>
### Start download

```Objective-C
NSString *bucket = @"YOUR_BUCKET";
NSString *objectKey = @"example/large-file.bin";
NSString *downloadFilePath = @"YOUR_DOWNLOAD_FILE_PATH";
NSString *downloadCheckpoint = TOSCheckpointPath(@"download-large-file.json");

TOSCancelHook *downloadCancelHook = [TOSCancelHook new];
TOSDownloadFileInput *downloadInput =
    TOSCreateDownloadInput(bucket,
                           objectKey,
                           downloadFilePath,
                           downloadCheckpoint,
                           downloadCancelHook);

TOSTask *downloadTask = [client downloadFile:downloadInput];
[downloadTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Download file failed: %@", finishedTask.error);
        return nil;
    }

    NSLog(@"Download file succeeded: %@", downloadFilePath);
    return nil;
}];
```


<span id="14edd982"></span>
### Pause and resume download

When the user triggers a pause, call the following interface to pause the download task:

```Objective-C
// Pause the download and retain the checkpoint and temporary files.
[downloadCancelHook cancel:NO];
```


After the original task callback completes, recreate the request with the same parameters:

```Objective-C
TOSCancelHook *newDownloadCancelHook = [TOSCancelHook new];
TOSDownloadFileInput *resumedDownloadInput =
    TOSCreateDownloadInput(bucket,
                           objectKey,
                           downloadFilePath,
                           downloadCheckpoint,
                           newDownloadCancelHook);

TOSTask *resumedDownloadTask = [client downloadFile:resumedDownloadInput];
[resumedDownloadTask continueWithBlock:^id(TOSTask *finishedTask) {
    if (finishedTask.error) {
        NSLog(@"Resume download failed: %@", finishedTask.error);
    } else {
        NSLog(@"Resume download succeeded: %@", downloadFilePath);
    }
    return nil;
}];
```


<span id="65cfcb22"></span>
### Terminate task

Calling `TOSCancelHook` immediately terminates the task and clears the resume state. If you call the related interface again after termination, the task will restart from the beginning.

Terminate the task using `TOSCancelHook` from each request:

```Objective-C
// Cancel download
[downloadCancelHook cancel:YES];
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">Do not reuse an old <code>TOSCancelHook</code> after a task has succeeded or terminated.</div>
