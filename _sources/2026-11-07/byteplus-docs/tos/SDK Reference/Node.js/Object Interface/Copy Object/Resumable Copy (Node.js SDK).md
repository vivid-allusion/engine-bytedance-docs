---
title: "Resumable Copy (Node.js SDK)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Breakpoint-resume-copy-node-js-sdk"
---

The TOS Node.js SDK provides a resumable copy feature that is suitable for copying large objects within a single bucket or between two buckets in the same region. This feature uses a local checkpoint mechanism to track successfully copied parts. If a copy operation is interrupted due to network issues or machine failure, you can call the same API again to resume the copy process. Resumable copy splits the source object into multiple parts and supports concurrent copying. After all parts are successfully copied, they are merged into a complete object. You can configure the part size, the number of threads for concurrent copying, and event callback functions for the resumable copy task. You can also cancel the task while it is running.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Cross\-region bucket copying is not supported when copying objects.

* To copy objects, the account must have read permission on the source object and write permission on the destination bucket.

* All metadata is retained by default when copying objects. You can also specify new metadata if needed. However, the ACL is not retained, and the copied object is set to private.


<span id=".56S65L6L5Luj56CB"></span>
## Sample code

<span id=".5pat54K557ut5Lyg5ou36LSd"></span>
### Resumable copy

The following code is used to copy the srcObject object from the srcBucket bucket to the dstBucket bucket, and set the object name to dstObject. It supports resuming the copy if it fails. If the network timeout error is returned during the replication process, `resumableCopyObject` will be called with the same parameters to resume the copy task.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  try {
    const srcBucket = 'node-sdk-test-bucket'; // Source bucket
    const srcObject = 'source-test'; // Source object
    const dstBucket = 'node-sdk-copy-bucket'; // Target bucket
    const dstObject = 'copy-test'; // Target object

    await client.resumableCopyObject({
      bucket: dstBucket,
      key: dstObject,
      srcBucket,
      srcKey: srcObject,
      // Specify the size of each downloaded part as 10M
      partSize: 10 * 1024 * 1024,
      // Specify the number of concurrent tasks for downloading parts
      taskNum: 5,
      // Specify the temporary file path for resumable downloads
      checkpoint: './example_dir/example.checkpoint',
    });

    // Query copy object information
    const headResult = await client.headObject({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('headResult', headResult);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id="6c85870f"></span>
### Configure event callbacks

The following code is used to customize the resumable copy callback function.

```JavaScript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { ResumableCopyEventType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  try {
    const srcBucket = 'node-sdk-test-bucket'; // Source bucket
    const srcObject = 'source-test'; // Source object
    const dstBucket = 'node-sdk-copy-bucket'; // Target bucket
    const dstObject = 'copy-test'; // Target object

    await client.resumableCopyObject({
      bucket: dstBucket,
      key: dstObject,
      srcBucket,
      srcKey: srcObject,
      // Specify the size of each part to be downloaded as 10M.
      partSize: 10 * 1024 * 1024,
      // Set the number of concurrent tasks for downloading parts.
      taskNum: 5,
      // Specify the temporary file path for resumable downloads.
      checkpoint: './example_dir/example.checkpoint',
      // Set a custom callback function to monitor the progress of the copy.
      copyEventListener: (event) => {
        switch (event.type) {
          case ResumableCopyEventType.CreateMultipartUploadSucceed: {
            console.log(`Resume Create Multipart Upload Success.`);
            break;
          }
          case ResumableCopyEventType.CreateMultipartUploadFailed: {
            console.log(`Resume Create Multipart Upload Fail.`);
            break;
          }
          case ResumableCopyEventType.UploadPartCopySucceed: {
            console.log(`Copy ${event.bucket} ${event.key} part success, CopyPartInfo:%o`, event.copyPartInfo);
            break;
          }
          case ResumableCopyEventType.UploadPartCopyFailed: {
            console.log(`Copy ${event.bucket} ${event.key} part fail, err:%o`, event.err);
            break;
          }
          case ResumableCopyEventType.UploadPartCopyAborted: {
            console.log(`Copy ${event.bucket} ${event.key} part aborted.`);
            break;
          }
          case ResumableCopyEventType.CompleteMultipartUploadSucceed: {
            console.log(`Copy ${event.bucket} ${event.key} success.`);
            break;
          }
          case ResumableCopyEventType.CompleteMultipartUploadFailed: {
            console.log(`Copy ${event.bucket} ${event.key} part fail, err: %o`, event.err);
            break;
          }
        }
      },
    });

    // Query copy object information
    const headResult = await client.headObject({
      bucket: dstBucket,
      key: dstObject,
    });
    console.log('headResult', headResult);
  } catch (error) {
    handleError(error);
  }
}

main();
```


<span id=".5Y-W5raI5py65Yi2"></span>
### Cancellation mechanism

The following code is used to pause or cancel the resumable copy task.

```javascript
// Import SDK, if the TOS Node.JS SDK version is less than 2.5.2, please change "TosClient" to "TOS" in the code below.
import { isCancel, CancelToken, ResumableCopyEventType, TosClient, TosClientError, TosServerError } from '@volcengine/tos-sdk';
import fsp from 'fs/promises';

// Create a client.
const client = new TosClient({
  accessKeyId: process.env['TOS_ACCESS_KEY'],
  accessKeySecret: process.env['TOS_SECRET_KEY'],
  region: "Provide your region", // Fill in the region where the Bucket is located. For example, if it is in China North 2 (Beijing), fill in "Provide your region" as cn-beijing.
  endpoint: "Provide your endpoint", // Enter the domain address.
});

function handleError(error) {
  if (error instanceof TosClientError) {
    console.log('Client Err Name:', error.name);
    console.log('Client Err Msg:', error.message);
    console.log('Client Err Stack:', error.stack);
  } else if (error instanceof TosServerError) {
    console.log('Request ID:', error.requestId);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Status Code:', error.statusCode);
    console.log('Response Header:', error.headers);
    console.log('Response Err Code:', error.code);
    console.log('Response Err Msg:', error.message);
  } else {
    console.log('unexpected exception, message: ', error);
  }
}

async function main() {
  // checkpoint file path
  const checkpointFilePath = './example_dir/example.checkpoint';

  try {
    const srcBucket = 'node-sdk-test-bucket'; // Source bucket
    const srcObject = 'source-test'; // Source object
    const dstBucket = 'node-sdk-copy-bucket'; // Target bucket
    const dstObject = 'copy-test'; // Target object

    try {
      // Generate cancelTokenSource.
      const cancelTokenSource = CancelToken.source();
      // Cancel the task in 5 seconds.
      setTimeout(() => {
        cancelTokenSource.cancel();
        console.log('cancel resumableCopyObject');
      }, 5_000);

      await client.resumableCopyObject({
        bucket: dstBucket,
        key: dstObject,
        srcBucket,
        srcKey: srcObject,
        // Specify the size of each part to be downloaded as 10M
        partSize: 10 * 1024 * 1024,
        // Specify the number of concurrent tasks for downloading parts
        taskNum: 5,
        // Specify the file path for resumable download checkpoint
        checkpoint: './example_dir/example.checkpoint',
        // Set a custom callback function to view the copy progress
        copyEventListener: (event) => {
          switch (event.type) {
            case ResumableCopyEventType.CreateMultipartUploadSucceed: {
              console.log(`Resume Create Multipart Upload Success.`);
              break;
            }
            case ResumableCopyEventType.CreateMultipartUploadFailed: {
              console.log(`Resume Create Multipart Upload Fail.`);
              break;
            }
            case ResumableCopyEventType.UploadPartCopySucceed: {
              console.log(`Copy ${event.bucket} ${event.key} part success, CopyPartInfo:%o`, event.copyPartInfo);
              break;
            }
            case ResumableCopyEventType.UploadPartCopyFailed: {
              console.log(`Copy ${event.bucket} ${event.key} part fail, err:%o`, event.err);
              break;
            }
            case ResumableCopyEventType.UploadPartCopyAborted: {
              console.log(`Copy ${event.bucket} ${event.key} part aborted.`);
              break;
            }
            case ResumableCopyEventType.CompleteMultipartUploadSucceed: {
              console.log(`Copy ${event.bucket} ${event.key} success.`);
              break;
            }
            case ResumableCopyEventType.CompleteMultipartUploadFailed: {
              console.log(`Copy ${event.bucket} ${event.key} part fail, err: %o`, event.err);
              break;
            }
          }
        },
        cancelToken: cancelTokenSource.token,
      });
    } catch (error) {
      if (!isCancel(error)) {
        throw error;
      }

      const checkpointFileContent = await fsp.readFile(checkpointFilePath, 'utf-8');
      console.log(`checkpoint file's content after cancel: `, checkpointFileContent);

      console.log('Continue to copy');
      // You can use the checkpoint file to resume copying.
      await client.resumableCopyObject({
        bucket: dstBucket,
        key: dstObject,
        srcBucket,
        srcKey: srcObject,
        // Specify the size of each part to be downloaded as 10M.
        partSize: 10 * 1024 * 1024,
        // Specify the number of concurrent tasks for part downloading.
        taskNum: 5,
        // Specify the file path for resuming interrupted downloads.
        checkpoint: './example_dir/example.checkpoint',
        // Set a custom callback function to monitor the progress of the copying process.
        copyEventListener: (event) => {
          switch (event.type) {
            case ResumableCopyEventType.CreateMultipartUploadSucceed: {
              console.log(`Resume Create Multipart Upload Success.`);
              break;
            }
            case ResumableCopyEventType.CreateMultipartUploadFailed: {
              console.log(`Resume Create Multipart Upload Fail.`);
              break;
            }
            case ResumableCopyEventType.UploadPartCopySucceed: {
              console.log(`Copy ${event.bucket} ${event.key} part success, CopyPartInfo:%o`, event.copyPartInfo);
              break;
            }
            case ResumableCopyEventType.UploadPartCopyFailed: {
              console.log(`Copy ${event.bucket} ${event.key} part fail, err:%o`, event.err);
              break;
            }
            case ResumableCopyEventType.UploadPartCopyAborted: {
              console.log(`Copy ${event.bucket} ${event.key} part aborted.`);
              break;
            }
            case ResumableCopyEventType.CompleteMultipartUploadSucceed: {
              console.log(`Copy ${event.bucket} ${event.key} success.`);
              break;
            }
            case ResumableCopyEventType.CompleteMultipartUploadFailed: {
              console.log(`Copy ${event.bucket} ${event.key} part fail, err: %o`, event.err);
              break;
            }
          }
        },
      });

      // Query copy object information.
      const headResult = await client.headObject({
        bucket: dstBucket,
        key: dstObject,
      });
      console.log('headResult', headResult);
    }
  } catch (error) {
    handleError(error);
  }
}

main();
```
